---
title: WinRT BackgroundWorker type
postDate: 2011-10-12T13:32:14.3463079-05:00
abstract: 
postStatus: publish
---
12 October 2011

There is no BackgroundWorker (BW) component in WinRT. Although that is arguably a good thing, I have CSLA .NET code that relies on this component. I can’t eliminate the BW from CSLA, because I need to continue to support .NET, Silverlight, and Windows Phone, even as I add support for WinRT.

Because .NET/SL/WP7 don’t (yet) have the async/await keywords, and WinRT doesn’t have BW, I need to come up with a solution that leaves existing code/behavior alone, and yet provides comparable behavior in WinRT.

To resolve this issue, I’ve created a BackgroundWorker type for WinRT. This type hasn’t gone through extensive testing, but it is a good start at least:

http://www.lhotka.net/cslacvs/viewvc.cgi/core/trunk/Source/Csla.WinRT/Threading/BackgroundWorkerBCL.cs


```
//-----------------------------------------------------------------------// <copyright file="BackgroundWorker.cs" company="Marimer LLC">//     Copyright (c) Marimer LLC. All rights reserved.//     Website: http://www.lhotka.net/cslanet/// </copyright>// <summary>Implementation of old BCL BackgroundWorker ported to WinRT.</summary>//-----------------------------------------------------------------------using System;using System.Collections.Generic;using System.Linq;using System.Text;using System.Threading.Tasks;using Windows.UI.Core;using Windows.UI.Xaml; namespace System.ComponentModel{  public class BackgroundWorker : DependencyObject  {    private CoreDispatcher _dispatcher;     public BackgroundWorker()    {      _dispatcher = this.Dispatcher;    }     public void CancelAsync()    {      if (!WorkerSupportsCancellation)        throw new NotSupportedException();      CancellationPending = true;    }     public bool CancellationPending { get; private set; }     public event ProgressChangedEventHandler ProgressChanged;     public void ReportProgress(int percentProgress)    {      ReportProgress(percentProgress, null);    }     public void ReportProgress(int percentProgress, object userState)    {      if (ProgressChanged != null)        _dispatcher.Invoke(CoreDispatcherPriority.Normal,          (sender, args) =>          {            ProgressChanged(this, new ProgressChangedEventArgs(percentProgress, userState));          },          this, null);    }     public bool WorkerReportsProgress { get; set; }    public bool WorkerSupportsCancellation { get; set; }    public bool IsBusy { get; set; }     public event DoWorkEventHandler DoWork;    public event RunWorkerCompletedEventHandler RunWorkerCompleted;    protected virtual void OnRunWorkerCompleted(RunWorkerCompletedEventArgs e)    {      if (RunWorkerCompleted != null)        RunWorkerCompleted(this, e);    }     public void RunWorkerAsync()    {      RunWorkerAsync(null);    }     public async void RunWorkerAsync(object userState)    {      if (DoWork != null)      {        CancellationPending = false;        IsBusy = true;        try        {          var args = new DoWorkEventArgs { Argument = userState };          await Task.Run(() =>          {            DoWork(this, args);          });          IsBusy = false;          OnRunWorkerCompleted(new RunWorkerCompletedEventArgs { Result = args.Result });        }        catch (Exception ex)        {          IsBusy = false;          OnRunWorkerCompleted(new RunWorkerCompletedEventArgs { Error = ex });        }      }    }  }   public delegate void DoWorkEventHandler(object sender, DoWorkEventArgs e);   public class DoWorkEventArgs : EventArgs  {    public DoWorkEventArgs()    { }     public DoWorkEventArgs(object argument)    {      Argument = argument;    }     public object Argument { get; set; }    public bool Cancel { get; set; }    public object Result { get; set; }  }   public delegate void RunWorkerCompletedEventHandler(object sender, RunWorkerCompletedEventArgs e);   public class RunWorkerCompletedEventArgs : EventArgs  {    public RunWorkerCompletedEventArgs()    { }     public RunWorkerCompletedEventArgs(object result, Exception error, bool cancelled)    {      Result = result;      Error = error;      Cancelled = cancelled;    }     public Exception Error { get; set; }    public object Result { get; set; }    public bool Cancelled { get; set; }  }}
```


```

```
