# Models of Identity

Joe Andrieu *Legendary Requirements* \<joe@legreq.com\>  
Nathan George *Sovrin Foundation* \<nathan@sovrin.org\>  
Christophe Macintosh *Clearmatics* \<cm@clearmatics.com\>  
Ouri Poupko *Weizmann institute* \<ouri.poupko@weizmann.ac.il\>  
Antoine Rondelet *Clearmatics* \<ar@clearmatics.com\>  
Andrew Hughes

## Abstract

Identity systems, both digital and in the non-digital world, rely upon use case assumptions and requirements that can lead to very different conclusions about the definition, shape and solutions for solving the “problem of identity”.  Considering different models for handling identity information allows reconciliation, and creates opportunities to address primary use cases across paradigms, increasing overall strength and security of a solution.  Considering multiple models also reveals general pitfalls and general structural problems that help improve the state of the art of available solutions.

Identity is how we recognize, remember, and respond to specific people and things. Identity systems acquire, correlate, apply, reason over, and govern information assets of subjects, identifiers, attributes, raw data, and context. That’s the functional approach to identity.
How we think about these processes and assets is driven by why we use identity in the first place; our primary uses of identity shape our internal mental models, which in turn shape the kinds of solutions we build. Differing priorities and perspectives also make it challenging to discuss identity with people speaking from alternate mental models.
We’ve identified five distinct mental models for identity, each with its own framing, its own purpose, and its own defining question. These are five valid, independent mental models of identity. By understanding them, we can better understand how apparently disjoint ideas of identity relate to each other, enabling the discussion and engineering of better, more broadly useful identity systems.
Identity can be use for any entity, but for our discussion, we focus on human identity.

What we’re addressing in this paper is the objective truth of identity. Recognition of a person depends on discerning that truth using available evidence. The evidence may be flawed or  the interpretation may be flawed, but the fundamental goal is to determine the truth. It’s useful to distinguish between essential truth of an identity from the means, quality, and confidence of the subjective conclusion derived from that evidence. In other words, the question we are seeking to answer in this paper is, when we are evaluating the evidence, what are we trying to determine? Each mental model approaches this differently. In effect, each mental model asks a distinct question.
When translated to technology, this means that technical solutions optimized for different mental models enable answering different questions for identity. Failing to account for the different questions that can be asked can lead to systems insufficient to the task, leading to frustration and even system insecurities.
Throughout our discussion, we will occasionally use the metaphor of Theseus’s Ship.

## Background
Outline:
- Introductions to models of identity (we think about this different ways)
    - What are the problems that we are trying to solve?
        - The models have interconnectedness that a single model doesn’t address alone -- how do we think about the intersections to reconcile between models.


## Five Mental Models

### Continuity  (Security - is this the same physical entity over time?)

The continuity mental model sees identity as resolving the question of the physical continuity of an entity, especially an individual. This is the dominant perspective in real-world security and advocated by many for online security.

**Does this physical body have continuity s the same one?**

The continuity mental model is necessary when enforcement targets the physical body. We put bodies in jail. We keep bodies out of restricted areas and off air planes. If we are going to restrict the liberty of, apply harm to, or even protect a person, it is vital to know the target is in fact the right physical body.
When you need to find a physical entity that does not want to be found resolving to physical continuity is often used to bypass the entities incentive not to disclose information, physical continuity may be used to establish the identity of the entity through external observation.
Theseus.

### Liberty (Presentation, self-representation or ability to chose when to assert/present/disclose?)

The liberty mental model sees identity as how we present ourselves to society. This is the mental model behind Vendor Relationship Management, user-centric identity, and self-sovereign identity.

**Is this how I want to be known?**

Whether you are gay, a Republican, or a gay Republican, it is your choice how you present yourself to the world. This mental model sees individually expressed identity as fundamental to privacy, self-determination, self-expression, and a free society. Adherents advocate for technical and regulatory systems that allow people to fulfill their own self-actualization, to become who they want to be, rather than simply playing a role assigned by someone else.

### Data (Attribute)

