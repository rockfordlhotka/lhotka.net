---
title: Software is too darn hard
postDate: 2006-01-23T11:41:13.375-06:00
abstract: Sure, the hard stuff is fun – but it rarely has business value…
postStatus: publish
---
23 January 2006

<font face="Times New Roman" size="3" color="#000000">[Warning, the following is a bit of a rant...]</font>

<font face="Times New Roman" size="3" color="#000000"></font>

<font face="Times New Roman" size="3" color="#000000"><a href="http://magenic.com/Services/CustomSoftwareDevelopment.aspx">Custom software development</a> is too darn hard. As an industry, we spend more time discussing “plumbing” issues like Java vs .NET or .NET Remoting vs Web Services than we do discussing the design of the actual business functionality itself.</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">And even when we get to the business functionality, we spend most of our time fighting with the OO design tools, the form designer tools that “help” create the UI, the holes in data binding, the data access code (transactions, concurrency, field/column mapping) and the database design tools.</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">Does the user care, or get any benefit out of any of this? No. They really don’t. Oh sure, we <i style="">convince</i> ourselves that they do, or that they’d “care if they knew”. But they really don’t.</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">The users want a system that does something useful. I think </font>[<font face="Times New Roman" size="3">Chris Stone</font>](http://www.sdtimes.com/article/opinion-20060115-02.html)<font face="Times New Roman" size="3" color="#000000"> gets it right in this editorial.</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">I think the underlying problem is that just building business software to solve users’ problems is ultimately boring. Most of us get into computers to express our creative side, not to assemble components into working applications. </font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">If we wanted to do widget assembly, there’s a whole lot of other jobs that’d provide more visceral satisfaction. Carpentry, plumbing (like with pipes and water), cabinet making and many other jobs provide the ability to assembly components to build really nice things. And those jobs have a level of creativity too – just like assembly programs do in the computer world.</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">But they don’t offer the level of creativity and expression you get by building your own client/server, n-tier, SOA framework. <i style="">Using</i> data binding isn’t nearly as creative or fun as <i style="">building</i> a replacement for data binding…</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">I think this is the root of the issue. The computer industry is largely populated by people who want to build low-level stuff, not solve high-level business issues. And even if you go with conventional wisdom; that Mort (the business-focused developer) outnumbers the Elvis/Einstein framework-builders 5 to 1, there are still enough Elvis/Einstein types in every organization to muck things up for the Morts.</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">Have you tried building an app with VB3 (yes, Visual Basic 3.0) lately? A couple years ago I dusted that relic off and tried it. VB3 programs are <i style="">fast</i>. I mean blindingly <i style="">fast!</i> It makes sense, they were designed for the hardware of 1993… More importantly, a data entry screen built in VB3 is every bit as functional to the user as a data entry screen built with today’s trendy technologies.</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">Can you <i style="">really</i> claim that your Windows Forms 2.0, ASP.NET 2.0 or Flash UI makes the user’s data entry faster or more efficient? Do you save them keystrokes? Seconds of time?</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">While I think the primary fault lies with us, as software designers and developers, there’s no doubt that the vendors feed into this as well.</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">We’ve had remote-procedure-call technology for a hell of a long time now. But the vendors keep refining it every few years: got to keep the hype going. Web services are merely the latest incarnation of a very long sequence of technologies that all you to call a procedure/component/method/service on another computer. Does using Web services make the user more efficient than DCOM? Does it save them time or keystrokes? No.</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">But we justify all <i style="">these</i> things by saying it will save <i style="">us</i> time. They’ll make <i style="">us</i> more efficient. So ask your users. Do your users think you are doing a better job, that you are more efficient and responsive, that you are giving them better software than you were before Web Services? Before .NET? Before Java? </font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">Probably not. My guess: users don’t have a clue that the technology landscape changed out from under them over the past 5 years. They see the same software, with the same mis-match against the business needs and the same inefficient data entry mechanisms they’ve seen for at least the past 15 years…</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">No wonder they offshore the work. We (at least in the <st1:country-region w:st="on">US</st1:country-region> and <st1:place w:st="on">Europe</st1:place>) have had a very long time to prove that we can do better work, that all this investment in tools and platforms will make our users’ lives better. Since most of what we’ve done hasn’t lived up to that hype, can it be at all surprising that our users feel they can get the same crappy software at a tiny fraction of the price by offshoring?</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">Recently my friend Kathleen Dollard made the comment that all of Visual Basic (and .NET in general) should be geared toward Mort. I think she’s right. .NET should be geared toward making sure that the <i style="">business developer</i> is exceedingly productive and can provide tremendous business value to their organizations, with minimal time and effort.</font>

<o:p><font face="Times New Roman" size="3" color="#000000">&nbsp;</font></o:p>

<font face="Times New Roman" size="3" color="#000000">If our tools did what they were <i style="">supposed</i> to do, the Elvis/Einstein types could back off and just let the majority of developers use the tools – without wasting all that time building new frameworks. If our tools did what they were supposed to do, the Mort types would be so productive there’d be no value in offshoring. Expressing business requirements in software would be more efficiently done by people who work in the business, who understand the business, language and culture; and who have tools that allow them to build that software rapidly, cheaply and in a way that <i style="">actually meets the business need</i>.</font>
