# Cryptographic and Data Modeling Requirements from RWoT
***RWoT Tribal Knowledge, Distilled - 200 Proof - May Cause Blindness***

by Manu Sporny, Dave Longley, and Chris Webber - ***Digital Bazaar***

RWoT is experiencing a groundswell of support and is busy welcoming new friends into the community. As people enter, some have a hard time navigating why we've made some of the technology choices that we have. For the uninitiated, it seems strange that we are so captivated by blockchains, zero knowledge proofs, graph-based data models, object capabilities, and other strange or experimental technologies.

This paper introduces the uninitiated to the requirements that have been identified over the years that are driving the community toward certain technological solutions.

## Introduction

Rebooting the Web of Trust is a community that is attempting to create a decentralized ecosystem that enables people to be in control of various aspects of their data and identity information. The group often talks about Decentralized Identifiers, Verifiable Credentials, Object Capabilities, ed25519 keys, cryptographic identifiers, and other technologies but rarely spends time documenting how we got here.

While it’s important to identify what this paper explores, it’s also important to note what it doesn’t talk about. We are not going to cover use cases in this document as there is ongoing work in this area. We are also not going to cover specifications and technology solutions as those are best discussed after understanding the content of this paper.

What this paper attempts to do is to collect some of the technical requirements around this decentralized ecosystem that we are all creating. Much of this information only exists as tribal knowledge at present. The hope is that by distilling this tribal knowledge, it will help people that are new to the group understand how we got to the technology solutions we are experimenting with today.

One could say that this paper exists in the vacuum between the use cases that the community is working on and the technological solutions the group is currently developing. The rest of this paper attempts to fill that vacuum with knowledge and documentation.

## Summary

In the event that readers are time constrained, this paper effectively identifies the following requirements created by the RWoT community over the last couple of years:

* The ideal RWoT data model is one that enables a person to assert anything about other people or organizations. Note that these assertions do not have to be true statements.
* Graph-based data models that enable semantically precise statements to be made are a requirement.
* The development of vocabularies that are used in these graph-based data models must be decentralized in nature and must guarantee conflict-free merging of knowledge graphs.
* The data that we express must be compatible with larger knowledge ecosystems.
* We need to be able to express data in HTTP-based APIs and HTML-based web pages, ideally using the same syntax.
* We need to support multiple syntaxes mapping to the same information model.
* Multiple mathematical proof formats need to be supported, including: proof lists and sets, proofs of work, zero knowledge proofs, object capabilities, and digital signatures.
* Ensuring that cryptographic keys have a specific purpose as well as expressing the purpose of a mathematical proof reduces the security attack surface.
* Developer ergonomics, which include, combining cryptographic options into simple choices that a novice developer can make with confidence, making code readability and debugging easier, and ensuring that the pieces that we have created are easily composable are important and will result in systems that are more secure.

The items above are explored in more depth throughout the rest of this paper.

## Our Open World Assumption

RWoT desires to empower people and organizations to own their identifiers (e.g., “My identifier is 1234”) and make claims about themselves and other entities (e.g. “1234 knows Jane.”). The types of claims one should be able to make are unbounded, just as it is in the real world. This requires a way of expressing data in what is called an “Open World”, as opposed to a “Closed World”.

Closed World systems are easier to build, secure, and write programs for. Most computing today happens in Closed World systems. Open World systems are much more powerful and expressive. They are also much harder to build, secure, and write programs for.

The Web is an Open World system. Concepts in one website link to concepts in other websites. The rest of this section identifies common requirements around open world systems, such as the one that RWoT is building.

### Graph-based Data Models

Open World systems are unbounded, meaning that things have relationships to other things and those relationships can extend far beyond the system that you are currently programming for. One way of representing this data is called a graph. A graph is a mathematical term for a set of nodes that are connected by lines (also known as edges).

The Web is naturally a graph-based data model. Web pages can be thought of as nodes, and they are connected by hyperlinks to other web pages. A large amount of human knowledge is encoded on the Web as a graph of web pages.

Concepts and knowledge on the Web can also be expressed as a graph-based data model. In fact, Google’s Knowledge Graph, Facebook’s Social Graph, and Microsoft’s Bing search engine all rely heavily on graph-based data models to answer search queries. It is a natural representation format for knowledge.

While there are other sorts of data structures such as lists, directed trees, and relational tables, only the graph is capable of efficiently expressing human knowledge and relationships. The ecosystem that RWoT is building is about expressing a graph of human knowledge and relationships. We are about putting people in control of their own graph of information.

### Semantically Rich Data Models

When people express concepts like “name”, it’s usually self evident what is meant. However, when someone says the word “address”, it’s not clear if the person means “home address”, “shipping address”, “email address”, or “IPv4 address”. The science of what a word means is called semantics.

