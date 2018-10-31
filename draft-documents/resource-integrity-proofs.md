# Resource Integrity Proofs
> Cryptographic linking provides discoverability, integrity, and scheme agility

Authors: Ganesh Annan and Kim Hamilton Duffy

Contributors: Manu Sporny, Dave Longley, David Lehn, and Bohdan Andriyiv


## Abstract
Currently, the Web provides a simple yet powerful mechanism for the dissemination of information via links. Unfortunately, there is no generalized mechanism that enables verifying that a fetched resource has been delivered without unexpected manipulation. Would it be possible to create an extensible and multipurpose cryptographic link that provides discoverability, integrity, and scheme agility? 

This paper proposes a linking solution that decouples integrity information from link and resource syntaxes, enabling verification of any representation of a resource from any type of link. We call this approach Resource Integrity Proofs (RIPs). RIPs provide a succinct way to link to resources with cryptographically verifiable content integrity. RIPs can be combined with blockchain technology to create discoverable proofs of existence to off-chain resources.

## Introduction
Cryptographic linking solutions today have yet to provide a generalized mechanism for creating tamper-evident links. The [Subresource Integrity](https://www.w3.org/TR/SRI/) standard limits this guarantee to script and link resources loaded on Web pages via the use of HTML attributes. [IPFS](https://ipfs.io/) provides a verification mechanism that is constrained to hash-based, content-addressable links, with no ability to complete content negotiation. [RFC6920](https://tools.ietf.org/html/rfc6920) proposes another mechanism that cannot be applied to existing links: it recommends the use of named information hashes and a resolution method that creates a content addressable URL [[1](#1-example-from-naming-things-with-hashes-rfc6920)]. Resource Integrity Proofs incorporates ideas from these standards and solutions to provide a new data format for cryptographic links that is fit for the open world. 

This paper describes use cases benefitting from RIPs, such as enabling [Verifiable Displays](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/verifiable_displays.md) and meeting regulatory compliance.

## Features

### Integrity
Resource Integrity Proofs use the representation of a resource as the input to a cryptographic hash function to generate a digest value. We can reproduce the digest value because the RIP data model requires recording of the content type and digest algorithm. Third parties can easily verify data received by 1) dereferencing the URL of the desired resource and 2) using the digest algorithm on the data to generate a matching digest value, ensuring that the data was not unexpectedly manipulated. The content received is now tamper-evident. RIPs may be placed on blockchains to simultaneously enable discoverability of off-chain resources and establish a proof of existence.

### Discoverability
Resource Integrity Proofs allow any party to find a given resource. This is achieved simply by including the URL of the resource in the data model. RIPs may be placed on blockchains to enable discovery of data whilst keeping sensitive data off-chain (i.e., private and secure).

### Scheme Agility
Resource Integrity Proofs make no assumptions on the URL scheme used. This scheme agility means that one can enable verification of the integrity of a resource using any URL scheme with any content type.

