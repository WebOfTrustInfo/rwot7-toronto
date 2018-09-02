
**Not-a-Bot: A Use Case for Decentralized Identity using Proximity Verification to generate a Web of Trust**

Presented by Moses Ma and Claire Rumore, FutureLab 

Submitted to the 7th Rebooting the Web of Trust Technical Workshop as a discussion paper

September 24-26, 2018, Toronto

**_Keywords:_** reputation, trust, verified claims, identity, blockchain, decentralized, self-sovereign, proximity computing, botnet, sockpuppet, catfishing, proof of personhood

**PROPOSAL**

We propose to facilitate the collaborative drafting of a technical paper that describes the principles and key design considerations for a use case that utilizes Decentralized IDs and proximity verification to generate an intelligent, self-optimizing web of trust. We will also describe other issues, including adaptive functionality, user centric needs analysis and cognitive models, and a model for tokenized behavioral economics. 

We base much of our work on key design considerations for decentralized identity, claims and reputation, developed by C. Allen, M. Sporny, D. Reed, and many others (see references), at previous RWOT design conferences, as well as Proof of Personhood, developed by M. Borge, E. Kokoris-Kogias, P. Jovanovic, L. Gasser, N. Gailly, B. Ford, at the ƒcole polytechnique fŽdŽrale de Lausanne, Switzerland.

**BACKGROUND**

The Decentralized ID movement offers a rare and unique opportunity to fix certain deep, systemic flaws in the methods that currently manage online identity. One critical flaw deals with the misuse of identity to implement bots and sockpuppets. A sockpuppet is an online identity used for purposes of deception, which can span from their use for shilling to promote questionable businesses, to "astroturfing" which is the practice of masking the sponsors of a message or organization to make it appear as though it originates from and is supported by grassroots participant, to the manipulation of public opinion through weaponized propaganda. 

What is not realized by the majority of users is the scale of the social media fakes: Facebook reportedly has around 170 million known fake accounts, and Twitter may have as many as 20 million fakes. Whole industries exist around creating and selling such accounts, many state actors rely on them to achieve their aims. They are currently used by the governments of USA, Russia, China, Mexico, Syria, Egypt, Bahrain, Israel, and Saudi Arabia. It needs to be realized that each of these governments are acting in their own best interests, but in doing so, are defending the innate centralization of power. If the decentralization movement is to be successful, this is the key victory that must be won.

Permissionless blockchain-based cryptocurrencies use proof-of-work (PoW) to insure security. In the case of Bitcoin, the goal is to prevent double spending attacks, which results in the blockchain emerging as a kind of "truth machine". For decentralized identity to succeed, and not be co-opted as just another way to empower sockpuppets and botnets, there needs to be an equivalent to proof-of-work, a mechanism that binds physical entities to virtual identities in a way that enables accountability while preserving anonymity. This is now being referred to as "proof of personhood".

Our proposal is to use proximity verification, implemented with software toolkits such as Google Nearby and p2pkit, to bind virtual identities to real people, in a way that preserves privacy, non-correlation, zero-knowledge proofs and pseudonymous operations. We're currently building a technology called _Not_a_Bot_, which provides proof of personhood through a variety of techniques. One technique is to verify that the user has actually met another actual person, in physical spaceÉ and is "not a bot". 

This would be useful in many situations. For example, if two people met over Craigslist to sell a used bicycle, then the system could verify that the two parties actually met and transacted. If two people found each other through a dating site, and followed up with a face to face meeting, then the system could verify that these people were actually in the stated city and not catfishers from Ukraine or Nigeria. Many other use cases are possible.

It should be noted that a single instance of meeting is not as trustable as an entire history of meeting many people. For a state actor generating a legend for a sockpuppet, this would entail an unattainable level of work to prove personhood. For a regular human being, it's relatively effortless to use the system in an organic and unobtrusive manner. Furthermore, these histories of meetings and verifications Ñ using location data to prove it was not in Nigeria, and time data to prove it wasn't in the middle of the night Ñ would be aggregated to increase the trustability of the personhood assessment. 

