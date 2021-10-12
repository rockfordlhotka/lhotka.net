---
title: Is Indigo compelling or boring?
postDate: 2005-04-18T23:13:06.109375-05:00
abstract: It all depends on your point of view…
postStatus: publish
---
18 April 2005

<font face="Times New Roman" color="#000000" size="3">Indigo is Microsoft’s code name for the technology that will bring together the functionality in today’s .NET Remoting, Enterprise Services, Web services (including WSE) and MSMQ. Of course knowing what it is doesn’t necessarily tell us whether it is cool, compelling and exciting … or rather boring.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Ultimately beauty is in the eye of the beholder. Certainly the Indigo team feels a great deal of pride in their work and they paint this as a very big and compelling technology.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Many technology experts I’ve talked to outside of Microsoft are less convinced that it is worth getting all excited.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Personally, I must confess that I find Indigo to be a bit frustrating. While it should provide some absolutely critical benefits, in my view it is merely laying the groundwork for the potential of something actually exciting to follow a few years later.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Why do I say this?</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Well, consider what Indigo is again. It is a technology that brings together a set of existing technologies. It provides a unified API model on top of a bunch of concepts and tools we already have. To put it another way, it lets us do what we can already do, but in a slightly more standardized manner.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">If you are a WSE user, Indigo will save you <i style="mso-bidi-font-style: normal">tons</i> of code. But that’s because WSE is experimental stuff and isn’t refined to the degree Remoting, Enterprise Services or Web services are. If you are using any of those technologies, Indigo won’t save you much (if any) code – it will just subtly alter the way you do the things you already do.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Looking at it this way, it doesn’t sound all that compelling really does it?</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But consider this. Today’s technologies are a mess. We have at least five different technologies for distributed communication (Remoting, ES, Web services, MSMQ and WSE). Each technology shines in different ways, so each is appropriate in different scenarios. This means that to be a competent .NET architect/designer you must know all five reasonably well. You need to know the strengths and weaknesses of each, and you must know how easy or hard they are to use and to potentially extend. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Worse, you can’t expect to easily switch between them. Several of these options are mutually exclusive.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But the final straw (in my mind) is this: the technology you pick locks you into a single architectural world-view. If you pick Web services or WSE you are accepting the SOA world view. Sure you can hack around that to do n-tier or client/server, but it is ugly and dangerous. Similarly, if you pick Enterprise Services you get a nice set of client/server functionality, but you lose a lot of flexibility. And so forth.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Since the architectural decisions are so directly and irrevocably tied to the technology, we can’t actually discuss architecture. We are limited to discussing our systems in terms of the technology itself, rather than the architectural concepts and goals we’re trying to achieve. And that is very sad.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">By merging these technologies into a single API, Indigo may allow us to elevate the level of dialog. Rather than having inane debates between Web services and Remoting, we can have intelligent discussions about the pros and cons of n-tier vs SOA. We can apply rational thought as to how each distributed architecture concept applies to the various parts of our application.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">We might even find that some parts of our application are n-tier, while others require SOA concepts. Due to the unified API, Indigo should allow us to actually do both where appropriate. Without irrational debates over protocol, since Indigo natively supports concepts for both n-tier and SOA.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Now <i style="mso-bidi-font-style: normal">this</i> is compelling!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">As compelling as it is to think that we can start having more intelligent and productive architectural discussions, that isn’t the whole of it. I am hopeful that Indigo represents the groundwork for greater things.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">There are a lot of very hard problems to solve in distributed computing. Unfortunately our underlying communications protocols never seem to stay in place long enough for anyone to really address the more interesting problems. Instead, for many years now we’ve just watched as vendors reinvent the concept of remote procedure calls over and over again: RPC, IIOP, DCOM, RMI, Remoting, Web services, Indigo.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">That is frustrating. It is frustrating because we never really move beyond RPC. While there’s no doubt that Indigo is much easier to use and more clear than any previous RPC scheme, it is also quite true that Indigo merely lets us do what we could already do.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">What I’m hoping (perhaps foolishly) is that Indigo will be the end. That we’ll finally have an RPC technology that is stable and flexible enough that it won’t need to be replaced so rapidly. And being stable and flexible, it will allow the pursuit of solutions to the harder problems.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">What are those problems? They are many, and they include semantic meaning of messages and data. They include distributed synchronization primitives and concepts. They include standardization and simplification of background processing – making it as easy and natural as synchronous processing is today. They include identity and security issues, management of long-running processes, simplification of compensating transactions and many other issues.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Maybe Indigo represents the platform on which solutions to these and other problems can finally be built. Perhaps in another 5 years we can look back and say that Indigo was the turning point that finally allowed us to <i style="mso-bidi-font-style: normal">really</i> make distributed computing a first-class concept.</font>
