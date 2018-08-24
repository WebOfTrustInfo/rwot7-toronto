# Zero Trust Computing with DIDs and DADs

Author: [Samuel M. Smith Ph.D.](sam@samuelsmith.org)


2018/08/24



This paper builds on the RWOT Spring 2018 [Decentralized Autonomic Data](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2018/blob/master/final-documents/DecentralizedAutonomicData.pdf) paper wherein a new class of data item called a DAD was introduced that used DIDS and Derived DIDs (DDIDs) as a self-certifying identifier to lay the ground work for data provenance. The focus of the DAD paper, however, was not data provenancing but simplified key management of the DIDs associated with DADs. Indeed, since the Spring RWOT 2018 workshop, the two new key management techniques proposed in that paper have been under active development. 

The first is a key pre-rotation service for DIDs. It includes a server and both a python command line client and javascript web client with associated SDKs.  These are open source (Apache2) and can be found here [Didery Server](https://github.com/reputage/didery), [Didery Javascript Client](https://github.com/reputage/didery.js), and [Didery Python Client](https://github.com/reputage/didery.py). Didery is a fully functional beta release.

The second is a 3D game mnemonic for key recovery called SeedQuest. This is also open source (Apache2) and can be found here [SeedQuest](https://github.com/reputage/seedQuest). SeedQuest is under active development and is planned for beta release sometime in October.

This Difuse Tust Computing paper focuses on using DIDs and DADs for data provenancing in distributed applications.  In an earlier paper in 2017 [Many Cubed](https://github.com/SmithSamuelM/Papers/blob/master/whitepapers/ManyCubed.pdf) we explored the architectural issues of building distributed computing infrastructure that applied the *Zero Trust* security model. This type of architecture we called *Zero Trust Computing* or more correctly *Difuse Trust Computing*. A simple way of explaining the Zero Trust security model is the mantra, *never trust, always verify*.  The paradigm of Zero Trust Networking was first popularized in 2013 by the NIST report here [Developing a Framework to Improve Critical Infrastructure Cybersecurity](https://www.nist.gov/sites/default/files/documents/2017/06/05/040813_forrester_research.pdf). More recently the principles have received much broader attention including the book [Zero Trust Networks](https://www.amazon.com/Zero-Trust-Networks-Building-Untrusted-ebook/dp/B072WD347M/ref=sr_1_1?ie=UTF8&qid=1535124339&sr=8-1&keywords=zero+trust+networking).  

The basic approach to Diffuse Trust Computing is to use a diffuse trust perimeterless security approach. Some call this a trustless or zero-trust security model but that is a misnomer. There is still trust, it is just diffused in such a way that security is greatly enhanced. See [Many Cubed](https://github.com/SmithSamuelM/Papers/blob/master/whitepapers/ManyCubed.pdf)



The assumptions and principles of diffuse trust perimeterless security are: 

1) The network is always hostile both internally and externally; locality is not trustworthy.

2) By default, every network interaction or data flow must be authenticated and authorized using best practices cryptography. 

3) By default, inter-host communication must be end-to-end signed/encrypted and data must be stored signed/encrypted using best practices cryptography; Data is signed/encrypted at motion and at rest.

4) Policies for authentication and authorization must be dynamically modified based on behavior (reputation).

5) Policies must be governed by distributed consensus.

Distributed consensus diffuses the trust for any policy decision to a group of hosts. In order to defeat the policy, an attacker must exploit some majority of the hosts. This makes exploits exponentially more difficult. Using end-to-end encryption and storage prevents exploits from anyone that merely has access to the network or the data storage device.  By authenticating and authorizing every network interaction or data flow, security becomes granular. A successful exploit of one interaction does not bleed into any other. Compromising one data flow does not compromise any other. Escalation opportunities are minimized. Many security exploits are discovered through repeated probes and experiments to find bugs, buffer overflows, or weaknesses in network protocols or software implementations. Dynamic policy modification that uses AI to first profile and detect anamalous behavior and then restrict the authorization of that user prevents discovery. This adds time as a defence.

This paper extends these principles with one more, that is,

6) By default, each data flow including transformation must be end-to-end provenanced using decentralized identifiers.

This additional principle establishes ownership and control over the data using a decentralized trust model and a decentralized web of trust, in this case based on DIDs. This approach enables truly decentralized governance models for distributed applications. After combining 6) with 3) above, the result is that data flows must be provenanced/signed/encrypted at motion and at rest.  

This paper will explore salient issues in using DIDs and DADs to maintain provenance over each step in a data processing flow including transformations of the data to enable credible uses of the data for various applications while maintaining a zero or difuse trust security model.



