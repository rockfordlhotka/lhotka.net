---
title: Allowing a WinRT app to do loopback network calls
postDate: 2012-03-14T20:57:34.6115275-05:00
abstract: 
postStatus: publish
---
14 March 2012

One issue I’ve encountered while building Metro-style WinRT apps on Windows 8 is the need to have my app interact with a WCF service running on the same machine.

This is obviously a common scenario for any n-tier or SOA app development. The challenge we face is that WinRT apps are blocked from calling back to localhost (127.0.0.1). The challenge and solution are described here:

http://msdn.microsoft.com/en-us/library/windows/apps/Hh780593.aspx

To find the real application name (moniker) necessary, I wrote a simple command line utility to read the registry:


> <font face="Courier New">using System;       <br>using Microsoft.Win32;</font>
>
> <font face="Courier New">namespace WinRtAppList       <br>{        <br>&#160; class Program        <br>&#160; {        <br>&#160;&#160;&#160; static void Main(string[] args)        <br>&#160;&#160;&#160; {        <br>&#160;&#160;&#160;&#160;&#160; var reg = Registry.        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; CurrentUser.OpenSubKey(&quot;Software&quot;).        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; OpenSubKey(&quot;Classes&quot;).        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; OpenSubKey(&quot;Local Settings&quot;).        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; OpenSubKey(&quot;Software&quot;).        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; OpenSubKey(&quot;Microsoft&quot;).        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; OpenSubKey(&quot;Windows&quot;).        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; OpenSubKey(&quot;CurrentVersion&quot;).        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; OpenSubKey(&quot;AppContainer&quot;).        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; OpenSubKey(&quot;Mappings&quot;);</font>
>
> <font face="Courier New">&#160;&#160;&#160;&#160;&#160; var items = reg.GetSubKeyNames();       <br>&#160;&#160;&#160;&#160;&#160; string query = null;        <br>&#160;&#160;&#160;&#160;&#160; if (args.Length &gt; 0)        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; query = args[0].ToLower();</font>
>
> <font face="Courier New">&#160;&#160;&#160;&#160;&#160; foreach (var item in items)       <br>&#160;&#160;&#160;&#160;&#160; {        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; var app = reg.OpenSubKey(item);        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; var displayName = app.GetValue(&quot;DisplayName&quot;).ToString();        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; if (string.IsNullOrEmpty(query) || displayName.ToLower().Contains(query))        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; {        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; Console.WriteLine(app.GetValue(&quot;DisplayName&quot;));        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; Console.WriteLine(&quot;&#160; SID:&#160;&#160;&#160;&#160; &quot; + item);        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; Console.WriteLine(&quot;&#160; Moniker: &quot; + app.GetValue(&quot;Moniker&quot;));        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; Console.WriteLine();        <br>&#160;&#160;&#160;&#160;&#160;&#160;&#160; }        <br>&#160;&#160;&#160;&#160;&#160; }</font>
>
> <font face="Courier New">&#160;&#160;&#160;&#160;&#160; Console.ReadLine();       <br>&#160;&#160;&#160; }        <br>&#160; }        <br>}</font>


Nothing fancy, but it helps avoid the need to dig around in the registry with regedit just to find the application moniker.
