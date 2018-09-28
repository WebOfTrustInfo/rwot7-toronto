# IPLD as a general pattern for DID documents

*By Christian Lundkvist, jonnycrunch, Anthony Ronning, Kim Duffy*

## Abstract

Numerous Decentralized Identifiers (DID) method specification have emerged since its introduction at a previous Rebooting the Web of Trust in 2016. Each DID method requires resolving a DID document that is cryptographically tied to the method specific identifier.  In this paper we present a generalized approach to resolve the DID document to a directed acyclic graph host on Interplanetary File System (IPFS) as an Interplanetary LInk Data (IPLD) node. 

## Background

[IPLD](https://ipld.io) is a way of representing hash-linked data to be used in content-addressed data retrieval systems like [IPFS](https://ipfs.io). We investigate using IPLD as a general pattern in creating DID methods. The main idea is to represent an initial DID document as IPLD data, and then define the DID itself as the hash of this data. This way resolving the initial DID document from the DID is tautological - the DID is merely a representation of the data in the DID document.

Context Identifiers (CID) are used for referencing content in distributed information systems, like IPFS. It leverages content addressing, cryptographic hashing, and self-describing formats. It is the core identifier used by IPFS and IPLD.  It uses cryptographic hashes to achieve content addressing. It uses several multiformats to achieve flexible self-description, namely multihash for hashes, multicodec for data content types, and multibase to encode the CID itself into strings.

Anatomy of a CID: 
`<mbase><version><mcodec><mhash>`

Where:

- `<mbase>` is a [multibase](multibase) prefix describing the base that encodes this CID. If binary, this is omitted.
- `<version>` is the version number of the cid.
- `<mcodec>` is a [multicodec-packed](https://github.com/multiformats/multicodec) identifier, from the CID multicodec table
- `<mhash>` is a cryptographic [multihash](https://github.com/multiformats/multihash), including: `<mhash-code><mhash-len><mhash-value>`
  
## CBOR 

IPLD makes uses Concise Binary Object Representation (CBOR).  is a binary data serialization format loosely based on JSON is a data format whose design goals include the possibility of extremely small code size, fairly small message size, and extensibility without the need for version negotiation.
  
  
**Example DID document stored on IPLD:**
```
{
  "@context": {
    "/": "zdpuAmoZixxJjvosviGeYcqduzDhSwGV2bL6ZTTXo1hbEJHfq"
  },
  "authentication": {
      "type": "EdDsaSASignatureAuthentication2018", 
      "publicKey": [
          "did:ipid:QmcEF77C6QKj6Rzru7MR2N5tSM33PHQYEqXYzQuVHHAvvv"
      ]
  },
  "created": "2018-07-14T17:00:00Z",
  "id": "did:ipid:QmcEF77C6QKj6Rzru7MR2N5tSM33PHQYEqXYzQuVHHAvvv",
  "previous": {
    "/": "zdpuArY8PA81cxdoNqsP42xT5itMHi6savk7GReyaVxBoCgkv"
  },
  "proof" : {
    "/": "z43AaGF42R2DXsU65bNnHRCypLPr9sg6D7CUws5raiqATVaB1jj"
  },
  "publicKey": [
    {
      "curve": "ed25519",
      "expires": "2019-07-08T16:02:20Z",
      "id": "did:ipid:QmcEF77C6QKj6Rzru7MR2N5tSM33PHQYEqXYzQuVHHAvvv",
      "publicKeyBase64": "lji9qTtkCydxtez/bt1zdLxVMMbz4SzWvlqgOBmURoM=",
      "type": "EdDsaPublicKey"
    }
  ],
  "signature": {
    "created": "2018-07-26T16:02:20Z",
    "creator": "did:ipid:QmcEF77C6QKj6Rzru7MR2N5tSM33PHQYEqXYzQuVHHAvvv",
    "message" : {
        "/" : "zdpuAugYQGm3qcg6YZxBKmQGqM3EaKNbkfVB14DToXNUWDGQu",
    },
    "signatureValue": "IOmA4R7TfhkYTYW87z640O3GYFldw0yqie9Wl1kZ5OBYNAKOwG5uOsPRK8/2C4STOWF+83cMcbZ3CBMq2/gi25s=",
    "type": "ed25519Signature2018"
  },
  "updated": "2018-07-09T02:41:00Z"
}
 
```

Note that the DID document is not complete since in this case the DID document cannot contain the DID itself. A placeholder such as `did:example:this` would need to be put in whenever the DID appears in the DID document, but it is trivial to derive the complete DID document from the template.

As it stands this is also not a self-contained DID method because the DID document is immutable. Modifying the DID document would modify its hash, thus creating a new DID. We can however create a new DID document and link it back to the initial DID document, thus creating a cryptographic link back to the original DID.

The initial DID document needs to contain information about where to discover the latest version of the DID document. For instance, in the [muPort](https://github.com/uport-project/muport-core-js) DID method an Ethereum smart contract is used to point to the hash of the latest version of the DID document, and the document can be retrieved using the content-addressed IPFS system. In the [IPID](https://github.com/jonnycrunch/ipid) DID method the IPNS system can used to point to the latest version of the DID document, by means of a published signed statement. The [Sidetree](https://github.com/decentralized-identity/did-methods/blob/master/sidetrees/explainer.md) DID method uses a scalable Merkle data structure that aggregates multiple DID document updates in a Merkle Tree and publishes the root hash in a blockchain such as Bitcoin or Ethereum. A sidetree node can use these data structures to aggregate the updates into a complete DID document.

![](ipld_did_documents/did_docs.png)

One large advantage of the IPLD approach described here is that the identity owner does not need to use a blockchain when initially creating an identity, thus making creation of identities fast and low cost (if not free). The DID and DID document will be cryptographically coupled by hashing. Only when the identity owner needs to update their DID document will they need a more costly tool such as a blockchain.

## Uses / Examples
### Use for microledgers and pairwise identifiers

The IPLD pattern may be good to use for pairwise identifiers. A pairwise identifier is a DID that is meant to be used only with one other entity. The idea is that when setting up a pairwise DID you can do it by generating the DID document, and send the DID as well as the DID document to the counterparty.

Since there is only one actor that needs to agree on the mapping from DID to DID document, there is no need to use a blockchain or similar consensus mechanism in this case. The phrase "microledger" is often used to describe the way that these kinds of pairwise DIDs are handled.

The counterparty can verify that the DID document hash is the DID. Then if the user decides to update the DID document (normally through the use of a digital signature from a "management key" specified in the DID document) they can just present the updated version of the DID document to the counterparty who can then verify the signatures and store the updated document in a local database.

Even though IPFS could be used for content addressing there would not be a need to connect to a wider IPFS network. The "ledger" in this case could just be a simple database hosted by the counterparty.
  
  
### Using IPLD in combination with IPNS (Interplanetary Name Space)
By itself, resolving an IPLD DID Document by itself will only resolve it at the current state (due to the immutability of IPFS). Some other DID methods have an aspect of "resolving the tip" that allows for updating a DID by spending the unspent transaction that created the DID in the first place.

In order to make updates to the IPLD, one could publish the original IPLD to IPNS, and then share the IPNS hash to an entity. As updates are made to the original IPLD, a new hash is created which can then be republished to IPNS. IPNS uses a pubsub system in order to provide real time updates, so whenever an IPLD is updated and IPNS is republished, it's able to resolve to the correct IPLD insantly. 

[IPID](https://github.com/jonnycrunch/ipid) uses this approach as well.

## Benefits

- Low cost / free scalable solution for DIDs
  - Ability to use bitcoin, ethereum and/or ethereum smart contracts, or github as an optional reference proof
- Ability to use [CBOR](http://cbor.io) as a schema less data model
- Cryptographic verifiable resolution of a document
- Ability to use microledgers
- Ability to self host documents or pay through services such as [Filecoin](https://filecoin.io)
- Easily resolve previous versions of the DID by linking
- Resolvable anywhere (local networks, mars, online, etc.)

## Drawbacks

- Not resolvable without hosting
- No resolving to the updated version of the document ("following the tip")
  - Requires use of something like IPNS to accomplish this 
- `@Context` is not a reserved word in IPLD.
