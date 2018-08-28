# Verifiable Offline Credentials

Author: Michael Lodder

2018/08/28

## Introduction
Self Sovereign Identity is now a widely discussed topic especially in the context
of verifiable credentials–attributes attested by third-parties about an individual or entity
that can be used as proof about them such as a digital drivers license or passport.
This has enabled new systems to be developed to address security and privacy issues. Sovrin
is a permissioned ledger to facilitate privacy preserving verifiable credentials using
zero-knowledge proofs.

## Review
All current solutions for verifiable credentials involve computer systems and networks. These systems
perform all the complex cryptographic algorithms on a user's behalf, communicate with all
involved parties, and are responsible for safeguarding the information. Developed countries
such as those in Europe and North America have no problem using these platforms, these solutions exclude parts of the word
that do not have the same sophistication. For example, the vast majority of Africa does not have access to
the internet. Many Africa locations that do, connection speeds are incredibly slow.
There are also possible scenarios where a computer system may not be available to individuals like refugees.
Refugees must still be able to prove attributes about themselves and relying parties must
still be able to validate that information.

## Premise
Offline credentials aims to fill this niche. The benefits to such a system
include an individual being able to carry the credentials with them, can be safeguarded without computers, and still be cryptographically
verified by relying parties. Offline credentials should not require the use of computer systems or other electronic devices, but may use them to implement pieces of the process.
Otherwise, this voids the entire idea of offline credentials. In addition, it is recommended any cryptographic algorithms and material remain offline to prevent
electronic compromises, alterations or theft. Offline encryption is also not susceptible to a malware attack; and side channel attacks require cameras to record the person performing the encryption.
Offline encryption systems have existed for centuries as ciphers. Only in the last few decades has
offline cryptography algorithms become sophisticated enough to offer the more powerful features of modern cryptography like authenticated encryption and yield ciphertexts with uniform random distribution of character frequencies.

Offline benefits encompass three categories: usability, deployability, and security.
Each of these come with risks and limits that computers already handle or solve. One argument is how this is
different than having a physical credential like a drivers license today. A drivers license or passport
cannot be cryptographically verified by hand and all information must be shown when presented to a relying party.
Offline credentials should also support selective disclosure–only the information that a credential holder
allows is shared with a verifier. This paper discusses possible solutions that could be implemented to create verifiable offline credentials
along with their pros and cons.

## Considerations
Before we can detail offline solutions, we need to cover the aspects of offline credentials that will be used to measure solutions
before a solution is considered viable. Some offline ciphers require more sophistication and are more prone to mistakes but hard to break, while others may be simpler with fewer mistakes possible but not hard enough for an attacker with sufficient resources to break.
Many of these terms are borrowed from [The quest to replace passwords](https://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-817.pdf) (particularly concerning usability and security) but adapted to offline credentials.
Below is a list of those considered relevant for offline credential systems.

#### Parties
1. *Holder*: A person or entity that physically holds offline credentials.
1. *Issuer*: A person or entity that creates offline credentials for *Holders*.
1. *Verifier*: A person or entity that receives a presentation of credentials from *Holders* and verifies their truthfullness.

#### Usability
1. *Memorywise-Effortless*: Holders do not have to remember *any* secrets at all or possibly *one* secret for everything.
1. *Scalable*: Dozens of credentials shouldn't increase the burden for the user. "Scalable" means only from the user's perspective.
1. *Nothing-to-carry*:  Users do not need to carry any additional physical object (electronic, mechanical key, piece of paper) other than the credential.
1. *Physically-Effortless*: Process does not require physical user effort beyond, say, performing a simple task like pressing a button.
1. *Easy-to-learn*: Users who don't know the process can figure it out and learn it without too much trouble, and then easily recall how to use it.
1. *Efficient-to-Use*: The time the user must spend for each presentation is acceptably short. The time required for enrolling with a new issuer, although possibly longer than presentation to a verifier, is also reasonable.
1. *Infrequent-Errors*: Process a user must perform should succeed when done by an honest and legitimate person. In other words, the system isn't so hard to use or unreliable that genuine users are routinely rejected (like when performing an authenticated encryption scheme by hand).
1. *Easy-Recovery-from-Loss*: Users can conveniently regain their credentials if lost or stolen. This combines other aspects like low latency before restored credentials; low user inconvenience (e.g., no requirement for physically standing in line); and assurance that recovery will be possible.
1. *Selective-disclosure*: Users can easily choose which attributes to present and retain the remainder.

#### Deployability
1. *Accessible*: Holders are not prevented from using the system by disabilities or other physical (not cognitive) conditions.
1. *Negligible-Cost-per-User*: The total cost per Holder is negligible.
1. *System-compatible*: The process could be done by computers if needed.
1. *Non-Proprietary*: Anyone can implement or use the process for any purpose without having to pay royalties to anyone else. Relevant techniques are generally known, published openly and not protected by patents or trade secrets.

#### Security
1. *Resilient-to-Physical-Observation*: An attacker cannot impersonate a user after observing them present a credential. Attacks include any form of observation.
1. *Resilient-to-Targeted-Impersonation*: It is not possible for an attacker to impersonate a holder without having their credentials and by exploiting knowledge of personal details.
1. *Resilent-to-Guessing*: Since offline credential presentations are done in person, relying parties can constrain guessing or detect an impersonator trying to guess.
1. *Resilent-to-Leaks-from-Other-Verifiers*: Nothing a verifier could possibly leak can help an attacker impersonate the user to another verifier.
1. *Resilent-to-Theft*: An attacker in possession of a Holder's credentials cannot use them for presentation to another party.
1. *No-Trusted-Third-Party*: The process does not rely on a trusted third party who could, upon being attacked or otherwise becoming untrustworthy, compromise a holder's security or privacy.
1. *Unlinkable*: Colluding verifiers cannot determine, whether the same holder is presenting to both.

## Options

(Place holder to explore various options and crypto to implement offline credentials and their various tradeoffs)
