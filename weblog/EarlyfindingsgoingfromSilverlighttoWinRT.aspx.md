---
title: Early findings going from Silverlight to WinRT
postDate: 2012-03-21T09:49:28.5586294-05:00
abstract: 
postStatus: publish
---
21 March 2012

I’ve been spending quite a bit of time working with WinRT over the past couple weeks. Specifically prepping for next week’s [Visual Studio Live!](http://www.vslive.com/) and [VS Connections](http://www.devconnections.com/) conferences.

As part of this process, I have a super early version of CSLA 4 version 4.5 that builds and (mostly) runs on WinRT. I’d done a lot of the work months ago when the Windows 8 developer preview came out, so getting it to work on the consumer preview took only a couple hours.

The only new feature I’ve added so far is support for the new async and await keywords for WinRT data portal code. I still need to add async/await support for the .NET data portal. I might refine some of my implementation, but right now I can use async/await to call the data portal in WinRT, and that’s cool!

The primary observation I want to make right now though, is that business classes created using CSLA 4 that target Silverlight will now recompile for WinRT with no code changes required. I took the entire ProjectTracker business library project and just recompiled it for WinRT and it works – unchanged.


> **<font style="background-color: #ffff00">If you want direct reuse of your business logic from .NET/Silverlight to WinRT, you should consider using CSLA 4.</font>**


Because I did add the async/await data portal support, I chose to add async factory methods to my business classes, alongside the existing .NET and Silverlight factory methods. From a porting/reuse perspective this is not necessary, but in terms of writing new code for .NET 4.5 and/or WinRT I think we’ll all tend to write these async factory methods.

In short, I added code like this:


> <font face="Courier New">#if WINRT       <br>&#160;&#160;&#160; public async static System.Threading.Tasks.Task&lt;ProjectList&gt; GetProjectListAsync()        <br>&#160;&#160;&#160; {        <br>&#160;&#160;&#160;&#160;&#160; return await Csla.DataPortal.FetchAsync&lt;ProjectTracker.Library.ProjectList&gt;();        <br>&#160;&#160;&#160; }        <br>#endif        <br></font>


This allows the viewmodel or other presentation layer code to retrieve business objects like this:


> <font face="Courier New">var obj = await ProjectList.GetProjectListAsync();</font>


No need for async callback handlers or the other messy goo from a typical WPF/Silverlight application. Of course WPF 4.5 will be able to use the await keyword too, so only SL/WP7 will still require the callback handler model when all is said and done.

Although these are early days, and I am still working through all the features of CSLA .NET to make sure they work on WinRT, it is nice to know that data binding, business/validation rules, and the data portal are all functional already. I expect to still do some work around authorization rules, and the local data portal implementation – but the vast majority of CSLA 4 functionality is already working just fine on WinRT and that makes me very happy!
