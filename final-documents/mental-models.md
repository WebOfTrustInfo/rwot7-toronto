# Five Mental Models of Identity

### by Joe Andrieu (joe@legreq.com), Legendary Requirements; Nathan George (nathan@sovrin.org), Sovrin Foundation; Andrew Hughes (andrewhughes3000@gmail.com), ITIM Consulting; Christophe MacIntosh (cm@clearmatics.com), Clearmatics; and Antoine Rondelet (ar@clearmatics.com), Clearmatics



Abstract
========

Engineers of identity systems, both digital and non-digital, have
assumptions and requirements that often lead to fundamentally different
ideas about useful solutions. One’s preferred use cases establish mental
models tailored to those uses, which in turn shape discussion and
engineering of identity systems. The differences between these mental
models consistently cause confusion and disagreement when advocates of
different models collaborate, often without the parties realizing that
others may be speaking from a distinctly different, yet valid, notion of
identity. Considering different mental models allows for constructive
dialogue and reconciliation of requirements, creating opportunities to
address a wider set of use cases and to build systems with better
overall applicability and quality.

We present five distinct mental models observed in conversations among
technologists and laypeople when discussing identity. We then discuss
observed patterns of discussion and design that result from the
intersection of some pairs of mental models. Finally, we close with
guidance for incorporating all five mental models when evaluating or
designing any real-world or digital-identity system. We propose that
understanding and considering these different mental models will result
in more fruitful collaboration and ultimately in better identity
systems.

Background
==========

The authors have been participants, speakers, and organizers at
identity-related professional gatherings for over a decade, including
the Internet Identity Workshop[1], Rebooting the Web of Trust[2],
ID2020[3], and EIC[4], to name just a few. They have held leadership
roles in identity-related standards efforts at the W3C[5], IETF[6],
Kantara Initiative[7], and ISO[8].

As active contributors to industry conversations about interoperable
digital-identity systems, we have witnessed how different communities
engage with emerging technologies to solve real-world identity problems.
In these conversations we have seen participants consistently struggle
to communicate clearly about “identity”, “digital identity”, and
“identity systems”. New participants often misconstrue established
jargon used by well-versed veterans, who themselves tend to make several
key assumptions. The motivation for simple and informal discourse leads
to unrigorous language that makes it hard to establish a common
understanding of identity.

While simple and informal terms can communicate and share ideas, they
risk introducing false understanding and confusion. Mistakes seep in
around the edges as developers, regulators, decision makers, and
end-users shift their use of language. What feels natural to one speaker
may not be understood with the same nuance by listeners. What is
intended to be specific and limited is often heard more broadly and
generally. These informalities ultimately undermine the shared goals of
building robust identity systems. As digital identity becomes
increasingly relevant to businesses, governments, and society at large,
it is vital that we find simpler, yet more rigorous, ways to communicate
more clearly about identity.

The ideas behind this paper were initially presented at *Rebooting the
Web of Trust V* in Boston in 2017[9] as a brief one-hour discussion,
followed by a session the next month at the 25th *Internet Identity
Workshop* in Mountain View[10].

The initial discussion proposed three mental models. Since then, a
fourth and fifth mental model have been incorporated based on feedback
from fellow professionals. The first presentation of the current set of
five mental models was submitted as an advanced reading topic paper
[11] for the *Rebooting the Web of Trust VII [12]* workshop that was
held in Toronto in September 2018. The same month, these mental models
of identity were adopted as a key framework for the design workshop of
the *International Identity Summit[13]* at the University of
Washington. It was at *Rebooting the Web of Trust VII* that the current
authors began collaborating on this paper.

We look forward to receiving feedback and suggestions about this mental
model approach and the five mental models we describe. Our hope is that
the ideas we present will help identity professionals, developers,
regulators, decision makers, and end-users communicate more clearly and
effectively, and as a result create digital identity systems that better
address the needs of all potential stakeholders.

Mental Models
=============

Mental models are psychological representations of real, hypothetical,
or imaginary situations [14]. In this paper, we are referring to the
psychological representations people have for “identity”. Our
experiences have shown that different people approach identity in
different ways, consistent with the mental models we discuss in this
paper.

