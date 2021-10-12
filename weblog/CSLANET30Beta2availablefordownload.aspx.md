---
title: CSLA .NET 3.0 Beta 2 available for download
postDate: 2007-06-22T16:30:47.8767488-05:00
abstract: CSLA .NET Version 3.0 Beta 2 is now available for download. This is the final test release of version 3.0. Any changes between now and release will be bug fixes.
postStatus: publish
---
22 June 2007

<font face="Calibri" color="#000000" size="3">CSLA .NET Version 3.0 Beta 2 is now available for </font>[<font face="Calibri" color="#800080" size="3">download</font>](http://www.lhotka.net/cslanet/download.aspx)<font face="Calibri" color="#000000" size="3">.</font>

<font face="Calibri" color="#000000" size="3">This is the final test release of version 3.0. Any changes between now and release will be bug fixes.</font>

<font face="Calibri" color="#000000" size="3">If you plan to upgrade please consider helping yourself and the community at large by downloading this version and testing it <i style="mso-bidi-font-style: normal">before July 5</i>. Let me know about any issues through the </font>[<font face="Calibri" color="#800080" size="3">forum</font>](http://forums.lhotka.net/forums/5/ShowForum.aspx)<font face="Calibri" color="#000000" size="3">.</font>

<font face="Calibri" color="#000000" size="3">CSLA .NET 3.0 provides support for Microsoft .NET 2.0 and 3.0.</font>

<font face="Calibri" color="#000000" size="3">If you want to build CSLA .NET 3.0 <i style="mso-bidi-font-style: normal">without .NET 3.0</i>, you must define the NET20 symbol in the project properties.</font>

<font face="Calibri" color="#000000" size="3">CSLA .NET 3.0 includes enhancements useful to all 2.1.4 users, including these highlights:</font>

**<font size="3"><font color="#000000"><font face="Calibri">Validation rules<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p></o:p></font></font></font>**

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">PropertyFriendlyName – specify a friendly name to use when displaying broken rule text</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Format – specify a format mask to use when displaying broken rule numeric values</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">StringMinLength – new validation rule method</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">DecoratedRuleArgs – useful for code generation of AddBusinessRules() methods</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Fix bug with stopProcessing and rule priorities</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">RegEx – rule method now supports options for dealing with null values</font></font>

**<font size="3"><font color="#000000"><font face="Calibri">Authorization<o:p></o:p></font></font></font>**

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">New CanExecuteMethod() functionality, similar to CanReadProperty() and CanWriteProperty()</font></font>

**<font size="3"><font color="#000000"><font face="Calibri">Undo and Data binding<o:p></o:p></font></font></font>**

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">If edit levels get out of sync an exception is thrown, making debugging of Windows Forms data binding much easier</font></font>

**<font size="3"><font color="#000000"><font face="Calibri">Interfaces<o:p></o:p></font></font></font>**

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Cleaned up and rearranged interfaces to provide more consistency – making it easier to create UI frameworks on top of CSLA business layers</font></font>

**<font size="3"><font color="#000000"><font face="Calibri">SmartDate<o:p></o:p></font></font></font>**

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Added TryParse() method</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Fix bug with CompareTo() method</font></font>

**<font size="3"><font color="#000000"><font face="Calibri">SortedBindingList and FilteredBindingList<o:p></o:p></font></font></font>**

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Allow access to underlying source list</font></font>

**<font size="3"><font color="#000000"><font face="Calibri">ProjectTracker\PTWin<o:p></o:p></font></font></font>**

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Reworked data binding code to address all known issues</font></font>

<font face="Calibri" color="#000000" size="3">See the </font>[<font face="Calibri" color="#800080" size="3">change log</font>](http://www.lhotka.net/Article.aspx?area=4&amp;id=0c94aa82-b975-455b-a0c5-f4f7196a2408)<font face="Calibri" color="#000000" size="3"> for a complete list of changes.</font>

<font face="Calibri" color="#000000" size="3">Of course the <i style="mso-bidi-font-style: normal">primary</i> focus of CSLA .NET 3.0 is support for Microsoft .NET 3.0. Highlights include:</font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri"><font size="3"><b style="mso-bidi-font-weight: normal">WcfProxy</b> – a data portal channel that uses WCF. You can <i style="mso-bidi-font-style: normal">transparently</i></font><font size="3"> move from any existing data portal channel to WCF by using this new proxy.</font></font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri"><b style="mso-bidi-font-weight: normal"><font size="3">DataContract</font></b><font size="3"> – support for using the WCF DataContract and DataMember attributes in your business classes</font></font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><b style="mso-bidi-font-weight: normal"><font size="3"><font face="Calibri">WPF<o:p></o:p></font></font></b></font>

<font color="#000000"><span style="FONT-FAMILY: 'Courier New'; mso-fareast-font-family: 'Courier New'"><span style="mso-list: Ignore"><font size="3">o</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">CslaDataProvider – a data provider control that can create, fetch, save and cancel edits on a CSLA .NET business object. In some cases this can lead to code-less data entry forms!</font></font>

<font color="#000000"><span style="FONT-FAMILY: 'Courier New'; mso-fareast-font-family: 'Courier New'"><span style="mso-list: Ignore"><font size="3">o</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Validator – a control that provides Windows Forms ErrorProvider-like behavior to WPF forms that are data bound to CSLA .NET objects.</font></font>

<font color="#000000"><span style="FONT-FAMILY: 'Courier New'; mso-fareast-font-family: 'Courier New'"><span style="mso-list: Ignore"><font size="3">o</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Authorizer – a control that provides Windows Forms AuthorizeReadWrite-like behaviors to WPF forms that are data bound to CSLA .NET objects.</font></font>

<font color="#000000"><span style="FONT-FAMILY: 'Courier New'; mso-fareast-font-family: 'Courier New'"><span style="mso-list: Ignore"><font size="3">o</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">ObjectStatus – a control that exposes IsValid, IsSavable and other properties from a CSLA .NET business object so they can be used by XAML data binding.</font></font>

<font color="#000000"><span style="FONT-FAMILY: 'Courier New'; mso-fareast-font-family: 'Courier New'"><span style="mso-list: Ignore"><font size="3">o</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">IdentityConverter – a value converter that can be used to work around an issue with data binding and refreshing the UI.</font></font>

<font face="Calibri" color="#000000" size="3">ProjectTracker\PTWpf</font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Added new WPF UI with equivalent functionality to PTWin.</font></font>

<font face="Calibri" color="#000000" size="3">ProjectTracker\PTWorkflow</font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Added new Workflow UI to illustrate how a workflow can use CSLA .NET business objects</font></font>

<font face="Calibri" color="#000000" size="3">ProjectTracker\PTWcfClient and PTWcfService</font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Added a WCF service illustrating how to expose CSLA .NET objects through WCF/SOA</font></font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Added a WCF client app illustrating how to call a WCF service</font></font>

<font face="Calibri" color="#000000" size="3">ProjectTracker\WcfHost</font>

<font color="#000000"><span style="FONT-FAMILY: Symbol; mso-fareast-font-family: Symbol; mso-bidi-font-family: Symbol"><span style="mso-list: Ignore"><font size="3">·</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></span></span><font face="Calibri" size="3">Added a WCF host for the data portal</font></font>
