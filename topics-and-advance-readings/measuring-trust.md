# Measuring Trust

The following is a digest of my paper [Measuring Trust](../supporting-files/measuring-trust.pdf).

I created a visualizer to accompany this paper: https://wot-vis.firebaseapp.com/

## Abstract

> “I'm not reading a good review on Yelp.”

> “That's not good, hmm? Mmm, you know what? Fuck it, 'cause this is usually just one pissed off dude who had a bad experience and then wrote, like, 50 bad reviews.”

This is an excerpt from the Netflix show Love (season 1, episode 5). It’s a trivial example of the more general problem of Sybil attacks, situations where a malicious actor games a system that relies on the assumption of unique identity by creating numerous fake accounts.

The concept of an open and permissionless system is philosophically appealing. However, there are certain applications that require the concept of trusted identities. At a minimum, all systems that involve voting rely on unique, trustworthy identities to cast a vote. This includes any consensus mechanism as well as any rating system. Such systems face a dilemma: how can we filter out bad actors without a centralized authority?

In this paper, I propose the concept of deriving relative trust scores using a given trust metric, one score for each identity from the perspective of another, in a web of trust. I then offer as examples multiple trust metrics, propose the concept of relative reputation, and explore the the idea of obtaining social consensus from a web of trust using trust scores.


## Economic Sybil-resistance

Existing solutions to the Sybil problem seem to generally rely economic incentives. Bitcoin (and other systems based on proof-of-work), for example, makes influence in the network computationally expensive. Proof-of-stake, as an alternative, requires tokens to be staked in exchange for influence. In other words, these solutions are pay-to-play; Sybil attacks are no longer feasible because they are expensive.

However, I am interested in exploring an alternative to economic-based systems. There are a couple of reasons for this. The first is philosophical; pay-to-play systems inherently favor the economically privileged, and are less accessible to those with less economic resources. I believe that true decentralization should not discriminate based on economic privilege.

The second reason I am interested in another solution is practical. I believe there exists at least one class of applications where economic incentives fall short. The class of applications I have in mind is reputation. I use the word reputation in a very broad sense; this could be anything from a personal reputation to a product rating. I believe that economic solutions to reputation fall short because they lack a key piece of information: trust. I contend that reputations, in the real world, are based on trust. More specifically, they are based on a peer-to-peer network of trust.

## A Relative Trust Score

Google’s PageRank algorithm is famously able to assign ranking scores to web pages from a directed graph, where edges represent links from one website to another. One major problem with PageRank, however, is that it is vulnerable to Sybil attacks. Indeed, after Google implemented PageRank we witnessed the phenomenon of link farms - a form of Sybil attack that takes advantage of the fact that (in the pure form of PageRank) all pages are first-class citizens with equal ability to cast “votes” in the algorithm, in the form of web links. Dummy web pages could be created cheaply to deceive the algorithm. Of course, it is now widely known that Google uses a much more sophisticated version of PageRank that is less susceptible to link farms (though the algorithm itself is kept secret).

Deriving trust scores in an open web of trust is similar to the problem of deriving web page rankings in an open internet, in many respects. Both the web of trust and the internet can be represented as a directed graph, where edges represent votes from one node in favor of another. Indeed, the defunct website Advogato used a web of trust with designated “seed nodes” in order to generate trust scores for members of the site [1]. Advogato’s solution was Sybil-resistant thanks to the seed nodes, and Google’s updated ranking algorithm may very well use a similar concept of “seed” websites to strengthen to protect against link farms (though I am only speculating here).
There is a problem with seed nodes, however. Seed nodes are inherently more powerful than other nodes - an inequality of power that we do not want in a decentralized system. Seed nodes seem to be necessary when these two requirements exist for a graph-based system: (1) that it must produce absolute scores for each node (2) that it must be Sybil-resistant. We want to keep the second requirement, obviously. But what if we were to relax the first?
I will demonstrate that we can have a seed-free, Sybil-resistant, decentralized system that produces relative trust scores, or scores that will vary based on the observer. While relative scores may not be sufficient for all applications, there are may be some problems that can be solved merely with relative trust scores.

I will define a trust score as the result of a function that receives at least 3 parameters: the web of trust itself (represented as a directed graph), the observing node, and the observed node. For the same web of trust and the same observed node, but a different observing node, it is possible to produce different trust scores. Hence they are considered relative.

The implementation of the function itself is left open for now. I will refer to a trust score generation algorithm as a trust metric (borrowing from Advogato’s terminology). This will allow us to discuss the concept of trust scores without being married to a particular implementation of them.

## A Definition of Sybil-resistance

So far I have been using the term Sybil-resistance rather vaguely. Here I will provide a precise definition that applies to the manipulation of trust scores in a web of trust.

To do this, I will borrow the concept of good nodes, confused nodes, and bad nodes from Advogato. Good nodes in a web of trust are honest and will not attempt to manipulate trust scores. Confused nodes are also honest and will not attempt to manipulate trust scores, but may mistakenly trust one or more bad nodes. Bad nodes, then, are those that will create fake nodes in order to game the system in some way.

The definition of a confused node is rather open-ended, however. Does a confused node trust a single bad node, or multiple bad nodes, or an unlimited number of bad nodes? For the sake of clarity, I will define an edge from a confused node to a bad node as a confused edge. I will also define a puppet node as a fake identity in a web of trust created by an attacker for the purpose of gaming the system. More precisely: puppet nodes are the subset of bad nodes that are not adjacent to a confused edge.