The data mental model sees identity as the set of attributes related to an entity. Enshrined in ISO/IEC 24760-1, an international standard for identity management, this mental model is the primary focus for many engineers.
Is this data about a particular entity?
Limiting the model of identity to related data, in a single system, makes it easier to build. It draws a bright line for engineers to focus on the accepted facts and information within the system they are developing. This model ignores the consequences of common identification across different systems for the sake of simplicity and feature management. It is the simplest model for engineering a system and, in part because of that, it is the only mental model that has a formal definition as an international standard.

### Relationship (Context)

The relationship mental model sees identity emerging through our interactions with others. It is the fundamental model in the South African idea of “Ubuntu,” meaning “I am because we are.”

**How is this person related to others?**

People change. Young whippersnappers become caring parents. Strangers become friends. Spies become traitors. The relationship mental model embraces change as core to how identity manifests in the world. Notions of “who somebody is” change as people learn and grow; what holds coherence over time and context is our relationships, given and earned through interactions with others, never to be fully perceived by any one observer, never to be fully known or capture at any point in time. The relationship mental model is the only mental model that explicitly embraces the fundamental fluidity of identity, rejecting the objective assessment of static, categorical identity for the emergent societal bonds that define us within our communities.

### Capability (Ability)

The capability mental model pragmatically defines identity in terms of an individual’s actual ability to perform some task. It is the inevitable approach for anyone in an emergency.

**What can this person actually do?**

Sometimes, what you need is an actual doctor. You are a reader if, and only if, you can actually read. You’re a killer if you can actually pull the trigger. Not everyone can do it, but if you can, the very capability defines part of who you are. Sometimes this notion is applied predictively, modeling future behavior based on belief in capability. Other times it is used descriptively, deriving assertions of capability from evidence. It may also be applied functionally—where the functional capability enables specific privileges. For example, “All lifeguards MUST be able to swim 300 yards continuously.” Fail the test, you don’t get to be a lifeguard. In the Object Capabilities model, authorization is managed by creating, sharing, attenuating, and using “capabilities” instead of, for example, access control lists. If you have a valid “capability”, you have the authorization. Like a car key, Object Capabilities may be used no matter who you are. This model shifts the burden of identification from error-prone correlations to directly work with individuals’ actual capabilities.

**Note:**
Disability (Independent section or extension of Capability ?)
Disability is inspired from capability.
Given a system, what can you do ?
Example: Puzzle e-mails

## Intersections and Pitfalls

For reference:

- Ideas and outlines of Pitfalls
- Pitfalls and Specific Guidance:
    - Security/Corporeal security alongside liberty
    - Correlation and security concerns around corporal data
    - Leakiness of unique identifiers (EMPI systems and challenges of 99% unique person:identifier issues)
    - Relational identity and reputation
    - Leakiness of the “data” view - “metadata is data too”
    - Contextuality of data for liberty and security
    - Game theory of credentials and ontology over time
        - “Yellow star” systems
        - Checks and balances trump principles for governance over time

When two people come to identity with different mental models, the conversation starts, and is often limited to, the intersection between those two models.

In the classic science fiction story [**Flatland:A Romance of Many Dimensions**][1] by Edwin Abbot, the author uses a fictional world to explain how two dimensional creatures would perceive three dimensional objects as they travel through the plane of their two dimensional world. The hero of the story realizes that these objects are, in fact, three dimensional, then struggles to explain his insight to his fellow two dimensional beings. They all think he’s crazy. Eventually he prevails, but the romance is in the hero’s struggle.

If we think of our mental models as two dimensional planes, and recognize that most of us approach identity from with these singular perspectives then we can consider how the intersection of these planes shape conversations. The intersection of two planes is a line, which is actually in both planes and, in our metaphor, fully understandable from within each plane’s two dimensional context. That is, people living in each plane can fully perceive, understand, and appreciate the line. In contrast, they would both struggle to understand concepts outside their planes.

In the next ten sections, we illustrate the ideas and projects of the models t driving their conversation, . When they engage with others whose mental model is different, the intersection of the two models can lead to limited, but fruitful conversations. Engineers and designers also often approach building systems from a particular model, which can create challenges when users have requirements or expectations from a different one. These intersections can inform us of interesting patterns, some which lead to unexpected problems, others which lead to common oversimplifications. Considering these intersections can give us insights for past, present, and future identity systems.

