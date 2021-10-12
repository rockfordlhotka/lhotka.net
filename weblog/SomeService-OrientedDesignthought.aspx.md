---
title: Some Service-Oriented Design thought
postDate: 2005-05-24T10:02:10.421875-05:00
abstract: More people are starting to think about service oriented design (rather than architecture or programming) and that is a welcome thing!
postStatus: publish
---
24 May 2005

It is clear to me that Service Oriented *Architecture*has gone about as far as it can go in a vacuum. And Service Oriented *Programming* continues to evolve somewhat randomly as vendors and/or standards bodies see fit (WSE, Indigo, etc).<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p>

<o:p>&nbsp;</o:p>

So there needs to be more rigorous thought apply to Service Oriented *Design*. If we assume the SOA concepts of autonomous entities communicating via contract-defined messages over negotiated channels. And if we assume we’ll have programming tools that provide contractual synchronous and asynchronous communication vectors, then we can move ahead and work on thought models for designing services and systems composed of services.<o:p></o:p>

<o:p>&nbsp;</o:p>

Note that there are two very different aspects here. One is how to create a service, the other is now to build systems where services interact. The inside view and the outside view. And the rules and concepts are very different for each.<o:p></o:p>

<o:p>&nbsp;</o:p>

In that vein, here's a good/interesting [article on SO design](http://blogs.msdn.com/richardt/archive/2005/05/20/420650.aspx) from Rich Turner at Microsoft. He’s taking the inside view and discussing some high-level design concepts for how you might build an autonomous service that still requires other services to function. He’s proposing a couple thought models that might be useful in design efforts – exactly the kind of dialog that is required to move SOD forward.<o:p></o:p>

<o:p>&nbsp;</o:p>

Personally I think that a number of the object-oriented design concepts behind CRC cards (class, responsibility, collaboration) apply equally well to services. In such a scheme, Rich’s relationships (constellation or fractal) would be listed as collaborators from a service.<o:p></o:p>

<o:p>&nbsp;</o:p>

I’m convinced that at least the first side of a CRC card, where the class (now service), responsibility and list of collaborators (other services) are a good design tool for services. Some of the other sides (like the list of behaviors) aren’t so useful, since a service is an atomic procedure and thus by definition has exactly one behavior. Still, applying those parts of CRC that do work is very helpful.<o:p></o:p>
