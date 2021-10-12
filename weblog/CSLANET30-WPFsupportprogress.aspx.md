---
title: CSLA .NET 3.0 - WPF support progress
postDate: 2007-03-15T22:37:24.2702512-05:00
abstract: I’ve been spending a lot of time in WPF-land over the past few weeks, and thought I’d share some of what I’ve learned...
postStatus: publish
---
15 March 2007

<font face="Calibri" color="#000000" size="3">I’ve been spending a lot of time in WPF-land over the past few weeks, and thought I’d share some of what I’ve learned. I haven’t been learning styles or UI layout stuff – Microsoft says that’s the job of the turtleneck-wearing, metrosexual GQ crowd, so I’ll just roll with that. Instead, I’ve been learning how to write data source provider controls, and implement Windows Forms-like behaviors similar to the ErrorProvider and my Csla.Windows.ReadWriteAuthorization control. </font>

<font size="3"><font color="#000000"><font face="Calibri">You know, manly programming </font><span style="FONT-FAMILY: Wingdings; mso-ascii-font-family: Calibri; mso-ascii-theme-font: minor-latin; mso-hansi-font-family: Calibri; mso-hansi-theme-font: minor-latin; mso-char-type: symbol; mso-symbol-font-family: Wingdings"><span style="mso-char-type: symbol; mso-symbol-font-family: Wingdings">J</span></span></font></font>

<font face="Calibri" color="#000000" size="3">The data source provider control is, perhaps, the easiest thing I’ve done. Like ASP.NET, WPF likes to use a data control concept. And like ASP.NET, the WPF data provider controls are easy to create, because they don’t actually do all that much at runtime. <span style="mso-spacerun: yes">&nbsp;</span>(I do want to say thank you to Abed Mohammed for helping to debug some issues with the CslaDataProvider control!)</font>

