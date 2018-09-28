# Digital Credential Wallet

Authors: Mike Brown, Darrell O’Donnell, Michael Ruther, Greg Slepak, Mikerah Quintyne-Collins, Heather Vescent, Christopher Allen

## Abstract

## Introduction

## What is a Digital Credential Wallet?
As methods and protocols to support the exchange of verifiable credentials (e,g. W3C Verifiable Claims Working Group), the need to begin defining the edge points for consumers, enterprises and non-person entities (NPE) interactions is growing. WIth the growth of cryptocurrencies, the associated ‘wallets’ for gathering, managing and exchanging token has grown. With respect to digital credentials some wallets (or often called agents) are emerging - usually specific to particular protocols. 

For the purpose of this paper, a digital credential wallet is considered to be the point through which verifiable credentials can be collected, managed and exchanged with other entities. A wallet may be a mobile app that a consumer is using for this purpose, it may be an application used within an enterprise to manage a very large set of credentials, or it may be a app running in an IOT device. There are some common ‘features’ for all of these wallets, as well as some unique aspects for individuals, enterprises and NPEs.

## Requirements of a Digital Credential Wallet
We identified several main requirements for a digital credential wallet. These may change whether it is a consumer wallet, an an enterprise wallet or a wallet for an NPE, for example, a vehicle, smart object or dumb object. 

## Current Solutions to Digital Credential Wallets

More complete examples

### Limited examples
*Apple Wallet* –  Apple wallet can stores a variety of credentials and authorizations, accessible only if a biometric or pin is used to open the wallet. But once opened, the Apple Wallet only supports additional validation/authentication for credit cards, but not for other credentials (which are purely bearer and do not support revocation, post issuance validation, receipts, consent, etc.) The Apple Wallet also does not support personas/multiple identities.

*Verified Organization Network (VON)* - The Verified Organization Book developed by the BC government stores enterprise credentials. This is a proof-of-concept that enables giving digital native credentials to organizations. https://von.pathfinder.gov.bc.ca/ & https://github.com/bcgov/von 


## How does a Digital Credential Wallet differ from a Cryptocurrency Wallet? 
Currently, when one hears the term wallet, one thinks of a cryptocurrency wallet due to the current mainstream attention of cryptocurrencies. Roughly, cryptocurrency wallets are used to store tokens or coins and digital credential wallets are used to store digital credentials. The purpose of this section is to distinguish between what is meant by a digital credential wallet and a cryptocurrency wallet. In outlining the similarities and differences between digital credential wallets and cryptocurrency wallets, we will arrive at constructive definitions of both types of wallets and in particular with regards to digital credential wallets, will complement the definition given in the previous section. 

Similarities 
The main similarities between digital credential wallets and cryptocurrency wallets are that they can be mobile, desktop and web applications and hardware devices, and  can store multiple addresses/credentials. Both wallets can be implemented as software applications or hardware devices. Software implementation of these wallets are mobile phone applications, desktop applications or web applications. The choice of software manifestation of these wallets give users a choice as to how much they want to control the information stored in these wallets. For example, with web applications wallets, most of them in use don’t give the user of their wallet control over the private/public keys that are associated with the wallet whereas with a desktop application wallet, the user will have full control over the private/public keys associated with the wallet. In the case of hardware wallets, the user has complete control over the private/public keys and have the option to store these completely offline. The issue of key management of cryptocurrency wallets is outside the scope of this paper and with regards to digital credential wallets, will be addressed in a later section of this paper. 

Differences

Both types of wallets require at least 2 parties in order to start and complete an interaction.  Generally, with cryptocurrency wallets, they are programmed to only handle 2 party interactions and not multiple party interaction. However, multi-signature wallets are used to require multiple signatures from different parties in order to authorize a transaction.

## Use Cases of Digital Credential Wallet

## Wallet Key Management

Digital Credential Wallets (DCWs) are used for *storing* credentials, not issuing them. However, there are circumstances when they may need to manage public/private keypairs. This section will first describe one such scenario, and then will go over methods for recovering from key loss (since that is always a concern when public-private keys are used).