![trust node diagram](../supporting-files/trust-node-diagram.png?raw=true)

I propose the following definition: a trust metric is Sybil-resistant if and only if the upper limit of the combined trust scores that can belong to bad nodes is bounded by the number of confused edges. Stated another way, a trust metric is Sybil-resistant if and only if there is a finite amount of combined trust an attacker can gain in a system merely by creating puppet nodes.
This definition alone is not sufficient when considering Sybil attacks. While it helps to know that the impact that a Sybil attack can have is bounded, we might also wish to know the degree of Sybil-resistance that a metric has. I will define the degree of Sybil-resistance as the maximum trust that an attacker can have with a single bad node, divided by the maximum combined trust that can be accumulated by an attacker with an unlimited number of puppet nodes. A metric where puppet nodes have no effect has a Sybil-resistance degree of one. A metric where puppet nodes can increase the combined trust score of an attacker has a Sybil-resistance degree less than one. And a metric where puppet nodes can increase the combined trust score of an attacker without bound has a Sybil-resistance degree of zero (i.e. is not Sybil-resistant).

## Use Case: Relative Reputation

Today’s online systems use absolute scores to portray the reputation of identities. Commonly known examples are ratings for businesses on Yelp or upvotes on Stack Exchange answers. I refer to these scores as absolute because everyone sees the same scores. In contrast, relative scores vary based on the observer. I am not aware of any current system that uses relative reputation.

The web of trust provides an information layer that makes relative reputation possible. For example, Amazon product ratings could be weighted by the trust score of the author of each review. With absolute reputation scores, the rating of an item will simply be the average of all posted ratings. But using relative reputation and a web of trust, the rating of an item could be a weighted average of the ratings, based on the trust score of the author. Because trust scores vary from observer to observer, two people could see completely different ratings for the same product.

I have discovered one project that used a similar concept. The Outfoxed browser extension (now defunct) allowed users to enter their “informers” (people they trusted), which essentially generated a web of trust. Websites were then tagged according to how trustworthy they were based on the user’s network of trust [2].

## Use Case: Social Consensus

As mentioned previously, consensus is a process that requires some mechanism to defend against Sybil attacks. By consensus, I simply mean the process by which a group of individuals can agree upon a shared state. Current decentralized consensus mechanisms generally rely on economic incentives to defend against Sybil attacks and bad influence. When I use the word economic here, I mean that influence in the system can usually be purchased with money, either directly or indirectly.

However, I am not entirely convinced that economic incentives are ideal for decentralization. In fact, I believe that true consensus is social and based on shared trust, even when the consensus mechanism itself is economic. I agree with Vitalik Buterin’s statement [3]:

> ...social considerations are what ultimately protect any blockchain in the long term.

However, he went on to say:

> ...blockchain protected by social consensus alone would be far too inefficient and slow, and too easy for disagreements to continue without end.

Perhaps this is true. Nonetheless, I would like to explore the possibility of achieving consensus through a web of trust.
Personally, I find Buterin’s theoretical social defense mechanism against 51% attacks in proof-of-stake valid but also awkward. He states:

> Theoretically, a majority collusion of validators may take over a proof of stake chain, and start acting maliciously. However… if they try to prevent new validators from joining, or execute 51% attacks, then the community can simply coordinate a hard fork and delete the offending validators’ deposits.

This is a social consensus defense mechanism, but it is an awkward one. So, to defend a proof-of-stake protocol against a 51% attack, the solution is to fork the protocol itself? I understand that such an attack may be unlikely. Yet there is a part of me that seeks a more elegant solution. I also believe that it is hard to estimate the possibility of such attacks, and even harder to predict how a community would react to them. I like the spirit of Buterin’s solution, but I wonder if we cannot do better.

I propose the following as food for thought: why can this forking process not be part of a protocol itself? More fundamentally, what if we had a protocol for social consensus? Perhaps this protocol would be “inefficient and slow”; perhaps more efficient layers would need to be built on top. Still, I think there may be significant value in a social consensus protocol. I also conjecture that if such a protocol were to exist, it would be based on a web of trust.

I will propose a naive concept as an example. Suppose some sort of efficient data sharing layer were to exist, one on which trust data between nodes could be easily stored and accessed. In this scenario, we could define the concept of a community as a set of nodes which mutually trust one another. That is, each node in the community would need to have a minimum trust of t as observed by all other nodes in the community. Each node in the community could be considered to have one vote in establishing a shared state for the community. Thus the community could achieve consensus.

I have not explored this proposal in depth. I can think of numerous concerns already. How would the data be stored and accessed reliably and efficiently? What trust metric and minimum trust score could be used to maximize inclusivity but deter malicious influence? I do not have answers to these questions at the moment. I am simply offering this proposal to stimulate thought and conversation around the idea of social consensus built on a web of trust.

## References

- [1]    [Advogato’s Trust Metric](https://web.archive.org/web/20170627230829/http://www.advogato.org/trust-metric.html.)
- [2]    S. James, [What is Outfoxed?](http://getoutfoxed.com/about)
- [3]    V. Buterin, [A Proof of Stake Design Philosophy](https://medium.com/@VitalikButerin/a-proof-of-stake-design-philosophy-506585978d51)
