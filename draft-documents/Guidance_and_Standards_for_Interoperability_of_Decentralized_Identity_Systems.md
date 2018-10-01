<!----- Conversion time: 2.636 seconds.


Using this Markdown file:

1. Cut and paste this output into your source file.
2. See the notes and action items below regarding this conversion run.
3. Check the rendered output (headings, lists, code blocks, tables) for proper
   formatting and use a linkchecker before you publish this page.

Conversion notes:

* GD2md-html version 1.0β12
* Fri Sep 28 2018 13:55:05 GMT-0700 (PDT)
* Source doc: https://docs.google.com/a/cloudcompass.ca/open?id=1tDX6LXJn6KITKIvNbbexHfcdWZ9z9TCElC5cZygaacw
----->



# Guidance and Standards for Interoperability of Decentralized Identity Systems

Source document: https://docs.google.com/a/cloudcompass.ca/open?id=1tDX6LXJn6KITKIvNbbexHfcdWZ9z9TCElC5cZygaacw

### Authors:  David Bissessar, Daniel Buchner, Dan Burnett, Stephen Curran, Kyle Den Hartog, Michael B. Jones, Christian Lundkvist, Olena Mitovska, Manu Sporny


### Contributors:  Mike Varley, Arturo Manzaneda


## Abstract [Mike J]

Use of applicable standards is critical to the interoperability of decentralized identity systems.  This paper provides high-level guidance for architects and builders of interoperable decentralized identity systems (including data models, cryptographic requirements, and data representations).  It inventories existing and emerging standards appropriate for building these systems, identifies gaps in the standards, and proposes means to fill them.  These include standards for representation of cryptographic inputs and outputs.  The final section focuses on issues specific to systems using DIDs and the DID specification itself.


## Introduction [Dan B.]

For several years now, the Rebooting the Web of Trust (RWoT) workshops have brought together specification writers, software developers, futurists, and other visionaries to discuss the needs of and possible solutions for decentralized identity.  Over the course of these workshops, the community that developed has gradually come to some realizations and, ultimately, guiding principles for any solutions to the challenges of providing such identity mechanisms.

However, the community has lacked not only a clear exposition of these principles but their relationship to the standards and other more formal work in this space.  By providing both, this document can serve as a quick guide to standards, guidelines, and best practices for both new members of the RWoT community and, more generally, architects, specification developers, and code developers who are interested in developing or working with DID-enabled decentralized identity systems.  Additionally, this document makes a first attempt at indicating where such standards and guidelines may have gaps that need to be filled for the ecosystem to reach its full potential. Intentionally, this document very carefully does not mandate behavior or constrain future innovation but rather aims to establish an overall framework within which innovative identity solutions can be developed while still encouraging interoperability in a manner that aligns well with a variety of global and regional regulatory requirements.

The document is structured into the following three main sections:  Guiding Principles, Applicable Standards, and DID-Specific Standards Content.  In the first section, Guiding Principles, the document provides high-level guidance with respect to data models, cryptographic requirements, and data representations.  The second section, Applicable Standards, inventories existing and emerging higher-level or general standards, both technical and regulatory, that are appropriate for these systems, and identifies a set of current gaps in those sets of standards, along with proposals for filling those gaps.  The final section, DID-Specific Standards Content, then does the same for the special case of systems using DIDs and the DID specifications themselves.


## Guiding Principles [Dan B.]

(TBD general text)


### Data Model [Manu, Olena, Arturo]

The guidelines below are intended to help ensure that an identity solution can support various identity types and accommodate a wide range of real-life transactions, interactions and use cases for identity. They will also help to align with other emerging regulatory standards for identity such as GDPR and Pan-Canadian Trust Framework.



*   Open world assumption - you can make statements about anything

We desire to empower people and organizations to control their identifiers (e.g., "My identifier is 1234") and make claims about themselves and other entities (e.g. "1234 knows Jane."). The types of claims one should be able to make are unbounded, just as it is in the real world. This requires a way of expressing data in what is called an "Open World", as opposed to a "Closed World".

Closed World systems are easier to build, secure, and write programs for. Most computing today happens in Closed World systems. Open World systems are much more powerful and expressive. They are also much harder to build, secure, and write programs for. 

