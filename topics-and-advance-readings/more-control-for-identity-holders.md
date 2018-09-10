# More control for Identity Holders

By [Ismenia Galvao](Ismenia.Galvao@ing.com) and [Arturo Manzaneda](Arturo.Manzaneda.Tudela@ing.com)

## Introduction

One of the main goals of Self Sovereign Identity (SSI) is to give more control and
power to individuals and organizations with regards to their digital data.
The European Union seems to be aligned with the same way of thinking; proof of it  is
the [General Data Protection Regulation (GDPR)]. This regulation aims to
give control to citizens and residents over their personal data and to simplify the
regulatory environment for international businesses by a unified european regulation.

Last year our innovation department at ING released a [paper comparing decentralized
Identity Frameworks]. As a bank, and specially a bank which believes in the future of
Blockchain and Distributed ledger technologies, Identity is a key control point for
enabling any related solutions. As a result of the comparison we decided to have a
deeper look at [Hyperledger Indy], by developing a proof of concept.

The purpose of this document is to describe some topics (some related to GDPR) which
are not fully covered by Indy nor by SSI Standards; and start a discussion, hopefully
continued during the RWOT7 workshop. We believe there is a need to enforce and
standardize even more the interaction flows and data formats, not only for being
GDPR-compliant but also for the interest of all identity holders.

## Who knows something about me?

When people ask me about the benefits of using the application that we are currently
building, I always explain that the main focus is to give more control to people to
better manage their personal data or identity in the digital world.

**What do you mean by giving more control?**

**- All users can be: Issuers, Verifiers and Identity Holders**

Nowadays, the way we share our identity to companies is always in one direction, us
to them. Our browser has a list of trusted certificate authorities (CA), and that's
the only check we do on our side. Usually the process is a sign up form with a checkbox
to accept some long terms and conditions (which nobody reads). After that we have an
account, username and password to access.

With decentralized identity all users including companies can act as Issuers, Verifiers
or Identity Holders. This means that we will also be able to request proofs to companies
before sharing our information with them. For example, asking for a quality certificate
of the security of their data centers.

**- Selective disclosure of attributes**

Users can generate multiple proofs from their credentials. They can combine attributes
from different issuers, which can be fully revealed, kept in secret (only proving that
you have a passport, signed by the Dutch Government) or semi-revealed using a
cryptographic technique known as Zero-Knowledge Proofs (prove you are 18+ but not
disclosing your birth date).

**- What, when and with who did we share information**

Some months ago, when GDPR became active, all EU citizens received lots of emails
requesting consent and allowing people to opt-out, or be forgotten. This emails
surprised most of us; Why does this company has personal information about me? When
did I share something? What do they know exactly about me?

This lack of knowledge makes us all feel less in control. One key benefit from our
application and Self Sovereign Identity is the possibility of recording all our
interactions. This will allow users to keep track of all the information/proofs they
shared, when and with who.

Unfortunately, as of today, this is not implemented by Hyperledger Indy. Although, it
is technically possible, the implementation of this feature relies on the hands of
developers.

> **Should the [Self Sovereign Identity Principles] include or refer to the
> capacity of the identity holder to keep track of _what_ they share _with who_
> and _when_?**

## Polices and data retention

> _[Self Sovereign Identity Principles] - Consent_
> <br/>
> <br/>
> Users must agree to the use of their identity. Any identity
> system is built around sharing that identity and its claims, and an
> interoperable system increases the amount of sharing that occurs.
> However, sharing of data must only occur with the consent of the user.
> Though other users such as an employer, a credit bureau, or a friend
> might present claims, the user must still offer consent for them to
> become valid. Note that this consent might not be interactive, but it
> must still be deliberate and well-understood.

**What do I need to know before agreeing on sharing my identity (consent)?**

The Identity Holder should be able to get all needed information related
to the use of his/her data before sharing it. Any user should be able to
clearly and on a quick view respond to the following questions:

- Why do the verifier needs the requested proofs or data attributes?
- How is it going to be used?
- Who would have access to it?
- How long do they need to be kept (legal requirements for data retention, if any)
- Maybe even how secure is the organization? CIA rating? Data center certificates?
- How sensible are the requested attributes?[1]

We believe the standardization of the data format for such agreements or policies,
specially the data retention is critical to ensure interoperability and to
give more control to the identity holders. If there is no standard in the format,
we will probably continue with long and unreadable terms and conditions documents.

[1]Some identity attributes are more sensible than others, specially the unique
identifiable ones like your passport number or social security number.

## Right to erasure (‘right to be forgotten’)

The right to erasure is one of the most complicated topics included in the
[GDPR Article 17]. The first time this topic was discussed was in 2006 and 12 years
after there is still not a clear solution on how to handle it. Removing digital data
is hard, specially with search engines keeping track of almost all published information
on the Internet.

Self Sovereign Identity can allow users to keep track of what, with who and when data
is shared. With this in place, we can easily implement a communication process to
request erasure. During this process the identity holder needs to collect two proofs:
Proof of Request and Proof of Erasure. Both proofs can be shared with regulators, so they
can audit companies and penalize them if the data was not properly deleted. The first one
would allow to prove the intent of the request and the second one the confirmation of erasure.

## References
- [paper comparing decentralized Identity Frameworks] - ING paper comparing different SSI frameworks
- [Hyperledger Indy] - Distributed ledger, purpose-built for decentralized identity
- [Self Sovereign Identity Principles] - 10 principles describing SSI
- [General Data Protection Regulation (GDPR)] - Website with GDPR document divided by sections
- [GDPR Article 17] - Right to erasure (‘right to be forgotten’)

---

> _"Ipsa scientia potestas est" ('knowledge itself is power')_ <br>
> Francis Bacon, Meditationes Sacrae (1597)

<!-- Links -->
[Hyperledger Indy]: https://www.hyperledger.org/projects/hyperledger-indy
[Self Sovereign Identity Principles]: https://github.com/WebOfTrustInfo/self-sovereign-identity/blob/master/self-sovereign-identity-principles.md
[paper comparing decentralized Identity Frameworks]: https://www.slideshare.net/TommyKoens/matching-identity-management-solutions-to-selfsovereign-identity-principles/1
[General Data Protection Regulation (GDPR)]: https://gdpr-info.eu/
[GDPR Article 17]: https://gdpr-info.eu/art-17-gdpr/
