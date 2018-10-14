# Draft Status

Name | Lead | Link | Status
---|---|---|---
Agent Communication Protocols | Adrian | [Draft](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/Agent-Communication-Protocols.md) | Oct 22
BTCR | Ryan | | 
Concept Map | Andrew, Ouri | | 
A DID for Everything | Sam | [Draft](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/A_DID_for_everything.md) | Oct. 22
Digital Credential Wallet | Mikerah | [Draft](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/Digital%20Credential%20Wallet.md) | Feb 1
Digital Identity for the Homeless | Matt | [Topic](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/Digital-Identity-for-the-Homeless.md) | Dec 5
Guidance and Standards for Interoperability of Decentralized Identity Systems | Manu, Mike J. | [Draft](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/Guidance_and_Standards_for_Interoperability_of_Decentralized_Identity_Systems.md) | Nov 1
How to Convince Dad* | Lucas | [Draft](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/convincing-dad.md) | Nov 9
IPLD as a General Pattern | Jonny | [Draft](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/ipld_did_documents.md) | Oct 22
Mental Models | Joe | [Draft](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/mental-models.md) | Jan 4
Peer to Peer Degrees of Trust | Tyler | [Draft](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/peer-to-peer-degrees-of-trust.md) | Nov. 8
Resource Integrity Proofs | Ganesh | [Draft](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/resource-integrity-proofs.md) | Nov 9
Use Cases and Proposed Solutions for Verifiable Offline Credentials | Mike L. | [Draft](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/Use%20Cases%20and%20Proposed%20Solutions%20for%20Verifiable%20Offline%20Credentials.md)| Nov 1

# Draft Abstracts

## Pandoc

_Please produce a .MD file of your document as it exists toward the end of Friday. If you're planning to continue working in a Google Doc or on some other cooperative platform, that's fine, but we want a current status of the document._

