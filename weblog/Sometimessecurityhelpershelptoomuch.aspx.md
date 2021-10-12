---
title: Sometimes security helpers help too much
postDate: 2006-04-12T18:34:54.125-05:00
abstract: Download zip file in IE, unzip contents, open in VS 2005 - security violation - WTF?!?
postStatus: publish
---
12 April 2006

I don't know how long this behavior has existed, but the other day I ran into an interesting (and unpleasant) side-effect of Microsoft's focus on security. I am guessing lots of people have run into this before me, but it was frustrating nonetheless.<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p>

It turns out that when you download a zip file with IE onto an NTFS drive, IE kindly puts a note in the file system indicating that the zip file came from an untrusted source (the Internet). When you unzip the contents to an NTFS drive, Windows kindly propagates that note, so all the unzipped files are marked as having come from an untrusted source.<o:p></o:p>

In many cases you may not notice this flag. But if you unzip a VS 2005 solution like this and then try to open it VS will tell you it came from an untrusted source – possibly causing you some issues.<o:p></o:p>

So of course the first question I asked was “how do I get rid of this note/flag so I can do my work?” There are some answers however.<o:p></o:p>

You can go file-by-file and open each file’s properties dialog. Then you can click a button to mark it as trusted. You can’t do this at the folder level, only file-by-file. So this is pretty useless for a large number of source files.<o:p></o:p>

You can copy the zip file and/or the unzipped contents to a FAT drive and back to your NTFS drive. Since FAT can’t store this metadata about the files, it is lost and your files are “fixed”.<o:p></o:p>

You can use Firefox to download the zip file in the first place. Firefox doesn’t collaborate with Windows to protect you, so these security features (which I think are good in general terms). I’m not too thrilled by this discovery actually, as I think it illustrates a security hole (of sorts) in Firefox – at least as compared to IE.<o:p></o:p>

I think you can mark the zip file as trusted (through its properties dialog) *before* unzipping the contents. Unfortunately I haven’t tried this (I actually stopped with using Firefox, because it did solve my problem :) )
