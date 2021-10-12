---
title: Message-based WebMethod "overloading"
postDate: 2005-05-03T11:15:53.453125-05:00
abstract: Microsoft technology expert Bill Wagner shows how to implement "method overloading" in asmx
postStatus: publish
---
03 May 2005

Over the past few weeks I've given a number of presentations on service-oriented design and how it relates to both OO and n-tier models. One constant theme has been my recommendation that service methods use a request/response or just request method signature:<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p>

<o:p></o:p>

response = *f*(request)<o:p></o:p>

or<o:p></o:p>

*f*(request)<o:p></o:p>

<o:p></o:p>

"request" and "response" are both messages, defined by a type or schema (with a little "s", not necessarily XSD).<o:p></o:p>

<o:p></o:p>

The actual procedure, *f*, is then implemented as a [Message Router](http://patternshare.org/default.aspx/Home.HW.MessageRouter), routing each call to an appropriate handler method depending on the specific type of the request message.<o:p></o:p>

<o:p></o:p>

In concept this is an ideal model, as it helps address numerous issues around decoupling the client and service, and around versioning of a service over time. I discussed many of these issues in my article on [SOA Covenants](http://www.theserverside.net/articles/showarticle.tss?id=SOAVersioningCovenant).<o:p></o:p>

<o:p></o:p>

Of course the devil is in the details, or in this case the implementation. Today's web service technologies don't make it particularly easy to attach multiple schemas to a given parameter - which we must do to the "request" parameter in order to allow our single endpoint to accept multiple request messages.<o:p></o:p>

<o:p></o:p>

One answer is to manually create the XSD and/or WSDL. Personally I find that answer impractical. Angle-brackets weren't meant for human creation or consumption, and programmers shouldn't have to see (much less type) things like XSD or WSDL.<o:p></o:p>

<o:p></o:p>

Fortunately there's another answer. In [this blog entry](http://www.srtsolutions.com/public/item/91025), Microsoft technology expert Bill Wagner shows how to implement "method overloading" in asmx using C# to do the heavy lifting. <o:p></o:p>

<o:p>&nbsp;</o:p>

While the outcome isn't totally seamless or perfect, it is pretty darn good. In my mind Bill's answer is a decent compromise between getting the functionality we need, and avoiding the manual creation of cryptic WSDL artifacts.<o:p></o:p>

<o:p>&nbsp;</o:p>

The end result is that it is totally possible to construct flexible, maintainable and broadly useful web services using VB.NET or C#. Web services that follow a purely message-based approach, implement a message router on the server and thus provide a good story for both versioning and multiple message format stories.<o:p></o:p>

<o:p>&nbsp;</o:p>

Indigo, btw, offers a similar solution to what Bill talks about. In the Indigo situation however, it appears that we’ll have more fine-grained control over the generation of the public schema through the use of the DataContract idea, combined with inheritance in our VB or C# code.<o:p></o:p>