Semantics are particularly important in computing because a computer doesn’t typically operate in the same fuzzy realm that humans do. While a human may have an easy time determining the semantics of “title” with a value of “Software Developer” as a job title, a computer may mistake the value to be the title of a book or a screenplay.

This problem is compounded in an Open World systems, such as the one that RWoT is building solutions for, because there are many systems with subtly different semantics behind their data models. Since RWoT is about expressing a graph of human knowledge and relationships, we must ensure that the semantics of the data models that we use are crystal clear to the software we are developing.

### Decentralized, Composable Data Vocabularies

Open World systems mean that development in those systems are typically happening in a decentralized and parallel way. Semantically rich data models are important, which means that how we develop and express semantics through data vocabularies are equally important.

One way to ensure that our data vocabularies do not conflict is to centralize all vocabulary development, which is typically done in Closed World systems. Unfortunately (for developers), Open World systems are, by their very nature, not centralized.

Since RWoT needs to empower people and organizations to express an unbounded set of claims, and because developers need to create vocabularies to do so in a decentralized way, the mechanism that we use to build vocabularies needs to be decentralized and composable in nature.

### Compatibility with Larger Ecosystems

The Web and Internet is built on standards and existing systems. Many of these systems that deal with human knowledge have many decades of experience behind them in building decentralized, scalable knowledge systems (such as the Web and Search Engines for the Web).

RWoT should be compatible with these graph-based knowledge systems, such as schema.org, which is a joint effort between Google, Microsoft, Yandex, and the major search engine companies to catalog semantically rich information that is published in a decentralized way via Web pages.

## Syntax Agnostic Expression

Expressing human knowledge has taken many forms throughout recorded history. From cave paintings, to hieroglyphics, to pictograms, to romanized languages, and mathematical languages. If there is one constant, it’s that the syntax of expression is continuously evolving while the fundamental information that is being expressed may not change at all.

For example, in mathematics, 1+1 has always equalled two. There are many ways to express that syntactically across a variety of languages, but there is fundamental information that doesn’t change between syntactic expressions.

Similarly, RWoT has a requirement to express data about people, organizations, and their relationships. That data can be expressed in a variety of different syntaxes, but ultimately the information related to those people, organizations and their relationships do not change.

### Expression in HTTP APIs

The systems that RWoT envisions will utilize at least HTTP APIs to exchange information. This establishes a requirement that the data model and syntax we use should be easily expressible in an HTTP API.

### Embeddable and Readable in HTML

The systems that RWoT envisions must also be able to utilize HTML web pages to express information, such as publicly available information: organizational credentials, public relationships between individuals and organizations, etc. This sort of information is already largely supported and consumed by search engine projects, such as schema.org.

The RWoT community should attempt to enable the expression of public data about people, organizations, and their relationships in a way that leverages broadly deployed infrastructure, such as schema.org.

### Canonicalization

There are three key observations about the expression of data in the systems that RWoT is building:

* Information may be expressed in a variety of syntaxes.
* The lifespan of information may be the lifespan of a human being, or longer in the case of an organization.
* The meaning of the information being expressed at an instant in time doesn’t change from syntax to syntax, and sometimes not over the course of decades.

These three observations lead to a suggestion that a canonical form to express information would be useful, especially for the purposes of digital signatures.

## Cryptographic Expressions

The ecosystem that RWoT is constructing is heavily reliant on a number of different cryptographic approaches to building the “Trust” part of “Web of Trust”. There are a variety of technologies that are being brought to bear on this problem. Understanding the requirements that led to these cryptographic solutions is important and often glossed over at RWoT meetings.

Of particular note is that people often jump to the conclusion that much of the “Trust” that we talk about at RWoT comes from digital signatures, but that is just a subset of the cryptographic toolkit in use.

At RWoT, we tend to focus on mathematical proofs such as proof of work, zero knowledge proofs, and capability invocation proofs, as well as the more well known digital signature proofs. The work we do here is about more than just digital signatures, it’s about expressing a variety of mathematical proofs that establish or enhance trust in decentralized systems.

### Signature Sets, Lists, and Composition

A Web of Trust is not generated by a single authority, but rather a collection of peers and organizations. This typically means that there is not just one digital signature issued by a single authority, but that there are many digital signatures involved in the RWoT ecosystem and the way those digital signatures are composed is important.

There are unordered sets of signatures, sometimes referred to as threshold signatures, where each party has equal authority. There are ordered lists of signatures, such as notarization, where one party must sign before the other party. There are also variations and compositions of unordered sets of signatures and ordered lists of signatures.

It is therefore important that the technology support sets of proofs, lists of proofs, and enables efficient composition and embedding of sets and lists of proofs.

### Proof of Work

