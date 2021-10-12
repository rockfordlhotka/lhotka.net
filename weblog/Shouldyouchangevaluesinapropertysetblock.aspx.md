---
title: Should you change values in a property set block?
postDate: 2007-01-17T15:45:30.3552848-06:00
abstract: My answer: of course, a setter is merely a formalized mutator method.
postStatus: publish
---
17 January 2007

<font face="Times New Roman" color="#000000" size="3">I recently had an email discussion where I was describing why I needed to solve the problem I described in </font>[<font face="Times New Roman" size="3">this article for WPF</font>](http://www.lhotka.net/weblog/DataBindingIssueInWPFWithSolution.aspx)<font face="Times New Roman" color="#000000" size="3"> and </font>[<font face="Times New Roman" size="3">this article for Windows Forms</font>](http://www.lhotka.net/weblog/WindowsFormsBindingIssueAComponentSolution.aspx)<font face="Times New Roman" color="#000000" size="3">. </font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">In both cases the issue is that data binding doesn’t refresh the value from the data source after it updates the data source from the UI. This means that any changes to the value that occur in the property set code aren’t reflected in the UI.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">The question he posed to me was whether it was a good idea to have a property set block actually change the value. In most programming models, goes the thought, assigning a property to a value can’t result in that property value changing. So any changes to the value that occur in the set block of a property are counter-intuitive, and so you simply shouldn’t change the value in the setter code.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">Here’s my response:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">The idea of a setter (which is really just a mutator method by another name) changing a value doesn't (or shouldn't) seem counter-intuitive at all.<o:p></o:p></font></font></font>

<font face="Times New Roman" color="#000000" size="3"></font>

<font face="Times New Roman" color="#000000" size="3">If we were talking about assigning a value to a public field I’d agree entirely. But we are not. Instead we’re talking about assigning a value to a property, and that’s very different.</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font face="Times New Roman" color="#000000" size="3">If all we wanted were public fields, we wouldn't need the concept of "property" at all. The concept of "property" is merely a formalization of the following:</font>

<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

1. <font size="3"><font color="#000000"><font face="Times New Roman">public fields are bad<o:p></o:p></font></font></font>
2. <font size="3"><font color="#000000"><font face="Times New Roman">private fields are exposed through an accessor method<o:p></o:p></font></font></font>
3. <font size="3"><font color="#000000"><font face="Times New Roman">private fields are changed through a mutator method<o:p></o:p></font></font></font>
4. <font size="3"><font color="#000000"><font face="Times New Roman">creating and using accessor/mutator methods is awkward without a standard mechanism<o:p></o:p></font></font></font>


<o:p><font face="Times New Roman" color="#000000" size="3">&nbsp;</font></o:p>

<font size="3"><font color="#000000"><font face="Times New Roman">So the concept of "property" exists to standardize and formalize the idea that we need controlled access to private fields, and a standard way to change their value through a mutator method.<o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman">Consider the business rule that says a document id must follow a certain form - like </font><span style="FONT-FAMILY: 'Courier New'">SOP433</span><font face="Times New Roman">. The first three characters must be alpha and upper case, the last three must be numeric. This is an incredibly common scenario for document, product, customer and other user-entered id values.<o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman">Only a poor UI would force the user to actually enter upper case values. The user should be able to type what they want, and the software will fix it.<o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman">But putting the upper case rule in the UI is bad, because code in the UI isn't reusable, and tends to become obsolete very rapidly as technology and/or the UI design changes. There's nothing more expensive over the life of an application than a line of code in the UI. So while it is possible to implement this rule in a validation control, in JavaScript, in a button click event handler - none of those are good solutions to the real problem.<o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman">Yet if that rule is placed purely in the backend system, then the user can't get any sort of interactive response. The form must be "posted" or "transmitted" to the backend before the processing can occur. Users want to immediately see the value be upper case or they get nervous.<o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman">So then we're stuck. Many people implement the rule twice. Once in the UI to make the user happy, and once in the backend, which is the <i style="mso-bidi-font-style: normal">real</i> rule implementation. And then they try to keep those rules in sync forever - the result being an expensive, unreliable and hard to maintain system.<o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman">I've watched this cycle occur for 20 years now, and it is the same time after time. And it sucks. <o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman">This, right here, is why VB got such a bad name through the 1990’s. The VB forms designer made it way too easy to write all the logic in the UI, and without any other clear alternative that's what happened. The resulting applications are very fragile and are impossible to upgrade to the next technology (like .NET). Today, as we talk, many thousands of lines of code are being written in Windows Forms and Web Forms in exactly the same way. Those poor people will have a hell of a time upgrading to WPF, because none of their code is reusable.<o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman">What's needed is <i style="mso-bidi-font-style: normal">one</i> location for this rule. Business objects offer a workable solution here. If the object implements the rule, and the object runs on the client workstation, then (without code in the UI) the user gets immediate response and the rule is satisfied. And the rule is reusable, because the object is reusable - in a way that UI code never can be (or at least never has been).<o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman">That same object, with that same interactive rule, can be used behind Windows Forms, Web Forms, WPF and even a web services interface. The rule is always applied, because it is right there in the object. And for interactive UIs it is immediate, because it is in the field's mutator method (the property setter).<o:p></o:p></font></font></font>

<font size="3"><font color="#000000"><font face="Times New Roman"><span style="mso-spacerun: yes">&nbsp;</span><o:p></o:p></font></font></font>

<font face="Times New Roman" color="#000000" size="3">So in my mind the idea of changing a value in a setter isn't counter-intuitive at all - it is the obvious design purpose behind the property setter (mutator). Any other alternative is really just a ridiculously complex way of implementing public fields. And worse, it leaves us where we've been for 20+ years, with duplicate code and expensive, unreliable software.</font>
