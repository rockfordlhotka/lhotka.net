---
title: Xamarin.Forms has some potential
postDate: 2014-06-18T22:45:08.7465106-05:00
abstract: 
postStatus: publish
---
18 June 2014

A couple of us at [Magenic](http://www.magenic.com) have been spending some time looking into the new [Xamarin.Forms](http://xamarin.com/forms) technology.

[![thQCCPSC1G](binary/WindowsLiveWriter/Xamarin.Formshassomepotential_13FF3/thQCCPSC1G_thumb.jpg "thQCCPSC1G")](binary/WindowsLiveWriter/Xamarin.Formshassomepotential_13FF3/thQCCPSC1G_2.jpg)

It has some nice potential, but is clearly at the prototype stage more than the ready-for-use stage.

The good potential centers around the start of a XAML dialect they’ve created that describes common UI elements and concepts across iOS, Android, and Windows Phone 8 (Silverlight). Using this dialect you can’t get at all the features of each platform, but you can get at enough features to create standard data entry and data viewing forms like you’d need for a typical business application. And there’s always an easy escape hatch that allows you to build per-platform forms for when a common form just isn’t enough.

The bad points are areas I hope they’ll address soon so the technology becomes more useful for real work.

The first roadblock is the almost complete lack of documentation or samples showing how to use their XAML dialect. They have samples showing how to build forms in C#, but not in XAML. It reminds me of the first few months when Microsoft introduced XAML for WPF.

Perhaps it is because of the lack of XAML samples/docs, but it is a real struggle to figure out how to do things like async loading of data, full implementations of data binding against standard data binding types, etc.

I think this whole thing has potential. WPF was really rough when it was introduced, and eventually Microsoft improved the docs and samples and designer tools. And they eventually smoothed over the most egregious data binding issues, allowing the vast majority of existing .NET types to bind into WPF.

I really hope Xamarin does the same thing with this technology.
