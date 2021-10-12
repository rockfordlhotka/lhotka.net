---
title: Executing a workflow
postDate: 2007-08-01T17:15:26.5704624-05:00
abstract: 
postStatus: publish
---
01 August 2007

I wrote the following for the *Using CSLA .NET 3.0* ebook, but I don't think I'm going to use it now, because I've wrapped most of this into a new class in CSLA .NET. Rather than letting this go to waste though, I thought I'd post it here. Remember that it is just draft content, so it may have typos or errors, but perhaps it will be useful to someone:

## *<font face="Arial" color="#000000">Basic Workflow Execution</font>*

<font face="Times New Roman" color="#000000" size="3">Executing a workflow is a little tricky, because workflows default to running on a background thread. That means you must take steps to ensure that the workflow completes before the host process terminates.</font>

<font face="Times New Roman" color="#000000" size="3">One way to solve this issue is to always execute a workflow synchronously. Another is to use a thread synchronization object to prevent the process from terminating until the workflow completes.</font>


<font size="3"><font color="#000000"><font face="Times New Roman"><b style="mso-bidi-font-weight: normal">Note: </b>It is also possible to suspend and resume workflows, and even to unload them from memory so they store their state in a database. Later you can reload that workflow instance and resume it. These advanced scenarios are outside the scope of this book</font></font></font>


### <font face="Arial" color="#000000">Synchronous Execution</font>

<font face="Times New Roman" color="#000000" size="3">The code to synchronously execute a workflow follows a standard pattern:</font>

<font face="Times New Roman"><span style="mso-list: Ignore"><font color="#000000"><font size="3">1.</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></font></span><font color="#000000" size="3">Create an instance of the </font></font><font face="Courier New" color="#008000">WorkflowRuntime</font><font face="Times New Roman" color="#000000" size="3">.</font>

<font face="Times New Roman"><span style="mso-list: Ignore"><font color="#000000"><font size="3">2.</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></font></span><font color="#000000" size="3">Create a synchronization object.</font></font>

<font face="Times New Roman"><span style="mso-list: Ignore"><font color="#000000"><font size="3">3.</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></font></span><font color="#000000" size="3">Set up event handlers.</font></font>

<font face="Times New Roman"><span style="mso-list: Ignore"><font color="#000000"><font size="3">4.</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></font></span><font color="#000000" size="3">Create workflow instance.</font></font>

<font face="Times New Roman"><span style="mso-list: Ignore"><font color="#000000"><font size="3">5.</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></font></span><font color="#000000" size="3">Ensure you have a valid principal object.</font></font>

<font face="Times New Roman"><span style="mso-list: Ignore"><font color="#000000"><font size="3">6.</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></font></span><font color="#000000" size="3">Start the workflow.</font></font>

<font face="Times New Roman"><span style="mso-list: Ignore"><font color="#000000"><font size="3">7.</font><span style="FONT: 7pt 'Times New Roman'">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></font></span><font color="#000000" size="3">Wait for the workflow to complete.</font></font>

<font face="Times New Roman" color="#000000" size="3">The only step unique to CSLA .NET is number 5, and that is only required if you are using custom authentication. The WF runtime will automatically ensure that the background thread that executes the workflow has the same principal as the thread that calls the workflow’s </font><font face="Courier New" color="#008000">Start()</font><font face="Times New Roman" color="#000000" size="3"> method, but you must ensure that the principal is set on the current thread before calling </font><font face="Courier New" color="#008000">Start()</font><font face="Times New Roman" color="#000000" size="3">.</font>

<font face="Times New Roman" color="#000000" size="3">The following code implements these steps to execute the </font><font face="Courier New" color="#008000">ProjectWorkflow</font><font face="Times New Roman" color="#000000" size="3"> implemented earlier in this chapter:</font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>using (WorkflowRuntime workflowRuntime = new WorkflowRuntime())</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Exeception error = null;</font></font>

<?xml:namespace prefix = o ns = "urn:schemas-microsoft-com:office:office" /><o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>AutoResetEvent waitHandle = new AutoResetEvent(false);</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>workflowRuntime.WorkflowCompleted += </font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>delegate(object sender, WorkflowCompletedEventArgs e) </font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>waitHandle.Set(); </font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>};</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>workflowRuntime.WorkflowTerminated += </font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>delegate(object sender, WorkflowTerminatedEventArgs e)</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>error = e.Exception;</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>waitHandle.Set();</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>};</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// create workflow instance</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Dictionary&lt;string,object&gt; parameters = new Dictionary&lt;string,object&gt;();</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>parameters.Add("ProjectId", projectId);</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>WorkflowInstance instance = </font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>workflowRuntime.CreateWorkflow(</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>typeof(PTWorkflow.ProjectWorkflow), </font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>parameters);</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// login before starting WF instance</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>ProjectTracker.Library.Security.PTPrincipal.Login("pm", "pm");</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// execute workflow</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>instance.Start();</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// wait for workflow to complete</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>waitHandle.WaitOne();</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span style="mso-spacerun: yes">&nbsp;</span>// throw any workflow exception</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>if (error != null)</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>throw error;</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>}</font></font>


