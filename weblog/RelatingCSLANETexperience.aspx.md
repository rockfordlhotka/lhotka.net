---
title: Relating CSLA .NET experience
postDate: 2010-01-26T11:29:00.0757471-06:00
abstract: 
postStatus: publish
---
26 January 2010

From time to time CSLA .NET users are able to provide me with a summary of their experiences with the framework. Here’s an account I thought I’d share (with permission of course). First, here are some useful links related to A.J.’s summary:

- [Purchase ebooks and training videos here](http://store.lhotka.net/)
- [Get information about code generators here](http://www.lhotka.net/cslanet/codegen.aspx)


Now to A.J.’s comments:

*To all those who struggle with CSLA:*

*I must admit that at the beginning I had a hard time with CSLA. I remember when I first looked at the ver. NET 2.0, it seemed that there were dozens of objects all over the place and it simply appeared overdeveloped. The whole move to .NET from VB6 seemed even more discouraging to me.*

*The good thing is that I am stubborn (must be my Slovak origin). I was equally determined to understand why particular approach was chosen, what exactly was the author (Rocky) thinking, what were his findings? So I started way back at VB6 Business Objects book. Shortly after that I moved to first VB.NET Business Objects and then the 2005…story continues.*

*At some point I had an idea to strip CSLA, make it leaner, less bloated. I figured “why not have some type of a framework that entirely runs locally and doesn’t need any of this extra stuff?”*

*So I started to strip out serialization, reflection (Data Portal), remoting, n-level undo, trimming validation rules, created new code gen templates, and I soon realized that I was gaining nothing other than trouble, wasting time, and giving away a lot not to mention that this new “low fat” thing of mine needed some serious testing and documentation. It is obvious that I didn’t “get it”.*

*Well, I went through the 2005 book again, this time at the slower pace. And again, and again. PT Tracker helps for sure.  Eventually it started to make sense. If you write down what functionality and behavior you would like to have in your business object and data access object, you soon realize that CSLA has it all and does it better that you originally wanted. A true "E pour si muove" moment for me.*

*I guess the message is not to give up. Everything that is there needs to be there. The alternatives were to try to make some sense of data sets, data islands, relations, contexts, EF, and who knows what else out of which none include comprehensive validation, authorization, and simplistic object relation.*

*Invest your time in CSLA. Get a decent code generation tool that has CSLA templates or write your own templates.*

*It's good for you. Have fun!*

*A.J.*

*Santa Monica, CA*

[![clip_image001](binary/WindowsLiveWriter/RelatingCSLA.NETexperience_912A/clip_image001_1d5964cf-f94b-44d7-8146-f7c4a546b236.jpg "clip_image001")](http://public.blu.livefilestore.com/y1pvTRhlVRGnmuHUOVytaW5Kg79T6KaBKfK4rse8UC4USLV3G6haGo-Ni4Am0J9NnjeIBBMir7eRxcuskW5Os1qTQ/IMG_0347.jpg?download)  [![clip_image001\[4\]](binary/WindowsLiveWriter/RelatingCSLA.NETexperience_912A/clip_image001%5B4%5D_1bc463ed-ae85-42af-927d-288bc13ed06b.jpg "clip_image001[4]")](http://public.blu.livefilestore.com/y1pV17qsesCakg6raPzMOHC3KmnkhjuETEmw6m2wgM_mcUmIInHOqMoM7-7qteinrSBmL3dJiACu6sArHRmC98d7g/IMG_0345.jpg?download)
