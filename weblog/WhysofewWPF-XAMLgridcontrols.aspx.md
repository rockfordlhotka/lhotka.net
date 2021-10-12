---
title: Why so few WPF/XAML grid controls?
postDate: 2008-01-22T12:17:53.3811008-06:00
abstract: 
postStatus: publish
---
22 January 2008

in a recent email thread someone was wondering why component vendors are being so slow in coming out with grid controls for WPF/XAML.

One obvious reason is that grid controls are hard to build, and WPF/XAML is radically different from Windows Forms or Web Forms. But still, it is fair to wonder why these highly experienced control vendors haven't overcome that challenge.

I think the reason is that technology isn't the issue. At least not in the raw "learn how to use XAML" way. I think the real issue is much bigger!

Consider the incredible risk a vendor would assume by creating a grid control now.

Microsoft hasn’t come out with a WPF grid, and so there are no standard interfaces in .NET to support data binding to a grid. Certainly the current interfaces used by WPF are not nearly powerful enough to get in-place grid editing like we have in Windows Forms – and that’s a requirement if WPF is ever going to replace Windows Forms for business development.

Windows Forms and Web Forms both have benchmark grids from Microsoft. They set the standard, and define the core interaction used by data binding. The other vendors can then build around that core to do cool stuff. In particular, Windows Forms defines a whole set of powerful interfaces to allow in-place editing so the user can navigate freely in a grid, edit cells, add rows and delete rows – and press ESC to cancel changes to whatever row they are on. All features most users would consider critical to the in-place experience. The majority of those interfaces are *not used by WPF today*!! Nor does WPF have replacements for them. And if they do replace those interfaces then you can’t bind to a DataTable, which shuts out most developers from WPF again – probably a bad idea.

The WPF team has already shown that they’ll supersede existing interfaces (INotifyCollectionChanged was invented even though IBindingList was already there). So it is somewhat hard to predict where Microsoft might go in this regard. It is quite possible they’ll do the “worse of all worlds” and support the DataTable (all the existing Windows Forms interfaces) *and invent a whole new model* *as well*… (again, see INotifyCollectionChanged – invented for WPF, but IBindingList is *also fully supported by WPF*)

So in WPF the poor component vendors are really stuck. There’s no defined standard for this kind of data binding, so they need to invent it. They’ll each invent something different from the other vendors – and NONE of them will likely match whatever Microsoft eventually does. That means they are all in deep trouble when Microsoft does set the standard. And so are all consumers of those grids (all of us!).

This is very much like pre-ODBC database access, except in this case it is a very safe bet that “ODBC” is coming (in the form of some standard grid definition) and so investing in building a proprietary solution is a known dead-end. A waste of money and very likely a way to make many, many angry customers who may hate you forever.

Nasty business just now… :(
