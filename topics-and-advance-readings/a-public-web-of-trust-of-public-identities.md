# A Public Web of Trust of Public Identities

By Ouri Poupko (ouri.poupko@weizmann.ac.il) and Ehud Shapiro (ehud.shapiro@weizmann.ac.il)

> In the world of people's public actions, privacy is not the name of the game, it is instead a well-known single public identity. - Tim Berners-Lee

Following Tim Berners-Lee design issue of [a public identity](https://www.w3.org/DesignIssues/PublicIdentity.html) we are investigating ways, not only for a person to manage and maintain both his private and public credentials, but also to obtain trust over his public identity. Such trust will have many benefits, including:
1. As Berners-Lee suggests, public figures would like to make sure that their public activity is clearly associated with them and no one else.
2. At least minimal trusted publicity is required to help reduce fake identities (sybils) and their [impact on social networks](https://www.telegraph.co.uk/technology/2017/11/02/facebook-admits-270m-users-fake-duplicate-accounts/)
3. It [enables democratic processes](https://cacm.acm.org/magazines/2018/8/229759-point/pdf), specifically voting, in a fully decentralized and distributed way based on self sovereign identities.

## definitions
We start by mathematically define the concepts of a **public identity** and a **public web of trust**<sup>[1](#fn1)</sup>. Let ![H](http://latex.codecogs.com/svg.latex?%5Cmathcal%7BH%7D) be a set of people and ![A](http://latex.codecogs.com/svg.latex?%5Cmathcal%7BA%7D) a set of attributes which are predicates over people. For each ![h in H](http://latex.codecogs.com/svg.latex?h%5Cin%5Cmathcal%7BH%7D) and ![a in A](http://latex.codecogs.com/svg.latex?a%5Cin%5Cmathcal%7BA%7D), ![ah is true](http://latex.codecogs.com/svg.latex?a(h)%3Dtrue) if the predicate ![a](http://latex.codecogs.com/svg.latex?a) holds for the person ![h](http://latex.codecogs.com/svg.latex?h).  A profile is a finite set of attributes ![A subset A](http://latex.codecogs.com/svg.latex?A%5Csubset%5Cmathcal%7BA%7D).

A person ![h in H](http://latex.codecogs.com/svg.latex?h%5Cin%5Cmathcal%7BH%7D) who created a key-pair ![K_P K_S](http://latex.codecogs.com/svg.latex?%28K_P%2CK_S%29) is the owner of ![K_P](http://latex.codecogs.com/svg.latex?K_P) and ![K_S](http://latex.codecogs.com/svg.latex?K_S). A **public identity** ![p equals K_P and A](http://latex.codecogs.com/svg.latex?p%3D%28K_P%2CA%29) consists of a public key ![K_P](http://latex.codecogs.com/svg.latex?K_P) and a profile ![A](http://latex.codecogs.com/svg.latex?A) signed with the corresponding private key ![K_S](http://latex.codecogs.com/svg.latex?K_S).  ![A](http://latex.codecogs.com/svg.latex?A) is called the profile of ![p](http://latex.codecogs.com/svg.latex?p). 

Let ![P](http://latex.codecogs.com/svg.latex?P) be a set of public identities with profile attributes in ![A](http://latex.codecogs.com/svg.latex?%5Cmathcal%7BA%7D).  A trust edge over ![P](http://latex.codecogs.com/svg.latex?P) is a directed edge ![e from p to p'](http://latex.codecogs.com/svg.latex?e%3Dp%5Cxrightarrow%7BT%7Dp%27),  ![T subset A](http://latex.codecogs.com/svg.latex?T%5Csubset%5Cmathcal%7BA%7D) and ![p,p' in P](http://latex.codecogs.com/svg.latex?p%2Cp%27%5Cin%20P). The trust edge ![e](http://latex.codecogs.com/svg.latex?e) is called truthful if ![T](http://latex.codecogs.com/svg.latex?T) is true of ![owner p'](http://latex.codecogs.com/svg.latex?%5Ctextrm%7Bowner%7D%28p%27%29) and an attack edge otherwise. A **public web of trust** over ![P](http://latex.codecogs.com/svg.latex?P), also called a trust graph, is a graph ![W is P and E](http://latex.codecogs.com/svg.latex?W%3D%28P%2CE%29) with a set of trust edges ![E](http://latex.codecogs.com/svg.latex?E) over ![P](http://latex.codecogs.com/svg.latex?P).

## DID implementation of a public web of trust

Next we describe an implementation of a public identity and a public web of trust, using the DID specification and the Verifiable Credentials specification. As DID supports privacy, but does not require it, most of the implementation is straight forward. A DID document can hold multiple public keys and can describe separate keys for authentication Vs. authorization. As long as all these keys are bounded together in a single public DID document, they can be regarded as synonyms for the one public key that identifies a public identity. A DID document can point to a verifiable credentials service that can expose the owner's attributes, whether cryptographycally encoded or not. Attributes can be attested by 3<sup>rd</sup> parties, or self attested by the owner on himself. A DID document with an accompanied verifiable credentials storage can therefor serve as a public identity as defined above.

To create a public web of trust we use a second verifiable credentials service, with our own defined context, defining a single field for the claim called 'trustedAttributes'. The 'id' field for this claim is the DID of the trusted person and the 'issuer' of this verifiable claim is the trusting person. See the image below for an example. A digital signature of the trusted claim, signed by the issuer, can prove the validity of the trust claim. Such a verifiable claim can serve as a trust edge as defined above, revealing only ids of the trusting person, the trusted person and his trusted claim. Storing all such trusted edges for a given community in a single service point can provide a complete trust graph for that community, as defined above.

![Public web of trust as verifiable credentials](https://github.com/ouripoupko/papers/blob/master/images/DIDDataStructure.png)

## further work

The e-Democracy group in the computer science department of the Weizmann institute of science, led by Prof. Udi Shapiro is investigating the computational foundations for e-Democracy. Towards this goal we add the following definitions<sup>[1](#fn1)</sup>:

A profile ![A](http://latex.codecogs.com/svg.latex?A) is true of a person ![h](http://latex.codecogs.com/svg.latex?h), ![Ah is true](http://latex.codecogs.com/svg.latex?A%28h%29%3Dtrue), if ![ah is true](http://latex.codecogs.com/svg.latex?a%28h%29%3Dtrue) for all ![a in A](http://latex.codecogs.com/svg.latex?a%5Cin%20A). Let ![HA in H](http://latex.codecogs.com/svg.latex?H_A%5Csubset%5Cmathcal%7BH%7D) be the set of people of which ![A](http://latex.codecogs.com/svg.latex?A) is true, ![HA definition](http://latex.codecogs.com/svg.latex?H_A%3D%5C%7Bh%3Ah%5Cin%5Cmathcal%7BH%7D%2CA%28h%29%3Dtrue%5C%7D). The profile ![A](http://latex.codecogs.com/svg.latex?A) is:

* fake if ![HA is empty](http://latex.codecogs.com/svg.latex?H_A%3D%5Cemptyset).
* transparent if ![HA has one item](http://latex.codecogs.com/svg.latex?%7CH_A%7C%3D1).
* opaque if ![HA has more items](http://latex.codecogs.com/svg.latex?%7CH_A%7C%3E1).

Let ![p equals K_P and A](http://latex.codecogs.com/svg.latex?p%3D%28K_P%2CA%29) be a public identity. The owner of ![p](http://latex.codecogs.com/svg.latex?p) is the person who owns its public key, ![owner p is owner kp](http://latex.codecogs.com/svg.latex?%5Ctextrm%7Bowner%7D%28p%29%3D%5Ctextrm%7Bowner%7D%28K_P%29). The public identity ![p](http://latex.codecogs.com/svg.latex?p) is:

* honest if its profile ![A](http://latex.codecogs.com/svg.latex?A) is true of its owner, ![A owner p is true](http://latex.codecogs.com/svg.latex?A%28%5Ctextrm%7Bowner%7D%28p%29%29%3Dtrue). Otherwise, ![p](http://latex.codecogs.com/svg.latex?p) is sybil.
* unique if it is the sole public identity owned by its owner, ![uniqueness](http://latex.codecogs.com/svg.latex?%5Ctextrm%7Bowner%7D%28p%29%3D%5Ctextrm%7Bowner%7D%28p%27%29%5CRightarrow%20p%3Dp%27). Otherwise, ![p](http://latex.codecogs.com/svg.latex?p) is non-unique.
* fake, transparent, or opaque if its public profile is so, respectively.

We expect an e-democracy to strive that its public identities be honest and transparent. To achieve this we use graph conductivity to analyze a trust graph and bound the number of sybils in a graph. A public web of trust as proposed here can serve as such a graph and hence enables the identification and eradication of sybils in a community based on self sovereign identities. Some relevant preliminary results can be found [here](https://arxiv.org/search/?query=ehud+shapiro&searchtype=author&source=header). Abstracts of ongoing research can be found [here](https://www.dropbox.com/sh/51lt6o1ak1to6zj/AACKIfEgi81q3_K3nxkDXKX-a?dl=0).

## References

<a name="fn1">1</a>: Poupko, O and Shapiro, E, _A Public Web of Trust of Public Identities: Supporting Sybil-Resilient e-Community Building_. In preparation, https://www.dropbox.com/s/lahp4shi2edstn4/public-web-trust.pdf?dl=0, 2018.