A number of the new systems that are employed in RWoT are composed of permissionless blockchains, which require proof of work to protect against attacks against the ledger.

 Expressing a proof of work as one of the types of mathematical proofs should be supported.

### Object Capability Invocations

Object capabilities are a novel authorization mechanism that is experiencing further development, implementation, and specification work at RWoT.

Most websites ask the question “Who are you?” before giving you access to a resource. This has a number of very tragic side-effects, such as company departments sharing website passwords to get access to shared resources.

Object capabilities ask the question “Do you have a key to access this resource?”, and enable the delegation of authorization to do things. An analogy to object capabilities is a car key. The car doesn’t care who you are, it just cares that you have a key that gives you access. You can then give that key to people that you trust to give them access to your car.

Expressing object capabilities is another type of cryptographic construct that should be supported by the data model and mathematical proof system.

### Zero Knowledge Proofs

Zero knowledge proofs are useful when a person needs to prove something without strongly identifying themselves. An example where a zero knowledge proof is useful is when one would want to prove that they are over the age of 21 without having to provide a driver’s license or any other strongly identifying data.

Expressing zero knowledge proofs is a cryptographic construct that should be supported by the data model and mathematical proof system.

### Signature Purpose

A phishing attack is described as an attack against a victim where they are tricked into doing something that reveals their private information, usually enabling the attacker to temporarily steal the victim’s identity. When it comes to digital signatures, phishing attacks trick the victim into digitally signing something that authorizes access to a critical resource, or makes a payment to the attacker without the victim realizing what they are doing at the time.

One such attack is to trick a victim into digitally signing something that would log the user into a website and then replacing the login with something the attacker wants, such as a transfer of $5,000 to the attacker’s bank account. These sorts of attacks can be mitigated by only allowing digital keys to be used for one purpose and then including the purpose of a digital signature in the signature block itself.

The technical solutions that are used for the ecosystem that RWoT is building should ensure that both cryptographic keys and digital signatures are strongly bound to their intended purpose.

## Developer Ergonomics

Developers spend a great deal of their time debugging programs. When developers make mistakes when using cryptography in their programs, the results can be catastrophic. Therefore, it is important that we not only make it easier for developers to debug the cryptography in their programs, but also make it harder for them to make mistakes when writing cryptographic code in the first place.

The rest of this section covers requirements that the RWoT community has identified around developer ergonomics.

### Avoid Footguns (e.g. Cryptographic Suites)

A footgun is a term of art among software developers for a tool that, when employed, has a high probability of blowing the programmers foot off. Cryptography libraries, while powerful, are often footguns. They provide a dizzying array of options where some of the options, when combined, result in catastrophic outcomes.

The solution to having too many options is for cryptographic security professionals to curate those options into cryptographic suites and then use plain language to expose these suites to software developers.
For example, a cryptographic suite labeled “RsaSignatureAuthentication2018” seems to express that the cryptographic suite employs an RSA signature for the purposes of authentication and the suite was created in the year 2018. A developer with only a small amount of cryptography knowledge using that suite in the year 2025 may be prompted to see if there is an updated cryptographic suite that they should be using by merely seeing the date on the authentication suite.

While designing systems like this may seem like common sense, many cryptographic libraries today employ cryptic options such as ECDHE-RSA-AES128-SHA256, which result in a variety of programming errors by software developers with little understanding about what each of those options mean.

The systems that RWoT designs should ensure that developers are not handed footguns and are instead provided with tools with sensible defaults and a limited set of easy to understand options.

### Enable Readability While Debugging

A great deal of a software developers time is spent tracking down and debugging programming errors. At times, the readability of debugging output greatly impacts the speed at which software errors can be found and fixed. For example, improving readability while debugging can be as simple as not base64 encoding content when it can be avoided.

RWoT systems should minimize the time developers spend debugging by enabling readability of code while debugging.

### Composability

Composition is a powerful tool in computer science. This paper has explained how the composition of knowledge graphs lead to larger and more complete knowledge graphs. It has also talked about how different types of mathematical proofs can be composed in a way that enhances trust more than any single proof can achieve.

One common thread in the requirements outlined in this specification is that the composition of simple building blocks create powerful systems.

## Next Steps

The authors of this document would like to explore the following items at the upcoming RWoT7 event:

* Does this paper help fill a gap in knowledge that people new to the community have?
* Have we missed some key insight that would allow us to use existing technologies to meet these requirements?
* Are we missing or unaware of experimental technologies that would simplify technological implementations?

## Acknowledgements

Portions of the work on this document have been funded by the United States Department of Homeland Security's Science and Technology Directorate under contract HSHQDC-17-C-00019. The content of this specification does not necessarily reflect the position or the policy of the U.S. Government and no official endorsement should be inferred.
