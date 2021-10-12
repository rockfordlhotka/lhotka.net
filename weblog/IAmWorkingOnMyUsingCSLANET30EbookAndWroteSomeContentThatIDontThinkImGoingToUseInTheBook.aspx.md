---
title: I Am Working On My Using CSLA NET 30 Ebook And Wrote Some Content That I Dont Think Im Going To Use In The Book
postDate: 2007-08-23T16:35:30.5524384-05:00
abstract: 
postStatus: publish
---
23 August 2007

I am working on my *Using CSLA .NET 3.0* ebook and wrote some content that I don't think I'm going to use in the book now. But I don't want to waste the effort, so I'm posting it here.

The text discusses an answer to a common question: how do I get my read-only list of X to know that some X data has been changed. Obviously the following technique can't detect that *some other user* has changed some data, but at least it detects and handles the case where the current user changes some data that would impact an existing read-only list in that same process.



<font face="Times New Roman" color="#000000" size="3">Another common example occurs when there is a read-only list that should be updated when an associated editable object is saved. For instance, you might have a </font><font face="Courier New" color="#008000">CustomerList</font><font face="Times New Roman" color="#000000" size="3"> object that should be updated any time a </font><font face="Courier New" color="#008000">Customer</font><font face="Times New Roman" color="#000000" size="3"> is saved.</font>

<font face="Times New Roman" color="#000000" size="3">To solve that issue, the </font><font face="Courier New" color="#008000">CustomerList</font><font face="Times New Roman" color="#000000" size="3"> object needs to subscribe to an event that is raised any time a </font><font face="Courier New" color="#008000">Customer</font><font face="Times New Roman" color="#000000" size="3"> is saved. Such an event should be a&nbsp;<span class="CodeInline"><span style="FONT-SIZE: 9pt; mso-bidi-font-size: 10.0pt; mso-bidi-font-family: 'Times New Roman'"><font face="Courier New" color="#008000">static </font></span></span>event on the </font><font face="Courier New" color="#008000">Customer</font><font face="Times New Roman" color="#000000" size="3"> class:</font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>public class Customer : BusinessBase&lt;Customer&gt;</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>{</font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>public static event EventHandler&lt;Csla.Core.SavedEventArgs&gt; CustomerSaved;</font></strong></font></font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font style="BACKGROUND-COLOR: #d9d9d9" face="Courier New" color="#000000"><strong>&nbsp;</strong></font></o:p>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>protected static virtual void OnCustomerSaved(Customer sender, Csla.Core.SavedEventArgs e)</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>{</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>if (CustomerSaved != null)</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>CustomerSaved(sender, e);</font></strong></font></font>

**<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>}</font></font></font>**

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>// ...</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>protected override Customer Save()</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>{</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Customer result = base.Save();</font></font>

**<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>OnCustomerSaved(this, new Csla.Core.SavedEventArgs(result));</font></font></font>**

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>return result;</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>}</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>}</font></font>


<font face="Times New Roman" color="#000000" size="3">The </font><font face="Courier New" color="#008000">CustomerSaved</font><font face="Times New Roman" color="#000000" size="3"> event is declared using the standard </font><font face="Courier New" color="#008000">EventHandler&lt;T&gt;</font><font face="Times New Roman" color="#000000" size="3"> model, where the argument parameter is of type </font><font face="Courier New" color="#008000">Csla.Core.SavedEventArgs</font><font face="Times New Roman" color="#000000" size="3">. The reason for the use of this type is that it includes a reference to the new object instance created as a result of the </font><font face="Courier New" color="#008000">Save()</font><font face="Times New Roman" color="#000000" size="3"> call.</font>

<font face="Times New Roman" color="#000000" size="3">Then the </font><font face="Courier New" color="#008000">Save()</font><font face="Times New Roman" color="#000000" size="3"> method is overridden so the </font><font face="Courier New" color="#008000">CustomerSaved</font><font face="Times New Roman" color="#000000" size="3"> event can be raised after the call to </font><font face="Courier New" color="#008000">base.Save()</font><font face="Times New Roman" color="#000000" size="3">.</font>

