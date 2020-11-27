---
layout: post
title: Why You Need To Be Very Careful About Google Authorization (OAuth)
summary: Since we have built the extension of Simple Gmail Notes, and mobile app of [Simple Mobile CRM](https://mobilecrm.io), we have come across all the power and danger of those Google authorization tokens.

---

Since we have built the extension of [Simple Gmail Notes](https://www.bart.com.hk/simple-gmail-notes/), and mobile app of [Simple Mobile CRM](https://mobilecrm.io), we have come across all the power and danger of those Google authorization tokens.

Today we would see, in plain English, how the Google authentication works, and how bad it could be when things go wrong. And there are a few advises at the end of the article.

How Google Authentication Works
-------------------------------

Whenever we try to install an Google service related extension, addon or app (iOS / Android), we would see the a prompt like this:

![](https://www.bart.com.hk/wp-content/uploads/2018/08/perm-sgn-sample.png)

This is called an [OAuth](https://en.wikipedia.org/wiki/OAuth) authentication screen. In short, it's an open standard for for people to authorize the application (Simple Gmail Notes in this case) to collect the required **authorization**. Google supports OAuth2 for most of its services, such as Gmail, Google Drive, Google Calendar, Google Plus and etc.

The main advantages of using OAuth over giving your username and password to other applications are:

1.  You could revoke the Google access of the applications anytime, without changing your password.
2.  You could limit how much permissions to be granted to that application. Actually, Google give some fine-grained permission control in the OAuth system.
3.  With username + password however, the user basically got the full access of all Google services, which is extremely dangerous, and you should **never** ever give your Gmail password to others.

[![](https://www.bart.com.hk/wp-content/uploads/2018/08/webflow.png)](https://www.bart.com.hk/wp-content/uploads/2018/08/webflow.png)

However, there is one tricky part about OAuth, after the authorization is granted once, the application could keep collecting the information (within that permission scope) **in future**. So, depends on the capability of token, the extension could have magnificent power over your account information. And by design, the tokens granted by OAuth will surpass the two-step authentication.

What Could Possibly Go Wrong
----------------------------

Now we are going to see the common permission scopes, and what's the **worst thing that could possibly happen** when your OAuth token is abused. The extension developer may not be the evil guy, but it's possible that:

![](https://www.bart.com.hk/wp-content/uploads/2018/08/blog-cash.png)

1.  The application server may be hacked by someone. Of course we would fully trust engineers of Google that they would fully protect our Gmail accounts from the most hacking attempts. However, could you trust the same way those extension vendors?
2.  The extension was acquired by someone. [It's more common that people thought](https://arstechnica.com/information-technology/2014/01/malware-vendors-buy-chrome-extensions-to-send-adware-filled-updates/). Sometimes the ownership transfer of extension is totally quiet, so you will never be aware what happened.

Common Permission Requests (and Worst Case Scenarios)
-----------------------------------------------------

### Google Profile Request

When you see the message as below:

![](https://www.bart.com.hk/wp-content/uploads/2018/08/perm-profile.png)

It means your profile information is going to be collected. This is normally a mildest permission request in most cases.

But in most cases, there will be a further permission screen following (see below).

### Gmail Readonly

You would see this message sometimes:

> This will allow xxx to: View your email messages and settings

![](https://www.bart.com.hk/wp-content/uploads/2018/08/perm-email-readonly.png)

It means the extension could read your emails. In particular, it could read all of your future and past emails in all of your mail boxes. But the extension could not compose, send or delete your emails.

**What could go wrong:**

Let's say, extension server is hacked, the hacker could then request a reset of your Facebook password in the Facebook website. The service provider will normally send out a reset URL to your email address. The hacker could then collect your password reset link using your authorized token, and do the reset.

Fortunately, in this case, you could still know something went wrong, because you would see a mystery password reset email. If that happened out of blue, and the reset link is indeed clicked, then you know there must be something weird happened, and you better [check your authentication tokens](https://myaccount.google.com/permissions).

### Gmail Full

The authorization should appear as following:

> This will allow xxx to: Read, send, delete and manage your email

![](https://www.bart.com.hk/wp-content/uploads/2018/08/perm-email-full.png)

The extension would now have **full access** of your Gmail account. It could read, write, send and delete the emails on your behalf. You have to be very careful when you are going to grant such permissions.

**What could go wrong:**

#### Case 1:

1.  The user could request reset password for your service (e.g. Facebook / Twitter)
2.  Collect the URL using the read permission
3.  Permanently delete the email in the inbox AND the trash bin
4.  Now, your Facebook password is reset but you can't see any clue about what's going on here because even the password reset email was destroyed by the hacker.

#### Case 2:

1.  The hacker check your previous invoice emails
2.  The hacker COMPOSE a new invoice email, but with the bank account of hacker as recipient
3.  The hacker SEND out the invoice using your Gmail account
4.  Hacker then delete the email forever
5.  Your customer send the money to the hacker account because he thought he got the email from you. (I know this happened before because I did see a similar complaint to another vendor's extension, which collected the full Gmail access.)

![](https://www.bart.com.hk/wp-content/uploads/2018/08/pexels-photo-941555.jpeg)

Therefore, always think **twice** before granting a such strong permission to applications. Do it only if you trust the vendor as much as you trust Google. And you should always [review your granted permission](https://myaccount.google.com/permissions) from time to time.

### Google Drive File Permission

You would read the message as

> This will allow xxx to: View and manage Google Drive files and folders that you have opened or created with this app

![](https://www.bart.com.hk/wp-content/uploads/2018/08/perm-drive-file.png)

It seems a lot, but actually it grants very limited permission. It basically means the extension will create files in your Google drive, but it could only read those files created by it self. And for those (sensitive and private) documents created by your self, the extension could not access them.

### Google Drive Full Permission

The permission line reads as:

> This will allow xxx to: View and manage the files in your Google Drive

![](https://www.bart.com.hk/wp-content/uploads/2018/08/perm-drive-full.png)

While it looks similar to the previous one, there is a huge difference actually.

**Implication**

This means the extension could fully read all documents created by you, including those sensitive proposals and invoices.

And the extension could even screw up those existing files if they wanted.

### Contact Readonly

The permission line reads as

> This will allow xxx to: View your contacts

![](https://www.bart.com.hk/wp-content/uploads/2018/08/perm-contact-readonly.png)

This means the extension could read all of your contacts.

**Worst case scenario**

It means the extension could collect all of your contacts, silently upload to a server on the other side of the world, and prepare for the next round of spamming. And they also know the existence of **linkage** between you and all those contacts, which is a treasure for some companies.

### Permissions Used By Our Apps

We tried hard to minimize the permissions required.

Currently, our Gmail extension, [Simple Gmail Notes](https://www.bart.com.hk/simple-gmail-notes/), used the most strict permission of Google Drive, and nothing else.

> View and manage Google Drive files and folders that you have opened or created with this app

We don't even collect the Gmail related permission for this extension, it's very hard actually, but we eventually worked it out.

And Our CRM App, [Simple Mobile CRM](https://mobilecrm.io), on other hand, asks for a medium level permission of Gmail ('Gmail readonly').

> View your email messages and settings

Actually we has been struggling hard to further reduce the CRM permission. Yet this is the minimum permission required to show up a full Gmail thread on the CRM App (we did not store the mails in our server). We would further reduce this scope whenever there are alternative approaches for this.

None of our products will collect the any contact related permission.

### Conclusions

Finally, one should bear in mind that:

![](https://www.bart.com.hk/wp-content/uploads/2018/08/access-airport-backpack-842921.jpg)

1.  Be very very careful when you try to grant your Google account authorizations to others, grant it only if it's absolutely necessary and you absolutely trust them. It's especially true when you try to grant out those full permissions (read and write).
2.  [Review your authorization tokens](https://myaccount.google.com/permissions) from time to time, if you have uninstalled the application and will never use it again, remember to remove it from the permission list.
