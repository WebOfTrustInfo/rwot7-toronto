
# Verifiable Displays

Authors: Kim Hamilton Duffy, Bohdan Andriyiv, and Lucas Parker

## Problem Statement

The [Verifiable Credentials Data Model](https://w3c.github.io/vc-data-model/) is an emerging standard for expressing credentials such as driver's licenses, degrees, and passports on the Web in a secure, privacy respecting manner. The "Verifiable" part is because they are designed to be _machine_ verifiable.

As a flexible data model, Verifiable Credentials (VCs) are appealing in a wide range of use cases -- even where standards already exist -- due to the interoperability they enable. For example, [Open Badges are Verifiable Credentials](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2018/blob/master/final-documents/open-badges-are-verifiable-credentials.pdf) describes the advantages of aligning Open Badges (and other well-known Educational/Occupational schemas/vocabularies) with Verifiable Credentials. VCs have minimal structural overhead, so they can easily be used as an envelope for well-known rich vocabularies, enabling interoperability with existing and new ecosystems.

This emphasis on machine verification is essential, but what's not in scope of the VC Data Model is scenarios where a human participates in verification. In the Educational/Occupational space, suppose a recipient has received an academic credential that they want to share with a potential employer. The potential employer can cryptographically verify the content, but the employer is typically not looking at the raw json content of the credential; instead they are looking at an image, PDF, or some friendlier visual representation. 

The question arises: how does the employer know that the friendly display they see is what the issuer intended? In general, how do they know the display matches the content? This is currently addressed in a variety of (sometimes incomplete) ways. 

This paper surveys existing solutions to the problem, and develops a set of requirements based on lessons learned. This proposes a general solution based on the authors' experiences developing Blockcerts and Validbook. 

We use the term "verifiable displays" to describe the end goal, which is avoiding a category of social engineering attacks introduced by the potential gap between content and its renderings in a human-readable display. 

> Note: This question is not necessarily relevant in machine-to-machine scenarios, but it's a factor of increasing importance as Verifiable Credentials grow in popularity and bridge existing systems, where a human is in the loop. 

## Motivation: Blockcerts

Blockcerts is an open standard and set of open source libraries for issuing and verifying blockchain-anchored credentials. Blockcerts is an [Open Badges (OB) v2 extension](https://github.com/IMSGlobal/cert-schema), and the [OB v2 specification](https://www.imsglobal.org/sites/default/files/Badges/OBv2p0/index.html) requires certain fields -- such as [title, description, image representing the accomplishment](https://www.imsglobal.org/sites/default/files/Badges/OBv2p0/index.html#BadgeClass) -- to be present in the credential. For badges, these nicely correspond to expected fields in a visual representation of a credential.

Open Badges itself uses a [badge "baking" process](http://www.imsglobal.org/sites/default/files/Badges/OBv2p0Final/baking/index.html), in which the credential is embedded into a PNG or SVG. This artifact is the understood to be the visual representation by issuers, verifiers, etc. The OB specifications do not include standards for detecting tampering of the outer image; the embedded content would have to be inspected manually to look for anomalies.

[Blockcerts also supports baking](https://github.com/blockchain-certificates/obi-baking), but we wanted to allow a variety of visual representations, targeting a variety of devices (web, mobile). To that end, v1.1 of Blockcerts enabled display customization through templates, providing extension mechanisms where issuers/viewers could register their desired templates. This could also include display of additional custom fields.

The content/template-driven approach was reasonable in very specific scenarios where the core required fields are the same (with only a small amount of additional custom metadata), but this approach was inadequate as Blockcerts adoption spread into a wider set of use cases. In these new use cases, the required fields from Open Badges didn't necessarily make sense and a large number of custom fields were added (1).

The potential for increasing drift along display templates introduced a concern about social engineering attacks, where a viewer/verifier could see a visual display of a credential that doesn't accurately reflect the content (e.g. a malicious view drops certain fields, adds others). The verification process cares about content, not display, and so we wanted to bridge that gap.

Furthermore, for certain issuers, tighter control over display, and ensuring it would look the same across different viewers, is critical for preserving their brand and integrity of their valuable credentials. 

For that reason, we added the ability to insert the display directly in the credential, changing the open source viewers (wallet, web component) to look for that field before considering a default template. The advantage is that, since the credential is tamper-evident, the embedded display information is also tamper-evident.

Below we'll describe the limitations of these approaches in depth, and why we are proposing an alternate method.

(1) The content side of this concern is being addressed through a collaboration enabling alignment of [Open Badges and Verifiable Credentials](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2018/blob/master/final-documents/open-badges-are-verifiable-credentials.pdf).

## Motivation: Validbook Statements 

[Validbook Statements Service](http://futurama1x.validbook.org/statements) is one of [Validbook Cooperation Services](http://futurama1x.validbook.org/) (a public utility; a set of core cooperation services used to optimize human cooperation, by making cooperation more transparent and reliable). Validbook Statements Service is used to sign and verify *Validbook Statements* – digital documents with cryptographicaly verifiable information (signatures, hashes). 

Validbook Statements are meant to be used for diverse range of documents (e.g. [contracts](http://futurama1x.validbook.org/statements/templates/Wedding%20Photography%201-13), [certificates](http://futurama1x.validbook.org/statements/templates/Certificate%20of%20Completion-15), credentials, statements of incorporation, court decisions, etc). 

Validbook Statements are meant to be read by people, as well as to be machine parsable and cryptographically verifiable. Therefore it is important for Validbook Statements to use standard that can both *store* cryptographically verifiable information and *present* a human readable display of the document.

One way to achieve this dual goal is - to create human readable displays of Verifiable Credentials, calculate their hashes (thus making them verifiable), reference Verifiable Displays from their Verifiable Credentials (thus creating permanently referenced, issuer approved displays of the Verifiable Credentials), and bundle Verifiable Displays with Verifiable Credentials into one HTML file. 



## Survey of Existing Solutions

In general, the existing solutions we found and considered fall in one of the following categories:

Some options that have been considered include:

1. Associate credentials with display templates by convention, or enforced by issuer 

2. Embed a display template, image, or other view in the certificate

3. Reference (as linked data) a display template or other view in the certificate

4. Display certification

5. **Embed hash(es) of the approved display artifact(s)** (proposed in this paper)

Note that some of the above are orthogonal or complementary to a cryptographically verifying displays. In this paper, we will focus on tamper-evidence versus reusability of display template.


### Associate credentials with display templates by convention, or enforced by issuer

TODO: define viewer (human vs tools); viewer vs displayer?

This relies on the fact that a credential is associated with 1 or more schemas (governing their content), for which 1 or more visualizations may be appropriate. These visualizations are use-case dependent, and are domain specific. This content-driven approach assumes the ability to register/retrieve a mapping between a credential schema (or type) and its display template. Viewers know to check this registry, maintained either by a single issuer or a community, to correctly render the credential.

This effectively shifts the burden to issuers/viewers (or domain-specific ecosystems of them) to create and maintain these mappings, which are only enforced by convention (although some certification process could be involved).

This approach is useful for communities generating similar credentials (e.g. belonging to a known alignment framework). But it is valuable more for its alignment and reusability potential than for its ability to enable tamper evidence -- there is no built-in way to ensure the templates haven't been changed. Furthermore, it can insert centralization points.  

Example: Originally, the Blockcerts open source solution to display extensibility relied on content-first approaches. The default viewer knew the set of required fields suitable for display and provided an  associated templates. The open source libraries provide extension mechanisms; for example, the open source cert-viewer project allows customization of displays through Flask themes, meaning the issuer can add/remove fields and control other aspects of display specific to their credentials.

### Embed a display template, image, or other view in the certificate

Embedding a display template, image or view is a way to end-run the problem. If viewers show what's embedded in the credential, and if the credential itself is tamper-evident (as with Verifiable Credentials and Blockcerts), then at least you have tamper-evidence of the display.

Example: The Blockcerts open source supports an optional `displayHtml` field, and the open source viewers understand to parse the HTML from that field. This prioritized embedding all the information in a single package (credential) for portability. That was only an experimental addition that we will likely not formalize. 

The main we found were that it can bloat the size of the credential; especially if targeting different devices. 


### Reference (as linked data) a display template or view in the certificate

This moves the template or view outside of the credential, and instead inserts a pointer to that inside the credential. If the credential is tamper-evident, then that _pointer_ is tamper-evident. However, the target must be in an immutable storage for this to be of any value. If the target is in a mutable storage, the template, image, or view can be altered after issuance and that wouldn't be detected during verification.

This also introduces additional hosting requirements, centralization points, and possible longevity issues. 

More importantly, publicly-available, hosted displays are not an option for credentials with sensitive information. (Hosted templates are an option, but still can be modified undetected if in an immutable store)

### Baking and Display Certification

As described previously, Open Badges uses a badge baking process that embeds the credential into an image. The validation process extracts the embedded credential but does not include a check that the image it's embedded in matches anything in the credential. This means that if the image is passed around between parties, one of them could have tampered with the outer image (resulting in a misleading badge display) and there is no means to automatically detect that.

This will not be a concern if the issuer is hosting the badge (i.e. the badge is not passing through intermediaries). But this introduces an ongoing dependency on the issuer, which interferes with the goal of recipient-owned, lifelong credentials.

In addition, Open Badges has a certification process to ensure an OB certified viewer is compliant. This ensures the display conforms to the Open Badges v2 specification guidelines.

Certification is a useful way to ensure consistency, but has some problems:
1. How do you ensure certified viewers remain compliant?
2. Introduces a certification body as a centralization point (which may be acceptable in some scenarios)

## Requirements

Our goal is to reduce social engineering attacks by helping humans know the view accurately represents the content, but without forcing them to look at the full certificate content.

### Verifiable Displays requirements

It is important for Verifiable Displays to be "universally openable", portable and verifiable.

In the future the average consumer of Verifiable Displays will treat them as paper documents. Just as nowadays, any person can store and read paper documents, in the future, people will double click or tap on a file that contains Verifiable Display open and read them in a _standard_ program - internet browser, image viewer.

The comparison to physical world also applies for a verification process. When people try to verify authenticity of the paper document (to be more precise signatures, stamps, watermarks) they go to experts they can trust (clerks, lawyers, issuer of the document). Similarly with the verification of Verifiable Displays, people will go to services (apps, wallets, web sites) they can trust to verify credentials and their displays.  

To ensure _portability_ Verifiable Displays should be bundled with Verifiable Credentials in one file or have Verifiable Credentials embedded in them.

To ensure universal _openability_ Verifiable Displays should be made using ubiquitously used standards, such as HTML, SVG.  

To ensure _verifiability_ of Verifiable Displays by different verifiers, verifiers should agree on a standard way 
* to calculate hashes of Verifiable Displays 
* to reference Verifiable Displays from Verifiable Credentials 
* to bundle or embed Verifiable Credentials with/into their Verifiable Displays.  

### Privacy and Security

f the credential contains sensitive data, neither credential content nor visual representations of the content should be hosted on the web or (in general) accessible to other than the intended parties.

## Proposal

We propose a way to create human friendly Verifiable Displays avoiding the pitfalls described above.

At the core, this is solved by adding a hash value to a credential, enabling easily enforcable checks for tampering.

Our goals are to enable interoperability and portability of this method, including:
- scheme for referencing Verifiable Displays from Verifiable Credentials
- incubate standard vocabulary for use in Verifiable Credentials ecosystem
    - additional options: metadata, location
- conventions or standards to bundle or embed Verifiable Credentials with or into their Verifiable Displays


### A way to reference Verifiable Displays from Verifiable Credentials  

Before issuing the credential, the issuer calculates the hash value of Verifiable Display, add this hash value into VC. 

This is the essential aspect providing tamper-evidence. We propose additional metadata that enables association of the external visual artifacts with the embedded hashes.

Tentative proposed solution: (see discussions https://github.com/w3c/vc-data-model/issues/135 and https://github.com/w3c/vc-data-model/issues/136)

Example:
```
 "reference":[  
         {  
            "type":[  
               "Presentation"
            ],
            "purpose":[  
               "Presentation"
            ],
            "hash":"0x5f435bf7d0af09da8b064416de2e9fa0d2c85b22b9fb16adadd1368b61fbd8d1",
            "id":"0x5f435bf7d0af09da8b064416de2e9fa0d2c85b22b9fb16adadd1368b61fbd8d1",
            "location":[  
               "BundledIntoHTML"
            ]
         }
      ]
```

### HTML bundles of Verifiable Credentials and their Verifiable Displays 

The proposal is to use HTML files to bundle together Verifiable Credentials and their Verifiable Displays. Such bundles will satisfy the main requirements of portability, universal openability and verifiablity of Verifiable Displays.

HTML bundles will remove the need to create separate standards to embed VCs into Verifiable Displays for each standard that can be sued for Verifiable Display (HTML, SVG, PNG, JPG etc.) HTML bundles will be easy to understand for all developers, not the case when working with SVG, PNG etc.

The proposal is store JSON of Verifiable Credential in invisible ```<head>``` block, within ```<script type="application/ld+json">``` element.

To store Verifiable Display the proposal is to use ```<div>``` element with  with attribute ```data-type``` = ```"Verifiable Display"```, and attribute ```id``` = ```"_hash_value_of_the_content_of_div"```  

Although, it is not crucial to define standard way to create Verifiable Displays, when we use HTML bundles, as long as Verifiable Displays can be rendered by the Internet browser, we propose to use SVG and HTML as standards to be used to create  Verifiable Displays. 

SVG is "universally openable" standard for images. The main advantage of SVG over other common image standards is that it allows to scale image without loss of quality. HTML is universally openable standard to present and markup text.

See examples, of proposed HTML bundles with [HTML](https://drive.google.com/file/d/1a87-uNSPoBJdav5rP6Q1sAp5Dnp-sCNV/view?usp=sharing) and [SVG](https://drive.google.com/file/d/1ePvJqpmFgrXcvdRxld104DMY129385gd/view?usp=sharing) Verifiable Displays. You can test, verify them here - http://futurama1x.validbook.org/statements


### Questions

- How to reference Verifiable Displays from Verifiable Credentials?
- How to store and transport Verifiable Credentials with Verifiable Displays so that they will not get separated, "lost" from each other?
- What is better - to embed Verifiable Credentials into Verifiable Displays or to bundle them in HTML file? 
- Many more to come
