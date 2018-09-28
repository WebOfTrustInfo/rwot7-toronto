# Title: Digital Credential Wallet

***Authors: Mike Brown, Darrell O’Donnell, Michael Ruther, Greg Slepak, Mikerah Quintyne-Collins, Heather Vescent, Christopher Allen

## Abstract

## Introduction

## What is a Digital Credential Wallet?
As methods and protocols to support the exchange of verifiable credentials (e,g. W3C Verifiable Claims Working Group), the need to begin defining the edge points for consumers, enterprises and non-person entities (NPE) interactions is growing. WIth the growth of cryptocurrencies, the associated ‘wallets’ for gathering, managing and exchanging token has grown. With respect to digital credentials some wallets (or often called agents) are emerging - usually specific to particular protocols. 

For the purpose of this paper, a digital credential wallet is considered to be the point through which verifiable credentials can be collected, managed and exchanged with other entities. A wallet may be a mobile app that a consumer is using for this purpose, it may be an application used within an enterprise to manage a very large set of credentials, or it may be a app running in an IOT device. There are some common ‘features’ for all of these wallets, as well as some unique aspects for individuals, enterprises and NPEs.


## Current Solutions to Digital Credential Wallets

More complete examples


Limited examples
Apple Wallet –  Apple wallet can stores a variety of credentials and authorizations, accessible only if a biometric or pin is used to open the wallet. But once opened, the Apple Wallet only supports additional validation/authentication for credit cards, but not for other credentials (which are purely bearer and do not support revocation, post issuance validation, receipts, consent, etc.) The Apple Wallet also does not support personas/multiple identities.

## How does a Digital Credential Wallet differ from a Cryptocurrency Wallet? 
Currently, when one hears the term wallet, one thinks of a cryptocurrency wallet due to the current mainstream attention of cryptocurrencies. Roughly, cryptocurrency wallets store private/public keys that give the owner of the wallet the ability to send and receive crypto-assets stored on a blockchain and digital credential wallets store credentials that are stored off-chain in the cloud or otherwise. In this section, we distinguish between cryptocurrency wallets and digital credential wallets.

First, we will outline the similarities between cryptocurrency wallets and digital credential wallets. 

Individuals typically have multiple roles or personas—each with their own context of use. For example, an individual associated with a university can be a student, an employee, and a member of a campus organization at the same time. Presentation of these personas should be the users choice.

## Requirements of a Digital Credential Wallet
The different needs of a consumer wallet, an enterprise wallet or a non human wallet
Receive and securely store digital credentials
Selectively disclose credentials (Minimize disclosure of information)
Desire: issue requirements to others

## Use Cases of Digital Credential Wallet

## Credential Recovery & Wallet Resilience

The first principle of Self-Sovereign Identity says people exist, that real-world identity trumps digital identity. This means that in the worst possible cases (Santa Rosa fires being a recent example) where all keys are lost, and where all key or local credential recovery is possible, there still should exist some way to allow the victim to recover given a brand new set of keys. For instance, the victim can personally go to some of the issuers and get claims that replace old credentials, and potentially use to recover even more credentials from others.

## Suggestions for Future work on Digital Credential Data

## References


Related work:

DIDs In DPKI (Decentralized Public-key Infrastructure): https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/dids-in-dpki.md

Decentralized Autonomic Data: https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2018/blob/master/final-documents/DecentralizedAutonomicData.pdf


