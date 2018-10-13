# IPLD as a general pattern for DID documents

*By Christian Lundkvist, jonnycrunch, Anthony Ronning, Kim Duffy*

## Abstract

Since the emergence of the Decentralized Identifier (DID) specification at the Fall 2016 Rebooting the Web of Trust, numerous DID method specifications have emerged. Each DID method specification defines how to resolve a cryptographically-tied DID document given a method-specific identifier. In this paper, we describe a way to represent an initial DID document as a directed acyclic graph via Interplanetary Linked Data (IPLD). This technique enables more cost-efficient, scaleable creation of DIDs and can be used across different DID method specifications.

## Background / Definitions

> Note: it's possible we should work them into the doc but they seems a bit disjoint in the previous draft. I'm moving these up while working on the main doc flow and then we can determine how to merge them in.

> Some of these definitions don't seem necessary...

### IPLD

[IPLD](https://ipld.io) is a way of representing hash-linked data to be used in content-addressed data retrieval systems like [IPFS](https://ipfs.io). 

### CID

[Content Identifiers (CIDs)](https://github.com/ipld/cid) are used for referencing content in distributed information systems, like IPFS. It leverages content addressing, cryptographic hashing, and self-describing formats. It is the core identifier used by IPFS and IPLD.  It uses cryptographic hashes to achieve content addressing. It uses several multiformats to achieve flexible self-description, namely multihash for hashes, multicodec for data content types, and multibase to encode the CID itself into strings.

Anatomy of a CID: 
`<mbase><version><mcodec><mhash>`

Where:

- `<mbase>` is a [multibase](multibase) prefix describing the base that encodes this CID. If binary, this is omitted.
- `<version>` is the version number of the cid.
- `<mcodec>` is a [multicodec-packed](https://github.com/multiformats/multicodec) identifier, from the CID multicodec table
- `<mhash>` is a cryptographic [multihash](https://github.com/multiformats/multihash), including: `<mhash-code><mhash-len><mhash-value>`

### CBOR 

IPLD makes use of [Concise Binary Object Representation (CBOR)](http://cbor.io/). CBOR is a binary data serialization format loosely based on JSON. Its design goals include the possibility of extremely small code size, fairly small message size, and extensibility without the need for version negotiation.

## Proposal

We investigate using IPLD as a general pattern for DID creating in DID methods. The main idea is to represent an initial DID document as IPLD data, and then define the DID itself as the hash of this data. This way resolving the initial DID document from the DID is tautological - the DID is merely a representation of the data in the DID document.

> 
> TODO: what's the correct terminology for IPID DID Document?

The IPID DID document is not complete because the DID (identifier) will not be known at time of creation. This is a general issue for immutable storage of DID document material that is addressed by other DID methods during DID resolution. 

We address this by including _at most_ the [DID fragment](https://w3c-ccg.github.io/did-spec/#dfn-did-fragment), which is the part of the DID identifier after `#`, in the relevant DID document fields, which include `id`, `creator`, and key material. We may omit these fields entirely if there is no DID fragment to include, since this is optional. At resolution time, the resolver applies these missing fields from the DID identifier itself. (Note this is similar to the BTCR resolver merging implicit tx data with explicit DID document data, which doesn't know the DID at time of creation)

As it stands this is also not a self-contained DID method because the DID document is immutable. Modifying the DID document would modify its hash, thus creating a new DID. We can however create a new DID document and link it back to the initial DID document, thus creating a cryptographic link back to the original DID. 

![](ipld_did_documents/did_docs.png)

The initial DID document needs to contain information about where to discover the latest version of the DID document (which is a requirement of DID resolution), but method specs can implement this in their own ways. 

For instance, in the [muPort](https://github.com/uport-project/muport-core-js) DID method an Ethereum smart contract is used to point to the hash of the latest version of the DID document, and the document can be retrieved using the content-addressed IPFS system. In the [IPID](https://github.com/jonnycrunch/ipid) DID method the IPNS system can used to point to the latest version of the DID document, by means of a published signed statement. The [Sidetree](https://github.com/decentralized-identity/did-methods/blob/master/sidetrees/explainer.md) DID method uses a scalable Merkle data structure that aggregates multiple DID document updates in a Merkle Tree and publishes the root hash in a blockchain such as Bitcoin or Ethereum. A sidetree node can use these data structures to aggregate the updates into a complete DID document.

One large advantage of the IPLD approach described here is that the identity owner does not need to use a blockchain when initially creating an identity, thus making creation of identities fast and low cost (if not free). The DID and DID document will be cryptographically coupled by hashing. Only when the identity owner needs to update their DID document will they need a more costly tool such as a blockchain.

## Examples

Example 1 shows the DID document before resolution. Note that `id` fields are omitted.

**Example 1: IPLD DID document stored in IPFS**

```
{
  "@context": {
    "/": "zdpuAmoZixxJjvosviGeYcqduzDhSwGV2bL6ZTTXo1hbEJHfq"
  },
  "authentication": {
      "type": "EdDsaSASignatureAuthentication2018", 
      "publicKey": [
          "did:ipid:QmcEF77C6QKj6Rzru7MR2N5tSM33PHQYEqXYzQuVHHAvvv" <<<< ?
      ]
  },
  "created": "2018-07-14T17:00:00Z",
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
      "publicKeyBase64": "lji9qTtkCydxtez/bt1zdLxVMMbz4SzWvlqgOBmURoM=",
      "type": "EdDsaPublicKey"
    }
  ],
  "updated": "2018-07-09T02:41:00Z"
}
 
```
  
**Example 2: final (after resolution) DID document**
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
