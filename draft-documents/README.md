This will be the location for papers created over the course of the design workshop.

   * [A DID for Everything](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/A_DID_for_everything.md)
   
*Abstract:* The decentralized identifier (DID) is a new type of globally unique identifier that offers a model for lifetime scope, portable digital identity that does not depend on any centralized authority and can never be taken away. DIDs are the “atomic units” of a new layer of decentralized identity infrastructure. However, it may be possible to extend DIDs from its primary use as an identifier of people to identify everything. We can use DIDs to help us identify and manage objects, machines or agents through their digital twins, to locations, to events, and even to autonomic data. The paper will present novel use-cases for DIDs that relate to the field of every author.

DIDs are only the base layer of decentralized identity infrastructure. The next higher layer -- where most of the value is unlocked -- is verifiable claims. This is the technical term for a digitally signed electronic credential that conforms to the interoperability standards being developed by the W3C Verifiable Claims Working Group. When a DID is extended to machines and autonomic data, those DIDs can also hold verifiable claims and attestations.

   * [Agent Communication Protocols](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/Agent-Communication-Protocols.md)
   
*Abstract:* The term agent has been used in many context within the self sovereign identity world. But what exactly we mean by an agent? This paper will try to summarize the agent concept and at the same time identify the main phases and messages they need to exchange in order to be able to connect, receive credentials and share proofs between each other. We will start by assuming the discoverability of those agents.

   * [Digital Credential Wallet Design](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/Digital%20Credential%20Wallet%20Design.md)
   
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

   * [Requirements and Standards for Increasing Interoperability of Decentralized Identity Systems](https://github.com/burnburn/rwot7/blob/patch-3/draft-documents/Requirements_and_Standards_for_Increasing_Interoperability_of_Decentralized_Identity_Systems.md)
   
*Abstract:* 
   1. Identify core high-level requirements for interoperable decentralized identity systems (including data modelling, cryptographic requirements, and data representations)
   2. Talk about importance of standards and conventions in facilitating interop, increasing adoption, and accelerating innovation
Come up with top categories of standards for interoperability - conventions for use of DIDDoc elements, key types and purposes, data format, and others
   3. Identify current applicable standards and specifications
   4. Identify gaps in current standards and specifications and propose ways to fill them
   5. Identify the four or five most used cryptographic key types and finalize their descriptions

   * [Resource Integrity Use Cases](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/resource_integrity_use_cases.md)
   
*Abstract:* Currently, the Web provides a simple yet powerful mechanism for the dissemination of information via hyperlinks. Unfortunately, there is no generalized mechanism that enables verifying that a fetched resource has been delivered without unexpected manipulation. Resource Integrity Proofs enable verification of any representation of a resource from any type of link. This paper describes how RIP solves use cases inspired by production deployments of self-sovereign technologies. One is the problem of Verifiable Displays, which seeks to ensure the rendering of the VC content matches what the issuer intended. Another is verifying integrity of referenced data; for example, if the referenced data is in a mutable store. Lastly, we discuss how RIPs can be used to layer Object Capabilities on top of legacy systems.

   * [Verifiable Claims and Promise Theory](https://github.com/WebOfTrustInfo/rwot7/blob/master/draft-documents/Verifiable_Claims_Promise_Theory.org)
   
*Abstract:* One of the goals of modern day peer-to-peer systems is to build self-composing, self-organizing, distributed systems of cooperating agents. However, it is a challenge to describe self-organizing systems from a top-down perspective, since agents may choose to offer a variety of services or capabilities and the approach hides an agent’s decision-making capabilities. A more reasonable alternative is to construct distributed systems using a bottom-up approach, whereby agents announce functions that they are willing to perform, and other agents can establish a commitment to receive such a service. Describing systems from a bottom-up approach thus enables reframing design perspectives on who is imposing vs offering the service. For this reason, we propose using Promise Theory, which advocates for agents to offer promises of services or credentials. A benefit of using promise theory is that promises can be used as a prerequisite to forming trust and certainty. We give two examples using promise theory in distributed systems: object capabilities and verifiable claims.
