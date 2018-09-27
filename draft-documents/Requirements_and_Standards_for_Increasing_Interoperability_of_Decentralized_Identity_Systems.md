<!----- Conversion time: 1.323 seconds.


Using this Markdown file:

1. Cut and paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* GD2md-html version 1.0β12
* Thu Sep 27 2018 13:28:15 GMT-0700 (PDT)
* Source doc: https://docs.google.com/a/cloudcompass.ca/open?id=1tDX6LXJn6KITKIvNbbexHfcdWZ9z9TCElC5cZygaacw
----->



## Requirements and Standards for Increasing Interoperability of Decentralized Identity Systems



*   Authors:  David Bissessar, Daniel Buchner, Dan Burnett, Stephen Curran, Kyle Den Hartog, Michael B. Jones, Christian Lundkvist, Arturo Manzaneda, Olena Mitovska, Manu Sporny, Mike Varley


## Abstract



*   Identify core high-level requirements for interoperable decentralized identity systems (including data modelling, cryptographic requirements, and data representations)
*   Talk about importance of standards and conventions in facilitating interop, increasing adoption, and accelerating innovation
*   Come up with top categories of standards for interoperability - conventions for use of DIDDoc elements, key types and purposes, data format, and others
*   Identify current applicable standards and specifications
*   Identify gaps in current standards and specifications and propose ways to fill them
*   Identify the four or five most used cryptographic key types and finalize their descriptions


## Outline



*   Introduction
    *   Defining an abstract data model for the specific domain of decentralized identity systems so the systems can be interoperable
*   Guiding Principles
    *   Data Model
    *   Syntaxes
    *   Cryptographic requirements
*   Applicable standards - inventory and discussion
    *   Existing standards
    *   Gaps in existing standards and corresponding recommendations
*   DID-specific standards content
    *   Key representation
    *   Signature representation
    *   Key usage
        *   Describe gaps in specifying usage of keys

Related Work



*   [The Role of Standards in Accelerating Innovation](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/The_Role_of_Standards_in_Accelerating_Innovation.md)
*   [DIDDoc Conventions for Interoperability](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/diddoc-conventions-for-interoperability.md)
*   [RWoT Crypto and Data Model Requirements](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/crypto-data-model-requirements.md) 


## Introduction


## Guiding Principles


### Data Model



*   Open world assumption - you can make statements about anything
*   Data structures representing entities can have local data and/or links to other entities
*   Entities and relationships can be defined to be interpreted in an unambiguous manner
*   Inclusive of the use of schemas for data as defined in particular application contexts
*   Enables decentralized innovation without need for central coordination between projects
*   Compatibility with existing ecosystems and standards that follow these principles
*   


### Syntaxes



*   JSON as the default
*   Base64url encoded JSON (or other formats) when necessary for data representation purposes
*   Some systems use canonicalization to create the signing input; some systems base64url encode content to sign it (Group specifically notes this is tabled for now and not agreed yet) 
*   Should be possible to transport representations over different transports, including HTML (transport agnostic)
*   Should be able to include representations in HTML pages using <script> tags


### Cryptographic requirements



*   Digital signatures
    *   Also sets of digital signatures, some of which may be dynamically added to
*   Encryption
*   HMACs
*   Some systems need representations of other kinds of mathematical proofs
    *   Including zero-knowledge proofs
    *   Satoshi proofs (BTCR uses this)
*   Nested cryptographic operations
*   Key representations
    *   Explicit key representation for certain keys
        *   Ed25519
        *   secp256k1
        *   RSA
        *   NIST P-256
*   Algorithms and cryptographic agility
*   (possibly still more to do here - paused for time reasons)


## Applicable standards - inventory and discussion


### Existing standards



*   
*   
*   
*   
*   


### Gaps in existing standards and corresponding recommendations



*   
*   
*   
*   
*   


## DID-specific standards content


### Key representation


### Signature representation


### Key usage

From DID-Spec:

There is an open issue in the DID-Spec where there is a gap in interoperability.  Implementers do not know how to declare how keys are intended to be used. 

Suite names such as "RSAAuthentication2018" conflate a key type and a key purpose.  There was agreement that these should be decoupled.


```
{
  "@context": "https://w3id.org/did/v1",
  "id": "did:example:123456789abcdefghi",
  "publicKey": [{
    "id": "did:example:123456789abcdefghi#keys-1",
    "type": "RsaVerificationKey2018",
    "owner": "did:example:123456789abcdefghi",
    "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
  }],
  "authentication": [{
    // this key can be used to authenticate as DID ...9938
    "type": "AuthenticationSuite2018",
    "publicKey": "did:example:123456789abcdefghi#keys-1"
  }],
  "service": [{
    "type": "ExampleService",
    "serviceEndpoint": "https://example.com/endpoint/8377464"
  }]
}
```


Restructured by Mike Jones:


```
{
  "@context": "https://w3id.org/did/v1",
  "publicKey": [{
    "jwk": {
	"kty": "RSA",
	"e": …
	"n": …
	"kid":  "did:example:123456789abcdefghi#keys-1",
    	"owner": "did:example:123456789abcdefghi",
	...
}
  }],
  "authentication": [{
    // this key can be used to authenticate as DID ...9938
    "kid": "did:example:123456789abcdefghi#keys-1"
  }],
  "service": [{
    "type": "ExampleService",
    "serviceEndpoint": "https://example.com/endpoint/8377464"
  }]
}
```



## Parking Lot



*   [Object capabilities](https://w3c-ccg.github.io/ocap-ld/) - enables constrained and delegated authorization to resources
*   
*   
*   
*   
*   

<!-- GD2md-html version 1.0β12 -->
