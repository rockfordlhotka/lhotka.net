---
title: Repro steps for issue with NuGet UWP packages
postDate: 2015-09-16T12:00:21.7445545-05:00
abstract: 
postStatus: publish
---
16 September 2015

Steps to repro the issue described in this github issue:

https://github.com/MarimerLLC/csla/issues/428

1. Pull the csla repo from
https://github.com/rockfordlhotka/csla.git

a. Switch to the NuGet-uwp branch
[![clip_image001](binary/Windows-Live-Writer/70968a68a482_A8AA/clip_image001_thumb.png "clip_image001")](binary/Windows-Live-Writer/70968a68a482_A8AA/clip_image001_2.png)

2. Open &lt;root&gt;\csla\Source\csla.build.sln

a. Build Release | All CPU
[![clip_image002](binary/Windows-Live-Writer/70968a68a482_A8AA/clip_image002_thumb.png "clip_image002")](binary/Windows-Live-Writer/70968a68a482_A8AA/clip_image002_2.png)

b. Don’t worry about the Xamarin projects – they don’t matter for this issue

c. Build results will be in &lt;root&gt;\csla\bin

i. including the problematic rd.xml files for the UWP projects

3. Open PowerShell, cd to &lt;root&gt;\csla\NuGet

a. Run ‘Build All.ps1’ /prerelease:Beta3

b. Run consolidatepackages.bat

4. Open &lt;root&gt;\csla\Samples\ProjectTracker\ProjectTracker.sln

a. Add a NuGet package source to &lt;root&gt;\Packages, for example:
[![clip_image004](binary/Windows-Live-Writer/70968a68a482_A8AA/clip_image004_thumb.jpg "clip_image004")](binary/Windows-Live-Writer/70968a68a482_A8AA/clip_image004_2.jpg)

b. Build Debug | All CPU

i. Ignore the *async method lacks await* warning – this is a testing artifact

ii. Ignore the warnings about our analyzers (unless you know how to fix them – this analyzer via NuGet stuff is challenging at best!!!!)

iii. You should end up with a build error:


| Severity | Code | Description | Project | File | Line |
| --- | --- | --- | --- | --- | --- |
| Error |   | Payload contains two or more files with the same destination path 'Csla\Properties\Csla.Uwp.rd.xml'. Source files: C:\Users\Rockford\.nuget\packages\CSLA-Core\4.6.172-Beta3\lib\uap10.0\Csla\Properties\Csla.Uwp.rd.xmlC:\Users\Rockford\.nuget\packages\CSLA-UWP\4.6.172-Beta3\lib\uap10.0\Csla\Properties\Csla.Uwp.rd.xml | ProjectTracker.Ui.UWP |   |   |

