---
title: CSLA .NET 3.0 available for download
postDate: 2007-07-10T09:56:10.06-05:00
abstract: 
postStatus: publish
---
10 July 2007

![](http://www.lhotka.net/images/csla30_logo1_72.png)CSLA .NET Version 3.0 is now available for [download](http://www.lhotka.net/cslanet/download.aspx)! Listen to the official announcement on [**.NET Rocks!**](http://www.dotnetrocks.com/default.aspx?showNum=253)

CSLA .NET 3.0 includes numerous enhancements and features of value to all CSLA .NET users, and of course version 3.0 adds support for Microsoft .NET 3.0 features like WCF and WPF.

You can use CSLA .NET 3.0 on either Microsoft .NET 2.0 or Microsoft .NET 3.0.

### Features for everyone

CSLA .NET 3.0 includes enhancements useful to all CSLA .NET 2.1.4 users, including these highlights:

#### **Validation rules**

- PropertyFriendlyName – specify a friendly name to use when displaying broken rule text
- Format – specify a format mask to use when displaying broken rule numeric values
- StringMinLength – new validation rule method
- DecoratedRuleArgs – useful for code generation of AddBusinessRules() methods
- Fix bug with stopProcessing and rule priorities
- RegEx – rule method now supports options for dealing with null values


#### **Authorization**

- New CanExecuteMethod() functionality, similar to CanReadProperty() and CanWriteProperty()


#### **Undo and Data binding**

- If edit levels get out of sync an exception is thrown, making debugging of Windows Forms data binding much easier


#### **Interfaces**

- Cleaned up and rearranged interfaces to provide more consistency – making it easier to create UI frameworks on top of CSLA business layers


#### **SmartDate**

- Added TryParse() method
- Fix bug with CompareTo() method


#### **SortedBindingList and FilteredBindingList**

- Allow access to underlying source list


#### **BusinessListBase**

- Fix some bugs where ListChanged/CollectionChanged events were raised when they shouldn't have been. The result is that some data binding scenarios now work where they didn't, and in other cases performance is improved.


#### **ProjectTracker\PTWin**

- Reworked data binding code to address all known issues


See the [**change log**](http://www.lhotka.net/weblog/ct.ashx?id=fe23b03e-c719-45fb-993b-ea4c1b74aa34&amp;url=http%3a%2f%2fwww.lhotka.net%2fArticle.aspx%3farea%3d4%26id%3d0c94aa82-b975-455b-a0c5-f4f7196a2408) for a complete list of changes.

Again, CSLA .NET 3.0 can be used *without Microsoft .NET 3.*0. If you want to build CSLA .NET 3.0 *without installing the Microsoft .NET 3.0 runtime*, you must [**define the NET20 symbol**](http://www.lhotka.net/Article.aspx?id=ac20fe4c-6afc-4176-bcb4-d74b5a370356) in project properties.

### Microsoft .NET 3.0 Features

Of course the *primary* focus of CSLA .NET 3.0 is support for Microsoft .NET 3.0. Highlights include:

#### **CSLA .NET**

- **WcfProxy** – a data portal channel that uses WCF. You can *transparently* move from any existing data portal channel to WCF by using this new proxy.
- **DataContract** – support for using the WCF DataContract and DataMember attributes in your business classes
- **WPF**
    - CslaDataProvider – a data provider control that can create, fetch, save and cancel edits on a CSLA .NET business object. In some cases this can lead to code-less data entry forms!
    - Validator – a control that provides Windows Forms ErrorProvider-like behavior to WPF forms that are data bound to CSLA .NET objects.
    - Authorizer – a control that provides Windows Forms AuthorizeReadWrite-like behaviors to WPF forms that are data bound to CSLA .NET objects.
    - ObjectStatus – a control that exposes IsValid, IsSavable and other properties from a CSLA .NET business object so they can be used by XAML data binding.
    - IdentityConverter – a value converter that can be used to work around an issue with data binding and refreshing the UI.


The Csla solution is a Visual Studio 2005 solution. You can open and build the solution in Visual Studio 2005 if you have the Microsoft .NET 3.0 runtime installed on your workstation. Or you can use the NET20 symbol to allow compilation without the Microsoft .NET 3.0 runtime.

The Csla solution automatically upgrades when opened in Visual Studio 2008, and you can build the solution in Visual Studio 2008 if you are using that environment.

#### **ProjectTracker\PTWpf**

- Added new WPF UI with equivalent functionality to PTWin.



> *Note that this project is built using Visual Studio 2008 (Orcas) Beta 1.*


#### **ProjectTracker\PTWorkflow**

- Added new Workflow UI to illustrate how a workflow can use CSLA .NET business objects



> *Note that this project is built using Visual Studio 2008 (Orcas) Beta 1.*


#### **ProjectTracker\PTWcfClient and PTWcfService**

- Added a WCF service illustrating how to expose CSLA .NET objects through WCF/SOA
- Added a WCF client app illustrating how to call a WCF service



> *Note that these projects are built using Visual Studio 2008 (Orcas) Beta 1.*


#### **ProjectTracker\WcfHost**

- Added a WCF host for the data portal



> *Note that this project is built using Visual Studio 2005 with the WCF extensions installed.*


The ProjectTracker solution includes WcfHost, but does not include the other new projects. The reason for this is that the ProjectTracker solution is still a Visual Studio 2005 solution, while these other projects are built using Visual Studio 2008. The ProjectTracker solution upgrades automatically when opened in Visual Studio 2008, and in that environment you can add the remaining projects to the solution.



### **Migration**

Migrating from version 2.1.4 to 3.0 should be relatively painless.

The only place you may encounter issues is that version 3.0 throws an exception if your edit levels get out of sync when using n-level undo. This may highlight pre-existing bugs in your UI code (especially in Windows Forms apps) that you should resolve. Look at the ProjectTracker\PTWin code for examples of the correct way to interact with Windows Forms data binding.

Migrating from 2.0.x to 3.0 has the same challenges as moving from 2.0 to 2.1. Version 2.1 introduced some significant, but important, changes to the handling of validation and authorization rules that can impact your business object code. See the [**CSLA .NET Version 2.1 Handbook**](http://www.lhotka.net/Article.aspx?area=4&amp;id=67dd2fc6-e716-48fe-8e5d-43d5eb7fbbc6) for detailed information about version 2.1.

Migrating from 1.x to 3.0 will require some effort. There are many new features in 2.1 and 3.0 as compared to 1.x, and taking advantage of those features requires changes to your business objects and your UI code. You can look at the Expert C#/VB 2005 Business Objects books and the CSLA .NET Version 2.1 Handbook to get details around the scope of the changes.

### **Futures**

I plan to write an ebook showing how to use the new features and enhancements in CSLA .NET 3.0. This ebook should be available in the third quarter of 2007 (probably September).

I’m working on CSLA .NET 3.5, based on Microsoft .NET 3.5 and focused on LINQ and various other new .NET features. Look for this in the first quarter of 2008.

I am also planning to update my Expert Business Objects books for Visual Studio 2008 and CSLA .NET version 3.5. This will probably come out in the second quarter of 2008.

You can [**see the roadmap here**](http://www.lhotka.net/cslanet/roadmap.aspx).
