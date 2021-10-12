---
title: Exactly what is blockchain?
postDate: 2017-04-07T11:02:32-05:00
abstract: 
postStatus: publish
---
07 April 2017

Trying to figure out the core "meat" behind blockchain is really difficult. I'm going to try and tease out all the hype, and all the references to specific use cases to get down to the *actual* technology at play here.

(this is my second blockchain post, in my previous post I [compare blockchain today to XML in the year 2000](http://www.lhotka.net/weblog/BlockchainIsTodayWhatXMLWasIn1998.aspx))

There are, of course, tons of articles about blockchain out there. Nearly all of them talk about the technology only in the context of specific use cases. Most commonly bitcoin and distributed ledgers.

But blockchain *the technology* is neither a currency nor a distributed ledger: it is a tool used to implement those two types of application or use case.

There's precious little content out there about the *technology* involved, at least at the level of the content you can find for things like SQL Server, MongoDb, and other types of data store. And the thing is, blockchain is basically just a specialized type of data store that offers a defined set of behaviors. Different in the specifics from the behaviors of a RDBMS or document database, but comparable at a conceptual level.

I suspect the lack of "consumable" technical information is because blockchain is very immature at the moment. Blockchain seems to be where RDBMS technology was around 1990. It exists, and  uber-geeks are playing with it, and lots of business people see $$$ in their future with it. But it will take years for the technology to settle down and become tractable for mainstream DBA or app dev people.

Today what you can find are discussions about extremely low-level mathematics, cryptography, and computer science. Which is fine, that's also what you find if you dig deep enough into Oracle's database, SQL Server, and lots of other building-block technologies on top of which nearly everything we do is created.

In other words, only hard-core database geeks really care about *how* blockchain is implemented - just like only hard-core geeks really care about how an RDBMS is implemented. Obviously we need a small number of people to live and breathe that deep technology, so the rest of us can build cool stuff *using* that technology.

So what *is* blockchain? From what I can gather, it is this: a distributed, immutable, persistent, append-only linked list.

Breaking that down a bit:

1. A linked list where each node contains data
2. Immutable
    1. Each new node is cryptographically linked to the previous node
    2. The list and the data in each node is therefore immutable, tampering breaks the cryptography
3. Append-only
    1. New nodes can be added to the list, though existing nodes can't be altered
4. Persistent
    1. Hence it is a data store - the list and nodes of data are persisted
5. Distributed
    1. Copies of the list exist on many physical devices/servers
    2. Failure of 1+ physical devices has no impact on the integrity of the data
    3. The physical devices form a type of networked cluster and work together
    4. New nodes are only appended to the list if some quorum of physical devices agree with the cryptography and validity of the node via consistent algorithms running on all devices
        1. This is why blockchain is often described as a "trusted third party", because the cluster is self-policing


Terminology-wise, where I say "node" you can read "block". And where I say "data" a lot of the literature uses the term "transaction" or "block of transactions". But from what I've been able to discover, the underlying technology at play here doesn't really care if each block contains "transactions" or other arbitrary blobs of data.

What we build on top of this technology then becomes the question. Thus far what we've seen are distributed ledgers for cryptocurrencies (e.g. bitcoin) and proof of concept ledgers for banking or other financial scenarios.

Maybe that's all this is good for - and if so it is clearly still very valuable. But I strongly suspect that, as a low level foundational technology, blockchain will ultimately be used for other things as well.

I'm also convinced that blockchain is almost at the top of the [hype cycle](https://en.wikipedia.org/wiki/Hype_cycle) and is about to take a big plunge as people figure out what it can and can't *actually* do.

Finally, I believe that blockchain, assuming there's money to be made in the technology, will become part of established platforms such as Azure, AWS, and GCP. And there might be some other niche players left, but the *majority* of the many, many blockchain tech providers out there today will ultimately be purchased by the big players or will just vanish.
