---
title: Not to keep harping on SOA, but really...
postDate: 2004-10-21T13:48:58.203125-05:00
abstract: The quote "services (and SOA) do not imply any distribution semantics" is highly disturbing...
postStatus: publish
---
21 October 2004

In the just published [Enterprise Architect magazine](http://enterprisearchitect.texterity.com/enterprisearchitect/2004fall/)is an article titled “SOA: Debunking 3 Common Myths”. The first and third myth I generally agree with. The second is problematic on several levels.<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p>

The myth in question is that SOA implies a distributed system. The author explains that SOA does *not* imply a distributed system, but rather is merely a message-based architecture of providers and consumers. So far I’m in agreement. SOA can be done in a single process. Whether that’s wise or not is another discussion, but it certainly can be done.<o:p></o:p>

Then the author goes on to suggest that a good architecture should include a Locator service so service providers can be moved to other machines if needed. Again, so far so good. This kind of flexibility is very important.<o:p></o:p>

But then we get my point of disgreement. The closing statement is that “services (and SOA) do not imply any distribution semantics”. Say what?<o:p></o:p>

If you are going to actually have the option of running a service on another machine, then you must design it to follow distributed semantics from day one. You must design it with course-grained, message-based interfaces. You must ensure that the service provider never trusts the service consumer and visa versa. You must ensure that there is no shared state between provider and consumer - including that they can't share a database or any other common resource.

In short, you must design the service provider and consumer with the *assumption* that they are running on separate machines. Then, having written them with distributed semantics, you can choose to collapse the physical deployment so they run in the same process on the same machine.<o:p></o:p>

Failure to view SOA as a distributed architecture is a big mistake. In SOA there’s the absolute implication that the provider and consumer may be distributed. Philosophically we are designing for a distributed scenario. The fact that we might *not* be distributed in some cases is immaterial. SOA means you *always* design using distribution semantics.
