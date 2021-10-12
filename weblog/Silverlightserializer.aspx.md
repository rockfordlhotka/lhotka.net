---
title: Silverlight serializer
postDate: 2008-04-13T20:42:40.513-05:00
abstract: 
postStatus: publish
---
13 April 2008

Silverlight 2.0 doesn't have an equivalent to the BinaryFormatter or NetDataContractSerializer. This makes some things quite challenging - in my case building CSLA Light. CSLA .NET requires high-fidelity serialization both for implementation of the Clone() operation and within the data portal.

I've been working on building a Silverlight-compatible equivalent to the BinaryFormatter/NDCS. It turns out to be quite hard due to the limitations of the Silverlight sandbox.

For example, Silverlight does have reflection, even against private fields. However, you can only get or set a private field with code *inside the same class as the field declaration*. You can't get/set a field from another object, or even from a base class or subclass. The reflection call must be *in the same class*!

At this point I have a [prototype serializer](http://www.lhotka.net/files/cslalight/cslalight-3.5.0-080413.zip) that works in some limited scenarios. It is a starting point. Some aspects aren't ideal, but may just be the way they are to get around how Silverlight works. Still, the end result is relatively cool.

To use the serializer:

1. Build the Csla project (it is a Silverlight Class Library) and reference it from your Silverlight application
2. In your business class, add a using/Imports statement for Csla.Serialization
3. Add the Serializable attribute to your class
4. You class must also *either* inherit from MobileObject or implement the IMobileObject interface (I recommend using inheritance, as otherwise you'll have to write a lot of nasty code)
5. You *must* override GetValue() and SetValue() in your class - these methods are called by the MobileFormatter so *you* can reflect against your private fields. See the example below to see how this works
6. You can now use the MobileFormatter much like you would the BinaryFormatter. See the example below


The MobileFormatter is far from complete. But it can serialize/deserialize fields of an object that contain primitive types (anything that works with Convert.ChangeType()). And it handles references to other serializable objects, both single objects and lists of serializable objects (if they implement IMobileObject or inherit from MobileList&lt;T&gt; ).

I'm pretty sure it can't handle arrays, nor can it handle any list type other than (effectively) List&lt;T&gt;. I'm not sure what it will do with enums or other types - just haven't gotten that far yet.

Here's a serializable object:


> using System;
> using Csla.Serialization;
>
> namespace SilverlightApplication1
> {
>   [Serializable]
>   public class Person : MobileObject
>   {
>     #region Serialization
>
> protected override object GetValue(System.Reflection.FieldInfo field)
>     {
>       if (field.DeclaringType == typeof(Person))
>         return field.GetValue(this);
>       else
>         return base.GetValue(field);
>     }
>
> protected override void SetValue(System.Reflection.FieldInfo field, object value)
>     {
>       if (field.DeclaringType == typeof(Person))
>         field.SetValue(this, value);
>       else
>         base.SetValue(field, value);
>     }
>
> #endregion
>
> public string Name { get; set; }
>
> [NonSerialized]
>     private DateTime \_birthdate;
>     public DateTime BirthDate
>     {
>       get { return \_birthDate; }
>       set { \_birthdate = value; }
>     }
>   }
> }


And here's how to serialize/deserialize the object:


> var p = new Person();
>
> var formatter = new Csla.Serialization.MobileFormatter();
> var buffer = new System.IO.MemoryStream();
> formatter.Serialize(buffer, p);
>
> buffer.Position = 0;
> var copyOfP = (Person)formatter.Deserialize(buffer);


Though it is unfortunate that every business class must implement GetValue() and SetValue(), I think that is a relatively small price to pay to get nearly the same capability as we have in .NET with the BinaryFormatter in terms of cloning objects, and more importantly in terms of serializing them across the network with full fidelity.
