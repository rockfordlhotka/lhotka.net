---
title: Binding a WPF ComboBox to a display source and a binding source
postDate: 2007-04-24T20:55:13.072544-05:00
abstract: Here's how to bind a WPF ComboBox so it gets its display data from one binding source, and sets the selected item from a property on your page's main data object.
postStatus: publish
---
24 April 2007

<font face="Calibri" color="#000000" size="3">I am building a WPF UI for my ProjectTracker <a href="http://www.lhotka.net/cslanet">CSLA .NET</a> sample app. On the whole this is going pretty well, and I anticipate being done within the next couple days. I’ve found and fixed a couple bugs in CSLA – one in BusinessListBase that’s been there forever, and one in ValidationPanel that caused a null reference exception. While I fixed that last one, I optimized the code a bit, which does seem to make the control a bit faster.</font>

<font face="Calibri" color="#000000" size="3">But one thing I spent a ridiculous amount of time on was the simple process of getting a ComboBox control to bind to one data source to get its list of items, and to the business object property for the key value. Google turned up a number of search results, none of which really addressed this particular scenario – which seems odd to me given how common a scenario it is…</font>

<font face="Calibri" color="#000000" size="3">In ProjectTracker, a person (resource) can be assigned to a project. If they are, they are given a role on that project. The Role property is numeric – a key into a name/value list, and a foreign key into the Roles table in the database. In Windows Forms and Web Forms the UI handles translating this numeric value to a human-readable value through ComboBox controls, and obviously WPF can do the same thing. The trick is in figuring out the XAML to make it happen.</font>

<font face="Calibri" color="#000000" size="3">Here’s the ComboBox XAML:</font>

<font size="3"><font color="#000000"><font face="Calibri"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>&lt;ComboBox </font></font></font>

<font size="3"><font color="#000000"><font face="Calibri"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>ItemsSource="{Binding Source={StaticResource RoleList}}" </font></font></font>

<font size="3"><font color="#000000"><font face="Calibri"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>DisplayMemberPath="Value"</font></font></font>

<font size="3"><font color="#000000"><font face="Calibri"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>SelectedValuePath="Key"</font></font></font>

<font size="3"><font color="#000000"><font face="Calibri"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>SelectedValue="{Binding Path=Role}" </font></font></font>

<font size="3"><font color="#000000"><font face="Calibri"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Width="150" /&gt;</font></font></font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Calibri" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Calibri" color="#000000" size="3">Let’s break this down.</font>

<font face="Calibri" color="#000000" size="3">The ItemsSource property specifies the data source for the data that will populate the display of the control. In my case it is referencing a data provider control defined like this:</font>

<font size="3"><font color="#000000"><font face="Calibri"><span style="mso-spacerun: yes">&nbsp; </span>&lt;Page.Resources&gt;</font></font></font>

<font size="3"><font color="#000000"><font face="Calibri"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>&lt;csla:CslaDataProvider x:Key="RoleList"</font></font></font>

<font size="3"><font color="#000000"><font face="Calibri"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>ObjectType="{x:Type PTracker:RoleList}"</font></font></font>

<font size="3"><font color="#000000"><font face="Calibri"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>FactoryMethod="GetList"</font></font></font>

<font size="3"><font color="#000000"><font face="Calibri"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>IsAsynchronous="False" /&gt;</font></font></font>

<font size="3"><font color="#000000"><font face="Calibri"><span style="mso-spacerun: yes">&nbsp; </span>&lt;/Page.Resources&gt;</font></font></font>

<o:p><font face="Calibri" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Calibri" color="#000000" size="3">This data provider control loads a name/value list object called RoleList (that inherits from Csla.NameValueListBase). The child objects in this collection expose properties Key and Value. </font>

<font face="Calibri" color="#000000" size="3">You can see how the ComboBox uses the DisplayMemberPath to specify that the Value property from the name/value list should be displayed to the user, and the SelectedValuePath specifies that the Key value from the list should be used to select the current item (the Key value is not displayed to the user).</font>

<font face="Calibri" color="#000000" size="3">Then notice that the SelectedValue property is used to bind to the main business object. This binding statement sets a path to a property on the overall DataContext for the ComboBox, which in my case is actually set through code at the Page object level:</font>

<font size="3"><font color="#000000"><font face="Calibri"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>this.DataContext = project;</font></font></font>

<font face="Calibri" color="#000000" size="3">So all controls on the entire page, by default, bind to a Project object, and this includes the ComboBox.</font>

<font face="Calibri" color="#000000" size="3">Remember though, that the Role property on the Project is a numeric index value. And so is the Key value from the name/value list. The ComboBox control connects these two automatically. So when the business object’s Role property changes, the ComboBox automatically changes the displayed/selected item. Conversely, when the user changes the ComboBox selected item, that automatically causes the business object’s Role property to change.</font>


