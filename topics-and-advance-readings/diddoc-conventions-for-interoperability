# DIDDoc Conventions for Interoperability
***A Survey of DID Usage and Interoperability***

by Stephen Curran (***BC Gov and C3I***), Olena Mitovska (***Ontario Gov***)  and collaborators

The [Decentralized Identifier Specification](https://w3c-ccg.github.io/did-spec/) is moving along the standards path and we are seeing the availability of DID Methods (including [resolvers](https://github.com/decentralized-identity)) that implement the specification. As hinted at in the [DID Primer](did-primer.md), DIDs are being used for a variety of purposes, including enabling a Verifiable Credentials infrastructure.

It has been the experience of the BC and Ontario Governments that as we have built out an initial version of the Verifiable Organizations Network ([VON]) using the Hyperledger Indy project that there is a lot that is not said in the DID Specification about how the use of DIDs will be interoperable. Our goal is to be able to recommend to our citizens and businesses Self Sovereign Identity (SSI) components that are both interoperable with what the Governments of BC and Ontario use and that meets expected privacy and security goals aligned with the [Pan-Canadian Trust Framework](https://diacc.ca/pan-canadian-trust-framework/). A crucial first step in accomplishing that interoperablility is aligning the conventions being used in DIDs and DID Documents (DIDDocs) across DID Method ecosystems.

The purpose of this paper is twofold - a pre-conference survey of progress made to this point on DIDDoc usage by each DID Method community, and then an attempt at RWoT to "compare and contrast" the different approaches to see what can be learned across the wider community and what alignment can be defined at this time that might lead to interoperability.

## DIDDoc Usage by DID Method Communities

The first task, done ideally before RWoT7, is to collect from those building DID Methods and associated ecosystems an outline of how they are using the elements of a DIDDoc. For example, if two arbitrary Identities that are using software developed by different vendors have exchanged DIDs, and one wishes to send the other a secure, privacy-preserving message, what parts of the Receiver's DIDDoc are used and how? More generally, a DIDDoc from an Identity has a series of entries (keys, authorizations, service endpoints). What are the purposes of those entries and how does the user of a DIDDoc know the purpose and expected use of those entries?

Ideally, a representative from each DID Method community will document (or at least come to RWoT7 ready to speak about) the progress made so far in the usage of DIDs, particularly focused on conventions that enable multi-vendor interoperability. For example, the Hyperledger Indy Agent to Agent Working Group has a (currently pending) [Proposed Enhancement](https://github.com/hyperledger/indy-hipe/blob/efba4bc0de42fd194a8d6af8864bcd96e6826f58/text/diddoc-conventions/README.md) that defines some preliminary expectations that one Identity can have about a DIDDoc received from another Identity. Having an equivalent type of document from each DID Method community would provide a number of perspectives on the planned uses for DIDs.

## Microledgers

Related and ideally included in the survey is the idea of a microledger between identities - DIDs and DIDDocs created by one identity and shared only with the identity(ies) with which the DID will be used. If different DID Method communities are planning on using microledgers, it will be useful for interoperability to discuss how the DIDDoc is intended to be managed on a microledger across the communities and to look for shared approaches.

# DIDDoc Conventions

During RWoT, the focus of the group will be on inventorying the concepts, aligning those that are common, and formalizing DIDDoc Conventions that are shared and those that are unique to specific communities. Coming out of the conference we'd like to see a published paper that outlines the conventions - a versioned document that evolves as the various implementations mature based on the different DID Methods. The paper will be a starting point for learning about the DIDDoc Conventions to implement and to provide guidelines for adding interoperable, DIDDoc-based concepts within each community.

