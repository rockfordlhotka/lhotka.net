---
title: More discussion on service-oriented and procedural programming
postDate: 2004-09-09T09:42:46.28125-05:00
abstract: Ted and John went off and started discussing this SOA thing, referencing my blog, so I thought I should clarify some of my thoughts (or muddy the waters?).
postStatus: publish
---
09 September 2004

<font face="Times New Roman" color="#000000" size="3">I just love a good discussion, and thanks to </font>[<font face="Times New Roman" size="3">Ted</font>](http://www.neward.net/ted/weblog)<font face="Times New Roman" color="#000000" size="3"> I&#8217;m now </font>[<font face="Times New Roman" size="3">part of one</font>](http://www.neward.net/ted/weblog/index.jsp?date=20040908#1094709676078)<font size="3"><font color="#000000"><font face="Times New Roman"> :-)</font></font></font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">A few days ago I posted </font>[<font face="Times New Roman" size="3">another blog entry</font>](/WeBlog/PermaLink.aspx?guid=5c0574f6-6ccc-4ba0-beed-b8580712bbd1)<font face="Times New Roman" color="#000000" size="3"> about service-oriented concepts, drawing a parallel to procedural design. Apparently and unsurprisingly, this parallel doesn&#8217;t sit too well with everyone out there.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I agree that SO has the <i style="mso-bidi-font-style: normal">potential</i> to be something new and interesting. Maybe even on par with fundamental shifts like event-driven programming and object-oriented design have been over the past couple decades. However, I am far from convinced that it really is such a big, radical shift &#8211; at least in most people&#8217;s minds.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">After all, at its core SO is just about enabling my code to talk to your code. A problem space that has been hashed and rehashed for more years than most of us have been in the industry.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Most people view SO as SOAP over HTTP, which basically makes it the newest </font>[<font face="Times New Roman" size="3">RPC</font>](http://sbc.webopedia.com/TERM/R/RPC.html)<font face="Times New Roman" color="#000000" size="3">/</font>[<font face="Times New Roman" size="3">RMI</font>](http://www.hyperdictionary.com/computing/rmi)<font face="Times New Roman" color="#000000" size="3">/</font>[<font face="Times New Roman" size="3">DCOM</font>](http://www.webopedia.com/TERM/D/DCOM.html)<font face="Times New Roman" color="#000000" size="3"> technology. And if that&#8217;s how it is viewed, then it is a pretty poor replacement for any of them&#8230;</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Some people view SO as a technology independent concept that can be used to describe business systems, technology systems &#8211; almost anything. </font>[<font face="Times New Roman" size="3">Pat Helland</font>](http://blogs.msdn.com/pathelland)<font face="Times New Roman" color="#000000" size="3"> makes this case in some of his presentations. I love the analogy he makes by using SO to describe an old-fashioned experience of coming in and ordering breakfast in a diner. That makes all the sense in the world to me, and there&#8217;s not a computer or XML fragment involved in the whole thing.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Yet other people view SO as a messaging technology. Basically this camp is all about SOAP, but isn&#8217;t tied to HTTP (even though there are precious few other transports that are available for SOAP today).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Obviously for SO to be a radical new thing, one of the latter two views must be adopted, since otherwise RPC has it covered.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">By far the most interesting view (to me) is of SO as a modeling construct, not a technological one. If SO is a way of describing and decomposing problem spaces in a new way, then <i style="mso-bidi-font-style: normal">that</i> is interesting. Not that there&#8217;s a whole lot of tool/product money to be had in this view &#8211; but there&#8217;s lots of consulting/speaking/writing money to be made. This could be the next RUP or something&nbsp;:-)</font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Less interesting, but more tangible, is the messaging view. Having worked with companies who have their primary infrastructure built on messaging (using MQ Series or MSMQ), I find this view of SO to be less than inspiring.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It has been <i style="mso-bidi-font-style: normal">done</i> people! And it works very nicely &#8211; but let&#8217;s face it, this view of SO is no more interesting or innovative than the RPC view. The idea of passing messages between autonomous applications is not new. And adding angle brackets around our data merely helps the network hardware vendors sell more equipment, it doesn&#8217;t fundamentally change life.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Again, I call back to FORTRAN and procedural programming. The whole idea behind procedural programming was to have a set of autonomous procedures that could be called in an appropriate order (orchestrated) in order to achieve the desired functionality. If we had not cheated &#8211; if we had actually passed all our data as parameters from procedure to procedure, it might have actually worked. But we didn&#8217;t (for a variety of good reasons), and so it collapsed under its own weight.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Maybe SO can avoid this fate, since its distributed nature makes cheating much more difficult. But even so, the design concepts developed 20 years ago for procedural design and programming should apply to SO today, since SO is merely procedural programming with a wire between the procedures.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So in short, other than SO as an analysis tool, I continue to seriously struggle with how it is a transformative technology.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Either SO is a new RPC technology, enabling cross-network component access using XML, or SO is a new messaging technology, enabling the same autonomous communication we have with queuing technologies &#8211; but with the dubious advantage of angle brackets. Neither is overly compelling in and of itself.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And yet intuitively SO <i style="mso-bidi-font-style: normal">feels</i> like a bigger thing. Maybe it is the vendor hype: IBM with their services and Microsoft with their products &#8211; everyone wants to turn the S in SOA into a $.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But there is this concept of <i style="mso-bidi-font-style: normal">emergent behavior</i>, which is something I&#8217;ve put a fair amount of energy into. Emergent behavior is the idea that simple elements &#8211; even rehashed technology concepts &#8211; can combine in unexpected ways such that new and interesting behaviors emerge.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Maybe, just maybe, SO will turn out to be emergent by combining the concepts of RPC, messaging and angle brackets into something new and revolutionary. Then again, maybe it is a passing fad, and SO is really just another acronym for </font>[<font face="Times New Roman" size="3">EDI</font>](http://www.webopedia.com/TERM/E/EDI.html)<font face="Times New Roman" color="#000000" size="3"> or </font>[<font face="Times New Roman" size="3">EAI</font>](http://computing-dictionary.thefreedictionary.com/EAI)<font face="Times New Roman" color="#000000" size="3">.</font>
