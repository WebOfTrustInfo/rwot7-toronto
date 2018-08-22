# SmartAuth
***Smart Authorization for Self-Sovereign Storage***

by Manu Sporny, Dave Longley, Chris Webber, and Ganesh Annan - ***Digital Bazaar***

As self-sovereign technologies gain marketshare, the question of who,
when, and how people can access your personal or corporate information
becomes increasingly important. The existence of
[Decentralized Identifiers](did-primer.md),
[Verifiable Credentials](verifiable-credentials-primer.md), and
[Object Capabilities](https://w3c-ccg.github.io/ocap-ld/)
enable new types of smarter access control to your information.

The concept covered in this document can be expressed by a simple analogy.
Imagine that you have invited a couple to visit for the weekend and offer
them the spare room in your home. You only have one key and you give
it to them to come and go as they please. In technical terms, you have
just provided an object capability, the key to your home, to them. You know
what this key opens (the front door) and doesn't open (the locked safe in your
room). You know that they can use the key now, and that they won't be able
to use the key after they return it to you. The couple is free to hand the
key off between each other without asking for your permission.

The analogy above is very close to the way many of us would like to provide
access to our personal and corporate data. The problem is that there are
technologies that do some of the things above well while failing miserably
at protecting our data in other ways. While this paper is not intended to go
into the
[confused deputy](https://en.wikipedia.org/wiki/Confused_deputy_problem) or
[ambient authority](https://en.wikipedia.org/wiki/Ambient_authority)
issues created by most server security systems today, it does propose a
simple, concrete example of a self-soverign storage authorization system.

## Introduction

At the heart of all access control systems is the following question:

*What is the safest way to give other people access to the data on this system?*

This document introduces a new access control mechanism for websites called
**SmartAuth** that combines self-soverign technologies in a way that avoids
previous pitfalls created by approaches such as
[Access Control Lists](https://en.wikipedia.org/wiki/Access_control_list),
[Role Based Access Control](https://en.wikipedia.org/wiki/Role-based_access_control), and
[Bearer Tokens](https://stackoverflow.com/a/25843058). In doing so, it avoids
perennial security issues such as the
[confused deputy](https://en.wikipedia.org/wiki/Confused_deputy_problem)
problem and goes quite far in mitigating
[ambient authority](https://en.wikipedia.org/wiki/Ambient_authority) issues.

## Enabling Technologies

As a great deal of the Web is powered by HTTP web servers, the solution is
intended for client to server and server to server communication over the
[HTTP protocol](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)
as this will most likely be the common interface used by
many self-soverign storage servers.

The approach described in this paper also utilizes the
[Signing HTTP Messages](https://tools.ietf.org/html/draft-cavage-http-signatures-10)
specification to perform digital signatures on HTTP headers.

The
[Object Capabilities for Linked Data](https://w3c-ccg.github.io/ocap-ld/)
specification is also leveraged for the expression of object capabilities
utilized by the self-sovereign storage server.

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
    // the type of digital signature
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
object-capability: type="application/ld+json", ocap=BASE64(OCAP_DOCUMENT),
  action=BASE64("ReadDocument")
authorization: Signature keyId="did:v1:z279m2...Xk8aC#ocap-invoke-key-1",
  headers="object-capability date host (request-target)",
  signature="P26kEk...o0rBQ=="
```

The first set of lines beings a standard HTTP/2 request:

```http
:method: GET
:scheme: https
:authority: example.com
:path: /data/puppies.jpg
date: Tue, 21 Aug 2018 21:38:35 GMT
```

The `object-capability` header specifies the base64 encoded object capability
(via `ocap`), the MIME Type of the encoded information (via `type`) and the
base64-encoded action that is being invoked:

```
object-capability: type="application/ld+json", ocap=BASE64(OCAP_DOCUMENT),
  action=BASE64("ReadDocument")
```

The `authorization` header specifies that a signature-based authorization is
being attempted, identifies the key (via `keyId`) that is being used for the
authorization, the `headers` that are being signed, and finally provides the
value of `signature`:

```
authorization: Signature keyId="did:v1:z279m2...Xk8aC#ocap-invoke-key-1",
  headers="object-capability date host (request-target)",
  signature="P26kEk...o0rBQ=="
```

The mechanism provided in this section is almost completely self-contained.
The only network access needed is to fetch the keys associated with the
Decentralized Identifiers.

The algorithm for checking the object capability invocation is roughly the
following:

1. Perform HTTP Signature verification on the HTTP headers.
2. base64 decode the object capability.
3. Perform JSON-LD Signature verification on the object capability.
4. Determine if the entity that delegated the object capability is authorized
   to do so. Perform this step repeatedly all the way up the object capability
   chain if `parentCapability` exists.
5. base64 decode the action and ensure that the action is listed in the
   object capability.

If all of these steps complete successfully, then the entity invoking the
object capability is authorized.

## Alternative Representations

It is possible for a more compact representation to be expressed. For example:

```
object-capability: type="application/ld+json",
  ocapMultihash=b250100a4ec6f1629e49262d7093e2f82a3278,
  actionMultibase=BASE58BTC("ReadDocument")
```

This approach replaces the direct embedding of the object capability with
a cryptographically equivalent mechanism that does not require the
transmission of the entire object capability.

While Decentralized Identifiers are used throughout this document, it is
possible to not use any decentralized identifiers and instead rely on purely
HTTP URL-based identifiers and storage for cryptographic key information.
Similarly, pure cryptographic identifiers may be used instead of
Decentralized Identifiers or HTTP URL-based identifiers.

## Next Steps

The authors of this document would like to explore the following items at
the upcoming RWoT7 event:

* Would it be possible to re-use this specification for the HIE of One
  Use Case as well as the Identity Hubs use case?
* Are there different representations of the message flow above that should
  be explored?
* What are the security considerations for this protocol?
* What are the various ways this protocol could be attacked?
