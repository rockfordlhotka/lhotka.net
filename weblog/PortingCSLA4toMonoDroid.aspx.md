---
title: Porting CSLA 4 to MonoDroid
postDate: 2011-01-19T23:30:11.7093957-06:00
abstract: 
postStatus: publish
---
19 January 2011

I’ve started the process of porting CSLA .NET version 4.1 to [MonoDroid](http://monodroid.net/). I expected this to be relatively easy because I’ve already got a version of CSLA 4 running on WP7, and from everything I know about MonoDroid it should be pretty comparable (excluding anything to do with XAML and UI concepts of course).

After a couple hours of trying to get the Android emulator to run on my machine, I discovered that the hybrid C++ and Java worlds really don’t “get” Windows. They interpret Windows configuration in different ways. I’m not sure which one is lame and out of date (by around a decade), but either C++ or Java apparently needs help…

Fortunately some googling (with [Bing](http://bing.com) of course ![Smile](binary/Windows-Live-Writer/Porting-CSLA-4-to-MonoDroid_14308/wlEmoticon-smile_2.png)) turned up the answer in the form of an environment setting named ANDROID\_SDK\_HOME that both C++ and Java will honor. The problem is that my User directory isn’t on the C drive, and either C++ or Java can’t handle this concept. Setting ANDROID\_SDK\_HOME to the path of my actual User directory solves the issue so the emulator works as expected.

The Android emulator is *extremely* slow, but functional. Just deploying my tiny little test app takes several minutes, and my computer is no slouch. It is clear that Android developers don’t round-trip very fast in terms of running their code to see if it works. I feel sort of like I’m back in 1992 on a VAX where the compile-link-run cycle took minutes. I’m obviously very spoiled with the performance of things like the WP7 emulator or the ASP.NET development web server, where the compile-debug/run cycle takes seconds (at most).

The process of getting CSLA 4 to at least build in MonoDroid took around 4 hours of work. Not that I’m done, but the code does compile at this point. The holdups and issues are:

1. MonoDroid doesn’t have ObservableCollection and a set of related types, so I’ve started implementing them myself
2. MonoDroid doesn’t know about “Add service reference”, it only knows about “Add web reference”, and that means I need to create a new data portal proxy/host pair
3. It doesn’t look like the System.ServiceModel assembly that comes with MonoDroid actually works – my one remaining build error has to do with this assembly – and this probably means some other client-side data portal elements will be affected (like LocalProxy) – I think this indicates some bad factoring on the part of CSLA in terms of the client-side data portal implementation though, so in an odd way this might be beneficial in that the problem highlights a design flaw that needs fixing
4. There are some bugs in MonoDroid in VS, where setting some project properties “doesn’t take” – change the property values in VS and they aren’t saved to the project file – but edit the project file in a text editor and the changes are honored – not a big deal, and MonoDroid is in an early beta, so this sort of thing is to be expected
5. There’s no XAML or directly comparable concept on Android, so I’m not even trying to port Csla.Xaml, only the core Csla project – I’ll probably need to create a Csla.Android project with UI components appropriate to the Android UI technology


I mocked up the initial types to implement ObservableCollection, and it won’t take a lot more effort to make them have the functionality required by CSLA. I don’t feel the need to completely replicate those types – only the parts CSLA cares about.

Creating a data portal proxy/host pair isn’t hard, the data portal is designed with this sort of flexibility in mind. However, this will be the first non-WCF proxy/host pair I’ve built on the Silverlight/WP7 code base, so I’m looking forward to establishing that it is as easy as it should be.

The unexpected dependencies on System.ServiceModel are probably the most worrisome aspect of this project so far. I suspect unraveling the dependencies and fixing the design/implementation may lead to some breaking changes in the Silverlight/WP7 code. On the other hand, if my early suspicions are correct, the design is probably flawed and I’ll be able to improve things as a result.

The question is whether I leave the SL/WP7 code alone and just fix the dependencies in the Android code base. That’s probably what I’ll do in the 4.x timeframe, because I really try to avoid substantial breaking changes in point releases…

The loss of Csla.Xaml is not ideal. At the very least I think a Csla.Android project will need ViewModelBase and ViewModel, but I suspect other Android-related UI components may be required.

Anyway, I’m quite impressed by MonoDroid. It seems pretty complete, pretty functional, and pretty well integrated into Visual Studio. Other than my issues with the emulator configuration the install was painless.

To head off this question before it is asked: I do expect I’ll create a version for MonoTouch at some point.

But MonoDroid has a much lower barrier of entry since it installs on Windows and works in Visual Studio. MonoTouch requires a non-trivial cash outlay to buy a Mac, and a non-trivial time outlay to learn the Mac, MonoDevelop, some Mac svn implementation, etc. Where I’ll probably have a working version of CSLA 4 for Android in under 20 hours, I strongly suspect it will take more than twice that long (and a lot of money) to get a version working in iOS.

In this regard I must give kudos to Google, Android and MonoDroid – they have a *much lower* barrier to entry than Apple currently provides.
