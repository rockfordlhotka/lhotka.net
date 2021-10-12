---
title: Does workflow compete with CSLA .NET?
postDate: 2007-02-04T01:03:57.1011344-06:00
abstract: The answer: no, like SOA, the technologies are complimentary. But then I'm afraid I went on a bit of a rant...
postStatus: publish
---
04 February 2007

<font face="Times New Roman" color="#000000" size="3">It seems that people are always looking for The Next Big Thing™, which isn’t surprising. What I do find surprising is that they always assume that TNBT must somehow destroy the Previous Big Thing™, which in the field of software development was really object-orientation (at least for most people).</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Over the past few years Web Services and then their reincarnation as SOA or just SO were going to eliminate the use of OO. As more and more people have actually implemented and consumed services I think it has become abundantly clear that SOA is merely a repackaging of EAI from the 90’s and EDI from before that. Useful, but hardly of the sweeping impact of OO, at least not in the near term.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Though to be fair, OO took more than 20 years before it became remotely “mainstream”, and even today only around 30% of developers (based on my informal, but broad, polling over the past couple years) apply OOD in their daily work. So you could question whether OO is “mainstream” even today, when the <i style="mso-bidi-font-style: normal">vast</i> majority of developers use procedural programming techniques.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Even though the majority of .NET and Java developers don’t actually use OO themselves, both the .NET and Java platforms are OO throughout. So there’s no doubt that OO has had an incredible impact on our industry, and that it has shaped the major platforms and development styles used by almost everyone.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So perhaps in 15-20 years SO really will have the sweeping impact that OO has had on software development. And I’m not sure that would be a bad thing, but it isn’t a near-term concern.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">However, I was recently confronted by a (so-called) newcomer: workflow. Yes, now workflow (WF) is going to kill OO, or so I’ve been told. In fact, Through indirect channels, my challenger suggested that the CSLA .NET framework is obsolete going forward because it is based on these “old-school” OO concepts.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Obviously I beg to differ :)</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It is true that some of the concepts I employ in CSLA .NET are quite old, but I am not ready to through OO into the “old-school” bucket just yet... The idea is somewhat ironic however, because WF is being put up as The Next Big Thing™. Depressingly, there's virtually no technology today that isn't a rehash of something from 20 years ago. That's more true of SOA and WF than OO. Remember that SOA is just repacking of message-based architecture, only with XML, and workflow is an extension of procedural design and the use of flowcharts. At least OO can claim to be younger than either of those two root technologies.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">Personally, I very much doubt the use of objects as rich behavioral entities will go away any time soon. Sure, for non-interactive tasks procedural technologies like WF might be better than OO (though that's debatable). And certainly for connecting disparate systems you need to use loosely coupled architectures, of which SOA is one (but not the only one). </font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">But the question remains: how do you create rich, interactive GUI applications in a productive and yet maintainable manner?</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">Putting your logic in a workflow reduces interactivity. Putting your logic behind a set of services reduces both interactivity and performance. Putting your logic in the UI is "VB3 programming". So what's left? For interactive apps you need a business layer that can run as close to the user as possible and using business objects is a particularly good way to do exactly that.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">Neither WF nor WCF/SOA are, to me, competitors to CSLA. Rather, I see them as entirely complimentary.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Perhaps ADO.NET EF and/or LINQ are competitors - that depends on what they look like as they stabilize over the next several months. Everything I’ve seen thus far leads me to believe these technologies are complimentary as well. (And Scott Guthrie agrees – check out his </font>[<font face="Times New Roman" color="#800080" size="3">recent interview on DNR</font>](http://www.dotnetrocks.com/default.aspx?showNum=208)<font face="Times New Roman" color="#000000" size="3">) Neither of them addresses the issues around support for data binding, or centralization of business logic in a formal business layer.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">But when it comes to SOA I still think it is a “fad”. It is either MTS done over with XML - which is what 95% of the people out there are doing with "services", or it is EDI/EAI with XML - which is a good thing and a move forward, but which is too complex and has too much overhead for use in a typical application. I think that most likely in 5-10 years we'll have a new acronym for it – just adding to the EDI/EAI/SOA list.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">Just like "outsourcing" became ASP which became SaaS. The idea doesn't die, it just gets renamed so more money can be made by selling the same stuff over again - often to people who really don't need/want it.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">The point is, our industry is cyclical. And we're heading toward into a period where "procedural programming" is once again reaching a peak of usage. This time under the names SOA and workflow. But if you step back from the hype and look at it, what's proposed is that we create a bunch of standalone code blocks that exchange formatted data. A set of procedures that exchange parameters. Dress it up how you like, that's what is being proposed by both the SOA and WF crowds.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">And there's nothing wrong with that. Procedural design is well understood. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And it could actually work this time around if we don't cheat. I still maintain that the reason procedural programming "failed" was because we cheated and used common blocks and global variables. Why? Because it was too inefficient and required too much code to formally package up all the data and send it as parameters.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">If we can stomach the efficiency and coding costs this time around - packing the data into XML messages - then I see no reason why we can't make procedural programming work in many cases. And by naming it something trendy, like SOA and/or workflow, we can avoid the negative backlash that would almost certainly occur if people realized they were abandoning OO to return to procedural programming.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">Having spent the first third of my career doing procedural programming, I wouldn't necessarily mind going back. In some ways it really was easier than using objects - though there are some very ugly traps that people will have to rediscover again on this go-round. Most notably the trap that a procedure can't be reused without introducing fragility into the system, not due to syntactic coupling or API changes, but due to semantic coupling (</font>[<font face="Times New Roman" size="3">about which I've blogged</font>](http://www.lhotka.net/weblog/SemanticCouplingTheElephantInTheSOARoom.aspx)<font face="Times New Roman" color="#000000" size="3">).</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">This is true for procedures and any other "reusable" code block like a workflow activity or a service. They all suffer the same limitation - and it is one that neither WSDL nor compilers can help solve...</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">Anyway, kind of went on a rant here - but I find it amusing that, in some circles at least, OO is viewed as the "legacy" technology in the face of services or workflow, which are even <i style="mso-bidi-font-style: normal">more</i> legacy than OO ;)</font>
