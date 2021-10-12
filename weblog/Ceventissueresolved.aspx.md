---
title: C# event issue resolved
postDate: 2005-01-06T20:58:17.90625-06:00
abstract: OK, I figured it out (I think)
postStatus: publish
---
06 January 2005

<font face="Times New Roman" color="#000000" size="3">OK, I figured it out (I think)</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>[NonSerialized]<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>EventHandler _nonSerializableHandlers;<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>EventHandler _serializableHandlers;<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>/// &lt;summary&gt;<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>/// Declares a serialization-safe IsDirtyChanged event.<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>/// &lt;/summary&gt;<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>public<font color="#000000"> </font>event<font color="#000000"> EventHandler IsDirtyChanged<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>{<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>add<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>if<font color="#000000"> (</font>value<font color="#000000">.Target.GetType().IsSerializable)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_serializableHandlers = <o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>(EventHandler)Delegate.Combine(_serializableHandlers, </font>value<font color="#000000">);<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>else<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_nonSerializableHandlers = <o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>(EventHandler)Delegate.Combine(_nonSerializableHandlers, </font>value<font color="#000000">);<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>}<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>remove<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>if<font color="#000000"> (</font>value<font color="#000000">.Target.GetType().IsSerializable)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_serializableHandlers = <o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>(EventHandler)Delegate.Remove(_serializableHandlers, </font>value<font color="#000000">);<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>else<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_nonSerializableHandlers =<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span style="mso-spacerun: yes">&nbsp;</span>(EventHandler)Delegate.Remove(_nonSerializableHandlers, </font>value<font color="#000000">);<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>}<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>}<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>/// &lt;summary&gt;<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>/// Call this method to raise the IsDirtyChanged event.<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>/// &lt;/summary&gt;<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>virtual<font color="#000000"> </font>protected<font color="#000000"> </font>void<font color="#000000"> OnIsDirtyChanged()<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>{<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>if<font color="#000000"> (_nonSerializableHandlers != </font>null<font color="#000000">)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_nonSerializableHandlers(</font>this<font color="#000000">, EventArgs.Empty);<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>if<font color="#000000"> (_serializableHandlers != </font>null<font color="#000000">)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_serializableHandlers(</font>this<font color="#000000">, EventArgs.Empty);<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>}<o:p></o:p></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">I temporarily forgot that C# makes you invoke the delegate directly anyway, so having a separate clause in the manual event declaration isn&#8217;t required. I still think it makes the code easier to read, but functionality is king in the end.</font>


