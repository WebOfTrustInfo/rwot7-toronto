# Five Mental Models of Identity
By Joe Andrieu, Legendary Requirements, joe@legreq.com

**Security**. **Liberty**. **Data**. **Relationship**. **Capability**.

Identity is how we recognize, remember, and respond to specific people and things. Identity systems acquire, correlate, apply, reason over, and govern information assets of subjects, identifiers, attributes, raw data, and context. That’s the functional approach to identity.

How we think about these processes and assets is driven by why we use identity in the first place; our primary uses of identity shape our internal mental models, which in turn shape the kinds of solutions we build. Differing priorities and perspectives also make it challenging to discuss identity with people speaking from alternate mental models.

We’ve identified five distinct mental models for identity, each with its own framing, its own purpose, and its own defining question. These are five valid, independent mental models of identity. By understanding them, we can better understand how apparently disjoint ideas of identity relate to each other, enabling the discussion and engineering of better, more broadly useful identity systems. 

## Security
The security mental model sees identity as resolving the question of the physical individual. This is the dominant perspective in real-world security and advocated by many for online security.

**Is this physical body the person you think it is?**

The security mental model is necessary when enforcement targets the physical body. We put bodies in jail. We keep bodies out of restricted areas and off air planes. If we are going to restrict the liberty of, apply harm to, or even protect a person, it is vital to know the target is in fact the right physical body.

## Liberty

The liberty mental model sees identity as how we present ourselves to society. This is the mental model behind Vendor Relationship Management, user-centric identity, and self-sovereign identity.

**Is this how I want to be known?**

Whether you are gay, a Republican, or a gay Republican, it is your choice how you present yourself to the world. This mental model sees individually expressed identity as fundamental to privacy, self-determination, self-expression, and a free society. Adherents advocate for technical and regulatory systems that allow people to fulfill their own self-actualization, to become who they want to be, rather than simply playing a role assigned by someone else.

## Data
The data mental model sees identity as the set of attributes related to an entity. Enshrined in ISO/IEC 24760-1, an international standard for identity management, this mental model is the primary focus for many engineers.

**Is this data about a particular entity?**

Limiting the model of identity to related data, in a single system, makes it easier to build. It draws a bright line for engineers to focus on the accepted facts and information within the system they are developing. This model ignores the consequences of common identification across different systems for the sake of simplicity and feature management. It is the simplest model for engineering a system and, in part because of that, it is the only mental model that has a formal definition as an international standard.

## Relationship

The relationship mental model sees identity emerging through our interactions with others. It is the fundamental model in the South African idea of “Ubuntu,” meaning “I am because we are.”

**How is this person related to others?**

People change. Young whippersnappers become caring parents. Strangers become friends. Spies become traitors. The relationship mental model embraces change as core to how identity manifests in the world. Notions of “who somebody is” change as people learn and grow; what holds coherence over time and context is our relationships, given and earned through interactions with others, never to be fully perceived by any one observer, never to be fully known or capture at any point in time. The relationship mental model is the only mental model that explicitly embraces the fundamental fluidity of identity, rejecting the objective assessment of static, categorical identity for the emergent societal bonds that define us within our communities.

## Capability

The capability mental model pragmatically defines identity in terms of an individual’s actual ability to perform some task. It is the inevitable approach for anyone in an emergency and core to the Object Capabilities security model.

**What can this person actually do?**

Sometimes, what you need is an actual doctor. You are a reader if, and only if, you can actually read. You’re a killer if you can actually pull the trigger. Not everyone can do it, but if you can, the very capability defines part of who you are. Sometimes this notion is applied predictively, modeling future behavior based on belief in capability. Other times it is used descriptively, deriving assertions of capability from evidence. It may also be applied functionally—where the functional capability enables specific privileges. For example, “All lifeguards MUST be able to swim 300 yards continuously.” Fail the test, you don’t get to be a lifeguard. In the Object Capabilities model, authorization is managed by creating, sharing, attenuating, and using “capabilities” instead of, for example, access control lists. If you have a valid “capability”, you have the authorization. Like a car key, Object Capabilities may be used no matter who you are. This model shifts the burden of identification from error-prone correlations to directly work with individuals’ actual capabilities.

