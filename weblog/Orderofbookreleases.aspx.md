---
title: Order of book releases
postDate: 2006-03-19T22:36:08.765625-05:00
abstract: A number of people have asked why the C# edition of my new Business Objects book is coming out before the VB edition. Here's the answer.
postStatus: publish
---
19 March 2006

A number of people have asked why the C# edition of my new [Business Objects](http://www.lhotka.net/cslanet/csla20.aspx) book is coming out before the VB edition. And yes, that is the case. The C# book should be out around the end of March, and the VB book about 2-3 weeks later.

As I've said before, I wrote the books "concurrently". Which really means I wrote one edition, knowing full well that I'd be coming through later to swap out all the code bits and change a few of the figures. It really didn't matter to me which one I did first, because I was going to have to go through every chapter to do this swapping process either way.

I *did* write the actual framework and sample app in VB first. The initial port to C# was handled by a fellow [Magenicon](http://www.magenic.com), Brant Estes. Believe it or not, he had the initial compilable code done in about three days! I am thinking he didn't do a whole lot of sleeping (because he did the port by hand, not with a tool - which is *awesome*, because it means the code style and quality is far higher).

I could give you a fluffy (if somewhat true) answer, that the reason I did the C# book first was to ensure that the C# code was fully tested and brought entirely into line with the VB code. And there really is some truth to that. By doing the C# edition first, I was able to go through every line and recheck, tweak and enhance that code. Several large chunks of functionality were actually added or altered in C# first (during the writing process) and I back-ported them into the VB version of the code.

But the *real* reason is what a few people have speculated: dollars. For better or worse, the fact is that the .NET 1.0 C# book is outselling the VB book by quite a lot. Nearly 2:1 actually. Due to this, my publisher *really* wanted to get the C# edition out first. I initially pushed back, but I personally have no rational reason to do one before the other. I do love VB very much, but that's an irrational and emotional argument that simply doesn't hold a lot of sway...

(That said, if there was more than a couple week difference in release dates, I would have insisted on VB first, and I would have won that argument. But you must pick your battles, and it made no sense to me to have a fight with my publisher over which book came out 3 weeks before the other...)

For what its worth, porting the *book* is far, far easier than porting (and maintaining) the *code.* I've said it before, and I'm sure I'll say it again, maintaining the same code in two languages is just a pain. Converting the book was a relatively rote process of copy-paste, copy-paste, copy-paste. But converting the code means retesting, double-checking and almost certainly *still* missing a thing or two...

Anyway, I thought I'd blog this just to make the order of release totally clear. For better or worse, it was simply a business decision on the part of my publisher.
