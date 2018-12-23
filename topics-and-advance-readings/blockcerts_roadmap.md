# Blockcerts -- where we are, and what's next

Authors: Kim Hamilton Duffy, Anthony Ronning, Lucas Parker, and Peter Scott

Table of Contents:
- [Blockcerts -- where we are, and what's next](#blockcerts----where-we-are--and-what-s-next)
- [About Blockcerts](#about-blockcerts)
- [Reasons for Success](#reasons-for-success)
- [Obstacles we faced](#obstacles-we-faced)
- [Current Challenges](#current-challenges)
  * [Remove centralization introduced by hosted Issuer Profiles](#remove-centralization-introduced-by-hosted-issuer-profiles)
  * [Remove centralization introduced by hosted revocation lists](#remove-centralization-introduced-by-hosted-revocation-lists)
  * [Handle recipient key lifecycle in a first-class way](#handle-recipient-key-lifecycle-in-a-first-class-way)
  * [Increase flexibility of schema across different use cases -- any privacy/security for sensitive claims](#increase-flexibility-of-schema-across-different-use-cases----any-privacy-security-for-sensitive-claims)
- [Roadmap](#roadmap)
  * [Open Badges / Verifiable Credentials Alignment](#open-badges---verifiable-credentials-alignment)
  * [Verifiable Displays (now Resource Integrity Proofs)](#verifiable-displays--now-resource-integrity-proofs-)
  * [DIDs](#dids)
  * [Revocation](#revocation)
  * [Blockcerts Governance](#blockcerts-governance)
- [Additional goals](#additional-goals)
  * [Scaleable distributed timestamps](#scaleable-distributed-timestamps)
  * [Privacy and security](#privacy-and-security)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


# About Blockcerts

Blockcerts is an open standard and [set of open source libraries](https://github.com/blockchain-certificates) for creating, issuing, viewing, and verifying blockchain-anchored credentials. In addition to commercial deployment by Learning Machine, it's used by hundreds of independent implementers (per github metrics and community discussion) and has a [thriving discussion forum for implementers and researchers](https://community.blockcerts.org/).

Blockcerts originated as an informal extension of Open Badges v1, and subsequently was reworked into a [proper extension of Open Badges v2, the schema of which is hosted by IMS Global](https://github.com/IMSGlobal/cert-schema).

# Reasons for Success

Blockcerts benefited heavily from the start by its adherence to open standards, release (and ease of use) of open source libraries, and focus on delivering a viable ecosystem for Educational and Occupational Claims. 

Key factors in its success include:

- Entirely open source and open standards-based
- Blockchain-agnostic, with current implementations on Bitcoin and Ethereum blockchains
- Credentials are recipient-owned and long-lived
- Free for recipients and verifiers due to ability to rely on blockchain APIs (with fallback and checking multiple providers for availability and avoiding centralization/trust on specific providers)
- Easy for recipients to receive and share credentials
	- Open source, free iphone and android Blockcerts wallet
	- Wallet contains HD key generation, easing key management for users
- Ability to adapt verification to higher-stakes verifying node deployments


# Obstacles we faced

As we started developing Blockcerts, we realized there was a vibrant Self-Sovereign Identity community thinking more broadly (and over a long period of time) about the hard problems we were facing. These problems were being discussed -- and solutions being developed -- in forums like the Internet Identity Workshop, Rebooting Web of Trust, and the W3C Credentials Community Group.

It was tremendously helpful finding these communities and their work, but we were very focused on shipping libraries enabling the primitives of recipient-owned credentials and ran into barriers resulting from the newness of standards and approaches. Some of these standards were in earliest phases of development, while others deferred tricky problems encountered in real-world deployments such as revocation. 

> Note that in some cases, versioning allows use of a standard under development, but this is not always possible pre-release, where the standards are changing greatly

The approach we used was two-fold:
- Favoring use of a released open standard over something that was in its infancy (and likely to change). For Blockcerts, Open Badges V2 was the clear choice, its real world deployments meant many corner-cases had been thought through.
- In areas where we want improvement (generally, around further reducing centralization points compromising recipient ownersip), contribute to interoperable standards in the Self-Sovereign Identity communities.

This has led to many productive collaborations with the Open Badges and Self-Sovereign Identity communities (who have very similar goals), allowed us to benefit from the experience of the communities, and allowed us to contribute back via prototypes, standards development, and more.


# Current Challenges

Our preference for comformance to released open standards necessitated compromises, resulting in undesirable centralization points.

Our highest priorities include addressing these limitations via these measures.

## Remove centralization introduced by hosted Issuer Profiles

The current approach to establishing issuer authenticity relies on Open Badges V2 Issuer Profile, typically implemented by a web-hosted list of current and expired keys. This is a centralization point that has implications for availability and even longevity.

> This limitation can be addressed by a new type of Decentralized Identifier (DID), which will be used in the next major version of Blockcerts.

## Remove centralization introduced by hosted revocation lists

The current approach to revocation relies on Open Badges V2 hosted revocation list. This is similarly a centralization point with the same availability, longevity risks.

> Through engagements with the Blockcerts community, we've protoptyped decentralized approaches that are being refined for inclusion in the standard.

## Handle recipient key lifecycle in a first-class way

While issuer key rotation is supported via the Issuer Profile schema (enabling lists of valid keys with timestamp ranges), there is no standard means supporting recipient key rotation, a threat to longevity. The only option at this point is for recipients to request the issuer to re-issue the credential.

> DIDs will also allow replacing public keys embedded in Credentials with these new identifiers, which will be a huge benefit to recipients' ability to prove ownership of the credentials over their lifetime.


## Increase flexibility of schema across different use cases -- any privacy/security for sensitive claims

Finally, the success of Blockcerts has introduced us with a good problem, which is that people want to use Blockcerts in an increasing number of scenarios. In some of these (e.g. transcripts) there is a different schema entirely that should be used. Continuing with the example of transcripts, these contain more sensitive data that should not be hosted and publicly available (as is the assumption in badges).

> Through Open Badges and Verifiable Credentials alignment, we ensure interoperability with both critical standards. Furthermore, the Verifiable Credentials data model has a rich spectrum of privacy and security concerns, enabling an alignment framework


# Roadmap

The general theme of our roadmap is enabling a more flexible range of credentials and privacy enhancing measures. Fortunately these are primarily achieved by alignment with Verifiable Credentials and the Decentralized Identifer specification.

## Open Badges / Verifiable Credentials Alignment

A critical foundational step is alignment of [Open Badges are Verifiable Credentials](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2018/blob/master/final-documents/open-badges-are-verifiable-credentials.pdf). This step combines the flexible structure of Verifiable Credentials with the widespread adoption / vibrant ecosystem of Open Badges.

More significantly, the Verifiable Credentials specification is intended for a range of credentials, and factors in a range of privacy and security concerns applicable for low-to-high stakes credentials. 


## Verifiable Displays (now Resource Integrity Proofs)

If all credentials being issued are identical in structure and vocabulary, it is possible to assume a common set of fields in a display. However, when these vary, social exploits are possible. 

The question is: even if the credential content verifies, how do you know the display of the credential you are seeing (e.g. HTML page, PDF, etc) matches the content (e.g. JSON file) without inspecting the raw content. 

This is a problem that's less relevant in machine-to-machine credential verification, but highly relevant for credentialing systems that bridge legacy systems, i.e. where a human is expected to view a credential.

The verifier and viewer must be able to know that the display they are seeing matches what was intended by the issuer and has not been tampered with.

A general solution for this is proposed in [Resource Integrity Proofs](https://github.com/WebOfTrustInfo/rwot7/blob/master/final-documents/resource-integrity-proofs.pdf)

## DIDs

Moving to Decentralized Identifiers removes the issuer profile as a single-point-of-failure. It improves longevity (enabling even life-long recipient ownership) by promoting key lifecycle to a first-class notion. I.e. any viable system must factor in the fact that cryptopgrahic keys should be rotated as a best practice, and should factor in key loss.

[Open Badges are Verifiable Credentials](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2018/blob/master/final-documents/open-badges-are-verifiable-credentials.pdf) also outlines how DIDs will appear in the new Blockcerts schema.

## Revocation

Removing the revocation lists as a centralization point is another big priority. This is not just an availability concerns, but also lacks auditability, meaning the issuer can change it as will. (I.e. at least if the transaction were on-chain, one would have history of the suspected malicious behavior).

Our [prototype of contract-based revocation is described here](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/final-documents/blockcerts-revocation.md). We can continue developing similar approaches, and investigate others.

> While an IPNS revocation list would address the centralization problem, there are practical concerns we need to explore. (1) IPNS requires regular republishing of the mapping and (2) it's not clear if auditability of revocation list changes is enabled

## Blockcerts Governance

Perhaps our highest priority is setting up an independent foundation to steward Blockcerts. While it's an open standard and open source, it's widely perceived as a codebase of Learning Machine. We do have plenty of contributors and deployments, but the perception of being tied to a single company is understandably a concern.

# Additional goals

## Scaleable distributed timestamps

Currently Blockcerts uses the blockchain transaction (associated with a credential) to determine both of these items during verification:
1. timestamp (proof of existence at a certain time)
2. issuer signing key
 
For future versions, we propose using a timestamping service (like Open Timestamps) for #1 and a separate issuer signature for #2. The flow could look like this:
1. issuer uses Open Timestamps to obtain an ots proof of the content; appends proof
2. issuer signs payload; appends proof

This has an added benefit that the second operation does not need to be on-chain, resulting in a more flexible/scaleable approach.

> TODO: A sketch of a Open Timestamps LD signature was developed woth Peter Todd at Decentralized Web summit (details to come).
> TODO: Work out the chained signature samples.

## Privacy and security

At the macro-level, privacy and security wins are enabled through alignment with the Verifiable Credentials data model. This includes not only a thorough consideration of the spectrum of concerns and scenarios, but is associated with standards enabling increased privacy. That means it is easier adapt to higher stakes scenarios in this interoperable framework.

Some specific items include, increasing in order of complexity:
- Break assumption of credential hosting, inherited from Open Badges conventions
- Improving non-correlatability through use of nonces
- Enabling data minimization and selective disclosure as standards emerge, promote best practices for different scenarios.




