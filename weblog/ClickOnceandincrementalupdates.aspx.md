---
title: ClickOnce and incremental updates
postDate: 2008-05-20T10:00:29.5934608-05:00
abstract: 
postStatus: publish
---
20 May 2008

I was just in a discussion about ClickOnce with several people, include Brian Noyes, who wrote the book on ClickOnce.

I was under the mistaken impression, and I know quite a few other people who have this same misconception, that ClickOnce downloads complete new versions of your application each time you publish a new version. In fact, I know of at least a couple companies who specifically chose not to use ClickOnce because their app is quite large, and re-downloading the whole thing each time a new version is published is unrealistic.

It turns out though, that ClickOnce does optimize the download. When you publish a new version of your app, all the new files are written to the server, that is true. But the client only downloads changed files. All unchanged files are copied from the previous install folder *on the client* to the new install folder *on the client*.

In other words, all unchanged files are reused from the copy already on the client, and so are not downloaded again. Only changed files are downloaded from the server.

The trick to making this work is to only rebuild assemblies that have actually changed before you do a publish. Don't rebuild unchanged assemblies, because that could change the assembly - and even a one byte change in the assembly would cause it to be downloaded because the file hash would be different.

Saying that gives me flashbacks to binary compatibility issues with VB6, but it makes complete sense that they'd have to use something like a file hash to decide whether to re-download each file.
