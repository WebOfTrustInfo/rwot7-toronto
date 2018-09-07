# Magenc Magnet URIs: Secure Object Permanence for the Web

Author: [Christopher Lemmer Webber](https://dustycloud.org/)

## Introduction

The web has been a great tool for the wide distribution of content.
Unfortunately, reliance on HTTP based URIs has meant that content is
liable to disappear or change unexpectedly.
Additionally, access control for private content is difficult to make
secure on the contemporary web.

Content Addressed Storage allows for us to refer to objects by their
hash without binding that object to a specific location, and may be
referred to with such addresses as [URNs](https://en.wikipedia.org/wiki/Uniform_Resource_Name) or [IPFS](https://ipfs.io/) addresses.
These are popularly combined with peer to peer distribution using the
[magnet URI scheme](https://en.wikipedia.org/wiki/Magnet_URI_scheme).
For example, a file with the text "foo bar baz" may be hashed with the
sha1 algorithm to get the address
`urn:sha1:4e4ced5ee12c698209feaab89fd33e93fb7890dd`
which is the content addressed URI for that file.
The magnet URI scheme allows for attaching additional metadata about
where that file may be retrieved such as over the Bittorrent protocol.
Such a magnet URI might look like:

    magnet:?xt=urn:sha1:4e4ced5ee12c698209feaab89fd33e93fb7890dd&tr=https://tracker.example/abc1

Additional metadata, such as a suggested filename, a suggested HTTP
URL location that may hold the file, or the size of the file are also
possible to add as query parameters to the magnet scheme:

    magnet:?xt=urn:sha1:4e4ced5ee12c698209feaab89fd33e93fb7890dd&as=https://filestore.example/foo.txt&xs=11

(Some liberties have been taken for the sake of visual clarity over
correctness; future magnet URIs in this article will correctly
percent-encode the query parameters.)

Unfortunately this leaves content distributed in cleartext.
This can be especially disastrous if we would like to distribute
private content while still taking advantage of peer to peer systems.
Worse yet, participants in a peer to peer system who may volunteering
their resources to help the network might be at risk of liability for
distributing or hosting content in the interest of helping the
protocol while having no knowledge of the content.

In this paper we introduce an extension to Magnet URIs we call
"magenc" by adding two more additional query parameters, the key and
the encryption algorithm used.
Magenc is inspired by such systems as [Tahoe-LAFS](https://tahoe-lafs.org/trac/tahoe-lafs), [libchop](http://www.nongnu.org/libchop/), and
capability systems such as [Waterken](http://waterken.sourceforge.net/) and the [E programming language](http://erights.org/).
We take advantage of magnet's URI composition by allowing for content
to be "sealed" and "unsealed": when content is distributed via its
content addressed representation without knowledge of the decryption
key, it is sealed.
Participants who are intended to be made knowledgeable of the file's
contents are given the magenc-extended magnet URI which contains the
key and algorithm information necessary to unseal its contents.
Additionally, we have provided mitigations against inferring content
based on file length via chunking and have provided optional file
deduplication via convergent encryption.

This paper addresses immutable content only; mutable content must be
added as a separate layer, but may use the designs in this
specification as part of its design.


## Magenc by example

Magenc is best understood by example.
Thankfully, a demo implementation exists.
First, install the Racket programming language.
Then, at the command line run:

    $ raco install magenc

This Magenc package comes with a demo content addressed storage
server.
It is not intended for production use, as it stores content in
memory only.
Let's start it up:

    $ raco cas-server
    Your Web application is running at http://localhost:8000.
    Stop this program at any time to terminate the Web Server.

Note that though we use an HTTP server in this demo, any sort of
storage system that knows how to dereference the eXactTopic links can
be used, from a local offline database to a full on peer to peer
network.
Also note that the magnet URI itself will never be provided to the
storage system, only the eXactTopic parameter.

This demo server only has two operations&#x2026; a POST request stores
the content and returns its content-addressed URN:

    $ curl -d "Hello CAS store" -X POST http://localhost:8000
    urn:sha256:y7y84K0IO8apO0FA9CWNPU7jqzpHFrR1W4YLChshm2w

Submitting it again will give us the same URN, since it is stored
based on its contents:

    $ curl -d "Hello CAS store" -X POST http://localhost:8000
    urn:sha256:y7y84K0IO8apO0FA9CWNPU7jqzpHFrR1W4YLChshm2w

We can then get the content back by requesting its location based on
this URN, which is its eXactTopic:

    $ curl http://localhost:8000?xt=urn:sha256:y7y84K0IO8apO0FA9CWNPU7jqzpHFrR1W4YLChshm2w
    Hello CAS store

Unfortunately, this is a fairly naive CAS store and no encryption is
performed directly.

Let's put ourselves in the feet of Carlos.
Carlos would like to write a sappy love letter to his significant
other Bob, but before he sends it he would like his friend Alice to
review.
Carlos pens a rough draft:

    $ echo "Dear Bob, my love for you is greater than the sum of stars. -- Carlos" > sappy-love-letter.txt

Perhaps we would like to pen a sappy love letter and send it to our
significant other.
But what if the administrator of the storage server could see it?
Carlos might be terribly embarrassed&#x2026; too embarrassed to ever post it.

Thankfully Carlos can seal the contents:

    $ raco magenc --upload sappy-love-letter.txt
    magnet:?xt=urn%3Asha256%3AX74UbU3NoLTA_Nupi8DhaJ_oQpQ95KFukMAkJJotKgo&ek=eekxqfiZIcEnc8cpR-sD_3X3qLaTzQW-KnovArMkGP0&es=aes-ctr

We can then get the contents back:

    $ raco magenc --get "magnet:?xt=urn%3Asha256%3AX74UbU3NoLTA_Nupi8DhaJ_oQpQ95KFukMAkJJotKgo&ek=eekxqfiZIcEnc8cpR-sD_3X3qLaTzQW-KnovArMkGP0&es=aes-ctr"
    Dear Bob, my love for you is greater than the sum of stars. -- Carlos

(Astute readers will note that we haven't mentioned signing contents
so that Alice and Bob know that Carlos really signed it.
Carlos could always distribute a file that signs the object
alongside or embedded in the file, but that is left as an exercise
for the reader.)

Let's unpack that Magnet URI.
It has three different query parameters:

-   **xt** is the eXactTopic, which gives the hash which refers to the
    relevant *encrypted* file.
-   **ek** is the EncryptionKey used to encrypt/decrypt the file
    and is base64 encoded.
    This is a Magenc extension to the `magnet:` uri scheme.
-   **es** is the EncryptionSuite, the encryption algorithm used.
    This is a Magenc extension to the `magnet:` uri scheme.

Carlos is suddenly worried that maybe the administrator is able to see
this content.
We can see exactly what file it uploaded by adding the `--verbose` flag.

    $ raco magenc --verbose --upload sappy-love-letter.txt
    DEBUG: posted urn:sha256:yWTt2U5hvAn4jGAByzzHrtMasN98xadFqjKLhA4EpXM
    magnet:?xt=urn%3Asha256%3AyWTt2U5hvAn4jGAByzzHrtMasN98xadFqjKLhA4EpXM&ek=Jb79KiJpHvxkF36hzQcvCthZX0r0GEfWoa4nLAf28Vg&es=aes-ctr

Ok, it looks like the file we uploaded is the same file as at the
eXactTopic.
Let's see what happens if we download that file from the CAS store
directly:

    $ curl http://localhost:8000?xt=urn:sha256:yWTt2U5hvAn4jGAByzzHrtMasN98xadFqjKLhA4EpXM
    <screen fills with garbage>

Yikes!
It spit out a bunch of binary junk&#x2026; Carlos can't tell what that is,
and thankfully neither can the storage administrator.

However, we could write out those contents out to a file and decrypt
it manually.
If we did, it would look like this:

    (3:raw70:Dear Bob, my love for you is greater than the sum of stars. -- Carlos\n)

&#x2026; followed by a bunch of bytes of whitespace.
The whitespace is easy to explain: to prevent side channel attacks
where content can be inferred by file length, additional padding is
added so that files fit within the relevant "chunk size".
(We are defaulting to a chunk size of 32 Kilobytes.)
If this file were larger, we would split it into multiple chunks
and the first object retrieved would be a `manifest` pointing at
the rest of the chunks.
Since this file is so small we can include it in a single chunk
without requiring a manifest, so it is a `raw` file.

Now, what's with the rest of the stuff in the file?
First of all, since the "raw" file is an optimization, we need
a way to distinguish between the raw file and a "manifest" file.
Second, while there isn't much to the raw file, manifest files
need more structure.
So we are using the world's simplest structured data format,
[canonical s-expressions](https://people.csail.mit.edu/rivest/Sexp.txt).
Canonical s-expressions have the advantage of being small and
easy to implement (an implementation can take as little time
as an hour or two for a seasoned programmer).
Canonical s-expressions combine two concepts: netstrings and
s-expressions.

Netstrings are the world's simplest non-structured data format.
The netstring for the word "cat" is `3:cat`.
Number of characters in base-10 of the object's size in bytes,
then the bytes.
This also has the advantage that binary data is easy to encode.

S-expressions are lists of items, delimited by parentheses.
So we could describe a zoo full of animals (where an animal
is described by its name, what it says, and what it eats) like:

    (zoo (animal cat meow kibble)
         (animal monkey ooh-ooh bananas))

(This is also more or less the "advanced encoding" of
canonical s-expressions.)

Canonical s-expressions replace the items in the lists with
netstrings.
So the canonical s-exp (in canonical form) for our zoo would look like:

    (3:zoo(6:animal3:cat4:meow6:kibble)(6:animal6:monkey7:ooh-ooh7:bananas))

Magenc implementations MUST only use the canonical implementation of
canonical s-expressions on the wire, so the implementation overhead
here is very small.

Knowing that, the format for a "raw" object in Magenc looks like:

    (raw <raw-data-goes-here>)

And that's it, hence the contents of the encrypted object.
But in general, users do not need to know about this.

Carlos sends the Magenc-extended Magnet URI to Alice.
She says that the letter is very nice, but that Carlos is such a nice
artist, so why not do a digital painting of a galaxy with the words
superimposed?
Carlos immediately agrees that this is a good and not at all
tacky improvement to the design and gets to work.

Carlos has finished the painting and uploads it.
This time he is curious about how many objects it will upload, so
he runs with `--verbose`

    $ raco magenc --verbose --upload sappy-love-painting.png 
    DEBUG: posted urn:sha256:7gfqd3hDTf56FEb9i_x9_cxwgVwjUNDwldJtC9v1T8o
    DEBUG: posted urn:sha256:E7XwTkJO2ufGW7cCc9qk5rNJPh2xTbxxDN0HMQHiP4s
    DEBUG: posted urn:sha256:JVdTXIHBBkF2dHvc_FW8wmKN_2ow9lSq3orWF0V0G4o
    DEBUG: posted urn:sha256:hClheQii8FoomnWNLiLc8E2A8HYtCWbVtA22xWblMCs
    DEBUG: posted urn:sha256:fwFIj8TIXaeiViqbH252V5L0mY3EOb5pPXhQg-Xci1c
    magnet:?xt=urn%3Asha256%3AfwFIj8TIXaeiViqbH252V5L0mY3EOb5pPXhQg-Xci1c&ek=IEbic8nd8V82n2K6huAyI6T_fq0vKVj5NDbBpn4JhiI&es=aes-ctr

Huh, that's interesting!
This time it uploaded more chunks than last time.
Let's decrypt the eXactTopic again.
Minus the padding (manifest files are padded to the length of the
nearest available multiple of the chunk size), it looks like:

    (8:manifest5:327686:12528654:urn:sha256:7gfqd3hDTf56FEb9i_x9_cxwgVwjUNDwldJtC9v1T8o54:urn:sha256:E7XwTkJO2ufGW7cCc9qk5rNJPh2xTbxxDN0HMQHiP4s54:urn:sha256:JVdTXIHBBkF2dHvc_FW8wmKN_2ow9lSq3orWF0V0G4o54:urn:sha256:hClheQii8FoomnWNLiLc8E2A8HYtCWbVtA22xWblMCs)

That's pretty hard to read, so here it is pretty-printed:

    (manifest "32768" "125286"
     "urn:sha256:7gfqd3hDTf56FEb9i_x9_cxwgVwjUNDwldJtC9v1T8o"
     "urn:sha256:E7XwTkJO2ufGW7cCc9qk5rNJPh2xTbxxDN0HMQHiP4s"
     "urn:sha256:JVdTXIHBBkF2dHvc_FW8wmKN_2ow9lSq3orWF0V0G4o"
     "urn:sha256:hClheQii8FoomnWNLiLc8E2A8HYtCWbVtA22xWblMCs")

Manifest files look like:

    (manifest <chunk-size> <file-size> <chunk1> <chunk2> ...)

So based on that, we can tell that the sappy love painting's manifest
indeed contains all the chunks we saw from the DEBUG messages of the
upload stage.

Alice downloads the file on her end:

    $ raco magenc --verbose --get "magnet:?xt=urn%3Asha256%3AfwFIj8TIXaeiViqbH252V5L0mY3EOb5pPXhQg-Xci1c&ek=IEbic8nd8V82n2K6huAyI6T_fq0vKVj5NDbBpn4JhiI&es=aes-ctr" --output carlos-love-painting.png
    DEBUG: got urn:sha256:fwFIj8TIXaeiViqbH252V5L0mY3EOb5pPXhQg-Xci1c
    DEBUG: got urn:sha256:7gfqd3hDTf56FEb9i_x9_cxwgVwjUNDwldJtC9v1T8o
    DEBUG: got urn:sha256:E7XwTkJO2ufGW7cCc9qk5rNJPh2xTbxxDN0HMQHiP4s
    DEBUG: got urn:sha256:JVdTXIHBBkF2dHvc_FW8wmKN_2ow9lSq3orWF0V0G4o
    DEBUG: got urn:sha256:hClheQii8FoomnWNLiLc8E2A8HYtCWbVtA22xWblMCs

This makes sense&#x2026; the first object that Alice's client retrieved was
the manifest, so that's the first object outputted in the DEBUG
messages, and then every file after that was listed as a chunk in the
manifest.
Alice's client takes care of details so she doesn't have to, from
decrypting the manifest and each chunk, to verifying that each chunk
matches the chunk size calculating how much to read from the last
chunk based on the total file size (the rest is padding).
But Alice doesn't need to worry about any of that.

Alice looks at the image and thinks it looks quite good.
She says as such to Carlos, who enthusiastically then passes the
magenc-extended magnet url along to Bob.

Bob really appreciates the painting, and Carlos, feeling relieved that
Bob enjoys it so much, consents to Bob's request that they share the
painting far and wide across their group of friends.

Bob and Carlos' friend group all use the same shared magenc-enabled
backup service and pay for the costs of that shared storage.
Why pay the additional storage cost for the same file?
We can see the potential problem when we try running the upload
command multiple times:

    $ raco magenc --upload sappy-love-painting.png
    magnet:?xt=urn%3Asha256%3AFY9rimPzXjqw8u3AfM-ErrGp072W4gYPE9fCJ8MhXuE&ek=NLeRbCuKcrPoQE8G9OWyDukaiDqQS_nhKZHkc4oCKzk&es=aes-ctr
    $ raco magenc --upload sappy-love-painting.png
    magnet:?xt=urn%3Asha256%3AV5FXelScKY2bv1Rl4emN6qFjHAojfExBkyMV-HMAvUI&ek=0Hf-JsD_olN7TESvaHBy-DyDqQUrzneIOc53nZdXXmc&es=aes-ctr
    $ raco magenc --upload sappy-love-painting.png
    magnet:?xt=urn%3Asha256%3AoYOvXseaJ3OdWtQ6EUiS83V5FRuG5VXejAgps-bWGIM&ek=EPf3E03lx1qpeLBlMMAOVjosSac8IVbyLUDTMhhu_Y8&es=aes-ctr

Uhoh&#x2026; each of those uploads creates a new random key, and thus
a new object.
Fortunately we can take advantage of a concept called "convergent
encryption" where instead we use the hash of the decrypted file as
the key (note that this will be different than the hash of the
encrypted objects, so having access to the hash of the encrypted
object used in the eXactTopic will not expose the contents).
(Note that convergent encryption should be fine in this case but
may have security risks for [certain data-sharing situations](https://tahoe-lafs.org/hacktahoelafs/drew_perttula.html).)
Let's see what happens now if we try uploading the same file
multiple times:

    $ raco magenc --upload sappy-love-painting.png --convergent
    magnet:?xt=urn%3Asha256%3AH9dDY4Y0y39K2rziDY5Ul9iBDfP51Fg9EAHncrIINDU&ek=rGVdQ2K4dGhEOFd-50eoRwNRYPGf1w0yIi_E5_bE5WY&es=aes-ctr
    $ raco magenc --upload sappy-love-painting.png --convergent
    magnet:?xt=urn%3Asha256%3AH9dDY4Y0y39K2rziDY5Ul9iBDfP51Fg9EAHncrIINDU&ek=rGVdQ2K4dGhEOFd-50eoRwNRYPGf1w0yIi_E5_bE5WY&es=aes-ctr
    $ raco magenc --upload sappy-love-painting.png --convergent
    magnet:?xt=urn%3Asha256%3AH9dDY4Y0y39K2rziDY5Ul9iBDfP51Fg9EAHncrIINDU&ek=rGVdQ2K4dGhEOFd-50eoRwNRYPGf1w0yIi_E5_bE5WY&es=aes-ctr

As we can see, this time all of the magnet URIs are exactly the same!
Using convergent encryption, Bob and Carlos' friend group can all
safely and back up the same file to the shared hosting service without
wasting space.
That will be extra helpful after all the photos and videos will be
shared amongst each other from their upcoming wedding!


## Conclusions

Using content addressed storage is a great way to distribute content
in a decentralized system which is robust against failing nodes, but
by default is unsuitable for anything but public content and puts a
great burden of responsibility for hosting providers and peer to peer
nodes that want to distribute content for the sake of the network's
operation but which do not want to be held responsible for the files'
contents.
Adding symmetric encryption provides privacy for participants sharing
content while also allowing general distribution of that content
without revealing information except to participants who have been
intentionally chosen to receive it.

The magnet URI scheme already composes other URIs with additional
metadata and is in wide use for many peer to peer networks.
This makes it a reasonable place to add metadata for the encryption
key and suite (although clients which are not aware of the magenc
extensions will receive the encrypted information without being
aware of how to interpret it).
Although this demo used URNs, since the magnet URI scheme does not
specify a specific URI scheme for the eXactTopic, other URI schemes
such as IPFS can be used to the same effect.

The decision to type the first file retrieved means that for
particularly small files, no more than one request is needed to
retrieve the entire file since the file may be tagged as "raw".
For larger files, the decision to use a single manifest file over a
merkle tree has the upside of ease of implementation and that the
number of requests is `n+1` where `n` is the number of chunks, whereas
a merkle tree would be `O(log(n))+n` requests.
However when a manifest file exceeds the chunk size it is rounded up
to the nearest multiple of the chunk size which leaks both that this
file is a manifest file and also gives some coarse grained information
about the approximate range of the file it references in megabytes.
However the author believes this tradeoff is worth it; one additional
benefit of the system described in this paper is that given a decent
programming language and a cryptography library, the entire system can
be written in one weekend, including the canonical s-expressions
library.
The author of this article wrote the demo tools used in this article
in a single day (although they had already written the canonical
s-expressions library on a different day).

Details about garbage collection, which nodes will host content,
and how to provide mutability are out of the scope of this paper
but may be composed separately in conjunction with its design.
For example, a gossip protocol plus a signed git-like merkle tree
could be used to allow entities to provide updates while referencing
immutable objects referenced by the magenc-extended magnet URIs
described in this paper.
If an enforced linear structure to those updates is necessary,
a consensus algorithm could be used.
As for garbage collection, entities may choose to pin or store the
objects they particularly care about, or services may use such
a policy such as deleting objects which have not been recently
requested.

Local tests against this not-particularly-optimized demo
implementation indicate that the general design is reasonably fast
for many use cases.
Uploading a 38 megabyte video file takes .8 seconds (excluding startup
time) against the demo http server CAS store, and against an
in-process memory store takes .6 seconds.
Fetching the same uploaded file takes 1.2 seconds against the HTTP
server and a mere .2 seconds against the memory store, indicating that
the primary overhead on retrieval is the HTTP server implementation
itself.


## Related work and thanks

[Tahoe-LAFS](https://tahoe-lafs.org/trac/tahoe-lafs) and [Libchop](http://www.nongnu.org/libchop/) are the primary sources of inspiration for
the ideas in this paper.
Both of those have the fundamental idea of distributing encrypted,
chunked copies of file to storage providers that are unaware of
the files' contents.
Much of this design came from reading the [Tahoe-LAFS paper](https://gnunet.org/sites/default/files/lafs.pdf) and
[this paper about libchop](https://hal.archives-ouvertes.fr/hal-00187069/en/).
Both Tahoe-LAFS and libchop provide some features that are not
in this paper for the sake of keeping things simple to implement,
such as compression and versioning.

[Waterken](http://waterken.sourceforge.net/) and [Zerobin](http://sebsauvage.net/wiki/doku.php?id=php:zerobin) both provided the idea of having a URI that
contains a secret which the source holding the content cannot see.
Both of these use the fragment identifier part of a URI to accomplish
this, but this would not work for us for two reasons: both of these
use a dynamic client (such as one using javascript) to interpret
incoming data, and also because motivating examples for this paper
include linked data systems where the fragment is already highly
overloaded and needed for such things as referring to vocabulary
terms.

Special thanks to Ludovic Courtès for discussing these ideas
and to Zooko for trying to convince Christopher Lemmer Webber
to take Tahoe-LAFS seriously for their projects, even if it took
Chris nearly a decade later to do so.
Thanks also to the capability community in general for listening
to and answering many questions, such as what the heck does a
sealer / unsealer pair mean anyway.
