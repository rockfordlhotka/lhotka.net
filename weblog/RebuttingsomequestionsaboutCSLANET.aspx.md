---
title: Rebutting some questions about CSLA .NET
postDate: 2007-09-22T14:36:43.135-05:00
abstract: 
postStatus: publish
---
22 September 2007

I recently received this email, and wanted to share my reply.


> Rocky,
>
> Our company is going through a transformation in the way we do software.  We’re a very large company with offices all over the world, and it’s only my location that is using CSLA at this point.  We’ll now we’re faced with defending our decisions to use CSLA as the rest of the company attempts to create a “toolbox” of approved methodologies for development.  Normally I would think this is a good idea, but it seems to me that the people providing the recommendations, who interviewed us, don’t seem to have things right, especially when it comes to CSLA.
>
> Now, I figure I can create my arguments just fine… however, I think your help would be very valuable.  Here is a list of comments made about CSLA that I feel I have to clarify or defend.  Personally, I know they are blatantly wrong, but nevertheless, they seem to be common misconceptions about CSLA.  What do you think?  Again, these are not my comments, just misconceptions that I’m hearing from the rest of the company that I need to clear up.  Also, one of the key misconceptions here is that we should use Enterprise Library as a replacement for CSLA, again, they don’t understand what CSLA  .NET is for
>
> Misconceptions:
>
> 1. CSLA .NET is an older concept, ported to .Net, unlike Enterprise Library which was written for .Net.
>
> 2. Many CSLA features can be accomplished with Enterprise Library.
>
> 3. CSLA .NET is a “niche” framework, when compared to the widely accepted Enterprise Library.
>
> 4. CSLA .NET was not built with new technologies like WPF or WCF in mind.
>
> 5. CSLA .NET is component based and wasn’t designed to take advantage/or be compatible with SOA.
>
> 6. CSLA .NET, tied to its legacy, looks at the future of .NET and the adoption of SOA as merely an afterthought.
>
> Those are the key misconceptions that I feel I have to address… any help you can provide in formulating my arguments would be greatly appreciated.
>
> Thanks!
>
> Jimbo


My reply follows:

Jimbo,

#### ***1. CSLA .NET is an older concept, ported to .Net, unlike Enterprise Library which was written for .Net.***

That is not strictly true. There is a strong and complete break between the COM-based CSLA and CSLA .NET. No code carried forward, and realistically the concepts in CSLA .NET were enabled by .NET itself, and have little to do with the limited world of COM.

It is true that CSLA uses some OO concepts that have been around for a long time. These concepts have stood the test of time, and have proven to be very valuable for designing and building software. It would be foolish to discard great ideas just because they've had time to age. That'd be like discarding the wheel because it is an older concept...

It is also important to recognize that CSLA .NET and Enterprise Library are entirely complementary. CSLA .NET solves a set of problems not addressed by EntLib, and EntLib solves a set of problems not addressed by CSLA .NET.

#### ***2. Many CSLA features can be accomplished with Enterprise Library.***

Again, EntLib is complimentary to CSLA .NET. Things like logging, caching, data access, configuration and logging are outside the scope of CSLA .NET.

Things like validation, authorization, data binding support and location transparency for n-tier development are the focus of CSLA .NET.

While EntLib does have a validation module, it is architecturally unsound, putting the business logic into the UI layer rather than encapsulating it in a separate business layer.

#### ***3. CSLA .NET is a “niche” framework, when compared to the widely accepted Enterprise Library.***

There is no doubt that using a niche framework is a risk. And any organization using CSLA .NET must be aware of the nature of the framework in that regard.

However, it is also important to realize that CSLA .NET is the most widely used framework of its kind in .NET. Yes, EntLib is more widely used, but it does not duplicate or replace what CSLA .NET provides.

If you don’t use CSLA .NET, you *still need to solve the problems it addresses*. Like it or not, there are gaps in .NET around data binding, validation, authorization and so forth. Gaps that CSLA .NET solves. As do other products like NetTiers, LLBLGen, Ideablade and others. Some commercial, some not.

But none have the broad user base of CSLA .NET at this point in time.

I’ve had several people approach me at conferences to point out that they replicated CSLA .NET. They’d read my book, didn’t want to use a “niche framework” and set out to do their own thing. Months later they looked at their app and realized that they’d re-solved all those same problems. Addressed all those same gaps. And that they’d largely recreated CSLA .NET. Usually they are sad about this, realizing just how much time they wasted recreating a framework that already exists.

#### ***4. CSLA .NET was not built with new technologies like WPF or WCF in mind.***

This is patently untrue. Sorry, but CSLA .NET 2.0 was written *specifically* with WCF and WPF in mind. I am on steering groups within Microsoft, and so help shape the nature of many of these developer-oriented products. I knew years ahead of time the basic shape and nature of .NET 3.0, and so in 2005 CSLA .NET was already prepared for these new technologies.

While most of the other bullets in the assessment are reasonable and well-considered (though I clearly dispute some conclusions), this bullet is simply absurd and discounts the many hundreds of hours of work I’ve put in over the past four or so years ensuring that CSLA .NET provides a seamless and transparent upgrade path from Windows Forms and Web Forms to WPF, and from Web services or Remoting to WCF.

I challenge you to find another framework that will allow a switch from Web services or Remoting to WCF through a simple configuration file change. And yet I accomplished this in CSLA .NET by preparing for these technologies way back in 2004 and 2005.

#### ***5. CSLA .NET is component based and wasn’t designed to take advantage/or be compatible with SOA.***

There are two aspects here.

First, CSLA is a brand. Whether “component-based scalable logical architecture” is still accurately descriptive (it isn’t) doesn’t even matter anymore, because the brand is what it is. In other words, don’t read too much into the name – I’m stuck with it.

Second, there is no doubt that CSLA is designed to support n-tier client/server architectures. Such architectures are currently the best way to build interactive applications with WPF, Windows Forms and Web Forms interfaces. Like it or not, SOA simply has too much overhead and is too high-cost to be effective for most interactive application development.

It would be foolish to consider that object-oriented design is dead in the face of SOA. Or workflow. In fact, they are highly complimentary.

A service or a workflow activity are, by definition, both atomic units of functionality. If they aren’t, then you are doing them wrong.

Effectively every service and every activity are “mini-applications”. They are also effectively a use case, from an OOD perspective.

Thus you can (and often should) design and implement your services and activities using OO concepts. And CSLA .NET is all about making it easier to apply OOD/P when building applications.

As a result, whether you are building applications that consume services or that provide services or activities, CSLA .NET is a great help.

#### ***6. CSLA .NET, tied to its legacy, looks at the future of .NET and the adoption of SOA as merely an afterthought.***

The reality is that CSLA .NET has been able to largely shield its users from the rapidly increasing rate of change and chaos in the Microsoft platform space. By enforcing a clear delineation between UI and business code, and by supporting .NET standard interfaces for data binding and other .NET features, CSLA .NET continues to act as a valuable buffer, allowing valuable business logic to easily move forward through time, even as interface technologies change and change and change.

More time is spent on “future-proofing” both CSLA .NET, and more importantly the users of CSLA .NET, from changes to Microsoft’s platform than any other feature of the framework. Clearly it is impossible to abstract all the changes Microsoft comes up with, but CSLA .NET strives to protect that which is most important and costly to build and maintain: your business rules and logic.