From our observations, we have identified five distinct mental models
for identity, each with its own framing, its own purpose, and its own
defining question. These are five orthogonal mental models of identity.
By understanding them, we can better understand how apparently disjoint
ideas of identity relate to each other, enabling the discussion and
engineering of better, more broadly useful, and more secure identity
systems.

These mental models are naturally emergent notions that arise from the
needs people have for identity. While these models can be taught, our
observations show that these models are more often argued for and
assumed (with the exception of the Attribute mental model, which is
enshrined in an international standard). This is the subtle nuance of
language: when we have internalized a particular notion we generally
assume that notion **is** what the concept means, even though a more
rigorous understanding would recognize that the notion is merely what
the concept means **to us**. It is exactly this implicit acceptance of
“what identity means” that makes it so hard to communicate with people
who have internalized a different notion of identity. The different
purposes we have for these identity processes and assets - why we use
identity in the first place - shapes our internal mental models, which
in turn shapes the conversations we engage in and the kinds of solutions
we build.

While these different mental models are orthogonal and distinct, we
believe that they are all, in fact, valid notions for identity. By
recognizing these “alternative” mental models, people will be able to
communicate more clearly and collaborate more effectively to build
identity systems that resolve the identity needs of all relevant
stakeholders.

Identity
========

In this paper we use the definition of functional identity [15] when
we refer to “identity”. As a consequence, “identity” is how we
**recognize**, **remember**, and **respond** to specific people and
things. The processes of identity system*s acquire, correlate, apply,
reason over,* and *govern* the information assets of *subjects,
identifiers, attributes, raw data,* and *context*. If a system
**recognizes**, **remembers**, or **responds** to specific people or
things, it is using identity in some form - even if those identities are
neither linked to traditional identifying information such as names and
addresses, nor represented in official documents like a birth
certificate or passport.

This paper addresses the search for a notionally objective “truth” of
the identity of a specific person or thing. Recognition of a subject
depends on evaluating available evidence in search of that truth. The
evidence may be flawed and the interpretation may be flawed, but the
fundamental goal of each mental model is to answer truthfully its core
question. We may not be able to determine that objective truth with 100%
certainty, but we must try. Every identity system attempts to resolve
the question of truth to its best ability based on the fundamental needs
of its stakeholders.

We distinguish essential truth of an identity from the means, quality,
and confidence of the subjective conclusion derived from the available
evidence. The question we are seeking to answer in this paper is the
following: *“When we are evaluating the evidence, what are we trying to
determine?”*. Each mental model approaches this differently.

Five Mental Models
==================

Each mental model takes a different approach to recognizing,
remembering, and responding to the “Who”. How do you determine
uniqueness? How do you recognize a candidate individual? How do you
record and correlate your observations about a subject? How do you
correlate external assertions to subjects? And how do you apply that
knowledge in interactions with the subject or with others? Answers to
these questions vary not just based on different technologies and
techniques, bust also based on the mental model brought to bear on the
question of identity.

Technical solutions optimized for different mental models answer
different questions of identity. Failing to account for these different
questions can lead to systems insufficient to the task, creating
end-user frustration and system insecurities.

The models we have identified may not be the complete set, and the
language we have used here may not be the best “canonical” definition.
However, these models capture the breadth of conversations we have seen
over time among and between identity professionals and laypeople.

Space-time
----------

The space-time mental model sees identity as resolving the question of
the physical continuity of an entity through space and time.

***Does the physical body under evaluation have a continuous link
through space and time to a known entity?***

This is the dominant perspective in real-world security and is advocated
by many for online security.

The space-time mental model is necessary when enforcement targets the
physical body. We put bodies in jail. We keep bodies out of restricted
areas and off airplanes. If we are going to restrict the liberty of,
apply harm to, or even protect a person, it is vital to know the target
is in fact the right physical body, based on its literal physical
continuity through space and time with the physical body we intend to
restrict, harm, or protect.

**Presentation**
----------------

The presentation mental model sees identity as how we present ourselves
to society. This is the mental model behind Vendor Relationship
Management [16], user-centric identity, and self-sovereign identity.

***Is this how the subject chooses to be known?***

