# Resource Integrity Use Cases

Authors: Ganesh Annan and Kim Hamilton Duffy

## Abstract
Currently, the Web provides a simple yet powerful mechanism for the dissemination of information via hyperlinks. Unfortunately, there is no generalized mechanism that enables verifying that a fetched resource has been delivered without unexpected manipulation. [Resource Integrity Proofs](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/resource-integrity-proofs.md) enable integrity verification of any resource with any URI scheme. This paper describes how RIPs solves use cases inspired by production deployments of self-sovereign technologies. We will first dive into the problem of [Verifiable Displays](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/verifiable_displays.md), which seeks to ensure the rendering of the Verifiable Credential content matches what the issuer intended. Next, we will envision a new age regulatory compliance system built on top of Decentralized Identifiers, Verifiable Credentials, and Object Capabilities. To conclude, we will explore additional applications leveraging RIPs.

## Use Cases

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
      "type": "ResourceIntegrityProof",
      "id": "https://raw.githubusercontent.com/WebOfTrustInfo/rwot7/master/draft-documents/images/exampleVerifiableDisplay.png",
      "contentType": "image/png",
      "proof": {
        "type": "Multihash2018",
        "digestValue": "41dd7b6443542e75701aa98a0c235951a28a0d851b11564d20022ab11d2589a8"
      }
    }
  },
  "proof": { ... }
}
```

In this example, we leverage the `ResourceIntegrityProof` type to say that the image identified by `id` is expected to have a sha256 hash matching the value in `digestValue`. 

### Meeting Regulatory Compliance
Organizations must provide documentation to regulators in order to maintain compliance. We can implement software to meet the full requirements of this use case by adding RIPs to the already composable Lego-like ecosystem of interoperable decentralized technologies such as DIDs, VCs, and OCAPs -- and by combining this ecosystem with a cryptographically auditable system, such as a blockchain. When an organization is preparing supporting documentation to meet compliance, they can post one or more RIPs and an OCAP for accessing each resource to a blockchain. This OCAP only grants access to the regulator and only to the specific items and for the duration that they need. Posting the RIP to a blockchain enables discoverability of the resource and establishes a proof of existence. The tamper-evident characteristics of the blockchain prove that the data existed as some point in the past, establishing trust via the cryptosystem rather than requiring it in the organization. The regulator then invokes the delegated OCAP to dereference the url in the RIP and to ensure the data was not changed since the time of submission.

### Additional Applications of RIPs

Tamper evidence of an image is critical to a range of high-stakes decentralized digital credentialing scenarios. 

Expanding on linked visual data examples, this method enables a pharmacist to ensure the prescription they are viewing matches the associated machine-readable content. If the credential contained sensitive data, we wouldn't want the image to be publicly-hosted. But this is also supported: `id` can be any URI, so the referenced visual rendering could be stored offline.

RIPs enable snapshot integrity proofs for general linked data; this can be used for credentials bridging legacy systems where data is stored in a mutable store.

The above example uses `ResourceIntegrityProof` type as is, but in general implementors could subclass this type with context-relevant metadata.

In a credentialing ecosystem aware of this convention, one can envision tooling enabling an icon (e.g. a green checkmark) signifying the targeted image has not been tampered with.
