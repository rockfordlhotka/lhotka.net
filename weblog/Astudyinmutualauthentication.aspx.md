---
title: A study in mutual authentication
postDate: 2007-07-25T15:45:17.099896-05:00
abstract: A real life experience that reinforces the complexity of bi-directional authentication.
postStatus: publish
---
25 July 2007

<font face="Calibri" color="#000000" size="3">Today I received a letter from a large (the largest?) US bank, offering me a special discount rate on charges made to my credit card.</font>

<font face="Calibri" color="#000000" size="3">To my knowledge, I have no account at this bank at all, including no such credit card. That’s never good!</font>

<font face="Calibri" color="#000000" size="3">So I called the number on the letter to find out what’s going on. Of course I got to the bank’s credit card service center, where they asked me my credit card number, let’s pick up there:</font>

<font face="Calibri" color="#000000" size="3">“That’s why I’m calling. I don’t have such a credit card” said I.</font>

<font face="Calibri" color="#000000" size="3">“I can look it up using your social security number” said she.</font>

<font face="Calibri" color="#000000" size="3">And this is when my brain finally kicked in. I had dialed the number <i style="mso-bidi-font-style: normal">from the suspicious letter!!</i> While the letter looked authentic, and the automated answering system on their end sounded authentic, how did I actually <i style="mso-bidi-font-style: normal">know</i> I was talking to this large bank?</font>

<font face="Calibri" color="#000000" size="3">“I’m not sure I want to provide that” I answered.</font>

<font face="Calibri" color="#000000" size="3">“Can I have you spell your name then?” she asked.</font>

<font face="Calibri" color="#000000" size="3">I did that, as my name is easily found, and the letter already had that. She then confirmed that I had an account with them, and asked “Can you confirm your birth date?”</font>

<font face="Calibri" color="#000000" size="3">“Umm, I’m not sure I want to provide that either. I need to look on the web site and see if your phone numbers match.”</font>

<font face="Calibri" color="#000000" size="3">“OK, can I put you on hold?”</font>

<font face="Calibri" color="#000000" size="3">“Sure.”</font>

<font face="Calibri" color="#000000" size="3">So I did. I went to their web site, clicked “Contact Us” and found different phone numbers. In the meantime she came back on the line.</font>

<font face="Calibri" color="#000000" size="3">“Did you find what you needed?” she asked.</font>

<font face="Calibri" color="#000000" size="3">“No, the numbers don’t match.”</font>

<font face="Calibri" color="#000000" size="3">“Well you have reached ____, and we do have an account in your name. If you provide your birthdate I can give you the account details.”</font>

<font face="Calibri" color="#000000" size="3">“Yeah, see that’s the problem. You can confirm <i style="mso-bidi-font-style: normal">my</i> identity, but there’s nothing you can give me that can confirm <i style="mso-bidi-font-style: normal">your</i> identity. I’m going to have to call the number on the web site to be sure.”</font>

<font face="Calibri" color="#000000" size="3">“This really is ____” she said in an exasperated tone.</font>

<font face="Calibri" color="#000000" size="3">“Well, I can’t be sure” I replied.</font>

<font face="Calibri" color="#000000" size="3">“Then do what you need to” she said, and hung up rather abruptly.</font>

<font face="Calibri" color="#000000" size="3">So I did call the number from the web site. I did have an account there. Some credit card I haven’t used since the middle of 2000. I was able to find that out without even talking to a human: their automated system handled the whole process, including my canceling the card.</font>

<font face="Calibri" color="#000000" size="3">But it sure goes to show just how complex bi-directional authentication can be. Makes a person really appreciate the work done to design Kerberos, SSL, Windows Card Services and all the other authentication schemes out there we take for granted every day…</font>
