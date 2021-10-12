---
title: An answer to the Remoting confusion
postDate: 2004-08-26T23:32:31.53125-05:00
abstract: Rich Turner gives an awesome presentation - very clear, concise and logical. Thank you!!
postStatus: publish
---
26 August 2004

<font face="Times New Roman" color="#000000" size="3">OK, now I feel better. Perhaps I jumped the gun with my </font>[<font face="Times New Roman" size="3">previous post</font>](/WeBlog/PermaLink.aspx?guid=aa092a06-253b-4a3a-9c5e-58011f941479)<font face="Times New Roman" color="#000000" size="3">.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3"><a href="http://blogs.msdn.com/richturner666">Rich Turner</a> gave an awesome presentation &#8211; totally on the mark from start to end.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">He was very, very clear that the prescriptive guidance is to use asmx (web services) to <i style="mso-bidi-font-style: normal">cross service boundaries</i> and to use Enterprise Services (COM+), MSMQ, Remoting or asmx <i style="mso-bidi-font-style: normal">inside a service boundary</i>.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Note that <i style="mso-bidi-font-style: normal">inside a service</i> might be multiple tiers. Multiple physical tiers. You might cross network boundaries (though that should be minimized), but that&#8217;s OK. This is all inside your service, within your control. Since it is inside your control, you should <a href="/WeBlog/PermaLink.aspx?guid=a70aad9c-79fd-45cc-875f-00dfd3dc0fb6">choose the appropriate technology</a> based on all criteria (such as performance, transactional support, security, infrastructure support, deployment and so forth).</font>

<o:p>&nbsp;</o:p>

<font face="Times New Roman" color="#000000" size="3">This is the best and most clear guidance I&#8217;ve heard from Microsoft yet. Very nice!</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>


