# **Decentralized Error Reporting**

*A submission to Rebooting the Web of Trust #7*

Jack Poole, jack.w.poole@gmail.com 

Within regulatory frameworks, inspectors can be deceived firsthand despite the fact that individuals witnessed that a violation occurred. The following ideas describe how self-sovereign identity frameworks such as Sovrin [1] and Idemix [2] could enable individuals to issue pseudonymous claims backed by verifiable credentials regarding violations others have made, empowering whistleblowers with a new set of tools. This idea builds upon the previous work from the Rebooting Web of Trust III workshop's Portable Reputation Toolkit [3] on decentralized verification and certification.  As violation claims can be a contentious issue, steps should be taken to protect the claim issuer’s identity. 

These ideas were inspired by the innovative work of the ixo Protocol on measuring sustainable impact with Verifiable Impact Claims [4]. As traditional blockchain architecture doesn’t support verification of off-chain data, the ixo Protocol utilizes qualified evaluation agents to verify external claims. As trust in a third party is limited, empowering network participants to make sovereign claims and report dishonest impact data could strengthen trust in off-chain data.

# **Background**

**Empowering Decentralized Error Reporting**

 

The Portable Reputation Toolkit Use Cases whitepaper [3] describes a framework utilizing web3 primitives to enable decentralized fact checking. This framework allows individuals to generate a DID (decentralized identifier) and associated keypair registered on a blockchain, make a JSON-LD assertion signed by their DID’s associated private key, timestamp the claim on a public blockchain, and publish a JSON-LD evidence claim signed with their private key that points to uploaded media stored on IPFS. Others can support or oppose the claim by signing an assertion or publishing new evidence with their own corresponding DID. 

One example use case outlined how decentralized Fair Trade supply chain certification could be enabled by empowering workers to report if they are being underpaid and dispute wrongfully certified products. This framework allows workers to communicate with consumers directly through a public blockchain, even if the supplier has already signed a Fair Trade assertion.

In this use case, the **Product Owner** signs a *Fair Trade Assertion* claim with their DID that their coffee has been purchased from a Fair Trade supplier, the **Supplier** posts *Evidence* of this transaction and signs an *Evaluation* claim that supports the **Product Owner’s** claim, but the **Worker** challenges this claim by posting *Evidence* they were underpaid and signs an *Evaluation* claim with their DID that opposes the **Product Owner’s** *Fair Trade Assertion* claim.

# **Selective Disclosure and Zero-Knowledge Credentials**

Issuing claims that expose others’ wrongdoings is a highly contentious issue. For example, making a claim of Fair Trade violations against an employer could have devastating consequences for a worker. Without privacy protections people are often intimidated to remain silent. Being able to safely share information while protecting one’s identity could play a vital role in ensuring that violations are reported. 

Sovrin [1] and Idemix [2] allow individuals to make claims and share verifiable credentials without exposing their true identity. This is enabled through the use of pairwise-unique DIDs, verifiable claims, and zero-knowledge proofs (ZKP). 

**Decentralized Fair Trade Supply Chain Certification**

To incorporate zero-knowledge credentials, consider that a **Product Owner** (claim issuer) uses their registered public DID to issue a verifiable *Employment* *Credential* to all of their workers’ corresponding DIDs (claim holders). The **Product Owner** signs the claim with their DID verifying the employment status of the **Worker’s** corresponding DID, who countersigns the claim.

This credential is signed with Camenisch-Lysyanskaya (CL) signatures [2], allowing the **Product Owner** and **Worker** to collaboratively compute a signature on the claim. The **Worker** can use this signature as a proof parameter to prove the claim issuer’s signature without exposing the contents of the claim, making this credential a zero-knowledge credential.

To contest the **Product Owner’s** *Fair Trade Assertion* claim, the **Worker** generates a zero-knowledge proof of employment. This proof is sent to a verification contract on the blockchain to verify that they hold a valid *Employment Credential*. 

This contract looks at the blockchain (identifier registry) as a decentralized key-value datastore to verify that the **Product Owner’s** DID has signed the credential. As this DID is registered on a blockchain, the **Product Owner** doesn’t need to be contacted. The verification contract also verifies that the **Worker** has not changed any values within the claim, and asks the **Worker’s** DID to sign a challenge to verify control of the DID through a DID Auth request.

If the **Worker** holds a valid credential, the verifier issues a *Proof of Employment* claim. This claim is issued to a new pseudonymous DID that the **Worker** holds the private keys to. With this claim the **Worker** can sign a *Evaluation* claim contesting the **Product Owner’s** *Fair Trade Assertion*. 

These tools would enable the **Worker** to prove that they hold a valid *Employment Credential* without disclosing any other aspects about their identity. By utilizing pairwise unique DIDs, the **Worker** signs the Fair Trade violation claim with a unique DID, keeping the DID used with the **Product Owner** private. As this violation claim appears pseudonymously to others, the *Proof of Employment* claim allows others to verify that the violation claim was signed by a current employee. 

# **Next Steps**

I would like to explore these ideas further in order to better understand the potential and limitations of the above framework as it applies to different use cases. Within blockchain protocols, these preliminary ideas hold the potential to strengthen the verification process of off-chain data yet several questions still remain, including:

What attack vectors, either in software or hardware vulnerabilities, exist within this framework that could expose a user’s identity? 

If the subject of a violation claim can’t remove a negative claim about their identity, how does this challenge their notion of self-sovereign identity? 

What types of verifiable credentials could be useful to back a pseudonymous violation claim? 

How to safeguard users from sharing multiple verifiable credentials that could be correlated to their real identity? 

Implementing domain pseudonyms [2] (limiting a user to a bounded number of pseudonyms within a given domain or time period) could add protection against sybil attacks, but would this be too restricting for a user?

**References:**

[1][https://sovrin.org/wp-content/uploads/2018/03/Sovrin-Protocol-and-Token-White-Paper.pdf](https://sovrin.org/wp-content/uploads/2018/03/Sovrin-Protocol-and-Token-White-Paper.pdf)

[2][http://domino.research.ibm.com/library/cyberdig.nsf/papers/EEB54FF3B91C1D648525759B004FBBB1/%24File/rz3730_revised.pdf](http://domino.research.ibm.com/library/cyberdig.nsf/papers/EEB54FF3B91C1D648525759B004FBBB1/%24File/rz3730_revised.pdf)

[3][https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/final-documents/reputation-toolkit.pdf](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2016/blob/master/final-documents/reputation-toolkit.pdf)

[4][https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/verifiable-claims-of-impact.md](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/verifiable-claims-of-impact.md)
