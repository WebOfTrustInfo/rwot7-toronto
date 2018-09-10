# Decentralized Identity – Hub Authentication & Message Encryption
In decentralized identity, an identity Hub is the off-chain storage location for all data owned by a DID. This may include user profile info, attestations, activity history, and much more. To keep this data secure, any request requires that a caller authenticate to a DID’s Hub. 

## Scope of this document
DID authentication is a term primarily used to describe the process by which an identity owner (often a user) proves their identity to a relying party. This process can take many different forms, several of which are described in DIF’s working DID auth document .

This document describes an implementation of DID authentication in one specific topology: a client authenticates to an Identity Hub, which is running as a web service exposed on the public internet over HTTP.

![](https://i.imgur.com/uCg9TkV.png)
 
We assume that the client has access to a credential (a private key) that is linked to the Hub owner’s DID via their DDO.

Note that in most scenarios, the client will not have access to the identity owner’s keys. We envision that the client would use its own dedicated key pair that is somehow resolvable by the hub and authorized to access the owner’s data. Provided such keys exists, the client could use the protocol in this document to authenticate to the hub.

To keep things simple, we’ll leave this problem out of scope and address it in another document. Moreover, all Hub authorization logic is omitted from this document. This document only describes how the Hub securely identifies the caller, not what access the caller is granted.

A simple use case that captures the scope of this document is:

> Alice has just registered her first DID by downloading & installing a popular user agent mobile application. Her user agent has access to her new DID’s private key. After registering, Alice wants to add some simple profile data to her Hub. She inputs a name and a photo into her user agent app, which then writes each to Alice’s Hub.

## Design goals

In addition to securing data that resides in the Hub, user’s data should be protected while in transit to/from the Hub, even when the HTTP channel used to transmit data is compromised. This means not only should the Hub authenticate the client, but also:

- the client should authenticate the Hub, so it does not submit user data to malicious parties.
- data exchanged between the client and Hub should be encrypted.

These are the basic goals of TLS (as well as message integrity). Unfortunately, TLS and its dependencies have proven to be insecure against certain attacks. Consider the following attack:

- A man-in-the-middle compromises the DNS servers/records used by the client, as well as the certificate authority used by the server.
- The client navigates to a URL and is routed to the attacker’s server.
- The attacker’s server returns a certificate, signed by a compromised CA.
- The client negotiates a shared secret with the server and begins sending encrypted messages.
- The server receives the message and decrypts it.
- The server forwards the request to the legitimate URL, receives a response, and returns that response to the client.

There have been many documented cases (see appendix) where certificate authorities have failed to protect users from such an attack, resulting in widespread violations of user privacy.

By circumventing the use of DNS and CAs, our DID authentication protocols can protect against their vulnerabilities while providing many of the same security and privacy guarantees of traditional TLS.

In designing Hub authentication, we strive to meet the following goals:

1.	The authentication scheme provides data security and privacy that is on-par or stronger than the current status quo based on TLS, DNS, and certificate authorities (see below).
2.	The scheme should be extensible to support new encryption and signing algorithms and new key types over time.
3.	The keys used for performing the scheme should be accessible in the application layer, such that keys can be provisioned and managed while providing good user experiences, without requiring the user to install certificates on their device.
4.	The scheme should avoid any major adoption hurdles, such as requiring OS platform updates or requiring the use of prohibitively large software packages.
5.	The scheme should minimize request size and server response time as much as possible.
6.	Ideally, the Hub’s authentication scheme would be re-usable for other web services that are secured by DIDs.
7.	Where possible, the scheme should reduce the amount of state that must be maintained on the client or Hub for each connection.

## Security requirements
More concretely, we have identified Tthe following basic qualities security requirements of existing for authentication and encryption schemes that we to aim to meetmust be met:

1. The client must be able to authenticate the Hub.
2.	The Hub must be able to authenticate the client.
3.	Messages exchanged between the Hub and client must be encrypted.
4.	Proof should be provided that messages have not been tampered with in transit.
5.	Requests and responses should be protected against replay attacks.
6.	Encryption should preserve forward secrecy.

There are certainly additional security properties that could be incorporated over time, but we believe this set is sufficient for the near future.


## v1 authentication protocol
The Hub requires end-to-end (two-way) authenticated encryption for all request-response exchanges using the JWS scheme. As a result of the additional message confidentiality requirement described earlier, all requests and responses are first JWS signed, then JWE encrypted. Specifically, every request sent to the Hub must be JWE encrypted using a public key specified in a Hub’s DID document. The ID of the public key must be specified in the kid JWE header parameter as a [DID fragment](https://w3c-ccg.github.io/did-spec/#fragments).

```sequence
Requester -> Requester:  1. Creates signed access request + nonce as a JWS.
Requester -> Requester:  1. Encrypts the JWS as a JWE using Hub's public-key.
Requester -> Hub:        2. JWE encrypted access request

Hub -> Hub:        3. Decrypts JWE blob.
Hub -> Hub:        3. Verifies requester-signed JWS.
Hub -> Hub:        4. Creates signed JWT.
Hub -> Hub:        5. Wraps signed JWT + requester-issued nonce as a JWS.
Hub -> Hub:        5. Encrypts JWS as a JWE using requester's public-key.
Hub --> Requester: 6. JWE encrypted Hub-signed JWT

Requester -> Requester:  7. Decrypts JWE blob.
Requester -> Requester:  7. Verifies Hub-signed JWS.
Requester -> Requester:  8. Verifies requester-issued nonce in JWS.
Note right of Requester: Note: Hub is authenticated at this point.
Requester -> Requester:  9. The requester caches the JWT for future communication.
Note right of Requester: Note: the cached JWT can be reused until expiry.
Requester -> Requester:  10. Creates Hub request and new nonce.
Requester -> Requester:  11. Signs Hub request + Hub-issued JWT + nonce as a JWS.
Requester -> Requester:  11. Encrypts JWS as a JWE using Hub's public-key.
Requester -> Hub:        12. JWE encrypted Hub request.

Hub -> Hub:        13. Decrypts JWE blob.
Hub -> Hub:        13. Verifies requester-signed JWS.
Hub -> Hub:        14. Verifies Hub-issued JWT.
Note right of Hub: Note: requester is authenticated at this point.
Hub -> Hub:        15. Processes the request.
Hub -> Hub:        16. Signs Hub response + requester-issued nonce as a JWS.
Hub -> Hub:        16. Encrypts JWS as a JWE using requester's public-key.
Hub --> Requester: 17. JWE encrypted Hub response

Requester -> Requester: 18. Decrypts JWE blob.
Requester -> Requester: 18. Verifies Hub-signed JWS.
Requester -> Requester: 19. Verifies requester-issued nonce.
Requester -> Requester: Parses Hub response.

```
Example JWE header:
```
{
  "kid": "did:example:123456789abcdef#keys-1",
  "alg": "RSA-OAEP-256",
  "enc": "A128GCM",
}
```

Example JWS header:
```
{
  "kid": "did:example:123456789abcdef#keys-1",
  "alg": "RS256",
  "did-requester-nonce": "p6OLLpeRafCWbOAEYp",
  "did-access-token": "..."
}
```

Example JWT payload:
```
{
  "jti": "3e2c9b3a-da11-47e2-a5d8-12a23a9...",
  "iss": "did:example:Hub-did",
  "sub": "did:example:requester-did",
  "iat": 1533168455,
  "exp": 1533172655
}
```

Since all messages exchanged are protected by JWE, JWE encryption and decryption steps are intentionally omitted to highlight the authentication steps in the description below.

> Note: Currently JWT encryption and decryption uses DID keys directly – this does not provide forward secrecy for messages. Future implementations should use a shared symmetric ephemeral key for encryption.

1.	The requester creates a self-signed access request as a JWS. A request to the Hub is considered an “access request” if the JWS header does not contain the did-access-token parameter. A nonce must be added to the did-requester-nonce JWS header parameter for every request sent to the Hub, the Hub must then include the same nonce header in the response to protect the requester from response replays. The requester nonce is included in the header rather than the payload to decouple authentication data from the request or response data. The Hub will ignore the actual payload in the JWS during this phase of the authentication flow.
2.	Requester sends the JWS to the Hub.
3.	The Hub verifies the JWS by resolving the requester’s DID then obtaining the public key needed for verification. The requester’s DID and the public-key ID can be derived from kid JWS header parameter. The same public-key must be used for encrypting the response.

> Note: Verification of JWS using public keys obtained via DID resolution is pending real implementation.

4.	The Hub generates a time-bound token for the requester to use in future communication. This token technically can be of any opaque format, however in the DID Hub Core Library implementation, the token is a signed JWT.
5.	The Hub signs/wraps the token (in our case a signed JWT) as the payload of a JWS. The Hub must also copy the did-requester-nonce JWS header parameter from the request into the JWS header.

> Note: Currently the DID Hub Core library authentication implementation is stateless, thus it is subject to request replays within the time-bound window allowed by the JWT. In the future, the requester nonce can be cached on the Hub to prevent all request replays.

6.	The Hub sends the JWS back to the requester.
7.	The requester verifies that JWS is signed by the Hub by resolving the Hub’s DID then obtaining the public key needed for verification. The Hub’s DID and the public-key ID can be derived from kid header parameter.

> Note: Currently the client will resolve the Hub’s DID by sending a request to a Universal Resolver web service. Future implementations will need to employ other means of public key resolution that do not depend on TLS & DNS security. See appendix for a brief discussion of options.

8.	The requester verifies the value in the did-requester-nonce JWT header parameter matches its requester-issued nonce.
9.	The Hub is authenticated after the step above. The requester caches the Hub-issued token (signed JWT) locally and reuse it for all future requests to the Hub until the Hub rejects it, most commonly due to token expiry, at which point the requester would request a new access token.
10.	The requester crafts the actual Hub request, and creates a new nonce.
11.	The requester signs the Hub request as a JWS, including the new nonce in the did-requester-nonce header parameter and the Hub-signed JWT in the did-access-token header parameter.
12.	The requester sends the signed Hub request to the Hub.
13.	The Hub verifies the JWS by resolving the requester’s DID then obtaining the public key needed for verification. The same public-key must be used for encrypting the response.
14.	The Hub verifies the signed JWT given in the did-access-token header parameter.
15.	The requester is authenticated after the step above. The Hub process the request and generates an in-memory response.
16.	The Hub signs the Hub response as a JWS, including the did-requester-nonce header parameter from the request in the JWS header.
17.	The Hub sends the signed Hub response back to the requester.
18.	The requester verifies that JWT is signed by the Hub by resolving Hub’s DID and obtaining the public key specified by the kid header in the JWT.  
19.	The requester verifies that the value in the did-requester-nonce JWS header parameter matches its requester-issued nonce.

## Signature and encryption algorithms
This section lists the signature and encryption algorithms currently supported (implemented and tested). In reality, the implementation uses Cisco’s JOSE library, which officially supports a few more algorithms such as ECDSA P256, but since we have not tested those curves end-to-end and those are considered insecure by some, they have not been added to the supported list.

## JWS Support
| Serialization         | Support |
| --------------------- | ------- |
| Compact Serialization | Yes     |
| JSON Serialization    | No      |

### Hub Response and Token Signing
| Algorithm          | Support           | JOSE specified | JWK specified | 
| ------------------ | ----------------- | -------------- | ------------- |
| RS256              | Yes               | Yes            | Yes           |
| ED25519            | To be implemented | To be added    | Yes           |
| SECP256K1          | To be implemented | To be added    | To be added   |

### Request Signature Verification
| Algorithm          | Support           | JOSE specified | JWK specified | 
| ------------------ | ----------------- | -------------- | ------------- |
| RS256              | Yes               | Yes            | Yes           |
| RS512              | Yes               | Yes            | Yes           |
| ED25519            | To be implemented | To be added    | Yes           |
| SECP256K1          | To be implemented | To be added    | To be added   |

> Note: ED25519 is defined in JWK specification, while SECP256K1 is not. Neither algorithms are listed in the [JOSE signature and encryption algorithms](https://www.iana.org/assignments/jose/jose.xhtml#web-signature-encryption-algorithms), and are not implemented in the node-jose NPM package used in the current implementation.


## JWE Support
| Serialization         | Support |
| --------------------- | ------- |
| Compact Serialization | Yes     |
| JSON Serialization    | No      |

> Discussion: Current implementation assumes Compact Serialization in the HTTP POST body and payload. We might want to support JSON serialization for POST body instead/in addition.

### Key Encryption
Asymmetric algorithms that can be used by the Hub to encrypt the symmetric content encryption key in the Hub response JWE:
| Algorithm                | Support           | JOSE specified | JWK specified |
| ------------------------ | ----------------- | -------------- | ------------- |
| RSA-OAEP                 | Yes               | Yes            | Yes           |
| ED25519                  | To be implemented | To be added    | Yes           |
| SECP256K1                | To be implemented | To be added    | To be added   |

### Key Decryption
Asymmetric algorithms that can be used by the Hub to decrypt the symmetric content encryption key in the Hub request JWE:
| Algorithm                | Support           | JOSE specified | JWK specified |
| ------------------------ | ----------------- | -------------- | ------------- |
| RSA-OAEP                 | Yes               | Yes            | Yes           |
| RSA-OAEP-256             | Yes               | Yes            | Yes           |
| ED25519                  | To be implemented | To be added    | Yes           |
| SECP256K1                | To be implemented | To be added    | To be added   |

### Content Encryption
Symmetric algorithms that can be used by the Hub to encrypt the content of the Hub response JWE:
| Algorithm                     | Support            | JOSE specified |
| ----------------------------- | ------------------ | -------------- |
| A128GCM                       | Yes                | Yes            |
| XSalsa20-Poly1305             | To be implemented  | To be added    |

### Content Decryption
Symmetric algorithms that can be used by the Hub to decrypt the content of the Hub request JWE:
| Algorithm                     | Support            | JOSE specified |
| ----------------------------- | ------------------ | -------------- |
| A128GCM                       | Yes                | Yes            |
| XSalsa20-Poly1305             | To be implemented  | To be added    |



## Cryptographic Algorithm Extensibility
This section describes how to add additional cryptographic algorithm support in the Hub.

#### JWE Content Encryption Key Encryption
Follow the steps below to add an additional algorithm for asymmetric key encryption:
1. Extend `getKeyEncryptionAlgorithm(...)` method in `JweToken.ts` to support a new JWK format.
1. Create a library function for the new encryption algorithm matching the `EncryptDelegate` definition found in `JweToken.ts`.
1. Reference the new encryption function in `encryptContentEncryptionKey(...)` method found in `JweToken.ts`.

These extensibility points are sufficient to allow users/clients of the hub to choose their own key types and algorithms used for authentication and encryption. They do not, however, enable hub implementers to choose their own key types and algorithms – the current implementation forces the use of RSA (see future work). 

#### JWS Signature Verification
Follow the steps below to add an additional algorithm for signature verification:
1. Create a library function for the new signing algorithm matching the `VerifySignatureDelegate` definition found in `JwsToken.ts`.
1. Reference the new signature verification function in the `verifySignature(...)` method found in `JwsToken.ts`.


## Future Work
We’ve identified the following areas of investment to improve the Hub authentication scheme:

- Complete verification of message signatures using public keys from DID documents.
- Implement a stateful nonce/challenge scheme to prevent any replay attack.
- Add stateful ephemeral key/forward secrecy support.
- Refactor extensibility model to something more developer-friendly
- Complete extensibility model for new algorithms and key types:
    - Add Decryption of JWE Content Encryption Key.
    - Add JWE Content Encryption.
    - Add JWE Content Decryption.
    - Add JWS Signing.
- Refactor modules to decouple client authentication from server authentication & message encryption. This would provide two advantages:
    - Makes it easy to use in test, development, and debugging.
    - Allows customers who accept TLS’s security level to use the protocol for client authentication only.
- Remove dependency on TLS for public key resolution via Universal Resolver (see appendix).
- Pen testing/stronger security review process
- Consider the following privacy features:
    - Message repudiation
    - Participation repudiation
    - Anonymity preservation
    - …others?


## Appendix 
### Comparison to related technologies – Transport Layer Security (TLS)
TLS and its predecessor SSL provide message integrity and confidentiality by encrypting messages between a client and server and authenticating the identity of the server. Without going into detail, it is dependent on the client trusting a set of certificate authorities (CAs) to remain robust to compromise. Some examples and reasons for lack of trust in CAs:

- [Security issues with certificate authorities](https://ieeexplore.ieee.org/document/8249081/?part=1)
- [Certificate Authority Collapse: Regulating Systemic Vulnerabilities in the HTTPS Value Chain](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2031409)
- [Everything you never wanted to know about PKI but were forced to find out](https://www.cs.auckland.ac.nz/~pgut001/pubs/pkitutorial.pdf)
- [The internet is broken: could we please fix it?](https://blog.cryptographyengineering.com/2012/02/28/how-to-fix-internet/)
- [5 serious problems with HTTPS and SSL Security on the Web](https://www.howtogeek.com/182425/5-serious-problems-with-https-and-ssl-security-on-the-web/)

While the TLS protocol provides many of the security and privacy guarantees necessary for secure Hub communication, it the dependency on CAs and DNS security that motivates a different solution. By replacing the role of CAs with a distributed ledger, we provide a stronger degree of message security.

There are several companies/projects today that are exploring the use of blockchains to replace existing internet infrastructure. Primary examples include Namecoin and Blockstack (to a degree), but a quick search will reveal several other efforts as well:

- [Namecoin](https://namecoin.org/)
- [Blockstack](https://blockstack.org/)
- [Blockstack vs. Namecoin](https://namecoin.org/docs/faq/#how-does-namecoin-compare-to-blockstack)
- [A blockchain based PKI management framework](https://medium.com/trustroot/disrupting-blockchain-security-can-a-decentralized-certificate-authority-improve-trust-in-1d7af5d7fb2)
- [Quora: can blockchain remove the need for an SSL certificate authority?](https://www.quora.com/Can-blockchain-remove-the-need-for-an-SSL-certificate-authority)

Blockchain based solutions, however, are not the only ongoing attempt to reduce reliance on/trust in CAs. Some other solutions, some active, some now discontinued, include:

- [The perspectives project from Carnegie Mellon](https://www.cs.cmu.edu/~dga/papers/perspectives-usenix2008/)
- [Dynamic public key pinning via Trust Assertions for Certificate Keys (TACK)](http://tack.io/draft.html)
- [The MonkeySphere project, which tries to apply PGP and web of trust principles](http://web.monkeysphere.info/)
- [Certificate transparency](https://en.wikipedia.org/wiki/Certificate_Transparency) and the [expect-ct header](https://httpwg.org/http-extensions/expect-ct.html)
- [HTTP public key pinning (HPKP) (deprecated)](https://en.wikipedia.org/wiki/HTTP_Public_Key_Pinning)
- [Cert pinning, which is appropriate in a limited set of use cases](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning)

Beyond CA vulnerabilities, TLS typically does not do anything to authenticate the identity of the client to the server – that is left as an exercise to the server developer, and different services take many different approaches. Client authentication is one of the main requirements for a complete Hub authentication proposal, which makes TLS on its own insufficient for our purposes.

### Comparison to related technologies – Mutual/Client TLS
A purported solution for client authentication based on TLS is known as Client TLS or Mutual TLS, in which the client authenticates the server and the server also authenticates the client. Mutual TLS is popular for server to server communication where both servers are owned by a single party.

While Client TLS integrates nicely with the exiting TLS infrastructure, it has its drawbacks in user-facing scenarios. Most importantly, using Client TLS requires the user to obtain and install a certificate from a trusted CA, which often involves interacting with low-level functionality on the device. Furthermore, use of the certificate must typically be approved by the user before any website or server can perform mutual authentication. Finally, the certificate used in Client TLS is shared across all applications on the device, rather than maintaining per-application credentials. This makes it more difficult to authenticate which client application might be making a particular request. For more detail on the shortcomings of client TLS, please refer to the following pages:

- [Introduction to client TLS](https://blog.cloudflare.com/introducing-tls-client-auth/)
- [Shortcomings of client TLS (in the context of token binding)](http://www.browserauth.net/tls-client-authentication)

### Public key resolution
The goal of this proposal is two-fold:

1.	To authenticate a client of an identity Hub and 
2.	To authenticate the Hub and encrypt messages in a way that prevents against the shortcomings of PKI.

Admittedly, this proposal does not quite achieve the latter. As noted in step 7 of the authentication protocol, the client must validate the signature provided by the Hub using the Hub’s public keys. The Hub’s public keys, however, are located on the distributed ledger where the Hub registered its DID.
The typical solution for resolving a DID into its public keys is to run an instance of the Universal Resolver. But unfortunately verifying the authenticity of the response received from a Universal Resolver requires an HTTPS request with reliance on the very PKI we were trying to circumvent.

To actually remove reliance on CAs, we must come up with an alternative strategy for resolving a Hub’s DID to its public keys in its DDO. Some possible solutions might include:

- Running a “lite client” on the client which participates in distributed ledger transaction protocols directly.
- The client pins to a set of public keys for a Universal Resolver, and that resolver implements key rotation/revocation scheme that is not dependent on existing PKI.
- The client trusts an instance of a Universal Resolver that’s running inside a local, protected network

Section III of [this pape](http://www.ieee-security.org/TC/SP2015/papers-archived/6949a232.pdf) provides a nice comparison of different technologies that are used for establishing trust in secure messages exchanges. 