Whether you are gay, a Republican, or a gay Republican, it is your
choice how you present yourself to the world. This mental model sees
individually expressed identity as fundamental to privacy,
self-determination, free speech, and a free society. Adherents advocate
for technical and regulatory systems that allow people to fulfill their
own self-actualization, to become who they want to be, rather than
simply playing a role assigned by someone else.

Attribute
---------

The attribute mental model sees identity as the set of attributes
related to an entity as recorded in a specific system. Enshrined in
ISO/IEC 24760-1, an international standard for identity management, this
mental model is the primary focus for many engineers.

***Who is this data about?***

ISO/IEC 24760-1 limits the model of identity to correlated data within a
single system, making such systems simpler and easier to build. It draws
a bright line for engineers to focus on the accepted facts and
information within the system they are developing, insofar as that data
are related to specific individuals or entities.

This model ignores the consequences of common identification across
different systems for the sake of simplicity and feature management. It
also ignores how that data came to be, what is done with it, and how it
is governed. In effect, it focuses on the bits and bytes and not on the
processes involved. It is the simplest model for engineering a system;
in part, because of that, it is the only mental model that has a formal
definition as an international standard.

**Relationship**
----------------

The relationship mental model sees identity emerging through
interactions and relationships with others. Our identity is not about
what we are in isolation from others, but is rather defined by the
relationships we have. This is the fundamental model in the South
African idea of “Ubuntu”, meaning “I am because we are.”

***How is this person related?***

We are our children’s parents. Our teachers’ students. Our ex-spouse’s
ex-husband. We are the guy who helped a friend move, the kind neighbor
who let a friend borrow a cup of sugar, the jerk in 4th grade who kept
pulling a girl’s pigtails.

Or as Senator McCarthy famously asked *“Are you now, or have you ever
been, a member of the communist party?*” [17] The relationship of
membership in the communist party was used by McCarthy to argue that
individuals were enemies of the state.

Our appearance changes. Our age changes. Our height and weight change.
Every cell in our body goes through a life cycle of birth, life, and
death. We literally are not the same set of physical cells we were just
a year ago. Presumed static traits often aren’t.

However, relationships often hold true across contexts when our physical
traits do not. Relationships are given and earned through interactions
with others, never to be fully perceived by any one observer, never to
be fully known or captured at any point in time. The relationship mental
model is the mental model that most directly embraces the fundamental
fluidity of identity, rejecting the objective assessment of static,
categorical identity for the emergent societal bonds that define us
within our communities.

**Capability**
--------------

The capability mental model pragmatically defines identity in terms of
an individual’s actual capability to perform some task, including their
physical ability now, in the past, or in the future. It is the
inevitable approach for anyone in an emergency.

***What can a subject actually do?***

Capabilities combine both the ability and the will to execute. The
question of an identity’s capability is truly a test of one’s
willingness and ability to take action.

Sometimes what you really need is a pilot[18]. It does not matter if
they are licensed or if they physically have a license. What matters is
whether or not they can safely land that plane. If they can, that’s a
defining element of who they are, just as much as if they can’t.

You are a killer if you can actually pull the trigger when faced with a
situation that demands it. In theory, anyone in good health is able to
physically pull a trigger, but not everyone can actually do it when it
needs to be done. If you are capable of doing so, this very capability
defines part of who you are.

To spend bitcoin, you must be able to generate the correct ScriptSig
[19], one that returns TRUE when evaluated against the scriptPubkey
[20] of an input transaction. Bitcoin doesn’t care what your name is
or what is recorded in some database. If you can post a transaction that
produces the right output, you can spend the coins.

Included in this mental model are demonstrable physical traits, such as
the test for being “At least this tall” to ride a roller coaster. It
also includes historically recognized abilities even though they may no
longer apply, e.g., “She’s a murderer,” as well as speculation of future
capability “He’ll never last, he’s a quitter.” Ultimately, you can only
truly know a capability by testing it, and that test may prove valid
only in a highly specific context, like “I didn’t know I could do it,
but when I saw my child in harms way, I had to stop that car.”

Intersections of mental models: Patterns and Pitfalls
=====================================================