<font face="Times New Roman" color="#000000" size="3">Creating the workflow instance involves setting up a </font><font face="Courier New" color="#008000">Dictionary&lt;string, object&gt;</font><font face="Times New Roman" color="#000000" size="3"> that contains name/value pairs for any parameters to be passed into th workflow instance:</font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// create workflow instance</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Dictionary&lt;string,object&gt; parameters = new Dictionary&lt;string,object&gt;();</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>parameters.Add("ProjectId", projectId);</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>WorkflowInstance instance = </font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>workflowRuntime.CreateWorkflow(</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;</span>typeof(PTWorkflow.ProjectWorkflow), </font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>parameters);</font></font>


<font face="Times New Roman" color="#000000" size="3">The name in the dictionary must correspond to the name of a dependency property defined by the workflow, and of course the type of the value must match the dependency property type.</font>

<font face="Times New Roman" color="#000000" size="3">Keep in mind that creating an instance of a workflow does not <i style="mso-bidi-font-style: normal">start</i> the workflow. The workflow won’t start executing until the </font><font face="Courier New" color="#008000">Start()</font><font face="Times New Roman" color="#000000" size="3"> method is called later in the code.</font>

<font face="Times New Roman" color="#000000" size="3">The </font><font face="Courier New" color="#008000">waitHandle</font><font face="Times New Roman" color="#000000" size="3"> synchronization object is the key to making this process synchronous. The </font><font face="Courier New" color="#008000">waitHandle</font><font face="Times New Roman" color="#000000" size="3"> object starts out unset because </font><font face="Courier New" color="#008000">false</font><font face="Times New Roman" color="#000000" size="3"> is passed to its constructor as its initial state:</font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>AutoResetEvent waitHandle = new AutoResetEvent(false);</font></font>


<font face="Times New Roman" color="#000000" size="3">At the bottom of the code is a line that calls </font><font face="Courier New" color="#008000">WaitOne()</font><font face="Times New Roman" color="#000000" size="3">, thus blocking the current thread until </font><font face="Courier New" color="#008000">waitHandle</font><font face="Times New Roman" color="#000000" size="3"> is set:</font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// execute workflow</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>instance.Start();</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// wait for workflow to complete</font></strong></font></font>


**<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>waitHandle.WaitOne();</font></font>**


<font face="Times New Roman" color="#000000" size="3">While the current (starting) thread is blocked, the workflow is busy executing on a background thread. In other words, the </font><font face="Courier New" color="#008000">Start()</font><font face="Times New Roman" color="#000000" size="3"> call returns immediately, having just started the workflow instance executing on a background thread. Without the </font><font face="Courier New" color="#008000">WaitOne()</font><font face="Times New Roman" color="#000000" size="3"> call, the current thread would exit the code block, which would dispose the WF engine instance while it is executing the workflow. The result would be an exception.</font>

<font face="Times New Roman" color="#000000" size="3">Notice how the event handlers for the </font><font face="Courier New" color="#008000">WorkflowCompleted</font><font face="Times New Roman" color="#000000" size="3"> and </font><font face="Courier New" color="#008000">WorkflowTerminated</font><font face="Times New Roman" color="#000000" size="3"> events both call </font><font face="Courier New" color="#008000">waitHandle.Set()</font><font face="Times New Roman" color="#000000" size="3">. These events are raised by the WF engine when the workflow either completes or terminates unexpectedly. Either way, by calling the </font><font face="Courier New" color="#008000">Set()</font><font face="Times New Roman" color="#000000" size="3"> method, the current thread is released so it can continue running.</font>

<font face="Times New Roman" color="#000000" size="3">In the case of a workflow terminating unexpectedly, the exception from the workflow is made available to the </font><font face="Courier New" color="#008000">WorkflowTerminated</font><font face="Times New Roman" color="#000000" size="3"> event handler. You can choose what to do with this information as appropriate for your application. One technique is shown here, which is to store the </font><font face="Courier New" color="#008000">Exception</font><font face="Times New Roman" color="#000000" size="3"> object in a field:</font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>delegate(object sender, WorkflowTerminatedEventArgs e)</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{</font></font>

**<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>error = e.Exception;</font></font></font>**

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>waitHandle.Set();</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>};</font></font>


<font face="Times New Roman" color="#000000" size="3">And then have the current thread throw the exception once it is unblocked:</font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// wait for workflow to complete</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>waitHandle.WaitOne();</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// throw any workflow exception</font></strong></font></font>

<font color="#000000"><font style="BACKGROUND-COLOR: #d9d9d9"><strong><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp; </span><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;</span>if (error != null)</font></strong></font></font>


**<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>throw error;</font></font>**


<font face="Times New Roman" color="#000000" size="3">The result of this code is that the workflow appears to run synchronously, even though it really executes on a background thread.</font>

### <font face="Arial" color="#000000">Asynchronous Execution</font>

