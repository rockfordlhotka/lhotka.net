---
title: Fire bad, tree pretty
postDate: 2005-02-18T12:11:26.671875-06:00
abstract: In a recent online discussion the question came up “If ‘the middle tier’ has no knowledge about the actual data it's transporting, then what value is it adding?”
postStatus: publish
---
18 February 2005

<font face="Times New Roman" color="#000000" size="3">In a recent online discussion the question came up “If ‘the middle tier’ has no knowledge about the actual data it's transporting, then what value is it adding?”</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">The answer: database connection pooling.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Pure and simple, in most rich client scenarios the only reason for a "middle tier" is to pool database connections. And the benefit can be tremendous. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Consider 200 concurrent clients all connecting to your database using conventional coding. They'll have at least 200 connections open, probably more. This is especially true since each client does its own "connection pooling", so typically a client will never close its connection once established for the day.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Then consider 200 clients going through a middle tier "app server" that does nothing but ferry the data between the clients and database. But it has the code to open the connections. Now those 200 clients might use just 3-4 connections to the database rather than 200, because they are all pooled on the server.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">Was there a performance hit? Absolutely. Was there a scalability gain? Absolutely. Is it more expensive and harder to build/maintain? Absolutely.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">This middle tier stuff is not a panacea. In fact its cost is typically higher than the benefit, because most applications don't actually have enough concurrent users to make it worth the complexity. But people are enamored of the idea of "n-tier", thinking it requires an actual physical tier...<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I blame it on Windows DNA and those stupid graphic representations. They totally muddied the waters in people's understanding the difference between n-layer (logical separation) and n-tier (physical separation). </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">People DO want n-layer, because that provides reuse, maintainability and overall lower costs. Logical separation of UI, business logic, data access and data storage is almost always of tremendous benefit.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">People MIGHT want n-tier if they need the scalability or security it can offer, and if those benefits outweigh the high cost of building a physically distributed system. But the cost/benefit isn’t there as often as people think, so a lot of people build physical n-tier systems <i style="mso-bidi-font-style: normal">for no good reason</i>. They waste time and money for no real gain. This is sad, and is something we should all fight against.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">I make my living writing books and articles and speaking about building distributed systems. And my primary message is <b style="mso-bidi-font-weight: normal"><i style="mso-bidi-font-style: normal">just say NO!</i></b></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">You should be forced into implementing physical tiers kicking and screaming. There should be substantial justification for using tiers, and those justifications should be questioned at every step along the way.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">At the same time, you should encourage the use of logical layers at all times. There should be substantial justification for <i style="mso-bidi-font-style: normal">not</i> using layers, and any argument against layering of software should be viewed with extreme skepticism. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Layering is almost always good, tiers are usually bad.</font>
