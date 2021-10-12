---
title: Dispose your Command objects!
postDate: 2004-06-02T11:33:20.796875-05:00
abstract: The results of an email discussion with Microsoft are in - and we should be disposing our ADO.NET Command objects!
postStatus: publish
---
02 June 2004

<font face="Times New Roman" color="#000000" size="3">Most people (including me) don&#8217;t regularly Dispose() their Command objects when doing data access with ADO.NET. The Connection and DataReader objects have Close() methods, and people are very much in the habit (or should be) of ensuring that either Close() or Dispose() or both are called on Connection and DataReader objects.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">But Command objects do have a Dispose() method even though they don&#8217;t have a Close() method. Should they be disposed?</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I posed this question to some of the guys on the ADO.NET team at Microsoft. After a few emails bounced around I got an answer: &#8220;Sometimes it is important&#8221;</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It turns out that the reason Command objects have a Dispose method is because they inherit from Component, which implements IDisposable. The reason Command objects inherit from Component is so that they can be easily used in the IDE on designer surfaces.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">However, it also turns out that <i style="mso-bidi-font-style: normal">some</i> Command objects really do have non-managed resources that need to be disposed. Some don&#8217;t. How do you know which do and which don&#8217;t? You need to ask the dev that wrote the code. </font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">It turns out that SqlCommand has no un-managed resources, which is why most of us have gotten away with this so far. However, OleDbCommand and OdbcCommand <i style="mso-bidi-font-style: normal">do</i> have un-managed resources and must be disposed to be safe. I don&#8217;t know about OracleCommand &#8211; as that didn&#8217;t come up in the email discussions.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Of course that&#8217;s not a practical answer, so the short answer to this whole thing is that you should <i style="mso-bidi-font-style: normal">always</i> Dispose() your Command objects just to be safe.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So, follow this basic pattern in VB.NET 2002/2003 (pseudo-code):</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000">Dim cn As New Connection("&#8230;")<o:p></o:p></font>

<font color="#000000">cn.Open()<o:p></o:p></font>

<font color="#000000">Try<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>Dim cm As Command = cn.CreateCommand()<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>Try<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>Dim dr As DataReader = cm.ExecuteReader()<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>Try<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>' do data reading here<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>Finally<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>dr.Close() ' and/or Dispose() &#8211; though Close() and Dispose() both work<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>End Try<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>Finally<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>cm.Dispose()<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>End Try<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">Finally<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>cn.Close() ' and/or Dispose() &#8211; though Close() and Dispose() both work<o:p></o:p></font>

<font color="#000000">End Try<o:p></o:p></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>



<font face="Times New Roman" color="#000000" size="3">And in C# 1.0 and 2.0 (pseudo-code):</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000">using(Connection cn = new Connection("&#8230;"))<o:p></o:p></font>

<font color="#000000">{<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>cn.Open()<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>using(Command cm = cn.CreateCommand())<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>{<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>using(DataReader dr = cm.ExecuteReader())<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>{<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// do data reading here<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>}<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>}<o:p></o:p></font>

<font color="#000000">}<o:p></o:p></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And in VB 8 (VB.NET 2005) (pseudo-code):</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000">Using cn As New Connection("&#8230;")<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>cn.Open()<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>Using cm As Command = cn.CreateCommand()<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>Using dr As DataReader = cm.ExecuteReader()<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>' do data reading here<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>End Using<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>End Using<o:p></o:p></font>

<font color="#000000">End Using<o:p></o:p></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>


