---
title: Dynamically loading assemblies from shadow directories
postDate: 2006-05-13T13:53:49.187-05:00
abstract: Dynamically loading assemblies is easy - unless they are in shadow directories managed by VS 2005...
postStatus: publish
---
13 May 2006

<font face="Times New Roman" color="#000000" size="3">I’ve run into a spot where I’m stuck, and I’m hoping someone has an idea.</font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">CSLA .NET 2.0 includes an ASP.NET data source control: CslaDataSource. This works well, except for one issue, which is that it doesn’t refresh the metadata for your business objects unless you close VS 2005 and reopen the IDE.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The reason for this problem is that your business assembly gets loaded into memory so the data source control can reflect against it to gather the metadata. That part works fine, but once an assembly is loaded into an AppDomain it can’t be unloaded. It is possible to unload an entire AppDomain however, and so that’s the obvious solution: load the business assembly into a temporary AppDomain.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">So this is what I’m trying to do, and where I’m stuck. You see VS 2005 has a very complex way of loading assemblies into ASP.NET web projects. It actually appears to use the ASP.NET temporary file scheme to shadow the assemblies as it loads them. Each time you rebuild your solution (or a dependant assembly – like your business assembly), a new shadow directory is created.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The CslaDataSource control is loaded into the AppDomain from the first shadow directory – and from what I can tell that AppDomain never unloads, so the control is always running from that first shadow directory. And then – even if I use a temporary AppDomain – the business assembly is also loaded from that same shadow directory, even if newer ones exist.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">And that’s where I’m stuck. I have no idea how to find out the current shadow directory, and even if I do odd things like hard-coding the directory, then I just get in trouble because the new AppDomain thinks it has a different Csla.dll than the AppDomain hosting the Web Forms designer.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Here’s the code that loads the Type object within the temporary AppDomain:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>public<font color="#000000"> </font>IDataSourceFieldSchema<font color="#000000">[] GetFields()<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>{<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>List<font color="#000000">&lt;</font>ObjectFieldInfo<font color="#000000">&gt; result = <o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>new<font color="#000000"> </font>List<font color="#000000">&lt;</font>ObjectFieldInfo<font color="#000000">&gt;();<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>System.Security.</font>NamedPermissionSet<font color="#000000"> fulltrust =<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>new<font color="#000000"> System.Security.</font>NamedPermissionSet<font color="#000000">(</font>"FullTrust"<font color="#000000">);<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>AppDomain<font color="#000000"> tempDomain = </font>AppDomain<font color="#000000">.CreateDomain(<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>"\_\_temp"<font color="#000000">,<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>AppDomain<font color="#000000">.CurrentDomain.Evidence,<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>AppDomain<font color="#000000">.CurrentDomain.SetupInformation,<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>fulltrust,<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>new<font color="#000000"> System.Security.Policy.</font>StrongName<font color="#000000">[] { });<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>try<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>// load the TypeLoader object in the temp AppDomain<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Assembly<font color="#000000"> thisAssembly = </font>Assembly<font color="#000000">.GetExecutingAssembly();<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>int<font color="#000000"> id = </font>AppDomain<font color="#000000">.CurrentDomain.Id;<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>TypeLoader<font color="#000000"> loader =<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>(</font>TypeLoader<font color="#000000">)tempDomain.CreateInstanceFromAndUnwrap(<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>thisAssembly.CodeBase, </font>typeof<font color="#000000">(</font>TypeLoader<font color="#000000">).FullName);<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>// load the business type in the temp AppDomain<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>Type<font color="#000000"> t = loader.GetType(<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_typeAssemblyName, _typeName);<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>// load the metadata from the Type object<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>if<font color="#000000"> (</font>typeof<font color="#000000">(</font>IEnumerable<font color="#000000">).IsAssignableFrom(t))<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>// this is a list so get the item type<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>t = </font>Utilities<font color="#000000">.GetChildItemType(t);<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>}<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>PropertyDescriptorCollection<font color="#000000"> props =<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>TypeDescriptor<font color="#000000">.GetProperties(t);<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>foreach<font color="#000000"> (</font>PropertyDescriptor<font color="#000000"> item </font>in<font color="#000000"> props)<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>if<font color="#000000"> (item.IsBrowsable)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>result.Add(</font>new<font color="#000000"> </font>ObjectFieldInfo<font color="#000000">(item));<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>}<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>finally<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>AppDomain<font color="#000000">.Unload(tempDomain);<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>}<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>return<font color="#000000"> result.ToArray();<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>}<o:p></o:p></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This replaces the method of the same name from ObjectViewSchema in the book.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Notice that it creates a new AppDomain and then invokes a TypeLoader class inside that AppDomain to create the Type object for the business class. The TypeLoader is a new class in Csla.dll that looks like this:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

