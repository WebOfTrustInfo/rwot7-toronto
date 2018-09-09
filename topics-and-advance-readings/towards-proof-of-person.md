# Towards Proof-of-Person
Peter Watts - weboftrust@peterwatts.net

## Introduction
When exploring the design space of decentralized applications and protocols, sybil attacks thwart a large portion of the possibilities. This is especially true for anything social, like voting, wealth distribution, or attention measuring, where humanity and uniqueness are valued. In such systems, “one-CPU-one-vote” is not enough. A reliable “Proof of Person” (PoP) is required. 

So, how do we get there? How can we build something that reaches a sufficient level of adoption and robustness that we can actually start building true person-based applications? 

## Basic Overview
Given the goal of being useful in decentralized applications, it’s important that a PoP system is itself decentralized, self-sovereign and privacy preserving. In such an environment, it’s impossible to prevent the creation of multiple accounts. Instead, it needs to be difficult to accumulate sufficient reputation across many accounts. An account’s reputation score can then act as the probability that it belongs to an individual. In order to limit actions to unique people, applications building on top would specify the score required to participate.

Reputation would most likely be acquired through a Web-of-Trust model. As users trust each other (verify that they are unique), a strong network of relationships forms. The system could then use the topology the network to generate a reputation score, similar to PageRank. In order to output a global score, you would need to “anchor” to some trusted accounts, in order differentiate the real network from shadow networks of fake accounts, who all trust each other, but aren’t connected to legitimate accounts.

Additionally, an element of incentivized coordination is probably required, to keep the majority of participants honest. The network needs to be able to identity and punish bad behavior. In essence, when you trust someone, you are making a bet on them, and staking some of your reputation towards it. This could be taken a step further, with edges in the network acting as mini prediction markets. In the case of a challenge, reputation flows from the losers to the winners. Whatever the exact mechanics are, it’s important to have some sort of incentives that make honesty the optimal strategy.

## Tactics
Assuming we can design something that works in theory (a big leap), getting it live and adopted is an equally monumental task. Here a few suggested strategies:

#### 1. A Dedicated Network

There is a [wide spectrum](https://sinahab.com/2018/09/identity-and-reputation-in-web-3/) of work being done in the decentralized identity space, from claims specifications to credit scoring. In many cases, Proof-of-Person is within the scope of these efforts. However, it’s rarely the main focus. For one, these projects are taking on very large problems, that could take years to see adoption. And secondly, they are often either too broad, or too specific, and may not actually deliver PoP as desired.

With that in mind, it’s worth exploring the idea of a network solely devoted to solving this problem. This potentially brings a number of advantages:

Speed - By staying laser focused on the bare minimum that is required to offer PoP, it should be faster to get to market with a solution. 

Composability - A system that does one thing very well is able to cater to many different use cases, and is more likely to become an integral piece of the Web 3 stack. 

Integration - As a lightweight protocol with less moving pieces, it’s less daunting to build into other applications. Given that it’s usefulness increases with scale, reducing any barriers to early adoption are critical.

Messaging - With a singular focus, it becomes easier to explain why it needs to exist, and why it should be built upon. 

Community - While there is a strong movement around decentralized identity in general, the effort to achieve PoP feels uncoordinated. Forming a community that is entirely dedicated to solving this problem could bring the necessary focus to get there.

#### 2. Cost-efficient Proofs

One of the key design challenges to emerge in the last couple of years is the importance of scalability and cost effectiveness. Users can’t be expected to make frequent Ethereum transactions to participate, especially in relation to identity, where the value tied to each action is low. At the same, it’s critical that the information a PoP system produces is available to smart contracts on the most popular platforms, in order to be utilized.

A great example of this newer, cost-conscious approach is uPort’s [lightweight identity model](https://github.com/ethereum/EIPs/issues/1056) that allows the creation of identities without any on-chain transactions. While this works well for self-sovereign systems, it probably won’t work in a system where actions need to happen frequently and be globally available. As such, a more viable solution may be a dedicated reputation chain that can interface with parent chains like Ethereum. 

One option for achieving this is to regularly publish a merkle root of the ledger’s state to the parent chain, as seen in [Plasma](https://plasma.io/plasma.pdf), so that particular values can be proven. For example, if a user wants to use a voting application, they can attach a proof that says they have 50 reputation, and this can be verified without all the reputation scores needing to live on the parent chain. However, the downside of this approach is that it requires someone to publish these merkle roots, which has a cost, in every parent chain that you want the information available to. 

The ideal scenario is to have a similar system, without the need for regularly publishing merkle roots. Instead, a contract on the parent chain would only need to be initialized once, and from that point onwards, would be able to verify proofs produced by the reputation ledger. It’s unclear if this is possible to do safely, but this is the sort of research that should be prioritized, because without a scalable way to accumulate and prove reputation, the system is unlikely to be used.

#### 3. Frictionless & Fun

Like any social network, a PoP system will have a chicken and egg problem, so it’s critical to think about ways to drive early usage. A common response in the space is to introduce financial incentives, in the form of a token. While this may indeed be the best path, it could also warp the more implicit incentives that centralized social networks have used so effectively to grow. So it’s worth considering alternatives.  

Frictionless - A key target for adoption is application developers. The target should be for any application that could potentially benefit from the protocol to verify their entire user base. They may not get immediate value, but the goal would be to make the cost low enough that applications do it “just in case”, similar to basic SEO. Eventually, as the network grows, applications could benefit from the discovery of fraudulent users, or the ability to reward high reputation users.

Fun - There is something almost addictive about building out a network of connections. Facebook and LinkedIn have leveraged this to great effect, turning the urge to “collect” relationships into viral growth. Building out your reputation on the decentralized PoP network should be equally fun and competitive. Consumer-oriented applications should be an early priority, and they should be gamified to feel more like Pokemon (catch em all!) than an address book.

The protocol should be designed with these adoption strategies in mind. For example, it should be possible to create an identity on the fly in whatever app you’re using, and easily unify accounts on different apps under a single identity (preserving privacy where possible). Or it may also make sense to be able to verify people before they have account, prompting them to join and giving them some reputation to begin with. 

## Next Steps
In summary, despite the many difficult challenges remaining, Proof-of-Person appears to be an attainable goal. And given the scope of what it would enable, it’s a problem worth solving. If anyone is interesting in working on it, or is already doing so, please [get in touch](mailto:weboftrust@peterwatts.net). 
