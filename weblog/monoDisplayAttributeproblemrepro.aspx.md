---
title: mono DisplayAttribute problem repro
postDate: 2016-05-25T13:51:26.0453276-05:00
abstract: 
postStatus: publish
---
25 May 2016

The CSLA PCL that supports Xamarin includes an implementation of `System.ComponentModel.DataAnnotations`, and that includes numerous types, one of which is `DisplayAttribute`.

The PCL uses type forwarding so at runtime the platform's DataAnnotations implementation is used (if available), and the CSLA implementation is only used at runtime for platforms where there's not already an implementation (WinRT Phone is the only remaining platform afaik).

There is a problem with Xamarin however, where all types seem to forward and work fine *except* for `DisplayAttribute`. The problem in this case is that at runtime it seems that mono is unable to locate the correct ctor for the type:


```
"System.MissingMethodException: Method 'DisplayAttribute..ctor' not found.\n  at (wrapper managed-to-native) System.MonoCustomAttrs:GetCustomAttributesInternal (System.Reflection.ICustomAttributeProvider,System.Type,bool)\n  at System.MonoCustomAttrs.GetCustomAttributesBase (ICustomAttributeProvider obj, System.Type attributeType, Boolean inheritedOnly) [0x00019] in /Users/builder/data/lanes/3236/ee215fc9/source/mono/mcs/class/corlib/System/MonoCustomAttrs.cs:128 \n  at System.MonoCustomAttrs.GetCustomAttributes (ICustomAttributeProvider obj, System.Type attributeType, Boolean inherit) [0x00040] in /Users/builder/data/lanes/3236/ee215fc9/source/mono/mcs/class/corlib/System/MonoCustomAttrs.cs:158 \n  at System.Reflection.MonoProperty.GetCustomAttributes (System.Type attributeType, Boolean inherit) [0x00000] in /Users/builder/data/lanes/3236/ee215fc9/source/mono/mcs/class/corlib/System.Reflection/MonoProperty.cs:317 \n  at Csla.Core.FieldManager.DefaultPropertyInfoFactory.GetFriendlyNameFromAttributes (System.Ty
pe type, System.String name) [0x00011] in <filename unknown>:0 \n  at Csla.Core.FieldManager.DefaultPropertyInfoFactory.Create[T] (System.Type containingType, System.String name) [0x00000] in <filename unknown>:0 \n  at Csla.ReadOnlyBase`1[T].RegisterProperty[P] (System.Linq.Expressions.Expression`1 propertyLambdaExpression) [0x0001c] in <filename unknown>:0 \n  at ProjectTracker.Library.ProjectInfo..cctor () [0x00000] in G:\\src\\rdl\\csla\\Samples\\ProjectTracker\\ProjectTracker.BusinessLibrary.Shared\\ProjectInfo.cs:10 "
```

This exception occurs when the consume app attempts to access the `DisplayAttribute` associated with a property to retrieve values from the attribute. It appears that mono is unable to create an instance of the attribute object because it can't find the ctor. The `DisplayAttribute` class has only a default ctor, but is typically initialized using named parameters, such as:


```
[Display(Name = "foo")]
```

I don't know what kind of ctor mono is looking for when it fails, but it obviously isn't finding the default ctor and then setting the property value, which is what would be the expected behavior.

I’m tracking this issue in the CSLA GitHub repo: https://github.com/MarimerLLC/csla/issues/579

### Steps to reproduce issue

The CSLA ProjectTracker reference app in my fork includes a repro of this issue. To see the issue, do the following:

1. Clone my fork of CSLA from https://github.com/rockfordlhotka/csla.git
2. Checkout the 505-xamarin branch: https://github.com/rockfordlhotka/csla/tree/505-xamarin
3. Open the \Samples\ProjectTracker\ProjectTracker.sln solution
4. Build the solution – it’ll pull down the CSLA .NET framework from NuGet
5. Set a breakpoint in the XamarinFormsUi.ViewModels.ProjectList class as shown here

[![snip_20160525134558](binary/Open-Live-Writer/mono-DisplayAttribute-problem-repro_C06D/snip_20160525134558_thumb.png "snip_20160525134558")](binary/Open-Live-Writer/mono-DisplayAttribute-problem-repro_C06D/snip_20160525134558_2.png)
6. Set the startup app to ProjectTracker.Ui.Xamarin.Droid
7. Run the app in debug mode (on an emulator or device)
8. On the first screen click the All Projects button

[![snip_20160525134836](binary/Open-Live-Writer/mono-DisplayAttribute-problem-repro_C06D/snip_20160525134836_thumb.png "snip_20160525134836")](binary/Open-Live-Writer/mono-DisplayAttribute-problem-repro_C06D/snip_20160525134836_2.png)


That’ll attempt to load the ProjectList page and ProjectList viewmodel. At this point the exception will occur and you’ll end up on the breakpoint because of the failure to create an instance of ProjectInfo, but that fails because mono can’t create an instance of DisplayAttribute (used on some properties in the ProjectInfo class).
