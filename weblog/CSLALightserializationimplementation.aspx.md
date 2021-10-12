---
title: CSLA Light serialization implementation
postDate: 2008-06-14T21:58:12.479-05:00
abstract: 
postStatus: publish
---
14 June 2008

We're nearly done with the final serialization implementation. At this point it is possible to clone objects on Silverlight and on .NET using the same MobileFormatter. By extension, this means that objects can be cloned from Silverlight to .NET and visa versa, though we don't have tests for that yet. (and there's a bunch of cleanup and detail work to be done for completeness - but the core engine is there and working)

The approach we've taken is automatic for managed backing fields in a subclass of BusinessBase or ReadOnlyBase. It is also automatic for BusinessListBase, ReadOnlyListBase, etc. It is *not* automatic for custom criteria classes, but is automatic for SingleCriteria.

The approach does allow for serialization of private backing fields, as long as you override a couple methods in your business class to get/set the field values. This is quite comparable to the PropertyBag scheme from VB6, and is conceptually similar to implementing ISerializable (though not the same due to some required features that aren't in Silverlight - there's a reason Microsoft didn't implement something like the BinaryFormatter).

What this means is that when using only managed backing fields, you have to do no work at all. Your objects will just serialize. If you are using one or more private backing fields you need to do something like this:


> namespace MyApp
> {
>   [Serializable]
>   public class CustomerEdit : BusinessBase&lt;CustomerEdit&gt;
>   {
>     protected override void OnGetState(SerializationInfo info)
>     {
>       base.GetState(info);
>       info.AddValue("MyApp.CustomerEdit.\_id", \_id);
>       info.AddValue("MyApp.CustomerEdit.\_name", \_name);
>     }
>
> protected override void OnSetState(SerializationInfo info)
>     {
>       base.SetState(info);
>       \_id = info.GetValue&lt;int&gt;("MyApp.CustomerEdit.\_id";
>       \_name = info.GetValue&lt;string&gt;("MyApp.CustomerEdit.\_name");
>     }
>   }
> }


Assuming, of course, that you have two private backing fields, \_id and \_name. The one important restriction is that the types of all fields must be primitive types, or types that can be coerced using Csla.Utilities.CoerceValue() (which means the value can be converted to/from a string as required by the DataContractSerializer).

Of course if you have a field value that can't be automatically converted to/from a string, you can do the conversion yourself in the OnGetState/OnSetState methods.

This will get a little more complex when we implement UndoableBase (which is the next item on the list), because your overrides must differentiate between "NonSerialized" and "NotUndoable" fields - by hand of course. I expect the final result will look more like this:


> namespace MyApp
> {
>   [Serializable]
>   public class CustomerEdit : BusinessBase&lt;CustomerEdit&gt;
>   {
>     protected override void OnGetState(SerializationInfo info, StateModes mode)
>     {
>       base.GetState(info);
>       if (mode == StateModes.Serialization)
>         info.AddValue("MyApp.CustomerEdit.\_id", \_id);
>       info.AddValue("MyApp.CustomerEdit.\_name", \_name);
>     }
>
> protected override void OnSetState(SerializationInfo info, StateModes mode)
>     {
>       base.SetState(info);
>       if (mode == StateModes.Serialization)
>         \_id = info.GetValue&lt;int&gt;("MyApp.CustomerEdit.\_id";
>       \_name = info.GetValue&lt;string&gt;("MyApp.CustomerEdit.\_name");
>     }
>   }
> }


The StateModes enum will have two values: Serialization and Undo. This will allow you to exclude certain fields that are serialization-only or perhaps undo-only. I think this is an edge case for the most part, but the option will be there.

Child objects in CSLA .NET 3.5 and later should always be kept in managed backing fields, and so will be handled automatically. If you have a pressing need to store a child object reference in a private backing field, there are also OnGetChildren() and OnSetChildren() methods you can override. The code is slightly more complex, but is very prescriptive (you either do it right or it won't work :) ) - but I see this as an edge case too, and so I'm not worried if it is a little more complex.

On the whole I'm pretty pleased with this approach. It automates as many cases as can be automated without using reflection, but provides a great deal of extensibility and flexibility for those who don't want to use managed backing fields.