- A DCW *could* do identity management via a Master DID, for example if you want to be able to sign in digitially to websites, but it doesn't have to
- A bare minimimum DCW does not need to involve a Master DID, and therefore doesn't need to do key management *necessarily* (unless it chooses to involve a Master DID). If it doesn't, then it just needs to store secrets. These secrets could be private keys (to public keys that are signed by the issuer), or they could be blinded secrets that are used in the generation of zero-knowledge proofs of knowledge of DMV signatures. In that latter case, the DCW just needs to protect these secrets (that are used to prevent the credential from being copied, and could be derived from the phone's hardware).
- An example where a Master DID could be useful is to replace Facebook Login, e.g. using a Master DID as a publicly-known global identity for you. In this case you are not actually using credentials to sign in. However, it's possible to associate a credential with a Master DID in such a way that the issuer knows what your Master DID is, but those you reveal your credential to don't know it. Or something (ask Mike about this). In this use case, no credentials (in the traditional sense) are being used. Instead a self-sovereign identifier is being used directly as an ID, and for this it makes sense to use a seperate app to login (that also includes functionality to manage keys for the Master DID). These should be separate. Whereas you may want people reading your comments online to know that it was you who wrote them and associate that with some globally recognized version of "you", credentials, such as those attesting to the fact that the government says the person owning your face is over 21, is all that is needed to gain entry to a bar, the bartender doesn't need to know your globally identifier/username/persona. Developers of DCWs may still choose to integrate these two separate concepts in the same app (for example, if they want to make it simple for an issuer to associate a Master DID with a credential when issuing it), but they would be wise, for privacy reasons, to keep this functionality clearly separated. **It is important not to confuse the concept of a Self-Sovereign ID with the concept of a credential.**
- The idea of credentials, and credential management, is very different from the idea of a global digital identifier used as part of a digital identity. Whereas creating a Master DID requires having something like a smart contract that manages (in a decentralized way) authorized devices and keys that can sign on behalf of you, and revocation of those devices (or recovery from key loss), this is fundamentally a different concept and use case from what we consider today as "credentials", which are issued by a third party (usually a government), and are in some way associated with biometric information (typically a photo of your face). Now it's possible to have a credential that includes as part of its attributes as Master DID (similar to having a social security number embedded into a passport), this too doesn't need for the "digital credential wallet" to include the necessary functionality for managing the keys to maintain a Master DID. Although, of course, a DCW *can* certainly combine these two aspects, it is not necessary for them to do so, and some may choose to have their DCW implementation only manage a list of credentials (and their corresponding secrets that prevent those credentials from being copied upon reveal to a verifier).

### Example: Using Keys As A Second Factor Authentication Method

Airport security checkpoints often ask visitors for their ID, typically a driver's license, as an example of a government-issued identity credential.

Our DCW could simply store a digitially-signed driver's license, and beam that information to the security guard, as proof of ID. And while this could be sufficient proof of identity in some scenarios, there is one issue with this example, and that is that the ID could have been stolen. It would be nice if there were some additional, second factor, showing 

When a person is asked for ID in the United States, they usually present a driver's license. How does the person asking for ID (the verifier), verify that the driver's license is both *authentic* and actually *belongs* to the holder?

To verify the ID is *authentic*, they verify that the ID has certain markings (for example, holograms and microprint) that is costly to forge.

To verify the ID *belongs* to the holder, they check that the photo on the ID matches the face of the holder, and might also quiz the holder on some of the data present on the ID (for example, their birthdate).

A DCW has the ability to improve upon this process by replacing the hard-to-forge physical identity card with a hard-to-steal digital secret called a *private key*. The wallet may still combine this secret with a digital photograph of the holder (signed using the private key) to fully replicate security properties of physical IDs. Note that the photograph does not need to be stored online, it just needs to be signed by the private key of the issuer.

So it seems that holder keys are only relevant when the holder goes to an issuer to receive their ID credential, in order to prove to the issuer that they are the owner of a DID.

### Recovering from Key Loss

The DPKI overview document [1] describes a recovery method via Shamir's Secret Sharing.

## Suggestions for Future work on Digital Credential Data

## References


Related work:

DIDs In DPKI (Decentralized Public-key Infrastructure): https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/dids-in-dpki.md

Decentralized Autonomic Data: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2018/blob/master/final-documents/DecentralizedAutonomicData.pdf


