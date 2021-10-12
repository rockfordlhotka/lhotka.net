---
title: Better version of the .NET 2.0 event/serialization solution
postDate: 2004-05-31T22:37:08.140625-05:00
abstract: As suggested, here's an updated version of the code that uses a pair of EventHandler delegates rather than a List(Of T) to store the delegates.
postStatus: publish
---
31 May 2004

<font face="Arial">A few weeks ago I <a href="/WeBlog/PermaLink.aspx?guid=776f44e8-aaec-4845-b649-e0d840e6de2c">posted an entry</a> about a solution to today's problem with serializing objects that declare events. It was pointed out that there's a better way to handle the list of delegates, and so here's a better version of the code.</font>

<font face="Courier New">&nbsp; <nonserialized()>_<br>&nbsp; Private mNonSerializable As EventHandler<br>&nbsp; Private mSerializable As EventHandler</nonserialized()></font>

<font face="Courier New">&nbsp; Public Custom Event NameChanged As System.ComponentModel.EventHandler<br>&nbsp;&nbsp;&nbsp; AddHandler(ByVal value As System.ComponentModel.EventHandler)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; If value.Target.GetType.IsSerializable Then<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; mSerializable = CType([Delegate].Combine(mSerializable, value), EventHandler)</font>

<font face="Courier New">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Else<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; mNonSerializable = CType([Delegate].Combine(mNonSerializable, value), EventHandler)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; End If<br>&nbsp;&nbsp;&nbsp; End AddHandler</font>

<font face="Courier New">&nbsp;&nbsp;&nbsp; RemoveHandler(ByVal value As System.ComponentModel.EventHandler)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; If value.Target.GetType.IsSerializable Then<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; mSerializable = CType([Delegate].Remove(mSerializable, value), EventHandler)</font>

<font face="Courier New">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Else<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; mNonSerializable = CType([Delegate].Remove(mNonSerializable, value), EventHandler)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; End If<br>&nbsp;&nbsp;&nbsp; End RemoveHandler</font>

<font face="Courier New">&nbsp;&nbsp;&nbsp; RaiseEvent(ByVal sender As Object, ByVal e As System.ComponentModel.EventArgs)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; If mNonSerializable IsNot Nothing Then mNonSerializable(sender, e)<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; If mSerializable IsNot Nothing Then mSerializable(sender, e)<br>&nbsp;&nbsp;&nbsp; End RaiseEvent<br>&nbsp; End Event<br></font>