using<font color="#000000"> System;<o:p></o:p></font>

using<font color="#000000"> System.Collections.Generic;<o:p></o:p></font>

using<font color="#000000"> System.Text;<o:p></o:p></font>

<o:p><font color="#000000">&nbsp;</font></o:p>

namespace<font color="#000000"> Csla.Web.Design<o:p></o:p></font>

<font color="#000000">{<o:p></o:p></font>

<font color="#000000">&nbsp; </font>/// &lt;summary&gt;<o:p></o:p>

<font color="#000000">&nbsp; </font>/// Loads a Type object into the AppDomain.<o:p></o:p>

<font color="#000000">&nbsp; </font>/// &lt;/summary&gt;<o:p></o:p>

<font color="#000000">&nbsp; </font>public<font color="#000000"> </font>class<font color="#000000"> </font>TypeLoader<font color="#000000"> : </font>MarshalByRefObject<o:p></o:p>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>{<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>/// &lt;summary&gt;<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>/// Returns a &lt;see cref="Type"&gt;Type&lt;/see&gt; object based on the<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>/// assembly and type information provided.<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>/// &lt;/summary&gt;<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>/// &lt;param name="assemblyName"&gt;(Optional) Assembly name containing the type.&lt;/param&gt;<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>/// &lt;param name="typeName"&gt;Full type name of the class.&lt;/param&gt;<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>/// &lt;remarks&gt;&lt;/remarks&gt;<o:p></o:p>

<font color="#000000">&nbsp;&nbsp;&nbsp; </font>public<font color="#000000"> </font>Type<font color="#000000"> GetType(<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>string<font color="#000000"> assemblyName, </font>string<font color="#000000"> typeName)<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>{<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>int<font color="#000000"> id = </font>AppDomain<font color="#000000">.CurrentDomain.Id;<o:p></o:p></font>

<font color="#000000">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </font>return<font color="#000000"> Csla.Web.</font>CslaDataSource<font color="#000000">.GetType(<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>assemblyName, typeName);<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>}<o:p></o:p></font>

<font color="#000000"><span style="mso-spacerun: yes">&nbsp; </span>}<o:p></o:p></font>

<font color="#000000">}<o:p></o:p></font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Since this object is created in the temporary AppDomain, the business assembly is loaded into that AppDomain. The Type object is [Serializable] and so is serialized back to the main AppDomain so the data source control can get the metadata as needed.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">This actually all works – except that it doesn’t pick up new shadow directories as they are created.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Any ideas on how to figure out the proper shadow directory are appreciated.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Honestly, I can’t figure out how this works in general – because obviously <i style="mso-bidi-font-style: normal">some part</i> of the VS designer picks up the new shadow directory and uses it – even though the designer apparently doesn’t. I am quite lost here.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">To make matters worse, things operate entirely differently when a debugger is attached to VS than when not. When a debugger is attached to VS then <i style="mso-bidi-font-style: normal">nothing</i> appears to pick up the new shadow directories – so I assume the debugger is interfering somehow. But it makes tracking down the issues really hard.</font>
