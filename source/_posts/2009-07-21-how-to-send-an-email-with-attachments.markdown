---
layout: post
title: Asp.Net发邮件，如何发送附件
comments: true
date: 2009-07-21 17:20
categories:
- ASP.NET
- Asp.net
- .Net其他
- C#
- 代码片段
- 邮件
---

<p>使用如下代码可以发送附件</p>
<pre>MailMessage mail = new MailMessage();
mail.To = "me@mycompany.com";
mail.From = "you@yourcompany.com";
mail.Subject = "this is a test email.";
mail.Body = "this is my test email body.";
MailAttachment attachment = new MailAttachment( Server.MapPath( "mailTest.txt" ) ); //create the attachment
mail.Attachments.Add( attachment );
SmtpMail.SmtpServer = "localhost"; 
SmtpMail.Send( mail );</pre>
<p>使用如下代码可以在用户上传附件后发生邮件:</p>
<p><!--more--></p>
<pre>if  (FileUpload1.HasFile)
{
    string  toAddress  =  "you@yourprovider.com";
    string  fromAddress  =  you@yourprovider.com  (2);
    string  mailServer  =  "smtp.yourprovider.com";

    MailMessage  myMailMessage  =  new  MailMessage();

    myMailMessage.To.Add(toAddress);
    myMailMessage.From  =  new  MailAddress(fromAddress);
    myMailMessage.Subject  =  "Test  Message";

    string  fileName  =  Path.GetFileName(FileUpload1.PostedFile.FileName);
    Attachment  myAttachment  =  
                                  new  Attachment(FileUpload1.FileContent,  fileName);
    myMailMessage.Attachments.Add(myAttachment);

    SmtpClient  mySmtpClient  =  new  SmtpClient(mailServer);

    mySmtpClient.Send(myMailMessage);
}</pre>				
