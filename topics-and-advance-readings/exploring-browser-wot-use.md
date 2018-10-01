# Exploring Browser Web of Trust Use Cases

## Intro
Brave is a software company with the goal of improving the web, frequently
by seeking aggressive changes to current web practices.  Currently these
focus in the area of privacy preserving changes to the web, such as Web API
modifications to restrict fingerprinting, alternate cookie policies to reduce
tracking online, and web resource blocking to improve browsing performance.

Brave is also considering other modifications to the web that would improve
our users' experience. Many of these focus on issues of trust and
decentralized identity. Web of Trust, and the systems that can be built on top
of web of trust, are promising, novel and interesting solutions to many of
these issues.

This document presents several use cases Brave is considering using Web of Trust,
or similar techniques, in the browser. **Note** that this document is
not a product map for Brave Software, and it should not be understood to be
indicating any particular problem, nor solution to a problem, that Brave
will deploy in the future. Instead, this document reflects ongoing conversations
between researchers, engineers and product managers at Brave, where we think
it may be mutually beneficial to engage with the web of trust community.


## Use Cases

### Browser Extensions
The primary way browser extensions are distributed to users. Most
commonly, they are distributed through a "web store", maintained by the browser
vendor. Extension authors upload their extensions to the store, the browser
vendor possibly provides some amount of vetting of the code to ensure the
extension performs as expected, and makes it available to users.

This extension distribution technique has proven useful, but comes with
significant downsides. First, it adds an additional location where the browser
vendor stands between the user and the web they wish to experience. Second,
it requires significant maintenance overhead (and, potentially, legal liability)
on the part of the browser vendor, which may be unacceptable for small browser
vendors.  And third, it places the browser vendor in a position of "trust
authorial" that it may be poorly equipped to handle (e.g. making statements
about how a browser extension will behave on a large position of the web).

Steps such as allowing users to install extensions from outside the web store,
creating user ranking systems within the web store, using static analysis
tools to detect malicious extensions, and performing graph analyses on
review systems to detect sybil attacks can be useful, but each carry with
non-trivial costs and benefits that are well understood and beyond the scope
of this paper to detail.

Web of trust may be a partial style solution to decentralized, trusted
extension distribution. A plausible system might involve a WoT style weighted
trust system for assessing of the worthiness of extensions.  Such extensions
could then be distributed in any number of ways, including directly through the
extension owner's server, or out of the extension stores of other browser
vendors. The browser vendor would only need to include tools in the browser
to help users understand the WoT assigned trustworthiness scores, potentially
contribute weights and votes back into the WoT, and a system for users
establishing trust between other browser users.


### Assisting Trusted Micropayments
The problems with current web funding systems are well known.  Funding through
advertising (as currently implemented) entails significant privacy violations
and performance degradation. Subscription schemes require a significant (and
sometimes prohibitive) step from users, and are generally only plausible
to the largest media properties (e.g. a paywall strategy is
feasible for the New York Times, but not The Village Voice). Crowdfunding
schemes require significant overhead captured by the crowdfunding platform.
And all the above are hampered by the well known problems of transaction fees;
payments below a certain threshold are infusible, since the processing costs
dwarf the exchanged amounts.

Crypto-currencies are a promising solution for avoiding transaction fees, but
without a system of trust or identify, the usefulness of such systems is
significantly diminished.  If its cheap to send funds, but expensive to
be confident who the funds are being sent to (possibly due to relying on a
centralized identification service), then micropayments are still unfeasible
in many cases.

Browser vendors could help users with such problems, by using WoT, and
distributed identity systems built on top of WoT, to help users build
confidence that the party they're transacting with is who they claim they
are. As a very trivial example, a WoT / DiD system integrated into a browser
with a crypto currency wallet could allow users to build trust with
distributed identities as they browse, giving them a more confident
basis on which to transfer funds later on.


### DNS Spoofing Resistance
Despite efforts like DNSSec, DNSCrypt, DNS over HTTP and DANE, DNS is still a
weak link in browser security. An active attacker can modify or out-race DNS
traffic, to trick a user to visit a domain under their control. Web of Trust
systems could potentially keep users safe from such attacks, but building
coordinated, distributed-consensus style understandings of domain to IP
mappings.

Such a system could operate similar to Convergence, but use a
distributed trust system, instead of a fixed set of trusted DNS resolvers.

There are many potential issues that arise when considering a WoT alternative
to standard DNS resolution. While such problems are not fatal to a WoT
based system, they present unique challenges to be taken up by the community.
These include how to provide the flexibility of DNS anycast functionality
within WoT, allowing updates to domain-to-ip mappings to percolate through
the WoT quickly when mappings change benignly, and creating a system that
prevents leaking users' browsing history to WoT.

---

**Authors:**
* Peter Snyder, Privacy Researcher, Brave Software, pes@brave.com
* Ben Livshits, Chief Scientist, Brave Software, ben@brave.com
