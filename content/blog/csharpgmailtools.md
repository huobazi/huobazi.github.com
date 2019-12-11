---
layout: post
title: 'C# .Net Gmail Tools '
comments: true
date: 2008-02-21
tags:
- ASP.NET
- Asp.net
- Gmail
---

<p>位于<font face="Verdana">code.msdn.microsoft.com</font>的一个小型Library<br /><br />你可以很简单的使用它来通过gmail发送邮件或者获取Gmail Atom Feed 。<br /><br /> <br /></p>
<p></p>
<div class="codeDiv">  
 //Send a message with one line of code <br /><br />   RC.Gmail.GmailMessage.SendFromGmail("username", "password", "toAddress@gmail.com", "subject", "message body"); <br /><br /><br /><br />   //Send a message with one line of code with a MailMessage object <br /><br />   RC.Gmail.GmailMessage.SendMailMessageFromGmail("username", "password", mailMessageObject); <br /><br /><br /><br />   //Use the GmailMessage object to create and send your message <br /><br />   RC.Gmail.GmailMessage gmailMsg = new RC.Gmail.GmailMessage("username", "password"); <br /><br />   gmailMsg.To = "RCcode@gmail.com"; <br /><br />   gmailMsg.From = "fromAddress@gmail.com"; <br /><br />   gmailMsg.Subject = "C# Test Message"; <br /><br />   gmailMsg.Body = "Test body"; <br /><br /><br /><br />   MailAttachment attachment = new MailAttachment(@"c:\testfile.txt"); <br /><br />   gmailMsg.Attachments.Add(attachment); <br /><br /><br /><br />   gmailMsg.Send();<br /><br /><p> </p>
</div>
<p></p>
<p><a href="http://code.msdn.microsoft.com/CSharpGmail" target="_blank" mce_href="http://code.msdn.microsoft.com/CSharpGmail"><strong>Visit here to download the GMail Tools</strong></a><br /><br /></p>
<div class="codeDiv">
<p>// Create the object and get the feed <br /><br />   RC.Gmail.GmailAtomFeed gmailFeed = new RC.Gmail.GmailAtomFeed("username", "password"); <br /><br />   gmailFeed.GetFeed(); <br /><br /><br /><br />   // Access the feeds XmlDocument <br /><br />   XmlDocument myXml = gmailFeed.FeedXml <br /><br /><br /><br />   // Access the raw feed as a string <br /><br />   string feedString = gmailFeed.RawFeed <br /><br /><br /><br />   // Access the feed through the object <br /><br />   string feedTitle = gmailFeed.Title; <br /><br />   string feedTagline = gmailFeed.Message; <br /><br />   DateTime feedModified = gmailFeed.Modified; <br /><br /><br /><br />   //Get the entries <br /><br />   for(int i = 0; i &amp;lt; gmailFeed.FeedEntries.Count; i++) { <br /><br />      entryAuthorName = gmailFeed.FeedEntries[i].FromName; <br /><br />      entryAuthorEmail = gmailFeed.FeedEntries[i].FromEmail; <br /><br />      entryTitle = gmailFeed.FeedEntries[i].Subject; <br /><br />      entrySummary = gmailFeed.FeedEntries[i].Summary; <br /><br />      entryIssuedDate = gmailFeed.FeedEntries[i].Received; <br /><br />      entryId = gmailFeed.FeedEntries[i].Id; <br /><br />   }<br /><br /></p>

</div>				
<br /><p><a href="http://code.msdn.microsoft.com/CSharpGmail" target="_blank" mce_href="http://code.msdn.microsoft.com/CSharpGmail"><strong>Visit here to download the GMail Tools</strong></a></p>