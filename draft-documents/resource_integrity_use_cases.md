# Resource Integrity Use Cases

Authors: Ganesh Annan and Kim Hamilton Duffy

Currently, the Web provides a simple yet powerful mechanism for the dissemination of information via hyperlinks. Unfortunately, there is no generalized mechanism that enables verifying that a fetched resource has been delivered without unexpected manipulation. [Resource Integrity Proofs](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/resource-integrity-proofs.md) enable verification of any representation of a resource from any type of link. This paper describes how RIP solves use cases inspired by production deployments of self-sovereign technologies. One is the problem of [Verifiable Displays](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/verifiable_displays.md), which seeks to ensure the rendering of the VC content matches what the issuer intended. Another is verifying integrity of referenced data; for example, if the referenced data is in a mutable store. Lastly, we discuss how RIPs can be used to layer Object Capabilities on top of legacy systems.


### Meeting Regulatory Compliance
Organizations must provide documentation to regulators in order to maintain compliance. We can implement software to meet the full requirements of this use case by adding RIPs to the already composable Lego-like ecosystem of interoperable decentralized technologies such as DIDs, VCs, and OCAPs -- and by combining this ecosystem with a cryptographically auditable system, such as a blockchain. When an organization is preparing supporting documentation to meet compliance, they can post one or more RIPs and an OCAP for accessing each resource to a blockchain. This OCAP only grants access to the regulator and only to the specific items and for the duration that they need. Posting the RIP to a blockchain enables discoverability of the resource and establishes a proof of existence. The tamper-evident characteristics of the blockchain prove that the data existed as some point in the past, establishing trust via the cryptosystem rather than requiring it in the organization. The regulator then uses the delegated OCAP to dereference the url in the RIP and to ensure the data was not changed since the time of submission.


### Verifiable Displays in EDU/OCC

In the Educational/Occupational Credentials space, RIPs allow issuers to specify a set of approved visual renderings associated with a signed claim. This enables any viewer of the claim to determine if the visual rendering differs from what was intended by the issuer -- an ability that's critical for detecting social engineering attacks introduced by tampering with the rendered image.The "verifiability" of a Verifiable Credential applies to the content of the claim -- not necessarily the human-readable display. As described in [Verifiable Displays](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/verifiable_displays.md), this risk has been generally been addressed in an ad-hoc, use case dependent way. But there is no clear standard or convention for tamper detection across different credential schemas and use cases. 

This example shows how we might use a RIP to address the problem of proving that a png file hashes to the value expected by a referencing Verifiable Credential:


```
{
  "@context": ["https://w3id.org/credentials/v1", "https://w3id.org/security/v2"],
  "id": "http://credentials.example.org/credentials/3732",
  "type": ["VerifiableCredential", "EmployeeOfTheMonthCredential"],
  "issuer": "did:example:12345678",
  "issuanceDate": "2014-01-02",
  "expirationDate": "2014-02-02",
  "claim": {
    "id": "https://raw.githubusercontent.com/WebOfTrustInfo/rwot7/master/draft-documents/images/exampleVerifiableDisplay.png",
    "accomplishment": "Employee of the Month Demonstrating Excellent Leadership Skills",
    "verifiableDisplay": {
      "type": "ResourceIntegrityProofType",
      "id": "https://raw.githubusercontent.com/WebOfTrustInfo/rwot7/master/draft-documents/images/exampleVerifiableDisplay.png",
      "proof": {
        "type": "MessageDigest2018",
        "contentType": "image/png",
        "digestAlgorithm": "sha256",
        "digestValue": "950ec4d6caaeed62d6b51c5bd521fd2504c2c5fc961990d130b330131e432712"
      }
    }
  },
  "proof": { ... }
}
```

In this example, we leverage the `ResourceIntegrityProofType` to say that the image identified by `id` is expected to have a sha256 hash matching the value in `digestValue`. 

### Additional Applications of RIPs

Tamper evidence of an image is critical to a range of high-stakes decentralized digital credentialing scenarios. 

Expanding on linked visual data examples, this method enables a pharmacist to ensure the prescription they are viewing matches the associated machine-readable content. If the credential contained sensitive data, we wouldn't want the image to be publicly-hosted. But this is also supported: `id` can be any URI, so the referenced visual rendering could be stored offline.

RIPs enable snapshot integrity proofs for general linked data; this can be used for credentials bridging legacy systems where data is stored in a mutable store.

The above example uses `ResourceIntegrityProofType` as is, but in general implementors could subclass this type with context-relevant metadata.

In a credentialing ecosystem aware of this convention, one can envision tooling nabling an icon (e.g. a green checkmark) signifying the targeted image has not been tampered with.
