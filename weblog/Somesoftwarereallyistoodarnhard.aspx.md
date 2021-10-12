---
title: Some software really is too darn hard
postDate: 2006-05-02T15:16:42.125-05:00
abstract: Just how much fun can you have writing data entry screens anyway?
postStatus: publish
---
02 May 2006

<font face="Times New Roman" color="#000000" size="3">You might wonder what’s up. I go and stir the pot by saying that software development is too darn hard, and that TDD is overhyped (and broadly misunderstood) and then disappear from the conversations.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Well, so far in 2006 I completed the <a href="http://www.lhotka.net/cslanet">CSLA .NET</a> framework (twice), finished two books, buried my last Grandmother, have been supporting my Mother through dealing with cancer (which has shut down her kidneys, so now she’s dealing with dialysis too), had the lower level of my house flood (with luck my office will be reclaimed for use late this week – at least my son has his bedroom back) and I’ve spoken at 9 events requiring travel (2 international). And things don’t look to change soon. I’m traveling 5 out of the next 7 weeks (1 international), and my Mom's chemo runs through the summer (fingers crossed).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In summary: I’ve been just a little busy, and blogging is comparatively quite low on the priority list. Certainly it falls below family, generating income and replacing carpets and walls.</font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">It isn't that I meant to stir the pot and then disappear - but the universe decided to complicate my life in some unexpected ways. So I'm sticking my head up when I can, and I hope you understand that the frequency of my participation in any dialog is a bit restricted at the moment.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">A while back I posted a blog entry suggesting that </font>[<font face="Times New Roman" size="3">software is too hard</font>](http://www.lhotka.net/WeBlog/SoftwareIsTooDarnHard.aspx)<font face="Times New Roman" color="#000000" size="3">. This was recently </font>[<font face="Times New Roman" size="3">republished by Fawcette</font>](http://www.ftponline.com/vsm/2006_04/magazine/departments/guestop/)<font face="Times New Roman" color="#000000" size="3">. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This generated a few emails from people saying that they agree; that their experience is like mine; that the process of analyzing business problems, then designing and building software to address them is fundamentally the same today as it was 15-20 years ago.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It has also generated some emails and comments from people who either disagree, or at least find the conclusion demoralizing or depressing. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Well, it was <i style="mso-bidi-font-style: normal">supposed</i> to be depressing, so in that I feel quite comfortable. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Let’s face it. Most software basically collects data from users, stores that data and then displays the data back to the same, or other, users in a different format. This type of system is often called forms-over-data (or if you remember terminals it was screens-over-data, or if you are a web person maybe it is pages-over-data).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman"><i style="mso-bidi-font-style: normal">This</i> is the software I’m saying is too darn hard. Why the hell is it so hard, does it take so much work, to create a data entry screen that dumps the data into a data store? And why can’t we just flip a switch to say we value performance over scalability, or scalability over security, or fault-tolerance over performance or whatever?</font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman"><i style="mso-bidi-font-style: normal">This</i> is where I’m saying the Elvis/Einstein personas and our vendors have failed us.</font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In fact, I’d suggest we’re going the other way. We’re coming up with ways to further complicate the most common types of application by adding in SOA, TDD, WinFx and more.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Now let me be clear here. Most applications are <i style="mso-bidi-font-style: normal">mostly</i> forms-over-data. Almost every application really does have some small bit of interesting complexity. In other words, out of perhaps 100 forms in an application, 1 or 2 might be more than simply forms-over-data. And of course, there are those precious few applications that are <i style="mso-bidi-font-style: normal">not</i> forms-over-data, and you people working on those projects should consider yourselves truly fortunate!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So the problem is this: we get so wound up trying to figure out how to do that 1-2% of the application that is interesting that we complicate the hell out of the 98% that <i style="mso-bidi-font-style: normal">should be</i> drop-dead trivial. We rule out tools, technologies and frameworks that could have trivialized the 98% because they can’t address the 2%. We adopt expensive methodologies to enhance productivity and/or quality because those methodologies are truly useful for that 2%. But then we <i style="mso-bidi-font-style: normal">apply the same ideas</i> to the 98%, needlessly increasing the complexity and cost of something that should have taken precious little effort.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">You can TDD/unit test/integration test until you are blue in the face. You can triple or quadruple the time and effort required to build a data entry form. And in the end you’ll still have a boring old data entry form. Worse yet, you can’t automate testing of the part that matters the most: the actual UI. The part that the <i style="mso-bidi-font-style: normal">user cares about</i> typically remains untested until the users try it out themselves.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This is what frustrates me. See, I fully understand and support the idea that you should test the hell out of the 2% of the app that’s hard. Whether you write the tests before, during or after the development to me seems like a secondary question – but actually doing the unit and integration testing should not be optional. But I think that development of the bulk of the app, the trivial forms-over-data part, should be so automated that we don’t actually “develop” it and thus don’t need to do any sort of low-level unit testing, or probably even integration testing.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Again, let me be clear. It is this forms-over-data stuff that’s too hard. It is this stuff we’ve been building basically the same way for at least 20 years. Why? I don’t know. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This problem space <i style="mso-bidi-font-style: normal">isn’t</i> that big or hard. Yet we keep rehashing it over and over and freakin’ over again. Now we’re going to rehash it with SOA and WPF, with a sprinkle of workflow just to make it <i style="mso-bidi-font-style: normal">really</i> hard.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Given that we actually need to <i style="mso-bidi-font-style: normal">code</i> forms-over-data, <i style="mso-bidi-font-style: normal">of course</i> we feel the need to tell people to do unit testing. If you code it, you should test it. Since people struggle with the discipline to write the tests during or after development, TDD is helpful in that it (maybe) provides the discipline to write the tests first. But again, the key is that if you write it you must test it.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But what I’m saying is this: <i style="mso-bidi-font-style: normal">we shouldn’t code this stuff</i>!!! Forms-over-data should be automated. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