## Data Model
The Resource Integrity Proof (RIP) is a data model built using the [Linked Data Proofs](https://w3c-dvcg.github.io/ld-proofs/) specification. It can be represented using many different syntaxes; examples are given here in [JSON-LD](https://w3c.github.io/json-ld-syntax/), N-Quads, and in a simple table.


**id**
> The location of the resource.

**proof**
> The Linked Data digital proof.

- **type**: The identifier for the digital [proof suite](https://w3c-dvcg.github.io/ld-proofs/#dfn-proof-suite).
- **contentType**: The content type for the resource.
- **multiDigest**: The [multibase](https://github.com/multiformats/multibase) encoded [multihash](https://github.com/multiformats/multihash) [[2](#2-generating-a-multibase-encoded-multihash)].

**JSON-LD Syntax**
``` json
{
  "@context": "https://w3id.org/security/v2",
  "id": "https://example.com/storage/ndBRHU8gqjRzkcRdrPC2XQ",
  "proof": {
    "type": "Multihash2018",
    "contentType": "application/json",
    "multiDigest": "zQmUvZSaVzgjVHCDDDAoNNBgpiAkN6wKmCcD37vvnmoKq6e"
  }
}
```

**N-Quads Syntax**
```
<https://example.com/storage/ndBRHU8gqjRzkcRdrPC2XQ> <https://w3id.org/security#proof> _:b0 .
_:b0 <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> <https://w3id.org/security#Multihash2018> .
_:b0 <http://schema.org/contentType> "application/json" .
_:b0 <https://w3id.org/security#multiDigest> "zQmUvZSaVzgjVHCDDDAoNNBgpiAkN6wKmCcD37vvnmoKq6e" .
```

**Table**
<table id="table" class="table table-condensed">
  <thead>
    <tr>
      <th>Subject</th>
      <th>Predicate</th>
      <th>Object</th>
      <th>Graph</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>
        <a href="https://example.com/storage/ndBRHU8gqjRzkcRdrPC2XQ">https://example.com/storage/ndBRHU8gqjRzkcRdrPC2XQ</a>
      </td>
      <td>
        <a href="https://w3id.org/security#proof">https://w3id.org/security#proof</a>
      </td>
      <td>
        _:b0
      </td>
      <td></td>
    </tr>
    <tr>
      <td>
        _:b1
      </td>
      <td>
        <a href="http://www.w3.org/1999/02/22-rdf-syntax-ns#type">http://www.w3.org/1999/02/22-rdf-syntax-ns#type</a>
      </td>
      <td>
        <a href="https://w3id.org/security#Multihash2018">https://w3id.org/security#Multihash2018</a>
      </td>
      <td>
        _:b0
      </td>
    </tr>
    <tr>
      <td>
        _:b1
      </td>
      <td>
        <a href="http://schema.org/contentType">http://schema.org/contentType</a>
      </td>
      <td>
        application/pdf
      </td>
      <td>
        _:b0
      </td>
    </tr>  
    <tr>
      <td>
        _:b1
      </td>
      <td>
        <a href="https://w3id.org/security#multiDigest">https://w3id.org/security#multiDigest</a>
      </td>
      <td>
        zQmUvZSaVzgjVHCDDDAoNNBgpiAkN6wKmCcD37vvnmoKq6e
      </td>
      <td>
        _:b0
      </td>
    </tr>
  </tbody>
</table>

## Use Cases

There are many compelling applications of RIPs in a decentralized ecosystem. We will first dive into the problem of [Verifiable Displays](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/verifiable_displays.md), which seeks to ensure that the rendering of the Verifiable Credential content matches what the issuer intended. Next, we will envision a new age regulatory compliance system built on top of [Decentralized Identifiers (DID)](https://w3c-ccg.github.io/did-spec/), [Verifiable Credentials (VC)](https://w3c.github.io/vc-data-model/), and [Object Capabilities (OCAP)](https://w3c-ccg.github.io/ocap-ld/).

### Verifiable Displays

In the Educational/Occupational Credentials space, RIPs allow issuers to specify a set of approved visual renderings associated with a signed claim. This enables any viewer of the claim to determine if the visual rendering differs from what was intended by the issuer -- an ability that's critical for detecting social engineering attacks introduced by tampering with the rendered image. The "verifiability" of a Verifiable Credential applies to the content of the claim, not necessarily the human-readable display. As described in [Verifiable Displays](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/verifiable_displays.md), this risk has been generally been addressed in an ad-hoc, use-case-dependent way. But there is no clear standard or convention for tamper detection across different credential schemas and use cases. 

This example shows how we might use a RIP to address the problem of proving that a PNG file hashes to the value expected by a referencing Verifiable Credential:

```
{
  "@context": ["https://w3id.org/credentials/v1", "https://w3id.org/security/v2"],
  "id": "http://credentials.example.org/credentials/3732",
  "type": ["VerifiableCredential", "EmployeeOfTheMonthCredential"],
  "issuer": "did:example:12345678",
  "issuanceDate": "2014-01-02",
  "expirationDate": "2014-02-02",
  "claim": {
    "id": "did:example:10011872",
    "accomplishment": "Employee of the Month Demonstrating Excellent Leadership Skills"
  },
  "verifiableDisplay": {
    "id": "https://raw.githubusercontent.com/WebOfTrustInfo/rwot7/master/draft-documents/images/exampleVerifiableDisplay.png",
    "proof": {
      "type": ["ResourceIntegrityProof", "Multihash2018"],
      "contentType: "image/png",
      "multiDigest": "zQmUvZSaVzgjVHCDDDAoNNBgpiAkN6wKmCcD37vvnmoKq6e"
    }
  },
  "proof": { ... }
}
```

In this example, we leverage the `ResourceIntegrityProof` and `Multihash2018` type to say that the image identified by `id` is expected to have a multibase encoded multihash that matches the value in `multiDigest`.

### Extensions to General Linked Data

Expanding on linked visual data examples, this method could enable a pharmacist to ensure the prescription they are viewing matches the associated machine-readable content. If the credential contained sensitive data, we wouldn't want the image to be publicly-hosted. But this is also supported: `id` can be any URI, so the referenced visual rendering could be stored offline.

RIPs enable snapshot integrity proofs for general linked data; this can be used for credentials bridging legacy systems where data is stored in a mutable store.

### Meeting Regulatory Compliance

Organizations must provide documentation to regulators in order to maintain compliance.

We can implement software to meet the full requirements of this use case by adding RIPs to the already composable Lego-like ecosystem of interoperable decentralized technologies such as DIDs, VCs, and OCAPs -- and by combining this ecosystem with a cryptographically auditable system, such as a blockchain.

When an organization is preparing supporting documentation to meet compliance, they can post one or more RIPs and an OCAP for accessing each resource to a blockchain. This OCAP only grants access to the regulator and only to the specific items and for the duration that they need. Posting the RIP to a blockchain enables discoverability of the resource and establishes a proof of existence. The tamper-evident characteristics of the blockchain prove that the data existed at some point in the past, establishing trust via the cryptosystem rather than requiring it in the organization. The regulator then uses the delegated OCAP to dereference the url in the RIP and to ensure the data was not changed since the time of submission.

## Appendix

#### [1] Example from Naming Things with Hashes ([RFC6920](https://tools.ietf.org/html/rfc6920))

Using an **Authority** of `example.com` and the **sha-256 hash** of the text `"Hello World!"` we can generate the following `ni` URI:

`ni://example.com/sha-256;f4OxZX_x_FO5LcGBSKHWXfwtSx-j1ncoSt3SABJtkGk`

The generated `ni` URI takes advantage of the `.well-known` URI ([RFC5785](https://tools.ietf.org/html/rfc5785)) format so that we can dereference the information using HTTP(S):

`http://example.com/.well-known/ni/sha-256/f4OxZX_x_FO5LcGBSKHWXfwtSx-j1ncoSt3SABJtkGk`

#### [2] Generating a Multibase encoded Multihash

An example using Node.js v8.12.0

``` javascript
const multibase = require("multibase"); // v0.5.0
const multihash = require("multihashes"); // v0.4.14
const crypto = require("crypto");

const hash = crypto.createHash('sha256').update('Hello World!', 'utf8').digest();
// hash is 7f83b1657ff1fc53b92dc18148a1d65dfc2d4b1fa3d677284addd200126d9069

const mh = multihash.encode(hash, 'sha2-256');
// mh is 12207f83b1657ff1fc53b92dc18148a1d65dfc2d4b1fa3d677284addd200126d9069

const mb = multibase.encode('base58btc', mh);
// mb is zQmWvQxTqbG2Z9HPJgG57jjwR154cKhbtJenbyYTWkjgF3e
```


