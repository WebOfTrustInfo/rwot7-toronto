# The Political Economy of Naming - RWoT Fall 2018

Kate Sills

kate@agoric.com

## Introduction

*This piece builds on discussions about petnames with Mark S. Miller, Christopher Lemmer Webber, and others during the 2018 Santa Barbara RWoT.*

Unique identifiers (such as public keys and public key hashes) are often not human readable. The lack of human readable names creates significant usability problems. Petname systems have been proposed as a solution.  

Petnames are names that are "secure, memorable, and private to the individual who refers to another entity... True petnames are 2-way associative: given a petname in a specific application on a specific machine, you can acquire the key, and given the key, you can acquire the petname. The mapping back from the key to the petname is always performed when presenting data to the user". ([Stiegler](#Stiegler)) The address book in a cell phone is an example of petnames mapping to phone numbers. 

Nick Szabo has observed that namespaces and "all such agreements of control, including control over the semantics of symbols, to be made and respected across trust boundaries are problems of agreeing on and maintaining property rights” ([Szabo](#Szabo)). This paper explores the extent to which this statement is true. Can naming be fully decentralized? Should it be? When is naming a matter of property rights?

## Centralized and Decentralized Names

Many of the naming systems that we are familiar with, such as DNS, are centralized and top-down. We cannot easily change a website’s name to our own personal choice, nor can we easily coordinate with others to change a website’s name within a group. 

On one end of the spectrum, address books in cell phones are completely decentralized. Users can put in whatever name they want for each phone number, and users can send each other the mappings (i.e. Alice can tell Bob that a certain phone number is "Carol’s Cell"). Importantly, there is no centralized canonical list of petnames for each phone number (outside of physical address books, that is.)

Advocates of decentralization may assume that complete decentralization in naming (i.e. each petname comes from an individual’s collection) is the ideal. However, this paper will argue that the ideal naming system uses bottom-up centralization, defined as individual entities voluntarily coordinating on intermediate naming hubs, while still retaining the option of switching to another hub dynamically. 

## Top-down Centralization

Currently, domain names pass the "moving bus test": “if you see the name on the side of a bus as it drives past you, you should be able to remember the name long enough to use it when you get home” (Stiegler). This is very useful when the method of transmission is offline - through physical advertisements or word of mouth. However, because the name is global in nature, domain names are often already bought, and disputes are common. Buying a domain name takes away the opportunity to use that name from every person in the world. This seems unnecessary.

Domain names have what are called “top-level domains” such as “.com,” “.org” and country extensions. Extensions help by creating new namespaces, but they are centrally determined and poorly organized. For example, the “.com” extension no longer means company, and is used for many things.

## Bottom-up Centralization

By contrast, we can imagine a system that starts with completely decentralized petnames for websites. We can ask our contacts to voluntarily share their petnames. As this process evolves, certain collections may become more popular. For instance, an entity such as Consumer Reports could have a generally trusted collection of petnames. We shall call these popular petname collections “naming hubs,” due to the tendency of petname routing to pass through them. 

This kind of centralization is very different than the DNS-style top-down centralization. With bottom-up centralization, end-users can easily change their petname routing to go through alternative entities, allowing for innovation and placing a check on the power of any particular naming hub. To keep their power, naming hubs must be better than any alternative, which is not true in the case of top-down centralization. Furthermore, the hub can use many different methods of arriving at the mappings - everything from voting protocols among a community to an individual’s decisions to randomness, giving a wide variety of options.

## Conclusion

There are obvious benefits of coordination in petnames, such as being able to share a petname offline and having the recipient know what you mean. However, coordination can occur without centralization, as shown by languages. Even without dictionaries, people have been able to understand each other, perhaps not perfectly, but well enough to communicate. In bottom-up centralization, coordination crosses trust boundaries, yet, because there is no one canonical central mapping, property rights are not an issue. It is only when there is a single canonical mapping that people are forced to reconcile their differences, whether they want to or not. Thus, Szabo is wrong to lump naming systems into issues of property rights. 

## Remaining questions

Future research is needed to show that decentralized naming is efficient enough to be usable. However, with the increased use of computer agents, a name being memorable may not be as much of a constraint as it currently is. 

## Works Cited

<a id="Stiegler"></a>[Stiegler][http://www.skyhunter.com/marcs/petnames/IntroPetNames.html]

<a id="Szabo"></a>[Szabo] [https://nakamotoinstitute.org/secure-property-titles/#selection-235.24-235.131]

