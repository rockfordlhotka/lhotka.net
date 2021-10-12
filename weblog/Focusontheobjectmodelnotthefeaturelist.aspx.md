---
title: Focus on the object model, not the "feature list"
postDate: 2006-02-02T14:06:08.593-06:00
abstract: It is fairly common for people to focus so much on the CSLA .NET “feature list” that they forget that the purpose of the framework is merely to enable the implementation of good OO designs. It is important to remember to focus first on the business object model.
postStatus: publish
---
02 February 2006

It is fairly common for people to focus so much on the CSLA .NET “feature list” that they forget that the purpose of the framework is merely to enable the implementation of good OO designs. Many times I’ll get questions or comments asking why CSLA .NET “only” supports certain types of objects, and why it doesn’t support others.

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p>&nbsp;</o:p>

The thing is, CSLA .NET doesn't dictate your object model. All it does is enable a set of 10 or so stereotypes (in CSLA .NET 2.0), providing base classes to simplify the implementation of those stereotypes:

<o:p>&nbsp;</o:p>

·         Editable root

·         Editable child

·         Editable root collection

·         Editable child collection

·         Read-only root

·         Read-only child

·         Read-only root collection

·         Read-only child collection

·         Name-value list

·         Command

·         Process

<o:p>&nbsp;</o:p>

CSLA .NET provides base classes to minimize the code a business developer must write to implement this set of common stereotypes. But the fact is that most systems will have objects that fit into other stereotypes, and that's great! CSLA .NET doesn’t stop you from implementing those objects, and it may help you.

<o:p>&nbsp;</o:p>

If you have objects that don’t fit the stereotypes listed above, you may still find that specific CSLA .NET features are useful. For instance, if your object must move between the client and application server, the data portal is extremely valuable. This is true even for objects that don’t actually use “data” (as in a database), but may have other reasons for moving between client and server. In other cases, an object may benefit from the Security functionality in CSLA .NET, such as authorization.

<o:p>&nbsp;</o:p>

The point is that you can pick and choose the features that are of use for your particular object stereotype. If you’ll be creating multiple objects that fit this new stereotype, I recommend creating your own base class to support their creation (not necessarily by altering the Csla project itself, as that complicates updates). As much as possible, I’ve tried to keep the framework open so you can extend it by creating your own base classes – either from scratch, or inheriting from something like Csla.Core.BusinessBase, or Csla.Core.ReadOnlyBindingList.

<o:p>&nbsp;</o:p>

The key point, is that you should develop your object model based on behavioral object design principles. Then you should determine how (and if) those objects map into the existing CSLA .NET stereotypes, thus identifying where you can leverage the pre-existing base classes and tap into the functionality they provide. For objects that simply don’t fit into one of these stereotypes you can decide what (if any) CSLA .NET functionality those objects should use and you can go from there.<o:p></o:p>

<o:p>&nbsp;</o:p>

In short, the starting point should be your object model, not the “feature list” of CSLA .NET itself.
