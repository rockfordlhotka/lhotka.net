---
title: CSLA 4 highlights
postDate: 2010-04-09T23:53:36.5272358-05:00
abstract: 
postStatus: publish
---
09 April 2010

In preparation for the Twin Cities Code Camp I put together a short list showing the biggest and most important changes in CSLA 4:

- Solution/project structure
    - Projects/assemblies better organized
    - Client profile support
    - Setup project
- Business objects
    - List types now ObservableCollection&lt;T&gt;
    - New RegisterProperty() overloads
    - Automatic use of description/display attributes
    - CommandBase/CriteriaBase/CslaIdentity generic
    - Parent property public
    - Widespread use/requirement of Csla.Core.IPropertyInfo
- Business rules
    - New business rule system
    - DataAnnotations
- Authorization rules (coming)
    - New authz rule system
    - Integrated into business rule system
- LINQ to CSLA
    - Remove 3.x implementation
    - Add LinqObservableCollection and ToSyncList()
- ASP.NET MVC
    - CslaModelBinder
    - Controller
    - IModelCreator
- Silverlight
    - IDataErrorInfo
    - INotifyDataErrorInfo (coming)
    - Browsable(false)
- XAML
    - MVVM (ViewModelBase/ViewModel)
    - TriggerAction
    - Unified PropertyStatus/BusyAnimation
- Data portal
    - Open up data portal for SL
    - Pluggable proxy objects to dynamically switch app servers
    - Compressed WCF example for .NET
    - Impersonation allowed via WCF
    - Client culture flows from SL client to app server
- Reflection
    - MethodCaller uses lambda expressions

