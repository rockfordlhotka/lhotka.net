---
title: Authors can't win
postDate: 2005-08-11T14:54:09.265625-05:00
abstract: Authors can't win. All we can do is choose the sub-group from which we're going to get nasty emails...
postStatus: publish
---
11 August 2005

Like any author who writes practical, pragmatic content I am constantly torn. Torn between showing how to write maintainable code vs fast code. Between distilling the essence of an idea vs showing a complete solution that might obscure that essence.<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p>

Just at the moment I'm building a demo application, including its database. Do I create the best database I can, hopefully showing good database design techniques and subsequently showing how to write an app against an "ideal" database? Or do I create the database to look more like the ones I see when I go to clients - so it will have good parts and some parts that are obviously ill-designed. This latter approach allows me to show how to write an app against what I believe to be a more realistic database.<o:p></o:p>

I'm opting for the latter approach. Yet sitting here right now, I know that I'll get lots of emails (some angry) berating me for creating and/or using such a poor database in a demo. "Demos should show the *right* approach" and so forth. Of course if I were to use a more ideal database design I'd get comments at conferences (some angry) because my demo app "isn't realistic" and only works in "a perfect world".<o:p></o:p>

See, authors can't win. All we can do is choose the sub-group from which we're going to get nasty emails...<o:p></o:p>

But that's OK. The wide diversity of viewpoints in our industry is one of our collective strengths. Pragmatists vie against idealists, performance-hounds vie against those focused on maintainability. Somewhere in the middle is reality – the cold, hard reality that none of us have the time to write performant, maintainable code using perfect implementations of all best practices and known design patterns. Somewhere in the middle are those hard choices each of us makes to balance the cost of development vs the cost of licensing vs the cost of hardware vs the cost of maintenance vs the cost of performance.<o:p></o:p>

I think ultimately that this is why computer books don’t sell in the numbers you’d expect. If there are 7+ million developers, why does a good selling computer book sell around 20,000 copies?<o:p></o:p>

(The exceptions being end-user books and theory books. End-user books because end users just want the answers, and theory books because they often rise above the petty bickering of the real world. Every faction can interpret theory books to say what they like to hear, so everyone likes that kind of book. Theory books virtually always “reinforce” everyone’s different world views.)<o:p></o:p>

I think the reason “good selling” books do so poorly though. Only a subset or faction within the computer industry will agree with any given book. That faction tends to buy the book. Other factions might be a few copies, but they get a bad taste in their mouths when reading it, so they don’t recommend or propagate the book. Instead they find other books that *do agree* with their world view.<o:p></o:p>

Note that I’m not complaining. Not at all! <o:p></o:p>

I’m merely observing that C# people won’t (as a general rule) buy a VB book, and Java people won’t buy a C# book. OO people won’t buy a book on DataSet usage, and people who love DataSets won’t waste money on an OO book. People who love the super-complex demos from Microsoft really hate books that use highly distilled examples, while people who just want the essence of a solution really hate highly complex examples (and thus the books that use them).<o:p></o:p>

As I write the 2<sup>nd</sup> editions of my Business Objects books I’m simultaneously writing both VB and C# editions. Several people have asked whether it wouldn’t be better to interleave code samples, have both languages in the book or *something* so that I don’t produce two books. But publishers have tried this. And the reality is that C# people don’t like to buy books that contain *any* VB code (and visa versa). Mixed language books simply don’t sell as well as single-language books. And like it or not, the idea behind publishing books is to sell them – so we do what sells.<o:p></o:p>

But that solution doesn’t work for realistic vs idealistic database designs – which is my current dilemma. You can’t really write a book twice – once with an ideal database and once with a more realistic one. Nor can you really double the size (and thus cost) of a book to fit both ideas into it at once.<o:p></o:p>

So I’m settling for the only compromise I can find. Parts of my database are pretty well designed. Other tables are obviously very poor. Thus some of my forms are trivial to create because they come almost directly from the “ivory tower”, while other forms rely on more complex and less ideal techniques because they come from the ugly world of reality.<o:p></o:p>

Maybe this way I can get nasty emails from *every* group :)<o:p></o:p>
