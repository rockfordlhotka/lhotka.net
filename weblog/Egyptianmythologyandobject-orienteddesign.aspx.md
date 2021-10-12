---
title: Egyptian mythology and object-oriented design
postDate: 2004-12-18T22:27:43.84375-06:00
abstract: It turns out that the goddess Maat is a great example of OO design following the class, responsibility and collaboration (CRC) approach.
postStatus: publish
---
18 December 2004

<font face="Times New Roman" color="#000000" size="3">I was relaxing today, visiting with my wife and she read me the text from </font>[<font face="Times New Roman" size="3">this link</font>](http://www.hranajanto.com/goddessgallery/maat.html)<font face="Times New Roman" color="#000000" size="3">. It got me thinking&#8230; (and yes, I am way too geeky for my own good sometimes ;-) )</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The ancient Egyptians had a pretty solid understanding of decomposition into object-oriented models al la </font>[<font face="Times New Roman" size="3">CRC</font>](http://www.csc.calpoly.edu/~dbutler/tutorials/winter96/crc_b/)<font face="Times New Roman" color="#000000" size="3">-style analysis.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">(Stargate SG-1&#8217;s </font>[<font face="Times New Roman" size="3">general misuse</font>](http://www.tvtome.com/tvtome/servlet/GuidePageServlet/showid-185/epid-187831/)<font face="Times New Roman" color="#000000" size="3"> of the goddess Maat notwithstanding, and totally ignoring the <i style="mso-bidi-font-style: normal">real world</i> speculation that Maat </font>[<font face="Times New Roman" size="3">was an alien</font>](http://www.amazon.com/exec/obidos/tg/detail/-/0425176584)<font face="Times New Roman" color="#000000" size="3">)</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Look at the description of the goddess Maat&#8217;s role. She has a very clearly delineated and focused responsibility. As an object, Maat&#8217;s job is to measure justice vs evil. Arguably this is the job of the <i style="mso-bidi-font-style: normal">scale</i>, but given that there&#8217;s a goddess involved, I&#8217;m giving more weight (pun intended) to her than to the inanimate scale.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">She doesn&#8217;t decide what to do about evil, or how to mete out justice. This is not her role.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Osiris on the other hand, doesn&#8217;t measure justice or evil, nor does he perform punishment. His responsibility is also clearly delineated as a single &#8220;business rule&#8221; wherein he passes the Judged off to the appropriate &#8220;handler&#8220;.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">To do this he collaborates with Maat (and technically with the scale) and with the Judged. He has a <i style="mso-bidi-font-style: normal">using</i> relationship with Ahemait, where he passes the Judged if they fail to meet the business requirement by having an excess quantity of evil (as measured by Maat).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The fact that the Egyptians realized that justice had two parts, or two responsibilities, is very interesting. They properly separated the responsibility of measuring evil (as a single, discrete concept) from the responsibility of judging outcomes based on that measurement. A distinction that was fortunately carried forward into the <?xml:namespace prefix = st1 ns = "urn:schemas-microsoft-com:office:smarttags" /><st1:country-region w:st="on"><st1:place w:st="on">US</st1:place></st1:country-region> justice system. The measurement of evil is the responsibility of the jury, while the judging is a separate concern as is the actual implementation of punishment. Next time you are called for jury duty, keep in mind that you are filling the role of the goddess.</font>

<o:p><font face="Times New Roman" color="#000000" size="3"></font></o:p>

<font face="Times New Roman" color="#000000" size="3">Not only did the Egyptians get the separation of responsibilities, but they understood the idea of object collaboration. This is illustrated by the fact that Osiris can&#8217;t do his job without collaborating with other &#8220;objects&#8221; in the system.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And to think. All this time I&#8217;ve been saying that object-orientation has been around for about 30 years. I guess I was off by a couple orders of magnitude. It is more like 3000 years :-)</font>