[<font face="Times New Roman" size="3">Scott Bellware says</font>](http://codebetter.com/blogs/scott.bellware/archive/2006/04/25/143303.aspx)<font color="#000000"><font face="Times New Roman"><font size="3"> “</font><span style="FONT-SIZE: 10pt">Software development isn't too hard.&nbsp; Software development is fun.&nbsp; It's a challenge - of that there's no doubt.&nbsp; And sometimes it's a tiger that won't be tamed.</span><font size="3">” And he’s right – at least in terms of that complex 2% of most applications. But no experienced developer is going to find forms-over-data “fun” after 15-20 years. And no amount of Extreme Agile anything is going to change the fact that what businesses mostly want is to have their computers store and regurgitate data.</font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">I’m working with a client now who’s designing an application that is virtually all forms-over-data. And just like countless applications before this, more time is spent discussing the “plumbing” issues – the use of ORM, WPF, WCF, WF, ADO.NET, WinFS, ASP.NET, LINQ, Windows Forms, XHTML, Javascript, layers, tiers, patterns – than is spent discussing the business issues. You know, <i style="mso-bidi-font-style: normal">the</i> <i style="mso-bidi-font-style: normal">whole reason for writing the damn app in the first place!</i></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Trying to pull the client out of the alphabet soup of techno-babble that is today’s technology, so we can actually discuss the business needs and thus determine how to proceed is like pulling teeth. Books from people like Eric Evans and David West are great tools – if you can get people to step out of techno-land and into a productive level of discussion.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But then there’s that ugly 2% of the app again. Every time you talk about the truly interesting bits of the app, there’s so much worry about whether the “technology can handle it” that the conversation instantly devolves into an argument about whether the COM interop overhead in Enterprise Services will be a roadblock or some equivalent. WTF?!?</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And worse. Even after you fight through that – continually bringing the dialog out of the murky depths of techno-babble and into a level where OOD is possible – the technical powers-that-be want to apply the complex technology needed for the complex parts of the app back into the trivial forms-over-data parts.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">“We need consistency.” “If it can solve the hard parts, it can sure handle the easy parts.” “Someday we might need to scale higher.” “What if we want to reuse the data someday?”</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So the forms-over-data must be written using overly complex technologies (for forms-over-data anyway). Thus it must be written by hand. Thus it must be tested. Thus it costs <i style="mso-bidi-font-style: normal">many times</i> what it should have cost.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And the most irritating consequence? All that time and money wasted on complicating the forms-over-data reduces the amount of time and money available to address the parts of the app that are actually hard, or interesting – or fun.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Just over 20 years ago I was an intern for a summer while in college/university. The IT director told me in no uncertain terms that I was wasting my time getting a degree in Computer Science. “They’ve got this new thing called CASE” she said. “In a few years anyone will be able to program computers.”</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Her presupposition was that CASE would actually trivialize software development to the point that “normal people” (presumably business analysts) would be able to create applications. Obviously that didn’t happen, much to my relief.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But it does make me wonder why there’s so much excitement around Software Factories and DSLs, since they look <i style="mso-bidi-font-style: normal">terribly</i> close to CASE… Perhaps, lurking deep in the bowels of the Software Factory concept, there’s some differentiating factor that will allow it to succeed where CASE merely limped along to a slow, agonizing death.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I hope so. Because it seems to me that Software Factories and/or DSLs are the only area of technology active today that might address the fact that software (at least the forms-over-data majority) is too darn hard to build.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Maybe, just maybe, forms-over-data will be automated by some of these Software Factory ideas, so we can just slap out that 98% of the application and spend our time on the fun parts: that interesting and truly complex 2%.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In the meantime, I’ve got to get back to designing a 3D rotating, infinitely scalable form to enter customer data (to keep the user from losing interest in their dead-end data entry job, and in case the company quadruples in size every month for the next decade)…</font>
