---
title: Windows 8 Terminology and Concepts
postDate: 2012-08-03T11:03:20.2568996-05:00
abstract: 
postStatus: publish
---
03 August 2012

With all the new terminology and conceptual surface area that comes with Windows 8, I think it is important to have some clarity and consistency around the terms and concepts.

Here are some of the basic terms:

- **Windows 8** – the new operating system that runs in a “dual mode”: Desktop (Win32) and WinRT (Windows Runtime)
- **Desktop** – the Win32 OS API that supports today’s applications in Win8 (basically Windows 7)
- **WinRT** – Windows Runtime: the new OS API that supports “modern” applications
- **Windows RT** – Windows 8 on ARM devices (note: Windows RT and WinRT are not the same thing)
- **Windows 8 UI style** – a user experience design language often used when building WinRT applications


Windows 8 basically includes two different operating systems.

One is the “old” Win32 OS we think of today as Windows 7. This is now called Windows 8 Desktop, and is available on Windows 8 Intel tablets, laptops, and desktops. This is only partially available on ARM devices, and you should not expect to build or deploy Win32 Desktop apps to ARM devices.

The other is the new Windows Runtime (WinRT) “operating system”. This is a whole new platform for apps, and is available on all Windows 8 machines (ARM, Intel, tablet, laptop, desktop). If you want the widest reach for your apps going forward, you should be building your apps for WinRT.

Confusingly enough, “Windows 8” runs on Intel devices/computers. “Windows RT” is Windows 8 for ARM devices. The only real difference is that Windows RT won’t allow you to deploy Win32 Desktop apps. Windows RT does have a Desktop mode, but only Microsoft apps can run there. Again, if you want to build a Windows 8 app that works on all devices/computers, build the app for WinRT, because it is consistently available.

Windows 8 UI style describes a user experience design language for the look and feel of WinRT apps. This isn’t a technology, it is a set of design principles, concepts, and guidelines.

Another source of confusion is that to build a WinRT app in Visual Studio you need to create a “Windows 8 UI style” app. What makes this odd, is that this type of app is targeting WinRT, and it is entirely up to you to conform to the Windows 8 UI style guidelines as you build the app.

“Windows 8 UI style” was called “Metro style”, but Microsoft has dropped the use of the term “Metro”. I am skeptical that this new “Windows 8 UI style” term will last long-term, because it obviously makes little sense for Windows Phone 8, Xbox, Windows 9, and other future platforms that may use the same UI style. But for now, this appears to be the term Microsoft is using.

Thinking about app development now, there are several options on the Microsoft platforms.


|   | **Technologies** | **Platforms** |
| --- | --- | --- |
| Full .NET 4.5 | ASP.NET, WPF, Windows Forms, WCF, WF | Windows 7, Windows 8 Desktop, Windows Server 2008, Windows Server 2012 |
| WinRT .NET 4.5 | Windows 8 UI style apps | Windows 8 WinRT, Windows Phone 8, rumored for next-gen Xbox |
| Full .NET 4 | ASP.NET, WPF, Windows Forms, WCF, WF | Windows 7, Windows Server 2008, Azure PaaS |
| Silverlight | Silverlight | Windows 7, Windows 8 Desktop, Windows Phone 7, Windows Phone 8 |