When two people discuss identity with different mental models, the
conversation inevitably focuses on the intersection between those
models, sometimes without either party realizing they are coming from
different perspectives.

In the classic science fiction story *Flatland: A Romance of Many
Dimensions* by Edwin Abbot [21], the author uses a fictional world to
explain how two-dimensional creatures would perceive three-dimensional
objects as they travel through the plane of their two-dimensional world.
The hero of the story realizes that these objects are, in fact, three
dimensional, and struggles to explain his insight to his fellow
two-dimensional beings. While they all think he is crazy, the hero
eventually prevails. The romance is in the hero’s struggle.

If we think of our mental models as two-dimensional planes, and accept
that most of us approach identity from a single perspective, then we can
consider how the intersection of these planes shape conversations. The
intersection of two planes is a line, which in both planes and, in our
metaphor, is fully understandable from within each model’s
two-dimensional context. That is, people speaking from each mental model
can fully perceive, understand, and discuss the line. In contrast, they
would each struggle to understand concepts outside their mental model,
just as people living in a single plane would struggle to understand the
idea of things outside that plane.

The following sections provide a few examples of intersections between
mental models.

Intersection between Space-time and Attribute
---------------------------------------------

When space-time-minded people discuss identity with attribute-minded
people, the conversation often leads to two key questions:

-   *“What are the minimum attributes to identify a particular (physical) individual?”, and *

-   *“Given the data we have, how can we identify particular individuals?”*

Because all modern information systems rely on data, it is inevitable
that space-time-minded applications intersect with the attribute mental
model. In naive implementations, this can lead to oversampling in an
attempt to increase certainty about a physical person, often referred to
as surveillance. If you record all the data possible about every
observable interaction throughout an individual’s day, you can
dramatically increase the likelihood that the system will correctly
identify that the person from the start of the day is actually,
physically the same person at the end of the day. If prison records the
actions of a prisoner 24 hours/day, 7 days/week, the prison can be
assured that the physical body being imprisoned has not escaped the cell
without their knowledge.

This intersection can also lead to overconfidence in the conclusions
about a physical person based on attributes stored in a database,
occasionally referred to as the “Tyranny of data”. Humorous consequences
can be seen in fiction when an official record indicates someone is
dead, when clearly they are not. Less humorous consequences occur, for
example, when subsidies people need to live are denied as a result of
errors in the Aadhaar identity service [22].

Intersection between Capability and Relationship
------------------------------------------------

Capabilities and relationship mental models intersect when a capability
implies a relationship or vice versa.

For example, US military academies offer guaranteed admission for
children of Congressional Medal of Honor recipients, the nation’s
highest honor. The reasoning is that, whether genetic or cultural, the
child of a Medal of Honor winner has at least as high potential to
become an outstanding officer as candidates vetted by congressional
representatives (the primary route for admissions).

We also see this in caste systems, including in European aristocracy and
Indian society. The presumption is that your familial relationships are
suitable indicators of your ability to perform certain societal roles.

As a mythical example, King Arthur’s ability to remove the sword from
the stone proved his lineage and right to govern the kingdom. His
capability re-established his relationship with the kingdom.

Intersection between Presentation and Relationship
--------------------------------------------------

An identity does not belong to one entity alone. It is built on the
perception the observer has of the subject, based on how the subject
presents themselves combined with other information. That information is
applied by the observer on their own judgment, which may change, distort
or recast the the presentation in non-obvious ways. While a subject may
present however they want, different observers will interpret those
presentations differently based on their relationship with the subject.
How you react when a friend or lover claims a privilege is often
different than if a rival or enemy claims the same.

As relationships move beyond bilateral interactions to societal
engagement, social norms dictate what information sharing is expected,
conventional, and allowed. Social agreements compel the disclosure of
certain data, such as giving a driver’s license to a law enforcement
officer or giving a passport to cross a border. They may also lead one
to take a topic out of civil discourse altogether; consider the quaint
but still relevant idea that it is rude to ask a woman about her age, a
man about his income, or a gender-neutral individual about their Y
chromosome. These social norms -- based on our relationships with others
-- shape a framework for presenting information that both enables and
restricts freedom of presentation [23].

