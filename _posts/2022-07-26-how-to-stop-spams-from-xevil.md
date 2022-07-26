---
layout: post
title: How to stop spams from xevil
date: 2022-07-26
summary: Here are some quick steps to stop spams from xevil
---

Xevil seems to have cracked hCaptcha and reCaptcha recently, so you may get a lot of **wordpress contact form spams even if you have captcha integrated**. Recently, I got a lot of spams like the following. 

![](/images/xevil-spam/spam-sample.png)


<br/>
The email address inside is invalid and changes every time, so there is no way to complain to the author. Since it’s a wordpress contact form enquiry, the email sender is actually our own email address so we could not simply block the sender.

However, you could still filter the submissions **based on the posted content**, and hence stop those spam emails from sending out at the last minute!


### Here are the detailed steps:


1\. install message filter for contact form

<https://wordpress.org/plugins/cf7-message-filter/>

2\. in the settings page of extension, mark the ‘xevil’ as restricted keyword

![](/images/xevil-spam/xevil-settings.png)

3\. now, all form submissions with such wording will be blocked:


![](/images/xevil-spam/contact-form-spam-blocked.png)
