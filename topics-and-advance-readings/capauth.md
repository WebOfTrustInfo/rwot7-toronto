# CapAuth
***Smarter Authorization for Self-Sovereign Storage***

by Manu Sporny, Dave Longley, Chris Webber, and Ganesh Annan - ***Digital Bazaar***

As self-sovereign technologies gain marketshare, the question of who,
when, and how people can access your personal or corporate information
becomes increasingly important. The existence of
[Decentralized Identifiers](did-primer.md),
[Verifiable Credentials](verifiable-credentials-primer.md), and
[Object Capabilities](https://w3c-ccg.github.io/ocap-ld/)
enable new types of smarter access control to your information.

While the technologies listed above may seem daunting to understand, the
concept is easily understandable through the following analogy.
Imagine that you have invited friends to visit for the weekend and offer
them the spare room in your home. You only have one key and you give
it to them to come and go as they please. In technical terms, you have
just given them an object capability, which is the key to your home. You
instinctively know a number of things about this key:

1. Authority - you know what this key opens (the front door) and
   doesn't open (the locked safe in your room).
2. Restrictions - You know that they can use the key now, and that they
   won't be able to use the key after they return it to you.
3. Delegation - The couple is free to hand the key off between each other
   without asking for your permission.

The analogy above is exactly how we protect the most important parts of our
property be it access to a bank vault or use of our personal vehicles.
It is also very close to the way many of us would like to provide
access to our personal and corporate data. The problem is that there are
technologies that do some of the things above well while failing miserably
at protecting our data in other ways. This paper does not go into detail
when explaining the benefits of
[Decentralized Identifiers](did-primer.md),
[Verifiable Credentials](verifiable-credentials-primer.md), or
[Object Capabilities](https://w3c-ccg.github.io/ocap-ld/). It also does not
attempt to explain the
[confused deputy](https://en.wikipedia.org/wiki/Confused_deputy_problem) or
[ambient authority](https://en.wikipedia.org/wiki/Ambient_authority)
issues created by most server security systems today. If these concepts are not
familiar to readers, they are urged to learn about them before reading the
rest of this document.

## Introduction

At the heart of all access control systems is the following question:

*What is the safest way to give other people access to the data on this system?*

This document introduces a new access control mechanism for websites called
**CapAuth** that combines self-soverign technologies in a way that avoids
previous pitfalls created by approaches such as
[Access Control Lists](https://en.wikipedia.org/wiki/Access_control_list),
[Role Based Access Control](https://en.wikipedia.org/wiki/Role-based_access_control), and
[Bearer Tokens](https://stackoverflow.com/a/25843058). In doing so, it avoids
perennial security issues such as the
[confused deputy](https://en.wikipedia.org/wiki/Confused_deputy_problem)
problem and goes quite far in mitigating
[ambient authority](https://en.wikipedia.org/wiki/Ambient_authority) issues.

## Enabling Technologies

The Web is built on the
[HTTP protocol](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol).
Since this is the most common interface that applications use to communicate
over the Internet, this document uses the same mechanism to provide access to
self-soverign storage servers.

Digital signatures on HTTP Headers are a core requirement of this protocol.
We use the
[Signing HTTP Messages](https://tools.ietf.org/html/draft-cavage-http-signatures-10)
specification, which benefits from a
[healthy number of implementations](https://github.com/w3c-dvcg/http-signatures/issues/1).

The final requirement is a concrete syntax for expressing object capabilities.
We use the
[Object Capabilities for Linked Data](https://w3c-ccg.github.io/ocap-ld/)
specification to express object capabilities utilized by the self-sovereign
storage server.

## Providing an Object Capability

The first step is to express an object capability. The concrete syntax we use
is the one specified in
[Object Capabilities for Linked Data](https://w3c-ccg.github.io/ocap-ld/).
Comments before each line explain the purpose of the property:

```javascript
{
  // specify the vocabulary in use for the document
  '@context': "https://w3id.org/ocap/v1",
  // the identifier for the object capability
  id: "urn:uuid:443731c2-3ba1-425e-9d0f-d4532ac6c91d",
  // the type of object (which is a capability)
  type: "Capability",
  // the action the capability is allowing - read a document on the server
  allowedAction: "ReadDocument",
  // which set of keys should be allowed to invoke the capability
  invoker: "did:v1:z279m2...Xk8aC",
  // the document that this capability operates on
  invocationTarget: "https://example.com/data/puppies.jpg",
  // the digital signature by the authority granting the capability
  proof: {
    // the digital signature suite that was used to create this signature
    type: "Ed25519Signature2018",
    // the reason the proof was generated - to delegate a capability
    proofPurpose: "capabilityDelegation"
    // when the digital signature was created
    created: "2018-08-09T17:49:54Z",
    // the key that created the digital signature
    creator: "did:v1:nym:z2SL3...ULUX#ocap-delegate-key-1",
    // the JSON Web Signature encoded signature value
    jws: "eyJhbGci...WP5yAA",
  }
}
```

The object capability above is then published or provided to an entity.
Note that it's not necessarily important where the object capability is
published as long as the invoker of the object capability and the server both
have access to the same document. This means that the object capability
may be placed on a web server, on a blockchain, on a distributed file system,
or stored locally and handed directly to the server during invocation.

## Invoking an Object Capability via HTTP

Once the object capability above has been published, it may be invoked. An
object capability is typically invoked during the process of authorization
when accessing a resource, such as retrieving a document from a server over
the HTTP protocol.

The rest of this section will use the following example:

```http
:method: GET
:scheme: https
:authority: example.com
:path: /data/puppies.jpg
date: Tue, 21 Aug 2018 21:38:35 GMT
object-capability: type="ocapld",
  ocap=BASE64URL(OCAP_DOCUMENT),
  action=BASE64URL("ReadDocument")
authorization: Signature
  keyId="did:v1:z279m2...Xk8aC#ocap-invoke-key-1",
  headers="object-capability date host (request-target)",
  signature="P26kEk...o0rBQ=="
```

The first set of lines is the start of a standard HTTP/2 request:

```http
:method: GET
:scheme: https
:authority: example.com
:path: /data/puppies.jpg
date: Tue, 21 Aug 2018 21:38:35 GMT
```

The `object-capability` header specifies the base64url-encoded object capability
(via `ocap`), the MIME Type of the encoded information (via `type`) and the
base64url-encoded action that is being invoked:

```
object-capability: type="ocapld",
  ocap=BASE64URL(OCAP_DOCUMENT),
  action=BASE64URL("ReadDocument")
```

The `authorization` header specifies that a signature-based authorization is
being attempted, identifies the key (via `keyId`) that is being used for the
authorization, the `headers` that are being signed, and finally provides the
value of `signature`:

```
authorization: Signature
  keyId="did:v1:z279m2...Xk8aC#ocap-invoke-key-1",
  headers="object-capability date host (request-target)",
  signature="P26kEk...o0rBQ=="
```

The mechanism provided in this section is almost completely self-contained.
The only network access needed is to fetch the keys associated with the
Decentralized Identifiers, a step that may benefit from appropriate caching.

The algorithm for checking the object capability invocation is roughly the
following:

1. Perform HTTP Signature verification on the HTTP headers.
2. base64 decode the object capability.
3. Perform JSON-LD Signature verification on the object capability.
4. Perform OCAP-LD verification on the object capability. This step
   determines if the entity that invoked the object capability is authorized
   to do so. Perform this step repeatedly all the way up the object capability
   chain if `parentCapability` exists.
5. base64 decode the action and ensure that the action is listed in the
   effective object capability.

If all of these steps complete successfully, then the entity invoking the
object capability is authorized. The processing speed of the steps above may
increased by caching certain outputs depending on the risk profile of the
application using CapAuth.

## Alternative Representations

It is possible for a more compact representation to be expressed. For example:

```
object-capability: type="url-ocapld",
  ocap="https://example.com/ocaps/e49262"
  ocapMultihash=zZeM3u9YD2obamakRCRczRzJza3,
  actionMultibase=z2ZBdVRTwAVvVSfUZh
```

This approach replaces the direct embedding of the object capability with
a cryptographically equivalent mechanism that does not require the
transmission of the entire object capability.

## Extensibility

There are a number of extensibility mechanisms that have been conceived of in
this document.

* While the expression of the object capability is currently in OCAP-LD, other
  expression formats, such as CBOR, are possible via the use of the `type`
  field.
* The use of multihash enables the extensible use of different
  hashing mechanisms such as SHA2, SHA3, and Blake using the same encoding
  scheme. This is done at the cost of implementation complexity.
* The use of multibase enables the extensible use of different encoding
  mechanisms such as Base64-URL and Base58-BTC. This is done at the cost of
  implementation complexity.
* While we use Decentralized Identifiers to identify keys and invokers,
  other identifiers are also possible. Every Decentralized Identifier-based
  URL can be replaced with an HTTP URL-based identifiers without loss of
  functionality to the proposal. Similarly, pure Cryptographic Identifiers,
  such as ed25519 public keys, may be used instead of Decentralized
  Identifiers. Implementers should be aware that using different identifiers
  for cryptographic information creates different privacy and security
  concerns.

## Next Steps

The authors of this document would like to explore the following items at
the upcoming RWoT7 event:

* Would it be possible to reuse this specification for the Identity Hubs
  use case as well as the HIE of One use case?
* Are there different representations of the message flow above that should
  be explored?
* What are the security considerations for this protocol?
* What are the various ways this protocol could be attacked?

## Acknowledgements

Portions of the work on this document have been funded by the United States
Department of Homeland Security's Science and Technology Directorate under
contract HSHQDC-17-C-00019. The content of this specification does not
necessarily reflect the position or the policy of the U.S. Government and
no official endorsement should be inferred.