Finally, self-asserting information may be enough for relying on certain
types of data (“this is my favorite food”), but not others (“I am not a
crook”). Many systems build trust or authority by involving other
parties, using systems of credentials to establish a sense of truth
based on the assertions of known actors. This information is projected
from the source, filtered and presented by the holder, and interpreted
through the lens of the relying party. This shared meaning is based on
multiple relationships and as such, is beyond the sole control of any of
these parties. The relationships enable and transform the presentations.
This is the architecture embodied in Verifiable Credentials [24] as
well as physical credentials such as driver’s licenses and passports.

Intersection between Presentation and Attribute
-----------------------------------------------

A persona represents, in data, information about a subject, as presented
by that subject to others. It is a subset of the information that a
subject could present, and independent of what the recipient may have
recorded about the subject. It is the attribute-centric vehicle for
presenting identity information. It is neither the totality of the
subject’s information, nor is it the only data known about them.

An individual may present different persona in different context,
sharing different information with different recipients or at different
times.

Self-asserted claims are fully in the intersection between presentation
and attributes. When an individual self-asserts a statement about
themselves, they are presenting an attribute on their own authority.

Intersection between Attribute and Relationship
-----------------------------------------------

We all interpret data differently based on the relationship we have with
its source. If one of our siblings tells us something, we take it
differently than if our parent tells us the same thing. A teacher
informing us about our children’s performance is perceived differently
than that a child’s self-reported assertion.

Moreover, social constructs shape the way entities deal with matters of
fact*.* The way to handle time, for example, differs tremendously
depending on where you originally come from. While several calendars
exist around the world, a person’s date of birth is a matter of fact. A
person is born at a specific moment in time. Nevertheless, the way to
construct and attribute this moment in time as a birth date is a social
construct. How we record and interpret that moment in time depends on
the social context of those recording it.

It is often assumed that entities with similar attributes are likely to
establish relationships, i.e., “birds of a feather flock together”.
Dating or matchmaking services often try to create relationships between
individuals based on their affinity as measured by their common
attributes. Of course, such matchmaking ignores the equally resonant
wisdom that “opposites attract”. Both, however, are examples where
attributes are used to evaluate the quality of a potential relationship.

Data analytics do something similar when evaluating known attributes of
individuals to seek out patterns and relationships. Sometimes this data
is used to infer a common group dynamic related to life events (a belief
the subject is pregnant) and buying patterns (the subject is likely to
buy a car) or even explicit relationships (the subject is a supporter or
member of a terrorist organization).

In short, one can use attributes to infer relationships (and vice-versa)
and relationships affect our interpretation of attributes.

Recommendation and Conclusion
=============================

When collaborating with others, consider multiple mental models for
better communication and better identity systems.

Whatever your own goals, we believe you are more likely to achieve them
if you can communicate clearly in terms others understand and can
incorporate the needs of others into your own work.

None of us have a complete picture of the universe. None of us have a
monopoly on the truth. The best identity solutions will come from a
frank and open engagement where every individual’s, and every
organization’s, needs are heard and considered. Implementations will
necessarily be a collection of trade-offs between security and freedom,
features and costs, and the needs of those building the systems and the
needs of those using them. We believe the best way to build the most
effective systems is to thoroughly understand where your collaborators
are coming from and what they need from identity and then to work
together to devise mechanisms that best achieve the common goals of all
stakeholders.

In short, be excellent to each other. Be open to new ideas and seek
first to understand, then incorporate the perspectives of others. What
might seem “wrong” at first hearing may turn out to be a vital component
simply unperceivable from your own initial mental model. Working
together is our best chance at getting it right.

References 
===========

