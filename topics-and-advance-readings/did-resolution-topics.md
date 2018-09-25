DID Resolution Topics
=====================
Markus Sabadello, Danube Tech (https://danubetech.com), Vienna, 20th September 2018

We know that DID Resolution is the process of obtaining the DID Document associated with a DID. Sounds simple, but what are some of the deeper questions and topics to be considered here?

These topics should be addressed in a future [DID Resolution](https://w3c-ccg.github.io/did-resolution/) specification. Some of the topics will be important for [DID Document Interoperability](https://github.com/WebOfTrustInfo/rwot7/blob/master/topics-and-advance-readings/diddoc-conventions-for-interoperability.md).

## Resolver Architecture

Most DID Resolution implementations envision an architecture where a common base component invokes a set of "drivers" or "plugins" or "modules" to implement method-specific functionality, e.g. see the DIF [Universal Resolver](https://github.com/decentralized-identity/universal-resolver), Digital Bazaar's [did-client](https://github.com/digitalbazaar/did-client), or the uPort [JavaScript DID Resolver](https://github.com/uport-project/did-resolver). We envision such "DID Resolver" tools to become as central to SSI infrastructure as DNS is for the web today.

**Topics:**

 * There are different ways how an application or service can use a DID Resolver (e.g. as a natively linked library, or via an HTTP API).
 * There are different ways how a DID Resolver can access a target system (e.g. direct access to a blockchain full node, access using a light client, or access via an intermediary blockchain explorer API).
 * These different deployment scenarios have trust implications. Ideally an application or service should be as "close" to a DID Resolver as possible, and the DID Resolver should be as "close" to the target systems as possible, in order to minimize intermediaries and attack surfaces.
 * A common topic is DID method governance, i.e. which DID methods should a DID Resolver support, and how should this question be governed (see [here](https://github.com/w3c-ccg/did-resolution/issues/6)).

## Input / Output

We can think of DID Resolution as a function with the DID as input and DID Document as output. It may make sense however to have additional input parameters and additional output data of the DID Resolution process.

**Topics:**

 * There could be input parameters that specify which part of a DID Document is needed, instead of the entire DID Document. For example, a client may only need a specific `publicKey` object (specified either by `id` or by `type`). Or a client may only need a specific `service` object (specified by `type`).
 * There could be an input parameter that specifies a minimum level of trust required for the DID Resolution process (e.g. should the DID Resolver have access to its own blockchain full node, or is it also acceptable to use a light client, or an intermediary blockchain explorer API).
 * There could be an input parameter that specifies whether cached results are acceptable, or whether a full DID Resolution process should be performed.
 * Input parameters could be "passed through" to the driver, this could help to optimize the DID Resolution process (e.g. in the case of the `btcr` DID method, if only the main on-chain `publicKey` object is needed, it may not be necessary to retrieve the off-chain DID Document).
 * There could be additional output data generic to the DID Resolver (e.g. duration of the DID Resolution process, or which driver was used).
 * There could be additional output data specific to the DID method (e.g. a state proof in the case of the `sov` DID method).
 * Such additional output data could either be nested inside the DID Document, or held by a separate data format outside the DID Document.

## HTTP Binding

Even though an application or service should ideally use a "built-in" (natively linked) DID Resolver, we also envision an HTTP Binding for DID Resolution functionality.

**Topics:**

 * A DID Resolution request could be modeled as a simple HTTP GET operation, e.g. `curl -X GET https://uniresolver.io/1.0/identifiers/did:sov:WRfXPg8dantKVubE3HX8pw`, which returns a DID Document.
 * We would specify ways how additional input parameters and additional output data are modeled in the HTTP Binding of DID Resolution, e.g. using URI query parameters.

## Resolution Logic

Most DID Resolution logic is method-specific and happens in the drivers, but there are also some topics to consider that apply to DID Resolution in general.

 * For the DID Document, we consider the DID to be the "Base IRI" in JSON-LD, which allows us to use relative IRIs in the DID Document (see [here](https://github.com/w3c-ccg/did-resolution/issues/9) and [here](https://github.com/w3c-ccg/did-spec/issues/97)).
 * Probably we should require a DID Resolver to validate DID Documents, i.e. only return DID Documents that conform to the specification.
 * It has been proposed that the `serviceEndpoint` URL could itself be a DID, in which case a second (child?) DID Resolution process would be initiated (see [here](https://github.com/w3c-ccg/did-resolution/issues/7)). This logic could be controlled by additional input parameters, and it could return additional output data.

## Non-DID Identifiers

While most attention right now is focused on DIDs, there are also many other kinds of identifiers, some of which can and some of which can not be considered decentralized (see [here](https://github.com/w3c-ccg/did-resolution/issues/8)). We can discuss whether DID Resolution and resolution of non-DID identifiers should be handled by the same kind of tool, or whether implementations should keep those separate.

**Topics:**

 * Linked local names (petnames) could potentially point to DIDs (see [here](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust/blob/master/topics-and-advance-readings/linked-local-names.md)).
 * Cryptographic identifiers (CIDs, cryptonyms) seem to be useful in some cases and resemble DIDs in some ways (see [here](https://github.com/w3c-ccg/did-spec/pull/55)).
 * DID Names have been suggested as decentralized, human-friendly identifiers (see [here](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-spring2017/blob/master/topics-and-advance-readings/did-names.md)). 
 * Domain names can point to DIDs using DNS records (see [here](https://datatracker.ietf.org/doc/draft-mayrhofer-did-dns/)].
 * HTTP URLs can point to DIDs using HTTP headers, HTML tags, or WebFinger (see [here](https://tools.ietf.org/html/rfc7033)).
 * To prove control of a non-DID identifier such as a domain name, the DID could have a "backreference" to that non-DID identifier.

## DID Revocation

The DID spec says that all DID methods MUST specify how a DID can be revoked on the target system.

**Topics:**

 * When resolving a revoked DID, the result could either be the same as for a DID that has never existed, or the result could be a DID Document with a special revocation flag or timestamp (see [here](https://github.com/w3c-ccg/did-resolution/issues/5)).

## DID Document Versioning

The DID spec says that all DID methods MUST specify how a DID can be updated on the target system.

**Topics:**

 * There could be additional input parameters to the DID Resolution process that allow clients to obtain earlier versions of a DID Document.
 * When resolving a DID, the DID Document could contain a version number or timestamp of the last update.
 * Note that while all DID methods MUST support updates, there is no requirement for DID methods to keep all previous DID Document versions, so this may be a method-specific feature.

## Caching

During the DID Resolution process, caching may occur in various ways.

**Topics:**

 * A DID Resolver may maintain a generic cache of DID Documents.
 * Individual drivers may maintain caches of method-specific data.
 * Caching behavior could be controlled by configuration of the DID Resolver, by additional input parameters of the DID Resolution process, or by contents of the DID Document (e.g. a "time-to-live" field), or by a combination of these options.

## Other Topics?

Additional topics/issues related to DID Resolution can be raised [here](https://github.com/w3c-ccg/did-resolution).
