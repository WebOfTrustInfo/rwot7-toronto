# Rebooting the Web of Trust VII: Toronto (September 2018)

This repository contains documents related to RWOT7, the seventh Rebooting the Web of Trust design workshop, which ran near Toronto, Canada, on September 26th to 28th, 2018. The goal of the workshop was to generate five technical white papers and/or proposals on topics decided by the group that would have the greatest impact on the future.

_Please see the [Web of Trust Info website](http://www.weboftrust.info/) for more information about our community. Watch for our [next event](https://www.weboftrust.info/next-event-page.html) March 1st-3rd in Barcelona, Spain._

## Final Papers


## [*BTCR v0.1 Decisions*](https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/final-documents/btcr_0_1.pdf) [(Text)](https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/final-documents/btcr_0_1.md)
#### Kim Hamilton Duffy, Christopher Allen, and Dan Pape

> The Bitcoin Reference (BTCR) DID method supports DIDs using the Bitcoin blockchain. This method has been under development through Rebooting Web of Trust events and hackathons over the past year. The BTCR method's reliance on the Bitcoin blockchain presents both advantages and design challenges. During RWOT7, the authors made a number of design and implementation decisions -- largely scope-cutting in nature -- in order to lock down a Minimum Viable Product (MVP) version, which we'll refer to as v0.1. This paper documents those decisions, which will apply to the upcoming v0.1 BTCR method specification and associated v0.1 BTCR reference implementation.

## [*A DID for Everything*](https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/final-documents/A_DID_for_everything.pdf) [(Text)](https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/final-documents/A_DID_for_everything.md)
#### Shaun Conway, Andrew Hughes, Moses Ma, Jack Poole, Martin Riedel, Samuel M. Smith Ph.D., and Carsten Stöcker

> The decentralized identifier (DID) is a new and open standard type of globally unique identifier that offers a model for lifetime-scope portable digital identity that does not depend on any centralized authority and that can never be taken away by third-parties. DIDs are supported by the W3C community and the Decentralized Identity Foundation (DIF). They are the "atomic units" of a new layer of decentralized identity infrastructure. However, DIDs can be extended from identifiers for people to any entity, thus identifying everything. We can use DIDs to help us identify and manage objects, machines, or agents through their digital twins; we can expand them to locations, to events, and even to pure data objects, which we refer to as decentralized autonomic data (DAD) items.

> The paper will present novel use-cases for DIDs and DADs and propose a new cryptographic data structure that is a self-contained blockchain of DADs. This enables the verification of the provenance of a given data flow. It builds on a prior paper and an associated reading.

## [*How to Convince Dad\* of the Importance of Self-Sovereign Identity*](https://github.com/WebOfTrustInfo/rwot7/blob/master/final-documents/convincing-dad.pdf) [(Text)](https://github.com/WebOfTrustInfo/rwot7/blob/master/final-documents/convincing-dad.md)
#### Shannon Appelcline, Kenneth Bok, Lucas Parker, Peter Scott, and Matthew Wong

> One of the major problems with bootstrapping self-sovereign identity is that it requires adoption by a large number of people. Pushing self-sovereign identity from the top-down is most likely to result in a technology that’s not actually used, but instead encouraging the average person to demand self-sovereign identity from the bottom-up will result in the organic development of a vibrant, well-utilized decentralized web-of-trust ecosystem.

> This paper addresses that need by offering arguments to a variety of people who might be reluctant to use self-sovereign identity, uninterested in its possibilities, or oblivious to the dangers of centralization. By focusing on the needs of real people, we hope to also encourage developers, engineers, and software business owners to create the apps that will address their reluctance and fulfill their needs, making self-sovereign identity a reality.

## [*IPLD as a general pattern for DID documents and Verifiable Claims*](https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/final-documents/ipld-did.pdf) [(Text)](https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/final-documents/ipld-did.md)
#### jonnycrunch, Anthony Ronning, Kim Duffy, Christian Lundkvist

> Since the emergence of the Decentralized Identifier (DID) specification at the Fall 2016 Rebooting the Web of Trust [1], numerous DID method specifications have appeared. Each DID method specification defines how to resolve a cryptographically-tied DID document given a method-specific identifier. In this paper, we describe a way to represent the DID document as a content-addressed Merkle Directed Acyclic Graph (DAG) using Interplanetary Linked Data (IPLD). This technique enables more cost-efficient, scaleable creation of DIDs and can be applied across different DID method specifications.

## [*Peer to Peer Degrees of Trust*](https://github.com/WebOfTrustInfo/rwot7/blob/master/final-documents/peer-to-peer-degrees-of-trust.pdf) [(Text)](https://github.com/WebOfTrustInfo/rwot7/blob/master/final-documents/peer-to-peer-degrees-of-trust.md)
#### Harrison Stahl, Titus Capilnean, Peter Snyder, and Tyler Yasaka

> Aunthenticity is a challenge for any identity solution. In the physical world, at least in America, it is not difficult to change one's identity. In the digital world, there is the problem of bots. The botnet detection market is expected to be worth over one billion USD by 2023, in a landscape where most digital activity is still heavily centralized. These centralized digital solutions have the advantage of being able to track IP addresses, request phone verification, and present CAPTCHAs to users in order to authenticate them. If this problem is so difficult to solve in the centralized world, how much more challenging will it be in the decentralized world, where none of these techniques are available?

> In this paper, we explore the idea of using a web of trust as a tool to add authenticity to decentralized identifiers (DIDs). We define a framework for deriving relative trust degrees using a given trust metric: a "trustworthiness" score for a given identity from the perspective of another identity. It is our intent that this framework may be used as a starting point for an ongoing exploration of graph-based, decentralized trust. We believe this approach may ultimately be used as a foundation for decentralized reputation.

## [*Resource Integrity Proofs*](https://github.com/WebOfTrustInfo/rwot7/blob/master/final-documents/resource-integrity-proofs.pdf) [(Text)](https://github.com/WebOfTrustInfo/rwot7/blob/master/final-documents/resource-integrity-proofs.md)
#### Ganesh Annan and Kim Hamilton Duffy

> Currently, the Web provides a simple yet powerful mechanism for the dissemination of information via links. Unfortunately, there is no generalized mechanism that enables verifying that a fetched resource has been delivered without unexpected manipulation. Would it be possible to create an extensible and multipurpose cryptographic link that provides discoverability, integrity, and scheme agility?

> This paper proposes a linking solution that decouples integrity information from link and resource syntaxes, enabling verification of any representation of a resource from any type of link. We call this approach Resource Integrity Proofs (RIPs). RIPs provide a succinct way to link to resources with cryptographically verifiable content integrity. RIPs can be combined with blockchain technology to create discoverable proofs of existence to off-chain resources.

## [*Use Cases and Proposed Solutions for Verifiable Offline Credentials*](https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/final-documents/offline-use-cases.pdf) [(Text)](https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/final-documents/offline-use-cases.md)
#### Michael Lodder, Samantha Mathews Chase, and Wolf McNally

> In this paper we cover various scenarios where some or all parties have intermittent, unreliable, untrusted, insecure, or no network access, but require cryptographic verification (message protection and/or proofs). Furthermore, communications between the parties may be only via legacy voice channels. Applicable situations include marine, subterranean, remote expeditions, disaster areas, refugee camps, and high-security installations. This paper then recommends solutions for addressing offline deployments.

##  Topics & Advance Readings

In advance of the design workshop, all participants produced a one-or-two page topic paper to be shared with the other attendees on either:

* A specific problem that they wanted to solve with a web-of-trust solution, and why current solutions (PGP or CA-based PKI) can't address the problem?
* A specific solution related to the web-of-trust that you'd like others to use or contribute to?

Here are the advanced readings to date:

* [Addressing Global/Local Barriers to Adoption of Decentralized Identity Systems](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/Adoption.md) by Eric Brown
* [Agent to Agent Communication Protocol Overview](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/a2a-comm-protocol-overview.md) by Kyle Den Hartog
* [Blockcerts -- Where we are and what's next](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/blockcerts_roadmap.md) by Kim Hamilton Duffy, Anthony Ronning, Lucas Parker, and Peter Scott
* [Can Curation Markets Establish a Sustainable Technology Commons](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/CanCurationMarketsEstablishSustainableTechnologyCommons.pdf) by Sam Chase
* [CapAuth](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/capauth.md) by Manu Sporny, Dave Longley, Chris Webber, and Ganesh Annan
* [A Concept Diagram For RWOT Identity Terms](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/towards-a-terminology-concept-map.md) by Andrew Hughes
* [Cryptocurrency Wallets as a Form of Functional Identity](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/Cryptocurrency%20wallets%20a%20an%20application%20of%20Functional%20Identity.md) by Mikerah Quintyne-Collins and Abdulwasay Mehar
* [Decentralized Error Reporting](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/decentralized-error-reporting.md) by Jack Poole
* [Decentralized Identities and eIDAS](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/leveraging-eidas-for-did.md) by Oliver Terbu
* [Decentralized Identity: Hub Authentication & Message Encryption](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/did-auth-jwe.md) by Daniel Buchner
* [DIDDoc Conventions for Interoperability](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/diddoc-conventions-for-interoperability.md) by Stephen Curran & Olena Mitovska
* [DIDs In DPKI](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/dids-in-dpki.md) by Greg Slepak
* [DID Resolution Topics](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/did-resolution-topics.md) by Markus Sabadello
* [Digital Identity for the Homeless](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/Digital-Identity-for-the-Homeless.md) by Matthew Wong, T. Tian & CG Chen
* [Exploring Browser Web of Trust Use Cases](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/exploring-browser-wot-use.md) by Peter Snyder and Ben Livshits
* [Five Mental Models of Identity](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/five-mental-models-of-identity.md) by Joe Andrieu
* [Identity Hub Permissions / Authorization](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/identity-hub-permissions.md) by Daniel Buchner
* [IPLD as a general pattern for DID Documents](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/ipld_did_documents.md) by Christian Lundkvist
* [Is a Decentralized Collective Identity Possible?](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/Decentralized-Collective-Identity.md) by Heather Vescent
* [Magenc Magnet URIs: Secure Object Permanence for the Web](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/magenc.md) by Christopher Lemmer Webber
* [Measuring Trust](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/measuring-trust.md) by Tyler Yasaka
* [More Control for Identity Holders](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/more-control-for-identity-holders.md) by Arturo Manzaneda and Ismenia Galvao
* [Nobody REALLY Trusts the Blockchain](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/Nobody_REALLY_Trusts_the_Blockchain.md) by Dan Burnett, Shahan Khatchadourian, and Chaals Nevile
* [Not-a-Bot: A Use Case for Decentralized Identity using Proximity Verification to generate a Web of Trust](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/not-a-bot.md) by Moses Ma & Claire Rumore
* [The Political Economy of Naming](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/political-economy-of-naming.md) by Kate Sills
* [A Public Web of Trust of Public Identities](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/a-public-web-of-trust-of-public-identities.md) by Ouri Poupko and Ehud Shapiro
* [Resource Integrity Proofs](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/resource-integrity-proofs.md) by Ganesh Annan, Manu Sporny, Dave Longley, and David Lehn
* [RWoT Tribal Knowledge: Cryptographic and Data Model Requirements](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/crypto-data-model-requirements.md) by Manu Sporny, Dave Longley, and Chris Webber
* [The Role of Standards in Accelerating Innovation](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/The_Role_of_Standards_in_Accelerating_Innovation.md) by Michael B. Jones
* [Scoped Presentation Request on Verifiable Credentials](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/presentation-request/presentation-request.md) by Martin Riedel
* [Secure Crypto-Wallet Introductions](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/Secure%20Crypto-Wallet%20Introductions.md) by Wolf McNally, Ryan Grant
* [Standards for Agency and Decentralized Information Governance - Early Experience](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/standards-for-governance.md) by Adrian Gropper, MD, Michael Chen, MD, and Lydia Fazzio, MD
* [Towards Proof of Person](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/towards-proof-of-person.md) by Peter Watts
* [A Trustless Web-of-Trust](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/trustless-web-of-trust.md) by Ouri Poupko
* [The United Humans](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/united-humans.md) by Bohdan Andriyiv
* [Verifiable Displays](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/verifiable_displays.md) by Kim Hamilton Duffy, Bohdan Andriyiv, and Lucas Parker
* [Verifiable Offline Credentials](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/verifiable-offline-credentials.md) by Michael Lodder
* [What (and Who) Is In Your Wallet](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/what-and-who-is-in-your-wallet.md) by Darrell O'Donnell
* [Digital Identity for the Homeless](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/Digital-Identity-for-the-Homeless.md) by Matthew Wong, T. Tian & CG Chen
* [Zero Trust Computing with DIDs and DADs](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/ZeroTrustComputingWithDidsAndDads.md) by Samuel M. Smith

### Primers
These primers overview major topics which are likely to be discussed
at the design workshop. If you read nothing else, read these. (But
really, read as much as you can!)

* [DID Primer](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/did-primer.md) — Decentralized Identifiers ([extended version](https://github.com/WebOfTrustInfo/rwot7-fall2018/blob/master/topics-and-advance-readings/did-primer-extended.md) also available)
* [Functional Identity Primer](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/functional-identity-primer.md) — A different way to look at identity
* [Verifiable Credentials Primer](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/verifiable-credentials-primer.md) — the project formerly known as Verifiable Claims
* [DIDs In DPKI](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/dids-in-dpki.md) - how DIDs fit into Decentralized Public-key Infrastructure