<font face="Times New Roman" color="#000000" size="3">Allowing a workflow to run asynchronously is just a slightly more complex version of running the workflow synchronously. The important thing is to ensure that your process doesn’t exit until the workflow is complete. This means that the synchronization object must be available at a broader scope so you can write code to prevent the application from closing if the workflow is still running.</font>

<font face="Times New Roman" color="#000000" size="3">You also must come up with a way to deal with any exception object in the case that the workflow terminates unexpectedly. One solution is to elevate the </font><font face="Courier New" color="#008000">error</font><font face="Times New Roman" color="#000000" size="3"> field from the previous example to a broader scope as well.</font>

<font face="Times New Roman" color="#000000" size="3">Finally, the </font><font face="Courier New" color="#008000">WorkflowRuntime</font><font face="Times New Roman" color="#000000" size="3"> instance must remain in memory until the workflow completes.</font>

<font face="Times New Roman" color="#000000" size="3">This means that you must define these fields so they exist at an application level, for instance using </font><font face="Courier New" color="#008000">static</font><font face="Times New Roman" color="#000000" size="3"> fields:</font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>private static AutoResetEvent _waitHandle = null;</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>private static Exception _workflowError = null;</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp; </span>private static WorkflowRuntime _workflowRuntime = null;</font></font>


<font face="Times New Roman" color="#000000" size="3">Then you can create a method to start the workflow:</font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>public static void BeginWorkflow(Guid projectId)</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>{</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_workflowRuntime = new WorkflowRuntime();</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_waitHandle = new AutoResetEvent(false);</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_workflowRuntime.WorkflowCompleted += </font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>delegate(object sender, WorkflowCompletedEventArgs e) </font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_waitHandle.Set(); </font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp; </span><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>};</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_workflowRuntime.WorkflowTerminated += </font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>delegate(object sender, WorkflowTerminatedEventArgs e)</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>{</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_workflowError = e.Exception;</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_waitHandle.Set();</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>};</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// create workflow instance</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>Dictionary&lt;string,object&gt; parameters = new Dictionary&lt;string,object&gt;();</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>parameters.Add("ProjectId", projectId);</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>WorkflowInstance instance = </font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_workflowRuntime.CreateWorkflow(</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>typeof(PTWorkflow.ProjectWorkflow), </font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>parameters);</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// login before starting WF instance</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>ProjectTracker.Library.Security.PTPrincipal.Login("pm", "pm");</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// execute workflow</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>instance.Start();</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>}</font></font>


<font face="Times New Roman" color="#000000" size="3">Notice that the </font><font face="Courier New" color="#008000">WorkflowRuntime</font><font face="Times New Roman" color="#000000" size="3"> object is no longer in a </font><font face="Courier New" color="#008000">using</font><font face="Times New Roman" color="#000000" size="3"> block, so it can remain in memory, not disposed, while the workflow instance is running on the background thread.</font>

<font face="Times New Roman" color="#000000" size="3">The workflow instance is created the same as before, and its </font><font face="Courier New" color="#008000">Start()</font><font face="Times New Roman" color="#000000" size="3"> method is called. At that point this method simply ends, returning to the caller.</font>

<font face="Times New Roman" color="#000000" size="3">Once you call </font><font face="Courier New" color="#008000">BeginWorkflow()</font><font face="Times New Roman" color="#000000" size="3"> the workflow is started on a background thread, but your current thread (often the UI thread) is free to continue working.</font>

<font face="Times New Roman" color="#000000" size="3">The final piece to the puzzle is a method your application can call before it exits, or when it otherwise can’t continue without the workflow having completed:</font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>public static void EndWorkflow()</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>{</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// wait for workflow to complete</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_waitHandle.WaitOne();</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>// dispose runtime</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>_workflowRuntime.Dispose();</font></font>

<o:p><font face="Courier New" color="#000000">&nbsp;</font></o:p>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span>if (_workflowError != null)</font></font>

<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span><span style="mso-spacerun: yes">&nbsp;</span>throw _workflowError;</font></font>


<font color="#000000"><font face="Courier New"><span style="mso-spacerun: yes">&nbsp;&nbsp;&nbsp; </span>}</font></font>


<font face="Times New Roman" color="#000000" size="3">It is important to realize that this method will block the current thread until </font><font face="Courier New" color="#008000">_waitHandle</font><font face="Times New Roman" color="#000000" size="3"> is set. If the workflow completes before this method is called, then </font><font face="Courier New" color="#008000">_waitHandle</font><font face="Times New Roman" color="#000000" size="3"> is already set, and this method runs immediately, but if the workflow is still running, this method will block until the workflow completes or terminates.</font>

<font face="Times New Roman" color="#000000" size="3">For this to work, you <i style="mso-bidi-font-style: normal">must</i> call </font><font face="Courier New" color="#008000">EndWorkflow()</font><font face="Times New Roman" color="#000000" size="3"> before your process terminates to properly dispose the runtime and to determine if the workflow terminated unexpectedly.</font>


