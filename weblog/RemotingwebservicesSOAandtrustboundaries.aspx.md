---
title: Remoting, web services, SOA and trust boundaries
postDate: 2004-04-08T20:13:51.4375-05:00
abstract: Rocky responds to an email query about the future of remoting, and how it relates to SOA and web services.
postStatus: publish
---
08 April 2004

Totally unrelated to my previous blog entry, I received an email asking me about the ‘future of remoting’ as it relates to web services and SOA.<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p>

It seems that the sender of the email got some advice from Microsoft indicating that the default choice for all network communication should be web services, and that instead of using conventional tiers in applications, that we should all be using SOA concepts instead. Failing that, we should use Enterprise Services (and thus presumably DCOM (shudder!)), and should only use remoting as a last resort.


Not surprisingly, I disagree. My answer follows…<o:p></o:p>

<o:p></o:p>


<font color="#000000">Frankly, I flat out disagree with what you've been told. Any advice&nbsp;that starts with "default choices" is silly. There is no such thing - our environments are too complex for such simplistic views on architecture.<o:p></o:p></font>

<font color="#000000">Unless you are willing to rearchitect your system to be a network of linked _applications_ rather than a set of tiers, you have no business applying SOA concepts. Applying SOA is a <i style="mso-bidi-font-style: normal">big</i> choice, because there is a very high cost to its application (in terms of complexity and performance). <o:p></o:p></font>

<font color="#000000">SOA is very, very cool, and is a very good thing when appropriately applied. Attempting to change classic client/server scenarios into SOA scenarios is typically the wrong approach.<o:p></o:p></font>

<font color="#000000">While SOA is a much bigger thing than web services, it turns out that web services are mostly only useful for SOA models. This is because they employ an open standard, so exposing your 'middle tier' as a set of web services really means you have exposed the 'middle tier' to any app on your network. This <i style="mso-bidi-font-style: normal">forces</i> the 'middle tier' to become an application (because you have created a trust boundary that didn't previously exist). As soon as you employ web services you have created a separate application, not a tier. This is a HUGE architectural step, and basically forces you to employ SOA concepts - even if you would prefer to use simpler and faster client/server concepts.<o:p></o:p></font>

<font color="#000000">Remoting offers superior features and performance when compared to web services. It is the most appropriate client/server technology available in .NET today. If you aren't crossing trust boundaries (and don't want to artificially impose them with web services), then remoting is the correct technology to use.<o:p></o:p></font>

<font color="#000000">Indigo supports the _concepts_ of remoting (namely the ability to pass .NET types with full fidelity, and the ability to have connection-based objects like remoting's activated objects). Indigo <i style="mso-bidi-font-style: normal">has</i> to support these concepts, because it is supposed to be the future of both the open web service technology and the higher performance client/server technology for .NET.<o:p></o:p></font>

<font color="#000000">The point I'm making, is that using remoting today is good if you are staying within trust boundaries. It doesn't preclude moving to Indigo in the future, because Indigo will also provide solutions for communication within trust boundaries, with full .NET type fidelity (and other cool features).<o:p></o:p></font>

<font color="#000000">Web services force the use of SOA, even if it isn't appropriate. They should be approached with caution and forethought. </font><font color="#000000">Specifically, you should give serious thought to where you want or need to have trust boundaries in your enterprise and in your application design. Trust boundaries have a high cost, so inserting them between what <em>should</em> have been tiers of an application is typically a very, very bad idea.<o:p></o:p></font>

<font color="#000000">On the other hand, using remoting between applications is an equally bad idea. In such cases you should always look at SOA as a philosophy, and potentially web services as a technical solution (though frankly, today the better SOA technology is often queuing (MQ Series or MSMQ), rather than web services).<o:p></o:p></font>

<o:p>&nbsp;</o:p>
