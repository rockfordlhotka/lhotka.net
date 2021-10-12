---
title: Codeless WPF data edit forms with CslaDataProvider
postDate: 2007-06-20T11:14:03.1268432-05:00
abstract: Using CslaDataProvider it is now possible to create a data edit form purely in XAML: no C# or VB code required!
postStatus: publish
---
20 June 2007

<font face="Calibri" color="#000000" size="3">A CSLA .NET user, Aaron Nottestad, has been helping test 3.0 and ran into some issues when using the new WPF CslaDataProvider with editable objects. Thanks Aaron!</font>

<font face="Calibri" color="#000000" size="3">As a result, I had to do some work with CslaDataProvider, so it can manage the object’s entire lifetime from create/fetch through to save/cancel. If it can’t manage the lifetime, especially the save, then it can’t get the new object that comes back as a result of save. And if it doesn’t get that new object, then neither does data binding, so the UI controls end up editing an old instance of the object.</font>

<font face="Calibri" color="#000000" size="3">So the CslaDataProvider now has Save() and Cancel() methods that you can call to trigger saving or canceling of the business object. Also, as the object is created/fetched CslaDataProvider automatically calls BeginEdit() on the object.</font>

<font face="Calibri" color="#000000" size="3">This behavior is all optional, and is controlled by the ManageObjectLifetime property of the CslaDataProvider control. So if you want this behavior, you have to set that property to True. If you leave it at False (the default), then you must manage everything through code – though honestly you <i style="mso-bidi-font-style: normal">can’t</i> manage editable objects through code while using CslaDataProvider. So maybe I should make the default be True? Hmm.</font>

<font face="Calibri" color="#000000" size="3">Anyway, this was easy enough to do and worked great. The resulting forms had exactly 4 lines of code – 2 to call Save() and 2 to call Cancel(). It occurred to me that there <i style="mso-bidi-font-style: normal">must</i> be a way to avoid writing those 4 lines of boring code, and Aaron put me onto the RoutedCommand concept in XAML.</font>

<font face="Calibri" color="#000000" size="3">A RoutedCommand allows a control like a button or menu item to invoke a method on another control – purely through XAML. There are many examples out there about how this works to create standard Copy/Paste menu items that run against the current TextBox control, and that sort of thing. But none that I found which routed a command to a data provider control.</font>

<font face="Calibri" color="#000000" size="3">The reason turns out to be that the <i style="mso-bidi-font-style: normal">target</i> of a command must be a UIElement, and data providers don’t inherit from that base class. Oops…</font>

<font face="Calibri" color="#000000" size="3">I thought I was stuck, because I really <i style="mso-bidi-font-style: normal">do</i> want to route the command to CslaDataProvider in this case. However, I figured out a solution.</font>

<font face="Calibri" color="#000000" size="3">CslaDataProvider now has a read-only CommandManager property. This property exposes a “command manager” object which does inherit from UIElement and which does handle the Save and Undo routed commands. When it is created by CslaDataProvider, it is given a reference to the CslaDataProvider control, so it simply delegates all Save commands to the CslaDataProvider.Save() method and all Undo commands to CslaDataProvider.Cancel().</font>

<font face="Calibri" color="#000000" size="3">With that done, you can route a command from a button or menu item (or any other valid command source) to this CommandManager object, which effectively means you’ve routed the command to the CslaDataProvider control.</font>

<font face="Calibri" color="#000000" size="3">The CslaDataProvider gets declared like this:</font>

<font color="#000000">&nbsp;&nbsp;&nbsp; &lt;csla:CslaDataProvider x:Key="ChildList"<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ObjectType="{x:Type this:ChildList}"<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; FactoryMethod="GetList"<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; IsAsynchronous="False"<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ManageObjectLifetime="True"&gt;<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; &lt;/csla:CslaDataProvider&gt;<o:p></o:p></font>

<o:p><font face="Calibri" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Calibri" color="#000000" size="3">Then the button controls get declared like this:</font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;Button <o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Command="ApplicationCommands.Save" <o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; CommandTarget="{Binding Source={StaticResource ChildList}, <o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Path=CommandManager, BindsDirectlyToSource=True}"<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; HorizontalAlignment="Left" IsDefault="True"&gt;Save&lt;/Button&gt;<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &lt;Button <o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Command="ApplicationCommands.Undo" <o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; CommandTarget="{Binding Source={StaticResource ChildList}, <o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Path=CommandManager, BindsDirectlyToSource=True}"<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; HorizontalAlignment="Left" IsCancel="True"&gt;Cancel&lt;/Button&gt;<o:p></o:p></font>

<o:p><font face="Calibri" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Calibri" color="#000000" size="3">The result is <i style="mso-bidi-font-style: normal">very</i> cool: a form that can edit an object without the need to write any C# or VB code at all. Coupled with the CSLA .NET ValidationPanel to display validation results, you can create a highly interactive data edit form purely with XAML – and of course a CSLA .NET style business object doing all the work behind the scenes.</font>

<font face="Calibri" color="#000000" size="3">These new capabilities will appear in CSLA .NET 3.0 Beta 2 - hopefully later this week.</font>
