---
title: Science fiction and SOA
postDate: 2004-09-21T08:59:04.625-05:00
abstract: Vernor Vinge's novel "A Deepness in the Sky" paints an interesting view of a future where service-oriented systems are the norm.
postStatus: publish
---
21 September 2004

<font face="Times New Roman" color="#000000" size="3">I read a lot of science fiction. I travel a lot (which you can tell from my </font>[<font face="Times New Roman" size="3">list of speaking engagements</font>](/presentations.aspx))<font face="Times New Roman" color="#000000" size="3"> and I find it very hard to work on a plane. You might think I&#8217;d read computer books, but I regard computer books as reference material, so I very rarely actually <i style="mso-bidi-font-style: normal">read</i> a computer book, as much as skim it or use the index to find answers to specific questions&#8230; Besides, they are all so darn big, and it gets heavy carrying them around airports :)</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So what&#8217;s the point of this post? I recently read a very excellent book that I believe has a great deal of meaning for the computer industry. Sure, it is science fiction, but it is also paints a picture of what computing could look like if today&#8217;s service-oriented concepts come to true fruition.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The book is Vernor Vinge&#8217;s </font>[<font face="Times New Roman" size="3">A Deepness in the Sky</font>](http://www.amazon.com/exec/obidos/tg/detail/-/0812536355)<font face="Times New Roman" color="#000000" size="3">, which is a prequel to </font>[<font face="Times New Roman" size="3">A Fire Upon the Deep</font>](http://www.amazon.com/exec/obidos/tg/detail/-/0812515285)<font face="Times New Roman" color="#000000" size="3">. <i style="mso-bidi-font-style: normal">Fire</i> is an excellent novel, and was written first. I highly recommend it. However, <i style="mso-bidi-font-style: normal">Deepness</i> is the book to which I&#8217;m referring when I talk about the links to the computer industry.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I doubt the links are accidental. Vernor Vinge is a retired </font>[<font face="Times New Roman" size="3">professor of Computer Science</font>](http://www-rohan.sdsu.edu/faculty/vinge/)<font face="Times New Roman" color="#000000" size="3"> in <?xml:namespace prefix = st1 ns = "urn:schemas-microsoft-com:office:smarttags" /><st1:place w:st="on"><st1:city w:st="on">San Diego</st1:city></st1:place>, and obviously has some pretty serious understanding of computer science and related issues.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I should point out that what follows could give away key points in the story. The story is awesome, so if you are worried about having it lose some of its impact then <b style="mso-bidi-font-weight: normal">STOP READING NOW</b>. Seriously. Take my word for it, go buy and read the book, then come back.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The technology used by the Qeng Ho (the protagonist race, pronounced &#8220;cheng ho&#8221;) in the book is based on two core concepts: aggregate systems and the wrapping/abstraction of older subsystems.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">First is the idea that all the systems are aggregates of smaller systems, which are aggregates of smaller systems and so forth. This is service-orientation incarnate. If you know the protocol/interface to a system, you can incorporate it into another system, thus creating a new system that is an aggregate of both. Extending this into something as complex as a starship or a fleet of starships gives you the effect Vinge describes in the book.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And this is a compelling vision. I have been in a bit of a funk over the past few months. It seems like our industry is lost in the same kind of rabid fanaticism that dominates the <st1:country-region w:st="on"><st1:place w:st="on">US</st1:place></st1:country-region> political scene, and that is very depressing. You are either Java or .NET. You are either VB or C#. That gets very old, very fast.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But Vinge has reminded me why I got into computers in the first place. My original vision &#8211; way back when &#8211; was to actually link two Asteroids arcade games together so multiple people could play together. It may sound corny, but I have been all about distributed systems since before such things existed.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And Vinge&#8217;s vision of a future where massively complex systems are constructed by enabling communication between autonomous distributed systems is <i style="mso-bidi-font-style: normal">exactly</i> what gets me excited! It is like object-oriented design meets distributed architecture in a truly productive and awesome manner. If this really is the future of service-orientation then sign me up!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The second main theme is the idea that most systems wrap older sub-systems. Rather than rewriting or enhancing a subsystem, it is just wrapped by a newer and more useful system. Often the new system is more abstract, leaving hidden functionality available to those who know how to tap directly into the older subsystem directly.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This second theme enables the first. Unless systems (and subsystems) are viewed as autonomous entities, it is impossible to envision a scenario where service-oriented architecture is a dominant idea. For better or worse, this includes dealing with the fact that you may not like the way a system works. You just deal with it, because it is autonomous.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">To digress a bit, what we&#8217;ve been trying to do for decades now is get computers to model real life. We tried with procedures, then objects, then components. They all miss the boat, because the real world is full of unpredictable behavior that we all just deal with. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">We deal with the jerks that use the shoulder as an illegal turn lane. We deal with the fact that our federal tax cuts just get redirected so we can pay local taxes and school levies. We deal with the fact that some lady is so busy on the cell phone that she rear-ends you at 40 mph when you are stopped at a red light. We deal with the fact that the networks run R rated movie commercials during primetime when our kids are watching TV.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The point is that people and all our real world systems and devices and machines are autonomous. All our interactions in the real world are done through a set of protocols and we just hope to high heaven that the other autonomous entities around us react appropriately.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Service-oriented architecture/design/programming is the same thing. It has the potential to be the most accurate model of real life yet. But this won&#8217;t be painless, because any software we write must be ready to deal with the autonomous nature of all the other entities in the virtual setting. Those other autonomous entities are likely to do the direct equivalent of using the shoulder as a turn lane &#8211; they&#8217;ll break the law for personal advantage and from time to time they&#8217;ll cause an accident and every now and then they&#8217;ll kill someone. This is true in the real world, and it is the future of software in the service-oriented universe.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">To bring this back to Vinge&#8217;s <i style="mso-bidi-font-style: normal">Deepness</i>, the various combatants in the book make full use of both the distributed autonomous nature of their computer systems, and of the fact that the systems are wrapping old &#8211; even ancient &#8211; subsystems with hidden features. It isn't understanding a computer language that counts, it is understanding of ancient, lost features of deeply buried subsystems that gives you power.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">We are given a vision of a future where systems and subsystems are swapped and tweaked and changed and the overall big system just keeps on working. At most, there&#8217;s adaptation to some new protocol or interface, but thanks to autonomy and abstraction the overall system keeps working.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It is perfect? Absolutely not. In fact I never saw the big twist coming &#8211; nor did the protagonists or antagonists in the book. The overall system was too complex, too autonomous. There was no way they could have anticipated or monitored what eventually occurred. Very cool (if a bit scary). But I don&#8217;t want to spoil it entirely, so I&#8217;ll leave it there.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Go read the book, hopefully it will inspire some of the same excitement I got by reading it. It certainly gave me an appreciation for the cool (and scary) aspects of a truly service-oriented world-view!</font>

<o:p><font face="Times New Roman" color="#000000" size="3"></font></o:p>