Examples of Open World systems include the Internet and the Web. These systems are decentralized and inclusive which enables innovation at the edges of the network. These are some of the same features we desire for the ecosystem that we are building and are a few of the reasons we make an Open World assumption.

There are two types of claims - self-asserted (i.e. I claim that I am a football fan) and verifiable (I claim that my name is Joe and the birth registry can confirm it). The value of each claim type is determined by a relying party's (aka identity consumer) needs. A football fan club is ok with accepting a self-asserted claim that I am a football fan, but a mortgage company will want to see a government-backed identity.

A good identity solution should be able to support both claim types.



*   Support all three core identity types

Identities are entities within an identity network that can interact and transact with each other. There are three core identity types:



    *   Individual
    *   Legal (aka business identity)
    *   Device

It is important to understand that only the first identity  - individual - can act on its own. The two other identity types must have links to (one or more) individual identities to represent them and their actions in a legal capacity. More on delegation of authority - implicit and explicit - below.

An individual identity must be assigned to a real person (and not to a computer simulation) and be unique within the population serviced by the identity solution. 



*   Data structures representing entities can have local data and/or links to other entities

Open World systems are unbounded, meaning that things have relationships to other things and those relationships can extend far beyond the system that you are currently programming for. In other words, data structures representing entities can have local data as well as links to other entities. One way of representing this data is called a graph. A graph is a mathematical term for a set of nodes that are connected by lines (also known as edges). 

The Web is naturally a graph-based data model. Web pages can be thought of as nodes, and they are connected by hyperlinks to other web pages. A large amount of human knowledge is encoded on the Web as a graph of web pages.

Concepts and knowledge on the Web can also be expressed as a graph-based data model. In fact, Google's Knowledge Graph, Facebook's Social Graph, and Microsoft's Bing search engine all rely heavily on graph-based data models to answer search queries. It is a natural representation format for Open World knowledge.

While there are other sorts of data structures such as lists, directed trees, and relational tables, only the graph is capable of efficiently expressing human knowledge and relationships. We are interested in building an ecosystem that is capable of expressing a graph of human knowledge and relationships. We desire to put people in control of their own graph of information and enable them to combine independent graphs of information together to say more.

As mentioned above, some identities can be represented by other identities, legal organizations are controlled by authorized individual representatives, lawyers represent their clients through the power of attorney, parents and guardians act on behalf of children and adults who cannot represent themselves legally for various reasons. In other cases, people voluntarily grant access to other people to access certain parts of their identity as it is often a case in families and marriages. Delegation of authority can be explicit - an identity can temporarily grant permission to another identity to represent it , or implicit - an individual identity is required to register a "device" identity, a legal identity has to be linked to an individual that will represent it and take actions of its behalf.

