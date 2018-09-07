# The Role of Standards in Accelerating Innovation

Use of standards accelerates innovation.  Oxymoron?  Not at all!

By building upon widely implemented industry standards, innovators are freed to focus on the innovative aspects of their work, letting existing standards do the heavy lifting for the needs of their projects that standards already address.  The potential for use of cryptographic and digital identity standards in decentralized systems illustrates this point.

Microsoft is deeply engaged with numerous innovators in building decentralized public-key based identity systems prototypes and is excited at the possibilities.  We love what’s happening and the way innovators are coming together to enable new digital identity possibilities.  All of us want these possibilities to achieve their promise as quickly as possible.  Integrating and maintaining interoperability with existing identity management systems – all based on standards – will be key to accelerating this process.

Standards play a huge role in enabling innovation in decentralized public-key based identity systems.  By using widely adopted industry cryptographic and data representation standards as an agreed framework, innovators in this space can achieve laser focus on the unique value that they’re adding.  Furthermore, use of standards, where applicable, will facilitate faster adoption as decentralized public-key based systems move from prototypes to production systems.

To make things concrete, we believe that use of the following standards will accelerate innovation when building decentralized identity systems:

- JWK \[[RFC 7517](https://tools.ietf.org/html/rfc7517)\] is a widely deployed representation of cryptographic keys.
- JWS \[[RFC 7515](https://tools.ietf.org/html/rfc7515)\] is a simple, flexible representation of digital signatures.
- JWE \[[RFC 7516](https://tools.ietf.org/html/rfc7516)\] is a no-nonsense JSON-based representation encrypted content.
- JWA \[[RFC 7518](https://tools.ietf.org/html/rfc7518)\] defines an initial set of algorithms for use with all the above.
- JWT \[[RFC 7519](https://tools.ietf.org/html/rfc7519)\] is a simple, powerful, widely deployed representation of claims (including that JWT is often used for representing verified claims).
- CBOR \[[RFC 7049](https://tools.ietf.org/html/rfc7049)\] defines a compact binary data representation, which can be used as an alternative to JSON \[[RFC 8259](https://tools.ietf.org/html/rfc8259)\] when size is at a premium.
- COSE \[[RFC 8152](https://tools.ietf.org/html/rfc8152)\] is the CBOR equivalent of JWK, JWS, JWE, and JWA.
- CWT \[[RFC 8392](https://tools.ietf.org/html/rfc8392)\] is the CBOR equivalent of JWT, providing a binary claims representation.
- [W3C Web Authentication](https://www.w3.org/TR/webauthn/) and [FIDO Client to Authenticator Protocol (CTAP)](https://fidoalliance.org/specs/fido-v2.0-id-20180227/fido-client-to-authenticator-protocol-v2.0-id-20180227.pdf) employ the building blocks above for public-key based authentication.

Great standards not only solve current use cases but enable solving new ones.  The JOSE [RFC 7515-7518] and JWT [RFC 7519] standards and their binary equivalents explicitly enable innovation while still using the standards.  How is this possible?

While JWA \[[RFC 7518](https://tools.ietf.org/html/rfc7518)\] defined how to a set of commonly-used cryptographic algorithms with JWS, JWE, and JWK, it also established the [IANA JOSE Algorithms registry](https://www.iana.org/assignments/jose/jose.xhtml) to enable additional algorithms to be used for new use cases, without having to revise the JOSE standards.  For instance, \[[RFC 8037](https://tools.ietf.org/html/rfc8037)\] defined how to use new elliptic curves with JWS, JWE, and JWK.  Microsoft is currently working with decentralized systems implementers on [registering the secp256k1 algorithm](https://tools.ietf.org/html/draft-jones-webauthn-secp256k1-00) for use with JWS and COSE.  And when new cryptographic algorithms are invented, new identifiers can and will be registered for them in the [IANA JOSE Algorithms registry](https://www.iana.org/assignments/jose/jose.xhtml).

Microsoft is building proof-of-concept decentralized public-key based identity systems using these robust industry standards.  We encourage others to accelerate innovation by doing the same.  We’re excited to see what we’ll achieve together!

<hr/>

Note:  A verstion of this position statement was posted by [Alex Simons](https://twitter.com/Alex_A_Simons), Microsoft VP of Program Management for Identity, at [The role of standards in accelerating innovation](https://cloudblogs.microsoft.com/enterprisemobility/2018/08/29/the-role-of-standards-in-accelerating-innovation/).

**Author:** Michael B. Jones [https://self-issued.info/](https://self-issued.info/), [@selfissued](https://twitter.com/selfissued)
