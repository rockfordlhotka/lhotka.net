---
title: Serializing business objects to Silverlight/AJAX?
postDate: 2007-11-05T23:53:58.514-06:00
abstract: 
postStatus: publish
---
05 November 2007



I was recently asked how to get the JSON serializer used for AJAX programming to serialize a CSLA .NET business object.

From an architectural perspective, it is better to view an AJAX (or Silverlight) client as a totally separate application. That code is running in an untrusted and terribly hackable location (the user’s browser – where they could have created a custom browser to do anything to your client-side code – my guess is that there’s a whole class of hacks coming that most people haven’t even thought about yet…)

So you can make a strong argument that objects from the business layer should never be directly serialized to/from an untrusted client (code in the browser). Instead, you should treat this as a service boundary – a semantic trust boundary between your application on the server, and the untrusted application running in the browser.

What that means in terms of coding, is that you don’t want to do some sort of field-level serialization of your objects from the server. That would be terrible in an untrusted setting. To put it another way - the BinaryFormatter, NetDataContractSerializer or any other field-level serializer shouldn't be used for this purpose.

If anything, you want to do property-level serialization (like the XmlSerializer or DataContractSerializer or JSON serializer). But really you don’t want to do this either, because you don’t want to couple your service interface to your internal implementation that tightly. This is, fundamentally, the same issue I discuss in Chapter 11 of *Expert 2005 Business Objects* as I talk about SOA.

Instead, what you really want to do (from an architectural purity perspective anyway) is define a service contract for use by your AJAX/Silverlight client. A service contract has two parts: operations and data. The data part is typically defined using formal data transfer objects (DTOs). You can then design your client app to work against this service contract.

In your server app’s UI layer (the aspx pages and webmethods) you translate between the external contract representation of data and your internal usage of that data in business objects. In other words, you map from the business objects in/out of the DTOs that flow to/from the client app. The JSON serializer (or other property-level serializers) can then be used to do the serialization of these DTOs - which is what those serializers are designed to do.

This is a long-winded way of saying that you really don’t want to do JSON serialization directly against your objects. You want to JSON serialize some DTOs, and copy data in/out of those DTOs from your business objects – much the way the SOA stuff works in Chapter 11.
