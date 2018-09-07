# A Trustless Web-of-Trust &ndash; establishing identity uniqueness

By Ouri Poupko (ouri.poupko@weizmann.ac.il)

Ever since the first days of PGP, the notion of a web of trust was always around &ndash; well what else &ndash; trust. [The PGP user's guide](https://web.pa.msu.edu/reference/pgpdoc1.html) defines two questions that it aims to answer with a web of trust:
> 1. Does the key actually belong to whom it appears to belong?
> 2. Does it belong to someone you can trust to certify other keys?

The second question entails subjective trust. PGP asks the signer to designate the signed person as either unknown, untrusted, marginally trusted, or completely trusted. It then delegates trust along the web to establish a trust level for a specific individual, or at least trust that a specific public key represents a specific individual. While this may be the only way to validate someone in a decentralized environment, there are some disadvantages in using subjective trust:
1. It is not transitive. My father is a republican, He voted for President Trump. Does this mean that I trust President Trump?
2. It clusters a large community into subgroups depending on the individual acquaintances, while we might want to build services that are equally accessible to all community members.
3. It might be more easily gained by some people than others, not necessarily because they are more trust-worthy, but rather because they have better political and social skills.

Creating self-sovereign identities, the next natural step is to create self-sovereign communities. One tempting approach might be 'a friend brings a friend' approach. A computer algorithm can then accept new members, if enough existing members endorsed them. However, can we trust this approach? When the community is big, and it can be as big as the global community of all humanity, it is not easy to identify the real members of the community, if there is no central authority to do so. In this case I claim not only that subjective trust won't help much in identifying the correct community members, but rather that an objective endorsement &ndash; one that does not require the endorser even to know the endorsed person &ndash; is the best key for establishing community membership. We call a graph of such endorsements, where the claims made by the signers are objective claims, a Trustless Web-of-trust (TWOT). In the global community of all humanity &ndash; the politician and the shy, or even the honest and the crook, should all have the same egalitarian membership within the community.

## Communities

In order to define a community of self-sovereign identities, there are two requirements that should hold for each identity:
1. The identity should be truthful, meaning that it should represent an individual that is in this community (same as question 1 above)
2. The identity should be unique, meaning that there is no other identity within this community that represents the same individual

The second requirement is hard to validate. It is impossible for a human being and quite hard for a computer. Trust will not help me. Even with my closest friend, I cannot know for sure that he does not have a second identity that he is holding away from me. A computer can do quite a good job in scanning profile images, biometric information and such and identifying duplicates, but there still isn't a perfect human identifier for which the computer cannot be fooled.

The first question, on the other hand, is quite simple for a human being and quite impossible for a computer.

> ...it is only in the realm of human consciousness that we can define what it means to be human.  
> ...algorithms lack any awareness about the patterns they are trained to recognize. ... only a person can recognize another person.  
> &ndash; [Democracy.earth](http://bit.ly/defpaper)

To answer the two requirements above we coin the term &ndash; Uniquely Verifiable Identifiers (UVI). A UVI is an identifier (profile image, fingerprints, national ID number or anything else) that satisfies the following:
1. A human being confronting, or knowing, another individual and having access to his UVI can evaluate with high probability, while using standard means, whether the UVI identifies this individual or not.
2. There cannot be two UVIs of the same type representing the same entity, and an algorithm, given a set of UVIs of the same type, can evaluate with high probability whether there are duplicates in the set or not.

Assuming UVIs exist, we leverage on them to create a Trustless Web-of-Trust (TWOT) as defined above. An edge in the underlying graph from identity _p_ to identity _p'_ attests that _h_, the owner of _p_, acknowledges that the UVI in profile _p'_ represents _h'_, the owner of _p'_. It is required that all nodes in a TWOT use the same type of UVI. This is similar to the concept of key signing parties that was used by PGP, yet without the trust element. Also, by verifying the UVI within the profile, rather than the public key, a TWOT actually becomes a community, where each individual in the community is only registered once (up to the efficiency of the UVI comparing algorithm).

## A simple example

> [Catalans reach referendum day uncertain if they'll get to vote](https://www.bloomberg.com/news/articles/2017-09-30/catalans-reach-referendum-day-uncertain-if-they-ll-get-to-vote)

The [Catalan independence referendum](https://en.wikipedia.org/wiki/Catalan_independence_referendum,_2017) was held on October 1<sup>st</sup>, 2017 in Catalonia, Spain. The Spanish government opposed this referendum and ordered the police to confront the Catalan voters and prevent them from voting. About 43\% of the registered voters did vote, out of which about 92\% voted in favor of Catalonia becoming an independent state. Yet it was estimated that about 15\% of the registered voters did not vote due to the police intervention. International observers declared that the referendum failed to meet minimum international standards to be considered valid elections. What makes this story interesting for our case, is that it demonstrates a situation where the individual already has a unique identifier (his Spanish citizenship), supplied to him by a trusted centralized authority (the Spanish government), yet this central authority does not collaborate with the wish of the community to organize and hold a public pole.

An existing ID number is a very good UVI. Two strangers can easily identify each other by inspecting each other's identity card. Enlisting all ID numbers (of Catalan residents in this case) in a single public database (a distributed blockchain for example) makes it trivial for any computer with access to this database to make sure no one is registered twice. We claim then, that with their existing ID numbers, and a TWOT consisting of mutual identification acknowledgments, the Catalans could have had a great tool for enlisting all Catalans with a distributed, decentralized, voting application and holding their referendum in a safe and public manner without confronting the police at all.

## Fending off sybils

We therefor suggest the following procedure for defining communities with unique identities, based on the assumption that there exists a UVI that meets the above requirements well enough:
1. Individuals create their own self-sovereign identities and embed in their profiles a UVI that identifies them.
2. People randomly meet with other people for mutual identification &ndash; validating that the UVI in the other person profile indeed identifies him and cryptographically signing this UVI to express this validation.
3. Computer algorithms scan the web of endorsements continuously and verify that each UVI is unique within a given web.
4. A community based application that requires registration will require that only well connected identities be able to register. One way to measure an identity whether it is well connected, is to count the nodes in the graph that are reachable from this identity in some fixed number of steps and measure the percent of nodes in the graph that are in this group of neighbors.

The above procedure assumes that two strangers can easily verify each other's UVI. It further assumes that someone that wants to be part of the community will be incentivized to choose random verifiers. This incentive intensifies if he is limited to have a fixed number of verifiers (edges in the trust graph). A sybil on the other hand will have harder time to convince strangers to endorse him, especially if we require an undirected trust graph where each identification process must be mutual. We therefor anticipate that a sybil will stand out in a TWOT, being less well connected than an honest identity. Sybils may endorse other sybils, but that will create clusters which will even be easier to identify over a randomly connected graph. Obviously such a procedure is not bulletproof, but should fend off sybils quite well. Further investigation is required to mathematically model this procedure and estimate its efficiency.
