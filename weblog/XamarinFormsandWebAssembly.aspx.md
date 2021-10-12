---
title: Xamarin Forms and WebAssembly
postDate: 2018-03-15T19:58:04-05:00
abstract: 
postStatus: publish
---
15 March 2018

There's some really wonderful work happening now that mono runs in webassembly. There's the [Blazor project](https://github.com/aspnet/Blazor), and perhaps more exciting is an initiative that has [Xamarin Forms running in webassembly](https://github.com/praeclarum/Ooui/wiki/Xamarin.Forms-with-Web-Assembly).

Blazor sits on mono in webassembly and provides a Razor style UI framework. You write your .NET (C#) code to run behind an html/css UI created using Razor syntax.

[Frank A. Krueger](https://twitter.com/praeclarum) just published a different approach, where Xamarin Forms runs in the browser via webassembly, so your Xamarin Forms app (XAML + C#) runs on the client inside the browser. If you follow the above link, you'll find a nice walkthrough on how to use the dotnet command line to create a simple project and run it in a browser.

I started there, and thought it would be fun to try a more robust Xamarin Forms project using Visual Studio, XAML and code-behind. Pretty much my standard approach when building apps for iOS or Android.

Here are my steps (and the code is in GitHub as [XFOouiDemo](https://github.com/rockfordlhotka/XFOouiDemo)):

1. Run through Frank's walkthrough - in my case on Ubuntu in Windows 10 WSL (Windows Subsystem for Linux), where I have dotnet installed, and of course Linux already has python - the result is that you should have XF running in your browser with a simple button that counts clicks
2. Put the walkthrough directory on `/mnt/c` somewhere so the files are available to Windows as well as Linux - my path is `/mnt/c/src`, which is `c:\src` on the Windows side
3. Open the csproj file in Visual Studio
4. Add a NuGet reference to Xamarin.Forms (at this point you won't be able to do a `dotnet build` on Linux because XF apparently doesn't yet work correctly with .NET Core)
5. Build the project - or maybe just restore NuGet packages
6. Close and re-open VS (I found this stabilized things a lot)
7. Add a new item to the project - specifically a Xamarin Forms `ContentPage`
8. Edit the xaml to show your content, or not, as you choose
9. Edit the `Program.cs` file as shown below
10. Build the project *in Visual Studio*
11. Switch back to your WSL window and run `python server.py` to rehost your new code
12. Again navigate to `http://localhost:8000` in your browser to load your updated app, and you should see your new XAML-based content


The updated `program.cs` file is this:


```c
using System;
using Ooui;
using Xamarin.Forms;

namespace MyFormsApp
{
  class Program
  {
    static void Main(string[] args)
    {
      // Initialize Xamarin.Forms
      Forms.Init();

      // Create the UI
      var page = new Page1();

      // Publish a root element to be displayed
      UI.Publish("/", page.GetOouiElement());
    }
  }
}
```

Basically just replace all the manual creation of controls with an instance of your XAML page (in my case `Page1.xaml`).

What might bend your brain a little here, is that it might appear that I'm compiling the code on Windows and running it on Linux. But that *is not what's happening*. Remember that the code is running in your browser, not on Windows OR on Linux. So it doesn't matter whether you compile on Linux or Windows, the output of the compilation is wasm code that's downloaded to the browser where it is executed.
