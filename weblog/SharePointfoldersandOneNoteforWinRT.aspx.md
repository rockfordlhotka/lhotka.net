---
title: SharePoint folders and OneNote for WinRT
postDate: 2013-01-16T18:12:19.8252809-06:00
abstract: 
postStatus: publish
---
16 January 2013

The OneNote app for WinRT (Windows 8 native) is quite nice. And it makes it smooth and easy to interact with notebooks stored on SkyDrive.

What it doesn’t make easy is to open a notebook stored on a SharePoint site. Today I finally figured out how to open a SharePoint-hosted OneNote notebook in the WinRT version.

Put the OneNote notebook file(s) into a SharePoint sub-folder in a shared document library. The name of the sub-folder matters, because this is the name that will appear for the notebook in OneNote.

Create a string URL like this (using NotePad or something like that):

onenote:http://sharepointsite.com/sharepointsite/Shared%20Documents/MyNoteBookFolder

Then open the WinRT version of IE and attempt to navigate to that URL. This will open the WinRT version of OneNote and you’ll probably be prompted for your domain credentials. Sign in and let OneNote find and open the notebook file(s) from that folder.

You’ll now see that folder name (“MyNoteBookFolder” in my example) as a notebook on the far left-hand side of the screen.

This could be a whole lot smoother if the OneNote app actually integrated with SharePoint, but it is a decent workaround for now.