### Security and Data (Joe)

When security minded folks talk identity with data minded people, the conversation often leads to two key questions. First, “What are the minimum attributes to identify a particular (physical) individual?” Second, “Given the data we have, how can we identify particular individuals?” You may recognize these questions from your own conversations with others.

Because all modern information systems rely on data, it is inevitable that security-minded applications intersect with the data mental model. In naive implementations, this can lead to oversampling in an attempt to increase certainty about a physical person: if you record all the data possible about every observable interaction throughout an individual’s day, you can dramatically increase the likelihood that the system can correctly identify the person from the start of the day is physically the same person at the end of the day. If you watch the prisoner 24 hours/day, 7 days/week, you can, presumably, rest assured that the prisoner is not going to sneak out without your knowledge.

A naive security-driven approach could lead to over reliance on the certainty that a known physical person can be trusted.
Security and Liberty (Joe?)

### Security and Relationship

### Security and Capability

### Capability and Relationship (Antoine?)

The Capability and Relationship aspects of an identity are very intertwined. In fact, an identity’s capability can easily influence its relationships.
For instance, An example to this, are “puzzle/e-mails”, where an entity needs to find the solution of the puzzle in order to be able to know the location of the meeting/event. Here, we clearly see that, capability impacts relationships. If you are able to solve the puzzle, you can meet the people that were also able to solve the puzzle (ie: People having the the same capabilities as you), if you can’t, you won’t be able to establish these relationships.
On the other hand, Relationship impacts Capability. For instance, having ties/relationships with French improves your capability to speak French.

### Liberty and Relationship (Nathan)

Any identity does not belong to one entity alone.  It is the shared perception of the information presented by the choice of both parties and the information that each party perceives about the other.  Additionally the information presented may be interpreted as the other party sees fit, which may change, distort or recast the meaning or intent in ways that aren’t communicated between them.  This is a normal part of any human communication or interaction that is often obscured by digital intermediation.  This interpretive lens is based on the relationship of the parties and can evolve as the relationship evolves.

Relationships may also dictate what information sharing is expected, conventional or allowed.  We establish social constructs to compel the disclosure of data, such as giving official documents to a law enforcement officer or to cross a border.  This balance between collective good can exist at the level of a relationship, community, government or any other society.

Finally self-asserting information may be enough for trusting certain types of data (“this is my favorite food”), but not others (“I am not a crook”).  Most systems build trust or authority by involving other parties, using systems of credentials to establish truth from some other entity, which constrains the useful statements that can be made to the information that other entities are willing to issue or sign for your use.  This information is projected through the interpretation of the issuer, the holder of the credential willing to share the proof and again through the lens of the relying party verifying the data.  This shared meaning is based on multiple relationships and the meaning isn’t in the sole control of any of these parties.

### Liberty and Data (Antoine?)

The notion of persona encapsulates the aspect of your character that you presented to others. As a consequence, your persona is your “self” perceived by others.

In order to dive into this section, it is important to go back to the functional definition of an identity, and remember that, your identity here is about how you are known, and not who you are.
An entity might wish to be known differently depending on the context, which can lead into different sets of attributes related to this entity. Hence, there is a correlation between the Liberty and Data models of a same identity.
Being free to decide how one wants to be known, one can shape the image of his “self” stored and remembered by his counterparts.

In that sense, the Liberty model of an identity is empowering, and gives a decisional power and a power of influence to entities.

### Liberty and Capability (Nathan?)

Proof of capability is dependent on my willingness to perform the capability
What I can do is defined by others perception or satisfaction, so can one’s define their own capabilities?  Ontology of capability is different depending on purpose, language and context, this means that interpretation of what constitutes a capability can be relative and crossing boundaries with functional definitions of capabilities can be difficult
Choice or volution may in itself be a capability, if I can pull the trigger I am a killer, not being able to pull the trigger, lack of a capability, is also identity information.

### Data and Relationship (Antoine)

We all interpret data differently based on the relationship we have with its source. If our child tells us something, we hear it differently than if our parent tells us the same thing. A teacher informing us about our children’s performance is heard differently than that child’s self-reported assertion.