[1]  “Internet Identity Workshop”, [*https://internetidentityworkshop.com*](https://internetidentityworkshop.com) (Accessed March 23, 2019)

[2]  “Rebooting the Web of Trust”, [*http://weboftrust.info*](http://weboftrust.info) (Accessed March 23, 2019)

[3]  “ID2020”, [*https://id2020.org/*](https://id2020.org/) (Accessed March 23, 2019)

[4]  “European Identity & Cloud Conference”, [*https://www.kuppingercole.com/events/eic2019*](https://www.kuppingercole.com/events/eic2019) (Accessed March 23, 2019)

[5]  “World Wide Web Consortium”, [*https://www.w3.org/*](https://www.w3.org/) (Accessed March 23, 2019)

[6]  “Internet Engineering Task Force”, [*https://www.ietf.org/*](https://www.ietf.org/) (Accessed March 23, 2019)

[7]  “Kantara Initiative”, [*https://kantarainitiative.org/*](https://kantarainitiative.org/) (Accessed March 23, 2019)

[8]  “International Organization for Standardization”, [*https://www.iso.org/home.html*](https://www.iso.org/home.html) (Accessed March 23, 2019)

[9]  “Rebooting the Web of Trust V”, [*https://github.com/WebOfTrustInfo/rwot5-boston*](https://github.com/WebOfTrustInfo/rwot5-boston) (Accessed March 23, 2019)

[10] “Internet Identity Workshop 25”, PDF of Proceedings, [*https://github.com/windley/IIW\_homepage/raw/gh-pages/assets/proceedings/IIWXXV\_Book\_of\_Proceedings.pdf*](https://github.com/windley/IIW_homepage/raw/gh-pages/assets/proceedings/IIWXXV_Book_of_Proceedings.pdf) (Accessed March 23, 2019)

[11] “Five Mental Models of Identity ”, [*https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/topics-and-advance-readings/five-mental-models-of-identity.md*](https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/topics-and-advance-readings/five-mental-models-of-identity.md) (Accessed March 23, 2019)

[12] “Rebooting the Web of Trust VII”, [*https://github.com/WebOfTrustInfo/rwot7-toronto*](https://github.com/WebOfTrustInfo/rwot7-toronto) (Accessed March 23, 2019)

[13] “International Identity Summit”, [*http://depts.washington.edu/uwconf/wordpress/idsummit/*](http://depts.washington.edu/uwconf/wordpress/idsummit/) (Accessed March 23, 2019)

[14] “What are mental models”, [*http://mentalmodels.princeton.edu/about/what-are-mental-models/*](http://mentalmodels.princeton.edu/about/what-are-mental-models/) (Accessed January 24, 2019).

[15] “A Primer on Functional Identity”, [*https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/topics-and-advance-readings/functional-identity-primer.md*](https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/topics-and-advance-readings/functional-identity-primer.md) (Accessed March 21, 2019)

[16] “Vendor Relationship Management”, [*https://en.wikipedia.org/wiki/Vendor\_relationship\_management*](https://en.wikipedia.org/wiki/Vendor_relationship_management) (Accessed March 21, 2019)

[17] “Joseph McCarthy”, [*https://en.wikipedia.org/wiki/Joseph\_McCarthy*](https://en.wikipedia.org/wiki/Joseph_McCarthy) (Accessed March 21, 2019)

[18] *Airplane.* Clip from YouTube [*https://www.youtube.com/watch?v=KSQyW\_l8OgE*](https://www.youtube.com/watch?v=KSQyW_l8OgE) (Accessed March 23, 2019)

[19] “Signature Script, ScriptSig”, [*https://bitcoin.org/en/glossary/signature-script*](https://bitcoin.org/en/glossary/signature-script) (Accessed March 21, 2019)

[20] “Pubkey Script, ScriptPubKey”, [*https://bitcoin.org/en/glossary/pubkey-script*](https://bitcoin.org/en/glossary/pubkey-script) (Accessed March 21, 2019)

[21] “FLATLAND: A Romance of Many Dimensions”, [*https://ned.ipac.caltech.edu/level5/Abbott/paper.pdf*](https://ned.ipac.caltech.edu/level5/Abbott/paper.pdf) (Accessed March 21, 2019)

[22] “Unique Identification Authority of India”, [*https://uidai.gov.in/*](https://uidai.gov.in/) (Accessed March 21, 2019)

[23] “Overton window” [*https://en.wikipedia.org/wiki/Overton\_window*](https://en.wikipedia.org/wiki/Overton_window) (Accessed March 21, 2019)

[24] “Verifiable Credentials Data Model 1.0”, [*https://w3c.github.io/vc-data-model/*](https://w3c.github.io/vc-data-model/) (Accessed March 21, 2019)


