---
title: .NET 2.0 solution to serialization of objects that raise events
postDate: 2004-05-15T23:52:16.625-05:00
abstract: In .NET 1.x there is a problem with serializing objects that raise events, where the handler of the event is not serializable. Here's at least one solution that is coming in .NET 2.0.
postStatus: publish
---
15 May 2004

In .NET 1.x there's a problem serializing objects that raise events when those events are handled by a non-serializable object (like a Windows Form). In .NET 2.0 there's at least one workaround in the form of Event Accessors.<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p>

The issue in question is as follows.<o:p></o:p>

I have a serializable object, say Customer. It raises an event, say NameChanged. A Windows Form handles that event, which means that behind the scenes there's a delegate reference from the Customer object to the Form. This delegate that is behind the event is called a *backing field*. It is the field that backs up the event and actually makes it work.<o:p></o:p>

When you try to serialize the Customer object using the BinaryFormatter or SoapFormatter, the serialization automatically attempts to serialize any objects referenced by Customer - including the Windows Form. Of course Windows Form objects are not serializable, so serialization fails and throws a runtime exception.<o:p></o:p>

Normal variables can be marked with the NonSerialized attribute to tell the serializer to ignore that variable during serialization. Unfortunately, an event is not a normal variable. We don't actually want to prevent the *event* from being serialized, we want to prevent the *target* of the event delegate (the Windows Form in this example) from being serialized. The NonSerialized attribute can't be applied to targets of delegates, and so we have a problem.<o:p></o:p>

In C# it is possible to use the field: target on an attribute to tell the compiler to apply the attribute to the backing field rather than the actual variable. This means we can use [field: NonSerialized()] to declare an event, which will cause the backing delegate field to be marked with the NonSerialized attribute. This is a bit of a hack, but does provide a solution to the problem. Unfortunately VB.NET doesn't support the field: target for attributes, so VB.NET doesn't have a solution to the problem in .NET 1.x.<o:p></o:p>

Though there is a solution in C#, the solution is not an elegant solution, so in both VB.NET and C# we really need a better answer. I have spent a lot of time talking with the folks in charge of the VB compiler, and hope they come up with an elegant solution for VB 2005. In the meantime, here’s an answer that will work in either language in .NET 2.0.<o:p></o:p>

In VB 2005 we’ll have the ability to declare an event using a “long form” using a concept called an Event Accessor. Rather than declaring an event using one of the normal options like:<o:p></o:p>

Public Event NameChanged()<o:p></o:p>

or<o:p></o:p>

Public Event NameChanged As EventHandler<o:p></o:p>

where the backing field is managed automatically, you’ll be able to declare an event in a way that you manage the backing field:<o:p></o:p>

Public Custom Event NameChanged As EventHandler<o:p></o:p>

AddHandler(ByVal value As EventHandler)<o:p></o:p>

End AddHandler<o:p></o:p>

RemoveHandler(ByVal value As EventHandler)<o:p></o:p>

End RemoveHandler<o:p></o:p>

RaiseEvent(ByVal sender As Object, ByVal e As EventArgs)<o:p></o:p>

End RaiseEvent<o:p></o:p>

End Event<o:p></o:p>

In this model we have direct control over management of each event target. When some code wants to handle our event, the AddHandler block is invoked. When they detach from our event the RemoveHandler block is invoked. When we raise the event (using the normal RaiseEvent keyword), the RaiseEvent block is invoked.<o:p></o:p>

This means we can declare our backing field to be NonSerialized if we so desire. Better yet, we can have two backing fields – one for targets that *can* be serialized, and another for targets that can’t be serialized:<o:p></o:p>

<nonserialized()>_<o:p></o:p></nonserialized()>

Private mNonSerializableHandlers As New Generic.List(Of EventHandler)<o:p></o:p>

Private mSerializableHandlers As New Generic.List(Of EventHandler)<o:p></o:p>

Then we can look at the type of the target (the object handling our event) and see if it is serializable or not, and put it in the appropriate list:<o:p></o:p>

Public Custom Event NameChanged As EventHandler<o:p></o:p>

AddHandler(ByVal value As EventHandler)<o:p></o:p>

If value.Target.GetType.IsSerializable Then<o:p></o:p>

mSerializableHandlers.Add(value)<o:p></o:p>

Else<o:p></o:p>

If mNonSerializableHandlers Is Nothing Then<o:p></o:p>

mNonSerializableHandlers = \_<o:p></o:p>

New Generic.List(Of EventHandler)()<o:p></o:p>

End If<o:p></o:p>

mNonSerializableHandlers.Add(value)<o:p></o:p>

End If<o:p></o:p>

End AddHandler<o:p></o:p>

RemoveHandler(ByVal value As EventHandler)<o:p></o:p>

If value.Target.GetType.IsSerializable Then<o:p></o:p>

mSerializableHandlers.Remove(value)<o:p></o:p>

Else<o:p></o:p>

mNonSerializableHandlers.Remove(value)<o:p></o:p>

End If<o:p></o:p>

End RemoveHandler<o:p></o:p>

RaiseEvent(ByVal sender As Object, ByVal e As EventArgs)<o:p></o:p>

For Each item As EventHandler In mNonSerializableHandlers<o:p></o:p>

item.Invoke(sender, e)<o:p></o:p>

Next<o:p></o:p>

For Each item As EventHandler In mSerializableHandlers<o:p></o:p>

item.Invoke(sender, e)<o:p></o:p>

Next<o:p></o:p>

End RaiseEvent<o:p></o:p>

End Event<o:p></o:p>

The end result is that we have declared an event that doesn’t cause problems with serialization, even if the target of the event isn’t serializable.<o:p></o:p>

This is better than today’s C# solution with the field: target on the attribute, because we maintain events for serializable target objects, and only block serialization of target objects that can’t be serialized.<o:p></o:p>


