
# Verifiable Displays

Authors: Kim Hamilton Duffy, Lucas Parker, and Anthony Ronning

Contributors: Bohdan Andriyiv

## Problem Statement

Blockcerts is an open standard and set of open source libraries for issuing and verifying blockchain-anchored credentials. Originating as an informal extension of Open Badges v1 (and subsequently a proper extension of Open Badges v2), Blockcerts' initial release was able to assume the presence of a set of standard Open Badge required fields to include in the display. 

Blockcerts and Open Badges allow additional fields to be included in the credential, and subsequent work will allow even more free-form credential content, through the work to align [Open Badges and Verifiable Credentials](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2018/blob/master/final-documents/open-badges-are-verifiable-credentials.pdf). 

The question arises: in an arbitrary Verifiable Credential, whose claim content is unknown in advance, how does an arbitrary viewer of the credential know that the presented display matches the content? Clearly the verification process ensures the content has not been tampered with, but how does the issuer ensure that the display presented to a viewer matches their intent?

The problem we refer to as "verifiable displays" is critical for avoiding certain social engineering attacks. This paper describes more context about how the problem is addressed in existing implementations, proposals for a general solution, and perhaps most importantly, proposes a set of requirements for a general solution.


## Blockcerts viewers, and how to customize
As an Open Badges v2 extension, Blockcerts' open source viewers display certain fields by default -- title, description, [image representing the accomplishment](https://www.imsglobal.org/sites/default/files/Badges/OBv2p0/index.html#BadgeClass), etc. These fields are assumed to be in a credential because they are required by Open Badges or Blockcerts schemas. 

The current Blockcerts ecosystem allows the display to vary across devices; i.e. the browser displays a larger set of fields than a more abbreviated mobile wallet view. But again, a common set of fields is assumed.

Display customization is enabled in the open source; for example, an issuer can customize their credential display by adding a Flask Themes to the cert-viewer project. All components are open source, so the issuer could extend/customize any component (such as the mobile wallet), although this involved more work.

The Blockcerts open source also supports a `displayHtml` field, and the open source viewers understand to parse the HTML from that field. But we do not promote the use of that (it was a tentative compromise solution), and this point we intend to deprecate that field, as it intertwines display and content, bloats the size, and generally is an inelegant solution.

These methods allow issuers to customize both the format of credentials (font, field order) and content (e.g. additional custom fields, in the case the issuer has added important extension fields).

Issuers emphasize that such customization is important for preserving their brand and integrity of their valuable credentials.


## Open Badges and Badge Baking

Open Badges has a standard way of preserving the issuer's desired display through the process of "baking", which embeds the credential as metadata in an image file (png or svg). The Blockcerts issuer doesn't bake badges by default, but it is supported through the [obi-baking open source library](https://github.com/blockchain-certificates/obi-baking).

There are a couple of problems with relying on this method, which can be addressed (as described later). For now, the relevant problem is -- does this suffice for optimizing across different devices? Or if not, would it suffice to have different baked images for different form factors? If so, this is a much simpler solution, but still has a critical integrity factor that would need to be addressed. Let's work up to that

## Thinking beyond a single issuer

Customizing displays in the manner I describe above is easily doable if we focus on a single issuer and a single type of credential, but the management and integrity of these custom displays presents complexities when we focus on the broader ecosystem.

A critical part of the Open Badge and Blockcerts ecosystem is the ability to accept/exchange/verify credentials, independent of the issuer/origin. This is supported and well understood from a credential _content_ perspective.

But focusing on display, how can issuers ensure their desired display is preserved in general? They can control the display in their own branded mobile wallet, credential web sites, etc, but what does it look like in another Blockcerts (or more broadly, credential) viewer?

Another question arises: can a malicious party entice people to use a misleading credential viewer for social engineering attacks? Maybe this party adds new fields to the display, removes others, so that the view in no way reflects the credential content. During verification, we check that the presented credential content verifies against the issuer signature, but how does a viewer know that what they see displayed accurately reflects the credential content without looking at the full json credential?

Revisiting the badge baking option, the baked image (content) isn't part of the signed/hashed payload, so in theory it can be tampered with to show a misleading badge.

## Reducing these concerns to requirements and use cases

Question 0: does display matter? i.e. is social engineering through the view not relevant
Question 1: how does an issuer ensure their design is preserved across viewers?
Question 2: how do we reduce social engineering attacks by helping humans know the view accurately represents the content? I.e. without forcing them to look at the fill certificate json


### Spectrum of display use cases

- display doesn't matter (e.g. social engineering of this form is not a concern; device only exchange)
- issuer requires that certain set of fields are displayed, but doesn't care exactly how (relevant for existing ecosystems, e.g. Open Badges)
- issuer "blesses" n displays (.pdf / .html / .png / ...) or artifacts / templates in an immutable store

### Additional privacy concerns

If the credential contains sensitive data, neither credential nor displays should not be assumed to be hosted.


## Solutions that have been considered


Some options that have been considered include:
1. Embed a display template, image, or other view in the certificate
	- problem: size of the certificate, especially if targeting different devices
	- problem: possible longevity issues (e.g dated templating technique)
2. Reference (as linked data) a display template in the certificate
	- problem: this display template can be altered after issuance and that wouldn't be detected during verification
3. Display certification: Open Badges already has a certification process to ensure an OB certified viewer is compliant. 
    - problem: in theory the view could be tampered with after certification
    - problem: having a certification authority -- even in display -- is a centralization point we'd like to avoid
4. **Embed hash(es) of the "blessed" display artifact(s)** (currently seen as the most promising approach)
	- advantage: allows the integrity to be established without size bloat
	- problem: management of these external artifacts
5. ("Let the issuers handle it") Over time issuers converge on a well-known set of schemas and corresponding display templates 
    - approach the problem per use case
    - e.g. if we restrict the problem to display of a certain type of  credential that belongs to a known alignment framework, perhaps it's easier for issuers to use widely used templates (e.g. EQF framework)
    - in some cases, the problem may be less critical; i.e. perhaps only the content is being exchanged between devices.

In a sense, I think it's best to think of #5 as orthogonal or complementary to a cryptographically verifiable display; this mixes reuability with tamper-evidence, which are very different problems.

## Current (tentative) proposal

Prototype proposed standards for:
- (minimum requirement) adding a hash value to a credential to check whether the display has been tampered with
    - incubate standard vocabulary for use in Verifiable Credentials ecosystem
    - additional options: metadata, location
- standard way to create human friendly presentation and embed credential for portability purposes

Tentative proposed form (presented by Bohdan Andriyiv); see discussion
https://github.com/w3c/vc-data-model/issues/135#issuecomment-410138282

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


### Questions

- Which are required fields?
- Can we assume credential is embedded in display artifact, or are they bundled in some way
- Many more to come