[Pandoc](https://pandoc.org/) is an easy program that does a decent job of converting files to .MD. You can [install for Windows, Mac, or UNIX](https://pandoc.org/installing.html).

If you have a Google doc, the following methodology should convert your file:

   1. In Google Docs, `File -> Download As -> Microsoft Word (docx)`, to download yourfile.docx
   2. On your local machine, run pandoc: `pandoc yourfile.docx -o yourfile.md`
   3. You can then upload the MD file using a pull request

## Draft Abstracts

This will be the location for papers created over the course of the design workshop.

   * [A DID for Everything](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/A_DID_for_everything.md)

*Abstract:* The decentralized identifier (DID) is a new type of globally unique identifier that offers a model for lifetime scope, portable digital identity that does not depend on any centralized authority and can never be taken away. DIDs are the “atomic units” of a new layer of decentralized identity infrastructure. However, it may be possible to extend DIDs from its primary use as an identifier of people to identify everything. We can use DIDs to help us identify and manage objects, machines or agents through their digital twins, to locations, to events, and even to autonomic data. The paper will present novel use-cases for DIDs that relate to the field of every author.

DIDs are only the base layer of decentralized identity infrastructure. The next higher layer -- where most of the value is unlocked -- is verifiable claims. This is the technical term for a digitally signed electronic credential that conforms to the interoperability standards being developed by the W3C Verifiable Claims Working Group. When a DID is extended to machines and autonomic data, those DIDs can also hold verifiable claims and attestations.

   * [Agent Communication Protocols](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/Agent-Communication-Protocols.md)

*Abstract:* The term agent has been used in many context within the self sovereign identity world. But what exactly we mean by an agent? This paper will try to summarize the agent concept and at the same time identify the main phases and messages they need to exchange in order to be able to connect, receive credentials and share proofs between each other. We will start by assuming the discoverability of those agents.

   * [Digital Credential Wallet](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/Digital%20Credential%20Wallet.md)

*Abstract:* Digital Credential Wallet Outline What is it? (Define it) A credential issued by a peer Existing solutions to doing credential wallets Centralized (Apple wallets, AndroidPay) What does it do?/Requirements Request a credential from a peer Share a credential Revoke a credential Message Manage Keys Consumer requirements vs Enterprise requirements vs NPE wallet requirements (Digital Twins) How do I take ownership for that thing I just bought? Applications Use Cases Identify some use cases What solutions are already there // Point out ones that are already there 3Rs of key management - let’s point at DPKI, DKMS … Depth - this is about the broad picture. General guideline is to stop at pointing at current (and needed) work. Avoid useless Rabbit Holes Future work

   * [How to Convince Dad\* of the Importance of Self-Sovereign Identity](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/convincing-dad.md)

*Abstract:* One of the major problems with bootstrapping self-sovereign identity is that it requires adoption by a large number of people. Pushing self-sovereign identity from the top down is most likely to result in a technology that’s not actually used, while instead encouraging the average person to demand self-sovereign identity from the bottom up will result in the organic development of a vibrant, well-utilized ecosystem.

This paper addresses that need by offering arguments to a variety of people who might be reluctant to use self-sovereign identity, uninterested in its possibilities, or oblivious to the dangers of centralization.

   * [IPLD as a general pattern for DID documents](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/ipld_did_documents.md)

*Abstract:* IPLD is a way of representing hash-linked data to be used in content-addressed data retrieval systems like IPFS. We investigate using IPLD as a general pattern in creating DID methods. The main idea is to represent an initial DID document as IPLD data, and then define the DID itself as the hash of this data. This way resolving the initial DID document from the DID is tautological - the DID is merely a representation of the data in the DID document.

   * [Mental Models](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/mental-models.md)

*Abstract:* Introductions to models of identity (we think about this different ways); Models Introduction; Pitfalls and Specific Guidance; Therefore what?

   * [Peer to Peer Degrees of Trust](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/peer-to-peer-degrees-of-trust.md)

*Abstract:* The concept of an open and permissionless system is philosophically appealing. However, there are certain applications that require the concept of trusted identities. At a minimum, all systems that involve voting rely on unique, trustworthy identities to cast a vote. This includes any consensus mechanism as well as any rating system. Such systems face a dilemma: how can we filter out bad actors without a centralized authority?

In this paper we propose a framework for reasoning about reputation using a web of trust. We briefly summarize the history of peer-to-peer reputation, define 3 layers required for peer-to-peer reputation, and explore possible applications of this framework.

   * [Guidance and Standards for Interoperability of Decentralized Identity Systems](Guidance_and_Standards_for_Interoperability_of_Decentralized_Identity_Systems.md)

*Abstract:* Use of applicable standards is critical to the interoperability of decentralized identity systems.  This paper provides high-level guidance for architects and builders of interoperable decentralized identity systems (including data models, cryptographic requirements, and data representations).  It inventories existing and emerging standards appropriate for building these systems, identifies gaps in the standards, and proposes means to fill them.  These include standards for representation of cryptographic inputs and outputs.  The final section focuses on issues specific to systems using DIDs and the DID specification itself.

   * [Resource Integrity Proofs](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/resource-integrity-proofs.md)

*Abstract:* Currently, the Web provides a simple yet powerful mechanism for the dissemination of information via links. Unfortunately, there is no generalized mechanism that enables verifying that a fetched resource has been delivered without unexpected manipulation. Would it be possible to create an extensible and multipurpose cryptographic link that provides discoverability, integrity, and scheme agility?

This paper proposes a linking solution that decouples integrity information from link and resource syntaxes, enabling verification of any representation of a resource from any type of link. We call this approach Resource Integrity Proofs (RIPs). RIPs provide a succinct way to link to resources with cryptographically verifiable content integrity. RIPs can be combined with blockchain technology to create discoverable proofs of existence to off-chain resources.

   * [Use Cases and Proposed Solutions for Verifiable Offline Credentials](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/Use%20Cases%20and%20Proposed%20Solutions%20for%20Verifiable%20Offline%20Credentials.md)

*Abstract:* Self Sovereign Identity is now a widely discussed topic especially in the context of verifiable credentials–attributes attested by third-parties about an individual or entity that can be used as proof about them such as a digital driver’s license or passport. This has enabled new systems to be developed to address security and privacy issues.

In this paper we cover various scenarios where some or all parties have intermittent, unreliable, untrusted, insecure, or no network access, but require cryptographic verification (message protection and/or proofs). Furthermore, communications between the parties may be only via legacy voice channels. Applicable situations include marine, subterranean, remote expeditions, disaster areas, refugee camps, and high-security installations. This paper then recommends solutions for addressing offline deployments.

   * [Verifiable Claims and Promise Theory](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/Verifiable_Claims_Promise_Theory.org)

*Abstract:* One of the goals of modern day peer-to-peer systems is to build self-composing, self-organizing, distributed systems of cooperating agents. However, it is a challenge to describe self-organizing systems from a top-down perspective, since agents may choose to offer a variety of services or capabilities and the approach hides an agent’s decision-making capabilities. A more reasonable alternative is to construct distributed systems using a bottom-up approach, whereby agents announce functions that they are willing to perform, and other agents can establish a commitment to receive such a service. Describing systems from a bottom-up approach thus enables reframing design perspectives on who is imposing vs offering the service. For this reason, we propose using Promise Theory, which advocates for agents to offer promises of services or credentials. A benefit of using promise theory is that promises can be used as a prerequisite to forming trust and certainty. We give two examples using promise theory in distributed systems: object capabilities and verifiable claims.
