---
title: CSLA 4 version 4.5 beta 1 released
postDate: 2012-09-24T15:16:59.8810183-05:00
abstract: 
postStatus: publish
---
24 September 2012

CSLA 4 version 4.5.2 is now online. This is Beta 1 of the 4.5 release, and is the start of the beta process. I expect to release a number of betas in relatively short order between now and the end of October. My plan is to have a final release before Windows 8 GA.

You can get this beta release from nuget (show unreleased versions), or via the installer from the [CSLA download page](http://www.lhotka.net/cslanet/download.aspx).

This release supports .NET 4, .NET 4.5, WinRT, and Silverlight 5.

This beta release is a *major* change over the previous preview releases.

1. CSLA now fully supports the new WinRT platform for Windows 8 development.
2. The data portal now supports async/await on the client and on the server. Additionally, the .NET, WinRT, and Silverlight data portal implementations are now the same. There is no longer a “Silverlight data portal”. To make this happen, the data portal pipeline underwent major changes. <font style="background-color: #ffff00">This includes a number of breaking changes.</font>
3. The MobileFormatter is now available for use by .NET applications (not just Silverlight and WinRT). This *might* allow .NET apps to run in partial trust, and certainly allows .NET apps to use the same data portal channel/endpoint  as a WinRT or Silverlight app.
4. Jonny has done a lot of work on the business rules engine. There shouldn’t be any real breaking changes, but there are a lot of good new features.
5. BusinessBase metastate properties (such as IsDirty) are now bindable – they raise PropertyChanged as you’d expect. This enables some XAML scenarios, but be careful because WinRT XAML doesn’t notice when the DataContext has changed, so you can run into some strange issues when saving an editable object in WinRT.
6. Johann put a lot of work into the nuget release process, allowing us to use nuget for prereleases like this one, and to create a nuget package with code templates for use in your projects.
7. We now support .NET 4.5 and 4.0 with CSLA 4.5, so you can use the same CSLA 4.5 on existing .NET 4 machines, on Windows Azure, and also use it on .NET 4.5 machines. A 4.5 client can talk to a .NET 4 server and visa versa.
8. WinRT now includes language resources.
9. A number of changes were made to the Windows Forms CslaActionExtender type.


Be aware that the .NET 4 and Silverlight 5 environments now *require* that you use the Async Targeting Pack from Microsoft (typically via nuget) so that CSLA and your code can use the async/await keywords and related functionality.

Be aware that [the data portal has breaking changes](http://www.lhotka.net/weblog/CSLADataPortalChangesInVersion45.aspx), especially for Silverlight users. Some highlights of breaking changes:

- The Enterprise Services, Remoting, and asmx data portal channels have been removed. If you need these wire transport technologies you can create your own proxy and host types based on the version 3.8 code (perhaps they’ll end up in CslaContrib at some point).
- The namespaces for proxy and host types that included “Silverlight” in the namespace now use the term “Mobile” instead. For example, Csla.Server.Hosts.IWcfPortal is now Csla.Server.Hosts.Mobile.IWcfPortal.
- The client-side ProxyMode concept is now eliminated entirely, and you should use the same RunLocal attribute in Silverlight as you do in .NET.
- All client-side DataPortal\_XYZ methods in Silverlight are now different, and no longer accept a callback handler parameter. Instead, code all client-side DataPortal\_XYZ methods for Silverlight just as you would for .NET.


Please direct any comments, suggestions, bug reports, or other feedback to the [CSLA forums](http://forums.lhotka.net/forums/5.aspx).