An identity solution must be able to support delegation of authority between identities. We recommend checking out [Object Capabilities Specification](https://w3c-ccg.github.io/ocap-ld/) for the direction on technical implementation of the relationships and support of delegation of authority.

Relationships between identities can be bidirectional and a separate of rules should govern delegation of authority for each direction. For example, a child gives his parent permission to act on behalf of their identity but cannot act on behalf of the parent's identity.

Delegation of authority can only apply to specific identity attributes or be valid for specific  actions only. For example, an elderly person grants authority to their caregiver to access medical records but not the financial information.



*   Entities and relationships can be defined to be interpreted in an unambiguous manner
*   Inclusive of the use of schemas for data as defined in particular application contexts
*   Enables decentralized innovation without need for central coordination between projects
*   Compatibility with existing ecosystems and standards that follow these principles


### Syntaxes [Stephen C.]

As a guiding principle for Decentralized Identity System interoperability, a then-current, developer-friendly de facto standard data syntax should be used. That standard is currently [JSON](https://tools.ietf.org/html/rfc8259) and it should be used. However, we recognize that the appropriate interoperability data syntax standard will change over time and that evolution should be embraced. The remainder of this section assumes JSON where appropriate.

Where necessary, Base64url encoded JSON should be used for data representation purposes. There are other formats that play a similar role to Base64url encoding that might be used.

Some Cryptographic operations like hashing and signing depend on the target data not changing during serialization, transport, or parsing. Canonicalization of the data is an approach to addressing this dependency and some systems use such techniques in those situations. Others find that the complexity of canonicalization actually increases the challenges in completing the operations and so choose not use those techniques. This is an area that will evolve as the challenges in using or not using canonicalization shift over time.

The data syntax must be transport agnostic - it must be possible to transport data represented using the syntax via any commonly available transport mechanism. An encoding/decoding process may be required for some transport mechanisms.

To promote interoperability, Decentralized Identity Systems must be able to easily express publicly available information: credential schema, organizational credentials, public relationships between individuals and organizations, etc. This sort of information is already largely supported and consumed by search engine projects, such as [schema.org](https://schema.org/). To support this, the data syntax must be able to be presented in directly in HTML pages using `<script>` tags with a corresponding mime type (e.g., `<script type="application/ld+json">`). This provides a simple way to present information with minimal reprocessing.



*   [JSON](https://tools.ietf.org/html/rfc8259) as the default
*   Base64url encoded JSON (or other formats) when necessary for data representation purposes
*   Some systems use canonicalization to create the signing input; some systems base64url encode content to sign it (Group specifically notes this is tabled for now and not agreed yet) 
*   Should be possible to transport representations over different transports, including HTTP (transport agnostic)
*   Should be able to include representations in HTML pages using `<script>` tags


### Cryptographic requirements [Mike J., Manu, David]

Cryptographic interoperability allows the exchange of reliable and confidentiality identities and claims across different vendor systems.  Due to the exacting requirements by the organizational and individual stakeholders of identity systems the cryptographic needs on DID and VC document are cross-cutting. Without cryptographic interoperability, signatures produced by one system are not verifiable by the other system, and as such no certainty can be obtained on source or integrity of information. As such the strongest attestation from a source system loses its reliability.  Similarly, without interoperable a confidential claim encrypted by one system will never be intelligibly decrypted by the intended recipient. 

This section will discuss cryptographic interoperability by looking at the following components. First, we will discuss 



*   Digital signatures
    *   Also sets of digital signatures, some of which may be dynamically added to
*   Encryption
*   HMACs
*   Some systems need representations of other kinds of mathematical proofs
    *   Including zero-knowledge proofs Satoshi proofs (BTCR uses this)
*   Nested cryptographic operations
*   Key representations
    *   Explicit key representation for commonly used keys
        *   Ed25519
        *   secp256k1
        *   RSA
        *   NIST P-256
*   Algorithms and cryptographic agility(possibly still more to do here - paused for time reasons)


## Applicable standards - inventory and discussion [Mike J., Mike V., Manu]


### Existing Standards [Mike J.]



*   JSON
*   JOSE ([JWS](https://tools.ietf.org/html/rfc7515), [JWE](https://tools.ietf.org/html/rfc7516), [JWK](https://tools.ietf.org/html/rfc7517), [JWA](https://tools.ietf.org/html/rfc7518), [CFRG Curves in JOSE](https://tools.ietf.org/html/rfc8037))
    *   [IANA JOSE Registries](https://www.iana.org/assignments/jose/jose.xhtml)
*   [JWT](https://tools.ietf.org/html/rfc7519)
    *   [IANA JWT Claims Registry](https://www.iana.org/assignments/jwt/jwt.xhtml)
*   JSON-LD
*   CBOR & COSE
*   WebAuthn & FIDO2
*   Algorithms and Key Representations:
    *   RSA, SHA-2, P-256, ED25519, AES-GCM


### Standards/Efforts in Progress [Mike J., Manu]



*   DID Spec + DID Method Specs
*   Verifiable Credentials
*   Credential Handler API
*   Credential Coordination Protocol
    *   [https://hackmd.io/9TuwUcHFTUq6Su_WYUH46Q](https://hackmd.io/9TuwUcHFTUq6Su_WYUH46Q) 
*   Linked Data Proofs/Signatures - RDF Dataset Normalization
*   LD Proof Suites / LD Signature Suites (includes ZKLang, PoW, PoK, Suites)
*   Identity Hubs
    *   [https://github.com/decentralized-identity/identity-hub/blob/master/explainer.md](https://github.com/decentralized-identity/identity-hub/blob/master/explainer.md) 
*   Multihash, Multicodec, Multibase, Multikey
*   IPFS
*   [DKMS](http://bit.ly/dkmsv3) 
*   DID Authenticated Encryption
    *   [https://hackmd.io/8onA9y7zSPGF4r5Rg17UAQ](https://hackmd.io/8onA9y7zSPGF4r5Rg17UAQ)
*   [Object capabilities](https://w3c-ccg.github.io/ocap-ld/) - enables constrained and delegated authorization to resources
    *   Olena described the Pan-Canadian Trust Framework, including verified relationships - for instance between organizations and people and parents and children
*   OpenID Connect
*   Token Binding


### Applicable existing standards and their gaps [Olena, Mike J., Arturo, Mike V.]


#### Algorithm Representations [Kyle]



*   Secp256k1 - Mike Jones has an Internet Draft
*   [ChaCha20-Poly1305_IETF](https://tools.ietf.org/html/rfc7539) - (AEAD)
*   XChaCha-Poly1305 - (AEAD)
*   X25519-XSalsa20-Poly1305 (public key authenticated encryption)
    *   This is the **box **function in the [nacl library](https://nacl.cr.yp.to/).
*   XSalsa20-Poly1305 (symmetric encryption + MAC)
    *   This is the **secretbox** function in the [nacl library](https://nacl.cr.yp.to/).
*   ECDH-SS+XS192KW


### Non-Technical Regulations and Standards

There are the number of non-technical standards that have emerged globally that aim to re-enforce the delivery of trusted, reliable, secure and privacy protected digital identity services. Depending on the jurisdiction where an identity solution operates, it has to demonstrate compliance with the local laws and regulations. However, in current days, companies with an online presence collects data for users from multiple jurisdictions and have to be aware of regulations in effect in each of these jurisdictions. Privacy and security requirements enforced by these regulations will have a direct impact on the design and technology choices for the identity solution. Some of the examples of the existing identity regulations and their potential implications for identity solutions are listed below:



*   Pan-Canadian Trust Framework

[The Pan-Canadian Trust Framework](https://diacc.ca/2016/08/11/pctf-overview/) (PCTF) establishes standards and guidelines for the delivery of trusted digital identity services for both the public and private sector in Canada.

The PCTF is being developed collaboratively by public and private sector stakeholders, recognizing that all parties have a role to play in building trusted digital identity services that will work across the Canadian digital economy for the benefit of Canadian citizens, businesses, non-profit and public services alike.

The Framework is in the early stages of development, the first public release is planned for the end of 2018. The framework puts emphasis on affirming user's consent before collecting or sharing any personal data.



*   European Union's General Data Protection Regulations (GDPR)

[GDPR](https://eugdpr.org/the-regulation/) is a regulation in EU law on data protection and privacy for all individuals within the European Union and the European Economic Area. It also addresses the export of personal data outside the EU and EEA areas, therefore, it applies to all companies processing the personal data of data subjects residing in the European Union, regardless of the company's location. This is one the strictest regulations and organizations in breach of GDPR can be fined up to 4% of annual global turnover or €20 Million (whichever is greater). 

Some of the key restrictions that may impact the design of the identity solution:



    *   Right to Access

Data subjects (aka identity owners) have the right to obtain confirmation from the holder of their data as to whether or not personal data concerning them is being processed, where and for what purpose. Therefore, the identity solution must ensure identity owners must have access their identity data easily, securely and at all times.



    *   Right to be forgotten support

Also known as Data Erasure, the right to be forgotten entitles the data subject to request the holder of his/her personal data to erase it, cease further dissemination of the data, and potentially have third parties halt processing of the data. Therefore, it is strongly recommended not to write any personally identifiable information into a persistent storage from where it cannot be erased (i.e. blockchain).



    *   Data Portability

GDPR introduces data portability – the right for a data subject to receive the personal data concerning them – which they have previously provided in a 'commonly use and machine-readable format' and have the right to transmit that data to another controller.

In order to ensure data portability, it is recommended to build an identity solution using open standards and interoperability guidelines and conventions that are stated in this document. 



    *   Privacy by Design

This provision aims to limit data being exchanges between an Identity Holder and a Verifier to a minimum set of attributes required to complete a transaction. A user should be able to select and share individual attributes within a credential. 



    *   Auditability

Audit trail is required to keep track of all uses and exchanges of personal data. It is important, however, to ensure that the logged data does not contain any personal or easily correlatable data.



    *   Consent
    *   TO BE CONTINUED
*   Links SSI & GDPR:
    *   [https://medium.com/evernym/is-self-sovereign-identity-ssi-the-ultimate-gdpr-compliance-tool-9d8110752f89](https://medium.com/evernym/is-self-sovereign-identity-ssi-the-ultimate-gdpr-compliance-tool-9d8110752f89)
*   Olena suggested **conformance criteria** for decentralized identity networks, as in the Pan-Canadian framework to make it easier for the network developers to assess themselves for compliance with the standards.


## DID-Specific Standards Content


### Key Representations [Mike J., Christian L., Dave Longley]

A number of different key representations is currently in use by DID Methods as well as existing key representation standards that can be utilized. In the DID-specific context key representations are mainly used in DID documents to represent the keys that are used by a specific DID. We list them here and discuss briefly where they are used.



*   [JWK](https://tools.ietf.org/html/rfc7517)
    *   This IETF standard is used by the [sidetree](https://github.com/decentralized-identity/sidetree-core) DID method being developed by Microsoft.
    *   The uPort DID method is looking to use JWKs as soon as secp256k1 curve keys are supported.
*   PEM-encoded
    *   Currently supported by the Veres One DID method.
    *   Can be used with output from OpenSSL
*   Base58BTC encoded Ed25519 public key bytes
    *   Used by the Sovrin DID method
    *   [https://en.m.wikipedia.org/wiki/Base58](https://en.m.wikipedia.org/wiki/Base58)
*   base64 representation of curve25519 public key bytes (for encryption)
    *   Used by uPort to represent encryption keys
    *   Public keys are 32 bytes long (see for instance the [tweet-nacl](https://github.com/dchest/tweetnacl-js) library) and can be represented as base64 strings.
*   Hashes of secp256k1 curve points w/ data in signature enabling public key recovery (Examples: [Bitcoin Addresses](https://en.bitcoin.it/wiki/Technical_background_of_version_1_Bitcoin_addresses) & [Ethereum Addresses](https://ethereum.stackexchange.com/questions/3542/how-are-ethereum-addresses-generated))
*   IPFS key representation
*   COSE_Key (not currently being used by DID implementations)


### Signature & Encryption Representations [Mike J., Christian L., Dave Longley]



*   [JWS](https://tools.ietf.org/html/rfc7515), [JWE](https://tools.ietf.org/html/rfc7516)
*   Sovrin/Evernym Zero Knowledge Camenisch/Lysyanskaya signature (no spec?)
*   LD Signatures & LD Proofs
*   COSE_Signature (not currently used by DID implementations)


### Proof Representations [Manu, David B.]



*   Equihash
*   Cuckoo Cycle
*   LD Proofs
*   Merkle Proofs (no spec?)
*   Accumulators (Revocation initially)


### Key Usage [Daniel B., Manu]

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



### Service Endpoints [Daniel Buchner, Kyle, Arturo, Dave B.]



*   There are no specifications for service endpoints [Dave B]
*   Identify some of the initial service endpoint descriptions that we want to have.
    *   Microblogging (ActivityPub, etc.)
    *   Data Storage Protocol
    *   Identity Hub personal datastores 
    *   Sovrin Protocol
*   Kyle: Listing service endpoints in the DID doc can enable correlation
*   Arturo & Kyle: Service endpoints should reflect transports - not application-level services


### Topics and Advanced Reading References:



*   [The Role of Standards in Accelerating Innovation](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/The_Role_of_Standards_in_Accelerating_Innovation.md)
*   [DIDDoc Conventions for Interoperability](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/diddoc-conventions-for-interoperability.md)
*   [RWoT Crypto and Data Model Requirements](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/crypto-data-model-requirements.md) 


## Parking Lot



*   There isn't a representation for elliptic curve group parameters

<!-- GD2md-html version 1.0β12 -->