<font face="Calibri" color="#000000" size="3">I’m sure, as designer support for data provider controls matures in tools like Visual Studio and Expression Blend, that life will get far more complex. Certainly the Visual Studio designer support for Csla.Web.CslaDataProvider has been the single most time consuming part of </font>[<font face="Calibri" size="3">CSLA .NET</font>](http://www.lhotka.net/cslanet)<font face="Calibri" color="#000000" size="3">, though I was able to create the runtime support in an afternoon…</font>

<font face="Calibri" color="#000000" size="3">What I have today, is a Csla.Wpf.CslaDataProvider control that works similar to the ObjectDataProvider. The primary difference is that CslaDataProvider understands how to call Shared/static factory methods to get your objects, rather than calling a constructor method. The result is that you can create/fetch CSLA .NET business objects directly from your XAML.</font>

<font face="Calibri" color="#000000" size="3">The really cool part of this, is that CslaDataProvider supports asynchronous loading of the data. To be fair, the hard work is done by the WPF base class, DataSourceProvider. Even so, supporting async is optional, and requires a bit of extra work in the control – work that is worth it though. If you construct a form that has multiple DataContext objects for different parts of the form, loading all of them async should give some nice performance benefits overall.</font>

<font face="Calibri" color="#000000" size="3">On the other hand, if your form is bound to a single business object the value isn’t clear at all. Though the data load is async, the form won’t actually display until all the async loads are complete, so for a single data source on a form my guess is that async is actually counter-productive.</font>

<font face="Calibri" color="#000000" size="3">The validation/ErrorProvider support is based on some work </font>[<font face="Calibri" color="#800080" size="3">Paul Stovell</font>](http://paulstovell.net/)<font face="Calibri" color="#000000" size="3"> published on the web. I conceptually based my work on similar concepts, and have created a ValidationPanel control that uses IDataErrorInfo to determine if any bindings of any controls contained in the panel are invalid. </font>

<font face="Calibri" color="#000000" size="3">The panel control loops through all the controls contained inside the panel. On each control it loops through the DependencyProperty elements defined for that control (in WPF controls, normal properties aren’t bindable, only dependency properties). And it then loops through any Binding objects attached to each DependencyProperty. I discovered that those Binding objects are complex little buggers, and that there are different kinds of binding that I need to filter out. Specifically relative bindings and control-to-control bindings must be ignored, because they don’t represent a binding to the actual business object.</font>

<font face="Calibri" color="#000000" size="3">To optimize performance the panel does a bunch of caching of binding information, and is relatively sparing in how often it refreshes the validation data – but it is comparable to ErrorProvider, in that changing one business object property does trigger rechecking of all other properties bound within the same ValidationPanel. I think this is necessary, because so many data source objects are constructed around the Windows Forms model. Not following that model would cause a lot of headache when moving to WPF.</font>

<font face="Calibri" color="#000000" size="3">The authorization support is implemented in a manner similar to the validation. Csla.Wpf.AuthorizationPanel uses the CSLA .NET IAuthorizeReadWrite interface and scans all bindings for all controls contained in the panel to see if the business object will allow the current user to read or write to the bound property. If the user isn’t allowed to read the property, the panel either hides or collapses the data bound control (your choice). If the user isn’t allowed to write to the property, the panel sets the control’s IsReadOnly property to true, or if the control doesn’t have IsReadOnly, it sets IsEnabled to false.</font>

<font face="Calibri" color="#000000" size="3">AuthorizationPanel doesn’t include the same level of caching as ValidationPanel, but I don’t think it is necessary. Where ValidationPanel refreshes on every property change, AuthorizationPanel only refreshes if the data source object is changed (replaced) or if you explicitly force a refresh – probably because the current user’s principal object has changed.</font>

<font face="Calibri" color="#000000" size="3">I want to pause here and point out that I’ve had a lot of help in these efforts from Paul Czywczynski. He’s spent a lot of time trying these controls and finding various holes in my logic. And the next control addresses one of those holes...</font>

<font face="Calibri" color="#000000" size="3">The IsValid, IsDirty, IsSavable, IsNew and IsDeleted properties on a CSLA .NET business object are marked as Browsable(false), meaning they aren’t available for data binding. In Windows Forms you can work around this easily by </font>[<font face="Calibri" color="#800080" size="3">handling a simple event</font>](http://www.lhotka.net/Article.aspx?area=4&amp;id=5faaee8e-8496-4845-86f7-787c6b64096c)<font face="Calibri" color="#000000" size="3"> on the BindingSource object. But in WPF the goal is to write no code – to do everything through XAML (or at least to make that possible), so such a solution isn’t sufficient.</font>

<font face="Calibri" color="#000000" size="3">Enter the ObjectStatusPanel, which takes the business object’s properties and exposes them in a way that WPF can consume. Using this panel, your object’s status properties (single object or collection) become available for binding to WPF controls, and if the object’s properties change those changes are automatically reflected in the UI. The most common scenario here is to bind a button’s enabled status to the IsSavable property of your editable root business object.</font>

<font face="Calibri" color="#000000" size="3">Most recently I’ve started refactoring the code in these controls. For the most part, I’ve now consolidated the common code from all three into a base class: Csla.Wpf.DataPanelBase. This base class encapsulates the code to walk through and find relevant Binding objects on all child controls, and also encapsulates all the related event handling to detect when the data context, data object, object property, list or collection have changed. It turns out that a lot of things can happen during data binding, and detecting all of them means hooking, unhooking and responding to a lot of events.</font>

<font face="Calibri" color="#000000" size="3">I wrote all these controls originally using the Dec 2006 CTP, and just started using them in the Mar 2007 CTP. As a pleasant surprise there was no upgrade pain – they just kept working.</font>

<font face="Calibri" color="#000000" size="3">In fact, they work better in the MarCTP, because the Cider designer (WPF forms designer) is now capable of actually rendering my custom controls. What I find <i style="mso-bidi-font-style: normal">very</i> interesting, is that the designer actually <i style="mso-bidi-font-style: normal">runs the factory method</i> of the CslaDataProvider control, so the form shows real data from the real objects right there in Visual Studio. I’m not sure this is a good thing, but that’s what happens.</font>

<font face="Calibri" color="#000000" size="3">There’s no doubt that I’ll find more issues with these controls, and they’ll change over the next few weeks and months.</font>

<font face="Calibri" color="#000000" size="3">But the exciting thing is that I’m now able to create WPF forms that have functional parity with Windows Forms, including validation, authorization and object status binding. And it can all be done in either XAML or code, running against standard CSLA .NET business objects.</font>

<font face="Calibri" color="#000000" size="3">People attending </font>[<font face="Calibri" color="#800080" size="3">VS Live</font>](http://www.vslive.com/)<font face="Calibri" color="#000000" size="3"> at the end of this month will be the first to see these controls in action – both in my workshop on Sunday the 25<sup>th</sup> and in my sessions during the week. And I plan to put a test version of CSLA .NET 3.0 online that week as well, so anyone who wants to play with it can give it a go.</font>

<font face="Calibri" color="#000000" size="3">Right now, if you aren’t faint of heart, you can grab the live code from my </font>[<font face="Calibri" color="#800080" size="3">svn repository</font>](http://www.lhotka.net/Article.aspx?id=5987a664-4b44-45a7-bc1d-695610964718)<font face="Calibri" color="#000000" size="3">. Keeping in mind, of course, that this is an active repository and so the code in trunk/ may or may not actually work at any given point in time.</font>