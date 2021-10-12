---
title: SOA, CSLA .NET and trust boundaries
postDate: 2004-06-11T19:25:44.796-05:00
abstract: Recently a reader of Rocky's business objects book asked about combining CSLA .NET and SOA concepts into a single application. Here are some thoughts on the topic.
postStatus: publish
---
11 June 2004

<font face="Times New Roman" color="#000000" size="3">I recently had a reader of my business objects book ask about combining </font>[<font face="Times New Roman" size="3">CSLA .NET</font>](/ArticleIndex.aspx?area=CSLA%20.NET)<font face="Times New Roman" color="#000000" size="3"> and SOA concepts into a single application. </font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Certainly there are very valid ways of implementing services and client applications using CSLA such that the result fits nicely into the SOA world. For instance, in Chapter 10 I specifically demonstrate how to create services based on CSLA-style business objects, and in some of my VS Live presentations I discuss how consumption of SOA-style services fits directly into the CSLA architecture within the DataPortal_xyz methods (instead of using ADO.NET).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But the reader put forth the following, which I wanted to discuss in more detail. The text in italics is the reader’s view of Microsoft’s “standard” SOA architecture. My response follows in normal text:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

*<font color="#000000"><font size="3"><font face="Times New Roman">1. Here is the simplified MS’s “standard” layering, <o:p></o:p></font></font></font>*

*<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>*

*<font color="#000000"><font size="3"><font face="Times New Roman">(a) UI Components <o:p></o:p></font></font></font>*

*<font color="#000000"><font size="3"><font face="Times New Roman">(b) UI Process Components [UI never talk to BSI/BC directly, must via UIP]<b><o:p></o:p></b></font></font></font>*

***<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>***

*<font color="#000000"><font size="3"><font face="Times New Roman">(c) Service Interfaces <o:p></o:p></font></font></font>*

*<font color="#000000"><font size="3"><font face="Times New Roman">(d) Business Components [UIP never talk to D directly, must via BC<b>]</b><o:p></o:p></font></font></font>*

*<font color="#000000"><font size="3"><font face="Times New Roman">(e) Business Entities<o:p></o:p></font></font></font>*

*<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>*

*<font color="#000000"><font size="3"><font face="Times New Roman">(f) Data Access Logic Components <o:p></o:p></font></font></font>*

*<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>*

*<font color="#000000"><font size="3"><font face="Times New Roman">I’m aware of its “transaction script” and “anemic domain model” tendency, but it is perhaps easier for integration and using tools.<o:p></o:p></font></font></font>*

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">To be clear, I think this portrayal of ‘SOA’ is misleading and dangerous. SOA describes the interactions between separate applications, while this would lead one into thinking that SOA is used <i style="mso-bidi-font-style: normal">inside</i> an application between tiers. I believe that is entirely wrong – and if you pay attention to what noted experts like Pat Helland are saying, you’ll see that this approach is invalid.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">SOA describes a loosely-coupled, message-based set of interactions between applications or services. But in this context, the word ‘service’ is synonymous with ‘application’, since services must stand alone and be entirely self-sufficient. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000"><font size="3"><font face="Times New Roman"><i style="mso-bidi-font-style: normal">Under no circumstance</i> can you view a ‘tier’ as a ‘service’ in the context of SOA. A tier is part of an application, and implements part of the application’s overall functionality. Tiers are not designed to stand alone or be used by arbitrary clients – they are designed for use by the rest of their application. I </font></font></font>[<font face="Times New Roman" size="3">discussed this earlier</font>](/WeBlog/PermaLink.aspx?guid=9e06bcfd-380d-4ef6-9263-2f8527492945)<font face="Times New Roman" color="#000000" size="3"> in my post on trust boundaries, and how services inherently create new trust boundaries by their very nature.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So in my view you are describing at least two separate applications. You have an application with a GUI or web UI (a and b or <b style="mso-bidi-font-weight: normal">ab</b>), and an application with an XML interface (c, d, e and f or <b style="mso-bidi-font-weight: normal">cdef</b>).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">To fit into the SOA model, each of these applications (<b style="mso-bidi-font-weight: normal">ab</b> and <b style="mso-bidi-font-weight: normal">cdef</b>) is separate and must stand alone. They are not tiers in a single application, but rather are two separate applications that interact. The XML interface from <b style="mso-bidi-font-weight: normal">cdef</b> must be designed to service not only the <b style="mso-bidi-font-weight: normal">ab</b> application, but any other applications that need its functionality. That’s the whole point of an SOA-based model – to make this type of functionality broadly available and reusable.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Likewise, application <b style="mso-bidi-font-weight: normal">ab</b> should be viewed as a full-blown application. The design of <b style="mso-bidi-font-weight: normal">ab</b> shouldn’t necessarily eschew business logic – especially validation, but likely also including some calculations or other data manipulation. After all, it is the job of the designer of <b style="mso-bidi-font-weight: normal">ab</b> to provide the user with a satisfactory experience based on their requirements – which is similar, but not the same, as the set of requirements for <b style="mso-bidi-font-weight: normal">cdef</b>.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Yes, this <i style="mso-bidi-font-style: normal">does</i> mean that you’ll have duplicate logic in <b style="mso-bidi-font-weight: normal">ab</b> and <b style="mso-bidi-font-weight: normal">cdef</b>. That’s one of the side-effects of SOA. If you don’t like it, don’t use SOA.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But there’s nothing to stop you from using CSLA .NET as a model to create either <b style="mso-bidi-font-weight: normal">ab</b> or <b style="mso-bidi-font-weight: normal">cdef</b> or both.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">To create <b style="mso-bidi-font-weight: normal">ab</b> with CSLA .NET, you’d design a set of business objects (with as little or much logic as you felt was required). Since ab doesn’t have a data store of its own, but rather uses <b style="mso-bidi-font-weight: normal">cdef</b> as a data store, the DataPortal_xyz methods in the business objects would call the services exposed by <b style="mso-bidi-font-weight: normal">cdef</b> to retrieve and update data as needed.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">To create <b style="mso-bidi-font-weight: normal">cdef</b> with CSLA .NET, you’d follow the basic concepts I discuss in Chapter 10 in my </font>[<font face="Times New Roman" size="3">VB.NET and C# Business Objects</font>](/ArticleIndex.aspx?area=CSLA%20.NET)<font face="Times New Roman" color="#000000" size="3"> books. The basic concept is that you create a set of XML web services as an interface that provides the outside world with data and/or functionality. The functionality and data is provided from a set of CSLA .NET objects, which are used by the web services themselves. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Note that the CSLA-style business objects are <i style="mso-bidi-font-style: normal">not </i>directly exposed to the outside world – there is a formal interface definition for the web services which is separate from the CSLA-style business objects themselves. This provides separation of interface (the web services) from implementation (the CSLA-style business objects).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>