Moreover, social constructs shape the way entities deal with matters of facts. An example of social construct is the way to handle time. While several calendars exist around the world, a person’s date of birth is a matter of fact. This very person has been given birth at a very specific moment in time. Nevertheless, the way to actually construct and attribute this moment in time as a birth date to the entity is a social construct.

In the larger extent, entities’ attributes  - part of the Data mental model -  are affected by the social context of entities.

Social constructs, however, vary from one entity to another. Furthermore, every of your relation possess a different identity of you than your “self vision” of your identity.
Creating social links with entities is accepting to give the liberty to your counterpart to keep a version of your “self”. Doing so, empowers your counterpart who is able to detain your identity, that you just cannot control.
As follows, each of the counterpart you tie links with are free to hold and mutate their version of your identity, and hold data about your identity.

While relationship and social construct have an impact on data, we can also study the impact of data on relationships. It is often assumed that entities with similar attributes are likely to establish relationships.  Dating services, or matchmaking services for instance, try to create relationships between individuals, based on their affinity, which is often a function of their common attributes. Whilst these services assume that two people are similar if they share common data, this often leads to mixed results, as it does not capture the entire set of dimensions characterizing an identity.

### Data and Capability (change in meaning over time) (Christophe)

- Interesting intersection between Data and Capability mental models when trying to tackle the temporal aspect of an identity.
- An identity might have a capability at time t but lose this capability at time t + alpha or vice versa (gain capability over time it didn’t have at time t).
- How does this interact with the data mental model?
    - The data mental model sees identity as the set of attributes related to an entity.

- Is it right to store a negative capability in a data system?

- However, the loss of a capability can be so that the identity keeps some level of capability; but lost part of it (not all).
- This brings questions about the definition of “being capable of” in some circumstances. I can be able to run from A to B in less than 10s (let’s say 6 sec) at time t, but I might be able to run from A to B in less than 10s (let’s say in 9 sec) at time t+alpha.
- In this scenario, my capability “decays” because of my growing age for instance.
- However, I am still capable at time t+alpha, but I am “less capable” than I was at time t.

- I guess my question is: Do we want to define capability as a single bit of information (0: can’t, 1: can), or do we want to define it as a continuous interval [0, 1], which encapsulates different levels of capabilities.
- Another example would be: “I am able to pull the trigger (if I am being threatened by someone and have a gun on my head)”.
- Thus, to the question: “Are you capable to pull off the trigger ?”, my answer would be yes; but here the interlocutor misses the entire context, as it decides to measure the capability as a binary information, and I end up being classified as someone able to pull the trigger.
- However, I can be 0.4 capable to pull the trigger; which encapsulates part of the context given in my answer, and my capability is measured is a way that better reflect my answer.
- Thus, how do we measure information about an identity ? What does it mean to be capable ?

*Object Capabilities is, in fact, the intersection of ability and data models.*

## Recommendations and Considerations

**The message we want to let at the end of the paper:**
Most importantly, keep talking, keep thinking. We’re not done here.

- Therefore what? - Conclusions and next steps (come and help call to action)
- Do we want to open the discussion to non-human identities ?
I feel like the 5 mental models can be applicable to software or any kind of agents in the broader sense. Eg: “Relationship” → Agents in the same system as one other agent and the agents the one agent is communicating with; Capability → What the agent can do, Liberty → Different APIs to present the agent differently to other agents and to society. An identifier can be a hash of the code. The physicality (mentioned in the “security” paragraph of the 5 mental models) of a software agent can be the set of machines it is running on (the same way our body is “the machine” hosting our mind. There are two parallels here: 1) the machine <-> our body and, 2) The software <-> our mind).

- With their relationships, human share ideas and impact identities of others in the same way as a software can be uploaded into another machine and spread. Having the liberty to be known and perceive as you wish gives the possibility to the entity to “upload” a version of “self” in the other entities and to mutate.
- A software is a mutable entity which body expands and evolves across time.
- The ports of a machine constitute
- Software expands, key duplication (key management) => expansion of the body of the software, and increase of the attack surface.


[1]: https://en.wikipedia.org/wiki/Flatland
