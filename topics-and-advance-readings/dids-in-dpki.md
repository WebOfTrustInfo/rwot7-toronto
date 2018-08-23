# DIDs In DPKI (Decentralized Public-key Infrastructure)

*This document seeks to act as a starting point to bridge the two worlds of [DPKI](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/final-documents/dpki.pdf) (which [appeared](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/final-documents/dpki.pdf) in the first RWOT) with DIDs (which [appeared](https://github.com/WebOfTrustInfo/ID2020DesignWorkshop/blob/master/final-documents/requirements-for-dids.pdf) at the second RWOT).*

**Author:** Greg Slepak ([twitter](https://twitter.com/taoeffect), [mastodon](https://mstdn.io/@taoeffect))

## Overview

Remember [DPKI](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/final-documents/dpki.pdf)?!

A quick reminder for those who don't:

- DPKI stands for *Decentralized Public-key Infrastructure*
- DPKI seeks to serve as an improved alternative/replacement for [X.509](https://en.wikipedia.org/wiki/X.509) (that thing securing today's Internet)
- DPKI changes the web's security model from 1000s of single-points-of-failure to *decentralized consensus groups* that create namespaces (sorta like what blockchains do!)
- DPKI is not a blockchain — it's a protocol for securely accessing blockchains and similar decentralized consensus systems
- DPKI has Top-Level Domains (TLDs) representing different blockchains (e.g. `.eth`, `.bit`, `.id` etc.)

For an overview of DIDs read the [DID Primer](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/did-primer.md).

## Timeline

We're kinda making this up as we go along, so there is no fixed timeline, but so far this is how things are turning out to be:

```
DPKI Overview (RWOT1)
|
+-> Requirements for DIDs (RWOT2)
    |
    +-> DID Data Model and Generic Syntax Draft 1 (RWOT3)
        |
        +-> Decentralized Identifiers v1.0 (RWOT6)
            |
            +-> ??? (RWOT7)
```

## DIDs In DPKI

A DID key looks like this:

```
did:namespace:identifier
```

A specific example might look something like this (taken from [BTCR DID Resolver Specification](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2018/blob/master/final-documents/btcr-resolver.pdf)):

```
did:btcr:xkyt-fzgq-qq87-xnhn
```

Obviously this is not useful (by itself) for dealing with human-readable TLDs.

What are we trying to do here, ultimately?

We are trying to [Square Zooko's Triangle](http://www.aaronsw.com/weblog/squarezooko):

```
    Decentralized
          /\
         /  \
        /    \
       /      \
      /________\ 
Secure          Human-readable
```

**So far DIDs give us `Secure <-----> Decentralized`**.

**We are still missing `Human-readable`.**

**That's where TLDs and Namespaces come in.**

## TLDs and Namespaces

But before we can talk about TLDs and Namespaces, we need to address a philosophical "debate" ("question"?) within the DID ethos.

### Are DIDs Human-readable?

The answer to this question is not clear.

Some have argued that DIDs should be "unique identifiers that last a lifetime". Meaning, no, they should not be human readable.

Instead they should act like a UUID that you can point other things to.

Still others say there's no reason they can't be unique and human readable.

So a DID could look like this:

```
did:btcr:xkyt-fzgq-qq87-xnhn
```

Or it could look like this:

```
did:btcr:my-great-website
```

One thing is clear: if a DID isn't human-readable, **you are still going to need a human-readable identifier within a secure namespace** to find it.

Why? Why can't you, for example, take the [GNUnet](https://en.wikipedia.org/wiki/GNUnet) approach (e.g. ["linked local names"](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/linked-local-names.md)) and create an inconsistent decentralized world, where everyone has their own personal address book, and they somehow discover and save a non-human-readable identifier to a local, human-readable contact card?

Well, they certainly *can* do that, but that is not what ***DPKI*** is about.

DPKI is about *global identifiers*, not local identifiers.

DPKI has to re-create the usual experience that we're used to, where you type in an easily memorized human-readable term, like `apple.com`, and *no matter where you are in the world, no matter what device you're using, you will find Apple's homepage with that tiny, easily memorized identifier.*

This is important not only for visiting websites, it's also important for making other protocols, like email, secure.

**So whether or not _ALL_ DIDs are human-readable is irrelevant to DPKI — In DPKI, DIDs Are Human-readable.**

In other words, identifiers in DPKI have these properties:

- They exist in a namespace secured through decentralized consensus, e.g. a blockchain (see also, [DCS Theorem](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/final-documents/dcs-theorem/The-DCS-Theorem.pdf))
- They are human-readable
- They are updateable
- They can expire
- They are looked up through a secure lookup mechanism that does not have a SPOF (single-point-of-failure)

### Past Discussion and Related Topics

- [Soverign Identity Namespaces](https://github.com/WebOfTrustInfo/ID2020DesignWorkshop/blob/master/topics-and-advance-readings/SovereignIdentityNamespaces.pdf) - note that none of the concepts described in this document are suitable for DPKI, because DPKI identifiers must be cryptographically secure *and* globally-unique *and* human-readable
- [DID Names](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/topics-and-advance-readings/did-names.md) - the `id:` scheme described here might be relevant, but it's also not clear that it's necessary. It could represent unnecessary complexity
- [Making DIDs invisible: Petnames and their secure user interfaces](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2018/blob/master/draft-documents/making-dids-invisible-with-petnames.md) - unclear whether this is relevant to DPKI, but might be worth discussing
- [Petnames for Self Sovereign and Human Readable Identifiers](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2018/blob/master/topics-and-advance-readings/petnames.md) - unclear whether this is relevant to DPKI, but might be worth discussing

## Next Steps

The RWOT community needs to come up with a protocol that fulfills the DPKI goals as stated in the [DPKI overview document](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/final-documents/dpki.pdf) (with amendments [one](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/issues/90) and [two](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/issues/89)).

We need to create a protocol that takes a normal-looking domain, for example:

```
https://bitcoin.btc
```

Look up `bitcoin.btc` in a secure, decentralized manner through the Bitcoin blockchain (or Ethereum if the TLD is `.ens`), do any additional lookups, and return two things:

1. An IP address to the server that's hosting that domain
2. A list of hashes representing valid public keys for that domain

Then it's up to the browser to connect to the IP address and retrieve the webpage.
