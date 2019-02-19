# Rebooting the Web of Trust VII (Fall 2018) Final Papers

_This is a listing for the RWOT7 papers to date. [Several more](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/README.md) are in process._

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
