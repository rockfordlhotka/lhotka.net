---
title: ctor bug in Xamarin/mono?
postDate: 2016-05-20T16:40:28.5945791-05:00
abstract: 
postStatus: publish
---
20 May 2016

I might have found a bug in mono, but want to see if anyone thinks I'm missing something.

The CSLA .NET framework has long included [an implementation of the System.ComponentModel.DataAnnotations namespace](https://github.com/MarimerLLC/csla/tree/master/Source/Csla.Shared/DataAnnotations) for platforms where Microsoft/Xamarin didn’t provide that functionality. These days I think that is only Windows Phone 8.1, but that includes PCL Profile111 (which is what Xamarin currently targets as well).

Of course the CSLA implementation includes the DisplayAttribute class, which is used to decorate properties in consuming classes like this:


```
[Display(Name = "blah")]
```

That "blah" value is a human readable name/label for a property.

Because mono actually provides a System.ComponentModel.DataAnnotations implementation, my PCL uses type forwarding so at runtime the PCL implementation is ignored in favor of the platform-specific implementation provided by mono. For example:


```
[assembly: System.Runtime.CompilerServices.TypeForwardedTo(typeof(System.ComponentModel.DataAnnotations.DisplayAttribute))]
```

This works great on all platforms - except Xamarin Android/iOS where mono throws an exception because it can't find a matching constructor.

The thing is that the DisplayAttribute class has only the default constructor. The syntax being used to set the Name property of the attribute is supposed to use the default ctor, and then the Name property is explicitly set. This is a relatively old feature of C# - but I kind of suspect mono has a bug around this area, as it seems to be looking for a ctor that accepts a parameter when it should use the default ctor.