Once a root personhood verification could be insured, then trustable pseudonyms could be generated. Adding this verification to decentralized identifiers, aka "DIDs", would provide trust in a trustless environment, as the DID could then provide identity and credentialing services in an environments that support, or even require, pseudonymity. Furthermore, tokenization could be used to drive the behavioral economics that could propel critical mass adoption and adaptive refinement of the technology to address continuously shifting tactics by centralizing powers and agents of deception.

**WHY THIS MATTERS**

Imagine a world where this technology has been deployed and globally adopted. Let us paint a picture for how this might be achieved. Imagine that this approach becomes part of a decentralized identity solution, driven by a robust and active developer community. The API produced would be integrated into applications that are used in e-commerce, social interaction, banking, healthcare, and so on. Now imagine that mobile telephony companies agree to embed the technology into the operating systems for all smartphones, and the dominant social network providers agree to use proof of personhood in their algorithms for determining which content to propel.

This would mean the end of phishing. The end of fake news. And the beginning of new era for society built on an interconnecting web of trust. This is greatly needed as trust in media is at an all time low, and centralized, algorithmic distribution have created a perfect storm for the rise of misinformation, disinformation and fake news. This is driving polarization while simultaneously undermining public trust in institutions.

However, realistically, there is no silver bullet that can solve the sock puppet problem. Proximity verification is one component of a multi-pronged solution that might work. Consider that certain highly problematic diseases can be treated with drug combinations consisting of antiretroviral compounds mixed with transcriptase inhibitors and steroids. The combinations are called "cocktails," and they're so effective that they're called the "Lazarus Effect," named for the biblical figure who was raised from the dead. Cocktails can turn an HIV death sentence into a manageable chronic condition. 

Just as complex and evolving health challenges must be addressed with complex and evolving multi-pronged solutions, the complex challenges of online identity require a comprehensive and systematic approach using multi-pronged solutions that synergistically combine to enable disruption, change and transformation at multiple levels. This paper aims help to determine what other solutions would need to be integrated, to create a "cocktail prescription" to address this problem. Automating the detection of misinformation is only half the problem. Preventing the weaponization of that propaganda is the other half, and this proposed technique could help provide at least part of a comprehensive cocktail prescription to address the issue of fake news. 

Clearly, we are in a burning house, as the Internet's current capacity to support democratic societies in making well-informed decisions is being subverted by globally networked state actors. However, there are additional benefits for this technology in social networking, connected governmental services, and e-commerce Ñ where the use of sockpuppets is more of an aggravation than a grave danger. For example, in terms of government service, we envision a system where elected officials could verify how many people they actually meet and how much time was spent with them, to back up claims of being a "man of the people". For a fully transparent politics, this system could provide the electorate with an accurate sense of whether a politician has actually met with leaders of social movements, or instead, is spending the majority of time with donors, lobbyists and political action committees.

**NEXT STEPS**

And so, our goal for this working paper is to map out functionality for such a system.  We wish to co-author, with members of the Rebooting the Web of Trust community, a position paper that seeks to address these these and related challenges and to produce meaningful solutions. And so, some of the deliverables we hope to develop during the workshop include:



1.  Create a user persona for a typical Not_a_Bot user to analyze tacit needs 
1.  Develop a number of detailed use cases, for different types of users and settings with different numbers of users meeting
1.  Develop an understanding for how DIDs would interoperate with proximity verification
1.  Develop a spec for the use of proximity verification with Verifiable Claims and Credentials
1.  Understand social/network interaction functionality between stakeholders and users to map out downstream functionality
1.  Examine how the system could help to drive non-correlation functionality
1.  Open discussion on other issues, such as cognitive models, optimization and AI models, the potential use of tokenization to drive behavioral economics

**REFERENCES**



1.  https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/did-primer.md
1.  Proof-of-Personhood: Redemocratizing Permissionless Cryptocurrencies, by Maria Borge, Eleftherios Kokoris-Kogias, Philipp Jovanovic, Linus Gasser, Nicolas Gailly, Bryan Ford. 2017 IEEE European Symposium on Security and Privacy Workshops (EuroS&PW), April 2017

Not_a_Bot.md
Displaying Not_a_Bot.md.
