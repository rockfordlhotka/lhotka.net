---
title: .NET Serialization wrappers
postDate: 2009-02-10T15:24:10.82412-06:00
abstract: 
postStatus: publish
---
10 February 2009

A ridiculously long time ago I was in a meeting at Microsoft, sitting next to Ted Neward. As you may know, Ted lives in both the Java and .NET worlds and kind of specializes in interop between them.

Somehow (and I don’t remember the specifics), we got to talking about object serialization and related concepts like encryption, signing and so forth. It turned out that Java had a library of wrapper types that worked with the serialization concept to make it very easy to sign and encrypt an object graph.

Thinking about this, it isn’t hard to imagine this working in .NET, and so I whipped up a similar library concept. I’ve used it from time to time myself, but never quite got around to putting it online for public consumption. Until now:

[Download the SerializationWrapper solution](http://www.lhotka.net/files/SerializationWrapper-090210.zip)

The download includes nunit tests, so you can figure out how to use it pretty easily by looking at those.

For example, to sign a serializable object graph, just do this:


> SignedWrapper&lt;string&gt; wrapper = new SignedWrapper&lt;string&gt;(data, hashKey);


You can then send the wrapper over the network as long as it is serialized using the BinaryFormatter or NetDataContractSerializer, and on the other end you can make sure it hasn’t been tampered with by verifying the signature:


> if (wrapper.Verify(hashKey))


Of course the really tricky part is key exchange. How did both ends of the process get access to the same hashKey value? That’s outside the scope of my library, and frankly that is the really hard part about things like security…

In fact, if you look inside the code for the various wrapper classes, you’ll find that I’m just delegating all the interesting work to the .NET cryptography subsystem. By using the various wrappers together you can do asymmetric public/private keys, symmetric keys. You can do signing, and encryption. I think I now cover all the different algorithms supported by .NET – in one nicely abstract scheme.

Also, if you look inside the solution you’ll see a compression wrapper. That was an experiment on my part, and I really didn’t find the result satisfying. My thought was that you’d wrap your object graph (maybe after it was encrypted and signed) in the compression wrapper, and then *that* would be serialized to go over the wire.

But it turns out that there are two flaws:

1. Serializing the compressed data makes it quite a bit bigger, and you are better off transferring the CompressedData value from the wrapper rather than allowing the wrapper itself to be serialized.
2. More importantly, compressing encrypted data doesn’t work well. Encrypted data is pretty random, and the two compression algorithms included in .NET don’t do a particularly good job of compressing that data. I don’t know if other algorithms are better at compressing encrypted data, but I was disappointed with the results I found here.


In any case, I’ve found the crypto wrapper classes to be generally useful in abstracting most of the complexity of dealing with the .NET crypto subsystem, and I thought I’d share the code in case anyone else can find it useful as well.