<font face="Times New Roman" color="#000000" size="3">The </font><font face="Courier New" color="#008000">CustomerList</font><font face="Times New Roman" color="#000000" size="3"> class can then handle this </font><font face="Courier New" color="#008000">static</font><font face="Times New Roman" color="#000000" size="3"> event to be notified as any </font><font face="Courier New" color="#008000">Customer</font><font face="Times New Roman" color="#000000" size="3"> object is saved:</font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>public class CustomerList : ReadOnlyListBase&lt;CustomerList, CustomerInfo&gt;</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>{</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>private CustomerList()</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>{</font></font>

**<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Customer.CustomerSaved += new EventHandler&lt;Csla.Core.SavedEventArgs&gt;(Customer_Saved);</font></font></font>**

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>}</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>private void Customer_Saved(object sender, Csla.Core.SavedEventArgs e)</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>{</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// find item corresponding to sender</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// and update item with e.NewObject</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Customer old = (Customer)sender;</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>if (old.IsNew)</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// it is a new item</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>IsReadOnly = false;</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Add(CustomerInfo.LoadInfo((Customer)e.NewObject));</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>IsReadOnly = true;</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>}</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>else</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// it is an existing item</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>foreach (CustomerInfo child in this)</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span><span style="mso-spacerun: yes">&nbsp;&nbsp;</span><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>if (child.Id == old.Id)</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span><span style="mso-spacerun: yes">&nbsp;&nbsp;</span><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;</span>{</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span style="mso-spacerun: yes">&nbsp;&nbsp;</span><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;</span>child.UpdateValues((Customer)e.NewObject);</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>break;</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>}</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>}</font></strong></font></font>

**<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>}</font></font></font>**


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>}</font></font>


<font face="Times New Roman" color="#000000" size="3">The final requirement is that the read-only </font><font face="Courier New" color="#008000">CustomerInfo</font><font face="Times New Roman" color="#000000" size="3"> business object implement a </font><font face="Courier New" color="#008000">LoadInfo()</font><font face="Times New Roman" color="#000000" size="3"> factory method, and an </font><font face="Courier New" color="#008000">UpdateValues()</font><font face="Times New Roman" color="#000000" size="3"> method.</font>

<font face="Times New Roman" color="#000000" size="3">The </font><font face="Courier New" color="#008000">LoadInfo()</font><font face="Times New Roman" color="#000000" size="3"> factory method is used to initialize a new instance of the read-only object with the data from the new </font><font face="Courier New" color="#008000">Customer</font><font face="Times New Roman" color="#000000" size="3"> object. Loading the data from the </font><font face="Courier New" color="#008000">Customer</font><font face="Times New Roman" color="#000000" size="3"> object avoids having to reload the data from the database when it is already available in memory:</font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>internal static CustomerInfo LoadInfo(Customer cust)</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>{</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>CustomerInfo info = new CustomerInfo();</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>info.UpdateValues(cust);</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>return info;</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>}</font></font>


<font face="Times New Roman" color="#000000" size="3">The </font><font face="Courier New" color="#008000">UpdateValues()</font><font face="Times New Roman" color="#000000" size="3"> method sets the read-only object’s fields based on the values from the </font><font face="Courier New" color="#008000">Customer</font><font face="Times New Roman" color="#000000" size="3"> object:</font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>internal void UpdateValues(Customer cust)</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>{</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>_id = cust.Id;</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>_name = cust.Name;</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>// and so on ...</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>}</font></font>


<font face="Times New Roman" color="#000000" size="3">The end result is that the </font><font face="Courier New" color="#008000">CustomerList</font><font face="Times New Roman" color="#000000" size="3"> object is updated to reflect changes to the saved </font><font face="Courier New" color="#008000">Customer</font><font face="Times New Roman" color="#000000" size="3"> object. The </font><font face="Courier New" color="#008000">CustomerSaved</font><font face="Times New Roman" color="#000000" size="3"> event notifies </font><font face="Courier New" color="#008000">CustomerList</font><font face="Times New Roman" color="#000000" size="3"> of the change, and (in most cases) </font><font face="Courier New" color="#008000">CustomerInfo</font><font face="Times New Roman" color="#000000" size="3"> can update itself without hitting the database by loading the data from the </font><font face="Courier New" color="#008000">Customer</font><font face="Times New Roman" color="#000000" size="3"> object that is already in memory.</font>
