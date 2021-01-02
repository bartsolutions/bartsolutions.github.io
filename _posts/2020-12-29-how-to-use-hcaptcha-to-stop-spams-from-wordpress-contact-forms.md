---
layout: post
title: How to Use hCaptcha to Stop Spams from Wordpress Contact Forms
date: 2020-12-29
summary: We got a bunch of spam emails from our contact forms recently, and the reCaptcha WP plugin seems not working.
---

We have two wordpress (WP) sites for our [company](https://www.bart.com.hk) and [CRM product](https://www.simplemobilecrm.com), respectively. As a technology company focused on latest technologies, wordpress is still our first choice for static site hosting. The reason is simple, there are [thousands of themes](https://themeforest.net/category/wordpress?term=theme) available for wordpress, which dramatically outnumbered most other web frameworks (Java, .NET, Python, Ruby, React, Vue.js or whatever). Some technologies make the website building extremely fast, but nothing could replace the effort of UI design. Should the background color be `#FEFEFE` or `#FAFAFA`? Will the margin look BETTER in 4 pixels or 5 pixels? It simply cannot be achieved by web frameworks. Some CSS frameworks like [bootstrap](https://getbootstrap.com) or [bulma](https://bulma.io) indeed make the web design easier, but no way it could work out a complete, coherent, fancy UI without heavy manual tuning. With wordpress, our designers could easily select a theme fit into our company the most, and then tune up each element later, by themselves.

![](/images/wp-hcaptcha/wordpress-theme-list.png)

Our products have been bringing us some fairly good web traffic and [Alexa ranking](https://www.alexa.com/siteinfo/bart.com.hk#trafficstats). However, recently our WP site got a bunch of abrupt spam emails, directly from our OWN contact forms. And the issue got even worse recently, we got 3-4 spams every day, and apparently we cannot block the emails sent from our own email host. Since we have already put the [reCatpcha plugin](https://wordpress.org/plugins/google-captcha/) in the contact form for submission checking, I thought there were some sort of hard working people continuously fill up the contact forms from the web sites every day, until I saw this promotion email one day:


![](/images/wp-hcaptcha/promotion-spam.png)

It seems there are some tools specifically for site contact form spams! And they could blast the huge amount of spam emails every day (just check out the promotion discount).


We also tried to use some other WP plugins for spam filtering, but it turned out they not only block the spams, but also block normal contact form requests. Since the contact form is the most important way for users to send out the feedbacks to us, such false positives are obviously not acceptable.

Finally we tried to look into the alternative of reCaptcha: [hCaptcha](https://www.hCaptcha.com/). The reason this directly popped into my mind is because I once saw a [related article](https://news.ycombinator.com/item?id=25212541) in hacker news, mentioning hCaptha captured 15% of market share, and unlike reCaptcha, they did not sell the data to others.  


The experience of installing hCaptcha on WP site is both easy and hard, here are the brief steps:
1. [Sign up for a hCaptcha account](https://www.hCaptcha.com/)
2. find out the secret key under your account, and copy out to any text editor (e.g. notepad or word).\
![](/images/wp-hcaptcha/hcaptcha-get-private-key.png)
3. create a new site in hCaptcha, and copy out the site key\
![](/images/wp-hcaptcha/hcaptcha-new-site.png)\
\
![](/images/wp-hcaptcha/hcaptcha-new-sitekey.png)
3. Install [WP plugin](https://wordpress.org/plugins/hCaptcha-for-forms-and-more/)
4. In `settings` -> `hCaptcha` of wordpress admin page, input the site key and secret key:\
![](/images/wp-hcaptcha/hcaptcha-wp-input-key.png)
5. Activate plugin for contact form 7, and save the changes.\
![](/images/wp-hcaptcha/wp-hcaptcha-contact-form-activation.png)

And that's it. I think the most confusing part is, ironically, the easiness. After the plugin is activated, I expect to set up something for the final integration with my contact forms, like reCaptcha. And I cannot find any instructions about that. It turns out you need not (and cannot) do anything further, after the set up is finished, it would magically appear at the bottom of each contact form.


Here is the result:

![](/images/wp-hcaptcha/wp-hcaptcha-result.png)


# Performance

After I switched to hCaptcha plugin, I did NOT get another spam email from my contact forms. Not sure what's the difference between this and reCaptcha technically, but it seems to be working really well.

