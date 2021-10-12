---
title: CSLA 4 version 4.3.0 alpha available
postDate: 2012-01-26T13:15:02.8723642-06:00
abstract: 
postStatus: publish
---
26 January 2012

I have posted an alpha version of CSLA 4 version 4.3.0 for download from the [CSLA download page](http://www.lhotka.net/cslanet/download.aspx).

Although Jonny has been extremely busy with a number of bug fixes and some feature changes, I think the biggest change in this alpha release is a major optimization of the [MobileFormatter](http://www.lhotka.net/weblog/CSLALightObjectSerialization.aspx).

MobileFormatter is used to serialize object graphs on Silverlight and Windows Phone. It is used by the data portal, and n-level undo (if you use that feature).

Until now, I have recommended that you use compression on the byte stream that flows over the data portal, because the XML created by the MobileFormatter is often quite large. It compresses efficiently, and we’re quite efficient about what we put into the byte stream, but it is just plain big.

Sergey did some really nice work for version 4.3, allowing the use of alternate reader/writer objects so the data can be serialized into something other than XML. Specifically, he created binary reader and writer objects that are around 70% more efficient in terms of byte stream size. That’s about as much as you could expect to get with compression!

The result is that you can probably avoid the CPU intensive overhead of compression and still get a small byte stream to transfer over the network.

The [CSLA 4 version 4.3.0 change log](http://www.lhotka.net/Article.aspx?area=4&amp;id=1c287e08-d428-4c27-b538-d588e3c55775) includes a discussion of the configuration settings you need to change to use the new reader/writer objects.

This is a non-breaking change, because the default is the same behavior as in 4.2. But this is a *big change* and we really appreciate your help in testing the new reader/writer objects to ensure they work across a wide range of applications.
