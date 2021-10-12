---
title: CSLA .NET 3.0 early test version available
postDate: 2007-03-26T13:18:02.3067776-05:00
abstract: 
postStatus: publish
---
26 March 2007

I have put an early test version of CSLA .NET version 3.0, along with some updates to the ProjectTracker app online for download at http://www.lhotka.net/cslanet/download.aspx.

At this time the code is C# only. I'll port to VB once I'm more comfortable that the code is stable. And that statement alone should reinforce that this is early test code!! :)

The CSLA framework code includes WCF and WPF support. I have not yet found a case where I've needed to do anything to CSLA itself to support WF - invoking workflows and using CSLA objects in activities works as-is. You can look at the change log document to see what I've done for WCF and WPF.

The ProjectTracker folder now has a PTWpf project and a PTWorkflow project.

*Neither of these are in the solution!* The reason they are not in the solution is because PTWpf is a March 2007 Orcas CTP project, and so it won't load under VS 2005, and PTWorkflow requires the WF additions for VS 2005, which not everyone has installed. To put this another way: if you have the WF additions installed on VS 2005, you can open the workflow project. But to open the PTWpf project you need to be running the March 2007 Orcas CTP.

That said, if you want to play with the WPF forms under 2005, you can certainly use the xaml and cs files - just grab the bits you need and use them in whatever tool you are using (xamlpad, notepad, the Dec CTP or whatever). The PTWpf project isn't complete, but the ProjectList and ProjectEdit forms both work and illustrate a couple ways to interact with CSLA-style business objects for both read-only and read-write purposes.

If you do try the 3.0 version, please let me know of any issues you find. I'm actively working on this code, and appreciate any bug reports or other input!
