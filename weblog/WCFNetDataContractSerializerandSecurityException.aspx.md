---
title: WCF NetDataContractSerializer and SecurityException
postDate: 2007-06-01T12:34:14.128-05:00
abstract: The NDCS appears to have a bug...
postStatus: publish
---
01 June 2007

The WCF NetDataContractSerializer is an almost, but not quite perfect, replacement for the BinaryFormatter.

The NDCS is very important, because without it WCF could never be viewed as a logical upgrade path for either Remoting or Enterprise Services users. Both Remoting and Enterprise Services use the BinaryFormatter to serialize objects and data for movement across AppDomain, process or network boundaries.

Very clearly, since WCF is the upgrade path for these core technologies, it had to include a serialization technology that was functionally equivalent to the BinaryFormatter, and that is the NDCS. The NDCS is very cool, because it honors both the Serializable model and the DataContract model, and even allows you to mix them within a single object graph.

Unfortunately I have run into a serious issue, where the NDCS is not able to serialize the System.Security.SecurityException type, while the BinaryFormatter has no issue with it.

The issue shows up in CSLA in the data portal, because it is quite possible for the server to throw a SecurityException. You'd like to get that detail back on the client so you can tell the user why the server call failed, but instead you get a "connection unexpectedly closed" exception instead. The reason is that WCF itself blew up when trying to serialize the SecurityException to return it to the client. So rather than getting any meaningful result, the client gets this vague and nearly useless exception instead.

By the way, if you want to see the failure, just run this code:

Dim buffer As New System.IO.MemoryStream
    Dim formatter As New System.Runtime.Serialization.NetDataContractSerializer
    Dim ex As New System.Security.SecurityException("a test")
    formatter.Serialize(buffer, ex)

And if you want to see it not fail run this code:

Dim buffer As New System.IO.MemoryStream
    Dim formatter As New System.Runtime.Serialization.Formatters.Binary.BinaryFormatter
    Dim ex As New System.Security.SecurityException("a test")
    formatter.Serialize(buffer, ex)

I've been doing a lot of work with the NDCS over the past several months. And this is the first time I've encountered a single case where NDCS didn't mirror the behavior of the BinaryFormatter - which is why I do think this is a WCF bug. Now just to get it acknowledged by someone at Microsoft so it can hopefully get fixed in the future...

The immediate issue I face is that I'm not entirely sure how to resolve this issue in the data portal. One (somewhat ugly) solution is to catch all exceptions (which I actually do anyway), and then scan the object graph that is about to be returned to the client to see if there's a SecurityException in the graph. If so perhaps I could manually invoke the BinaryFormatter and just return a byte array. The problem with that is in the case where the object graph is a mix of Serializable and DataContract objects - in which case the BinaryFormatter won't work because it doesn't understand DataContract...

In the end I may just have to leave it be, and people will need to be aware that they can never throw a SecurityException from the server...
