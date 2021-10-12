---
title: It is only 8, how can it be legacy???
postDate: 2009-11-04T21:20:16.7841055-06:00
abstract: 
postStatus: publish
---
04 November 2009

Of course I’m referring to Windows Forms, which is about 8 years old. Even in dog years that’s not old. But in *software years* it is pretty old I’m afraid…

I’m writing this post because here and in other venues I’ve recently referred to Windows Forms as “legacy”, along with asmx and even possibly Web Forms. This has caused a certain amount of alarm, but I’m not here to apologize or mollify.

Technologies come and go. That’s just life in our industry. I was a DEC VAX guy for many years (I hear Ted Neward laughing now, he loves these stories), but I could see the end coming years before it faded away, so I switched to the woefully immature Windows platform (Windows 3.0 – what a step backward from the VAX!). I know many FoxPro people who transitioned, albeit painfully, to VB or other tools/languages. The same with Clipper/dBase/etc. Most PowerBuilder people transitioned to Java or .NET (though much to my surprise I recently learned that PowerBuilder still actually exists – like you can still buy it!!).

All through my career I’ve been lucky or observant enough to jump ship before any technology came down on my head. I switched to Windows before the VAX collapsed, and switched to .NET before VB6 collapsed, etc. And honestly I can’t think of a case where I didn’t feel like I was stepping back in time to use the “new technology” because it was so immature compared to the old stuff. But every single time it was worth the effort, because I avoided being trapped on a slowly fading platform/technology with my skills becoming less relevant every day.

But what is “legacy”? I once heard a consultant say “legacy is anything you’ve put in production”. Which might be good for a laugh, but isn’t terribly useful in any practical sense.

I think “legacy” refers to a technology or platform that is no longer an area of focus or investment by the creator/maintainer. In our world that mostly means Microsoft, and so the question is where is Microsoft focused, where are they spending their money and what are they enhancing?

The answers are pretty clear:

- Azure
- Silverlight
- ASP.NET MVC
- WPF (to a lesser degree)
- ADO.NET EF
- WCF


These are the areas where the research, development, marketing and general energy are all focused. Ask a Microsoft guy what’s cool or hot and you’ll hear about Azure or Silverlight, maybe ADO.NET EF or ASP.NET MVC and possibly WPF or WCF. But you won’t hear Windows Forms, Web Forms, asmx web services, Enterprise Services, Remoting, LINQ to SQL, DataSet/TableAdapter/DataTable or numerous other technologies.

Some of those other technologies aren’t legacy – they aren’t going away, they just aren’t sexy. Raw ADO.NET, for example. Nobody talks about that, but ADO.NET EF can’t exist without it, so it is safe. But in theory ADO.NET EF competes with the DataSet (poorly, but still) and so the DataSet is a strong candidate for the “legacy” label.

Silverlight and WPF both compete with Windows Forms. Poor Windows Forms is getting no love, no meaningful enhancements or new features. It is just there. At the same time, Silverlight gets a new release in less than 12 month cycles, and WPF gets all sorts of amazingly cool new features for Windows 7. You tell me whether Windows Forms is legacy. But whatever you decide, I’m surely spending zero cycles of my time on it.

asmx is obvious legacy too. Has been ever since WCF showed up, though WCF’s configuration issues have been a plague on its existence. I rather suspect .NET 4.0 will address those shortcomings though, making WCF as easy to use as asmx and driving the final nail in the asmx coffin.

Web Forms isn’t so clear to me. All the buzz is on ASP.NET MVC. That’s the technology all the cool kids are using, and it really is some nice technology – I like it as much as I’ll probably ever like a web technology. But if you look at .NET 4.0, Microsoft has done some really nice things in Web Forms. So while it isn’t getting the hype of MVC, it is still getting some very real love from the Microsoft development group that owns the technology. So I don’t think Web Forms is legacy now or in .NET 4.0, but beyond that it is hard to say. I strongly suspect the fate of Web Forms lies mostly in its user base and whether they fight for it, whether they make Microsoft believe it continues to be worth serious investment and improvement into the .NET 5.0 timeframe.

For my part, I can tell you that it is amazingly (impossibly?) time-consuming to be an expert on 7-9 different interface technologies (UI, service, workflow, etc). Sure CSLA .NET supports *all of them*, but there are increasing tensions between the stagnant technologies (most notably Windows Forms) and the vibrant technologies like Silverlight and WPF. It is no longer possible, for example, to create a collection object that works with all the interface technologies – you just can’t do it. And the time needed to deeply understand the different binding models and subtle differences grows with each release of .NET.

CSLA .NET 4.0 will absolutely still support all the interface technologies. But it would be foolish to cut off the future to protect the past – that way lies doom. So in CSLA .NET 4.0 you should expect to see support for Windows Forms still there, but probably moved into another namespace (Csla.Windows or something), while the main Csla namespace provides support for modern interface technologies like WPF, ASP.NET MVC, Silverlight, etc.

I am absolutely committed to providing a window of time where Windows Forms users can migrate their apps to WPF or Silverlight while still enjoying the value of CSLA .NET. And I really hope to make that reasonably smooth – ideally you’ll just have to change your base class types for your business objects when you switch the UI for the object from Windows Forms to XAML – though I suspect other minor tweaks may be necessary as well in some edge cases.

But let’s face it, at some point CSLA .NET does have to drop legacy technologies. I’m just one guy, and even with Magenic being such a great patron it isn’t realistic to support every technology ever invented for .NET :)  I don’t think the time to drop Windows Forms is in 4.0, because there are way too many people who need to migrate to WPF over the next 2-3 years.

On the other hand, if you and your organization aren’t developing a strategy to move off Windows Forms in the next few years I suspect you’ll eventually wake up one day and realize you are in a bad spot. One of those spots where you can’t hire anyone because no one else has done your technology for years, and nobody really remembers how it works (or at least won’t admit they do unless you offer them huge sums of money).

I don’t see this as bad. People who want stability shouldn’t be in computing. They should be in something like accounts receivable or accounts payable – parts of business that haven’t changed substantially for decades, or perhaps centuries.
