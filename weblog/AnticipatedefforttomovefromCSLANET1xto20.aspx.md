---
title: Anticipated effort to move from CSLA .NET 1.x to 2.0
postDate: 2005-11-02T11:08:19.343-05:00
abstract: Quite a few people have asked me about the effort that will be required to move an application from CSLA .NET 1.0 to CSLA .NET 2.0, so here's a high level answer.
postStatus: publish
---
02 November 2005

<font face="Times New Roman" color="#000000" size="3">Quite a few people have asked me about the effort that will be required to move an application from CSLA .NET 1.0 to CSLA .NET 2.0. The list of changes in the </font>[<font face="Times New Roman" size="3">change log</font>](http://www.lhotka.net/Articles.aspx?id=1b043659-c5e2-4832-ae48-048ca281c038)<font face="Times New Roman" color="#000000" size="3"> can look daunting after all…</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Fortunately most of the changes in the change log are internal – they don’t directly impact your code in a business class all that much, at least for code written using more recent versions of the framework (1.3 or higher).</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">In fact, the closer your code is to version 1.51 (the current version) the easier the port will be. The closer to the original 1.0 version in the books the harder.<o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman">The three big change areas are generics, BrokenRules and the DataPortal.<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Generics mean there are new and different base classes from which you inherit. In most cases changing to the new base class means removing some now unneeded code from your business class. The following table lists the base classes:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>


| <font face="Times New Roman" color="#000000">Old</font> | <font face="Times New Roman" color="#000000">New</font> |
| --- | --- |
| <font face="Times New Roman" color="#000000">BusinessBase</font> | <font face="Times New Roman" color="#000000">BusinessBase(Of T)</font><br><br><font face="Times New Roman" color="#000000">BusinessBase&lt;T&gt;</font><br><br><font face="Times New Roman" color="#000000">T = your business object type</font> |
| <font face="Times New Roman" color="#000000">BusinessCollectionBase</font> | <font face="Times New Roman" color="#000000">BusinessListBase(Of T, C)</font><br><br><font face="Times New Roman" color="#000000">BusinessListBase&lt;T, C&gt;</font><br><br><font face="Times New Roman" color="#000000">T = your collection type</font><br><br><font face="Times New Roman" color="#000000">C = child object type</font> |
| <font face="Times New Roman" color="#000000">NameValueCollectionBase</font> | <font face="Times New Roman" color="#000000">NameValueListBase(Of K, V)</font><br><br><font face="Times New Roman" color="#000000">NameValueListBase&lt;K, V&gt;</font><br><br><font face="Times New Roman" color="#000000">K = type of the key or name</font><br><br><font face="Times New Roman" color="#000000">V = type of the value</font> |
| <font face="Times New Roman" color="#000000">ReadOnlyBase</font> | <font face="Times New Roman" color="#000000">ReadOnlyBase(Of T)</font><br><br><font face="Times New Roman" color="#000000">ReadOnlyBase&lt;T&gt;</font><br><br><font face="Times New Roman" color="#000000">T = your business object type</font> |
| <font face="Times New Roman" color="#000000">ReadOnlyCollectionBase</font> | <font face="Times New Roman" color="#000000">ReadOnlyListBase(Of T)</font><br><br><font face="Times New Roman" color="#000000">ReadOnlyListBase&lt;T&gt;</font><br><br><font face="Times New Roman" color="#000000">T = child object type</font> |


<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The only place where you need to add code is BusinessBase(Of T), where there’s a new GetIdValue method you must implement (typically with one line of code). In all cases you will remove code such as the System.Objects overrides region and tons of code in collections.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">A much bigger changes is that BrokenRules has been replaced by ValidationRules and now only supports the idea of rule methods. The BrokenRules.Assert() concept is gone. This will be the biggest change for most people, as all Assert calls must be converted to rule methods. Fortunately that's not terribly hard, but it is work.<o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman">DataPortal used to call DataPortal_Update, forcing you to write a nested If..Then statement inside DataPortal_Update. It now calls DataPortal_Insert, DataPortal_Update or DataPortal_DeleteSelf as appropriate. So now you write 3 methods instead of 1, but each method is very focused and requires no conditionals. Also, DataPortal now calls MarkNew and MarkOld automatically so you don't need to make those calls (or forget to make them like I typically did...).<o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman">The end result is that all properties in a BusinessBase(Of T) business object will now look like this:<o:p></o:p></font></font></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000">private string _name = string.Empty;<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">public string Name<o:p></o:p></font>

<font color="#000000">{<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>get<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>{<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>if (CanReadProperty())<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>return _name;<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>else<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>throw new System.Security.SecurityException(<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>"Property get not allowed");<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>}<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>set<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>{<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>if (CanWriteProperty())<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>if (_name != value)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_name = value;<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>PropertyHasChanged();<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>}<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>else<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>throw new System.Security.SecurityException(<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>"Property set not allowed");<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>}<o:p></o:p></font>

<font color="#000000">}<o:p></o:p></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Or </font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font color="#000000">Private mName As String = ""<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000">Public Property Name() As String<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>Get<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>If CanReadProperty() Then<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Return mName<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>Else<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Throw New System.Security.SecurityException( _<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>"Property get not allowed")<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span><span style="mso-spacerun: yes">&nbsp;&nbsp;</span>End If<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>End Get<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>Set(ByVal value As String)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>If CanWriteProperty() Then<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>If mName &lt;&gt; value Then<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>mName = value<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>PropertyHasChanged()<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>End If<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>Else<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Throw New System.Security.SecurityException( _<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>"Property set not allowed")<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span><span style="mso-spacerun: yes">&nbsp;&nbsp;</span>End If<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>End Set<o:p></o:p></font>

<font color="#000000">End Property<o:p></o:p></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font face="Times New Roman" color="#000000" size="3">The new Expert VB/C# 2005 Business Objects books and thus the CSLA .NET 2.0 framework are slated for public release in Mar/Apr 2006.</font>
