---
title: Using CSLA .NET 3.0 ebook available (and CSLA .NET version 3.0.2)
postDate: 2007-09-28T16:21:26.962-05:00
abstract: 
postStatus: publish
---
28 September 2007

[![](http://www.lhotka.net/images/csla30cscover-165.jpg)](http://store.lhotka.net)

CSLA .NET version 3.0 adds support for Microsoft .NET 3.0 features. This ~120 page ebook covers how to use these new capabilities:



- Windows Presentation Foundation (WPF)
    - Creating WPF forms using business objects
    - Using the new controls in the Csla.Wpf namespace
        - CslaDataProvider
        - Validator
        - Authorizer
        - ObjectStatus
        - IdentityConverter
    - Maximizing XAML and minimizing C#/VB code
- Windows Communication Foundation (WCF)
    - Using the new WCF data portal channel to seamlessly upgrade from Remoting, Web services or Enterprise Services
    - Building WCF services using business objects
    - Applying WCF security to encrypt data on the wire
    - Sending username/password credentials to a WCF service
        - Including use of the new Csla.Security.PrincipalCache class
    - Using the DataContract attribute instead of the Serializable attribute
- Windows Workflow Foundation (WF)
    - Creating activities using business objects
    - Invoking a workflow from a business object
    - Using the WorkflowManager class in the Csla.Workflow namespace


Version 3.0 is an *additive update*, meaning that you only need to use the .NET 3.0 features if you are using .NET 3.0. CSLA .NET 3.0 *is useful [for people using .NET 2.0](http://www.lhotka.net/Article.aspx?area=4&amp;id=ac20fe4c-6afc-4176-bcb4-d74b5a370356)!!* These features include:

- Enhancements to the validation subsystem
    - Friendly names for properties
    - Better null handling in the RegExMatch rule method
    - New StringMinLength rule method
    - Help for code generation through the DecoratedRuleArgs class
- Data binding issues
    - Fixed numerous bugs in BusinessListBase to improve data binding behavior
    - Throw exception when edit levels get out of sync, making debugging easier
    - N-level undo changed to provide parity with Windows Forms data binding requirements
- AutoCloneOnUpdate
    - Automatically clone objects when Save() is called, but only when data portal is local
- Enhancements to the authorization subsystem
    - CanExecuteMethod() allows authorization for arbitrary methods


CSLA .NET 3.0 includes numerous bug fixes and some feature enhancements that benefit everyone. If you are using version 2.0 or 2.1, you should consider upgrading to 3.0 to gain these benefits, even if you aren't using .NET 3.0.

See the change logs for [version 3.0](http://www.lhotka.net/Article.aspx?area=4&amp;id=0c94aa82-b975-455b-a0c5-f4f7196a2408), [version 3.0.1](http://www.lhotka.net/Article.aspx?area=4&amp;id=4534c39c-c5d8-4553-88af-bdc1c8149cbc) and [version 3.0.2](http://www.lhotka.net/Article.aspx?area=4&amp;id=7360998d-d842-49f6-b1f0-a21b517798e3) for a more detailed list of changes.

*Using CSLA .NET 3.0* is completely focused on how to use the new features in version 3.0. The book does not detail the internal changes to CSLA .NET itself, so all ~120 pages help you use the enhancements added since version 2.1.

<font size="5">Get the book at </font>[<font size="5">store.lhotka.net</font>](http://store.lhotka.net/)<font size="5">. <br>(C# available now, VB available in early October)</font>

Download the 3.0.2 code from the [CSLA .NET download page](http://www.lhotka.net/cslanet/download.aspx).
