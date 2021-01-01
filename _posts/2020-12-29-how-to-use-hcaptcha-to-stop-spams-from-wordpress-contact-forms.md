---
layout: post
title: How to Use hCaptcha to Stop Spams from Wordpress Contact Forms
date: 2020-12-29
summary: We got a bunch of spam emails from our contact forms recently, and the reCaptcha WP plugin seems not working.
---

We have two wordpress (WP) sites for our [company](https://www.bart.com.hk) and [CRM product](https://www.simplemobilecrm.com), respectively. As a technology company focused on latest technologies, wordpress is still our first choice for static site hosting. The reason is simple, there are [thousands of themes](https://themeforest.net/category/wordpress?term=theme) available for wordpress, which dramatically outnumbered most other web frameworks (Java, .NET, Python, Ruby, React or whatever). Some technologies make the website building extremely easy, but nothing could replace the effort of UI design. Should the background color be `#FEFEFE` or `#FAFAFA`? Will the margin look BETTER in 4 pixels or 5 pixels? It simply cannot be achieved by web frameworks. Some CSS frameworks like [bootstrap](https://getbootstrap.com) or [bulma](https://bulma.io) indeed make the web design easier, but no way it could work out a complete, conherent, fancy UI without heavy tuning. With wordpress, our designers could easily select a theme fit into our company the most, and then tune up each element later, by themselves.

[IMAGE]

Our products have been bringing us some fairly good web traffic and alexa ranking. However, recently our WP site got a bunch of abrupt spam emails, directly from our OWN contact forms. And the issue got even worse recently, we got 3-4 spams every day, and apparently we cannot block the emails sent from our own email host. Since we put the [reCatpcha plugin](https://wordpress.org/plugins/google-captcha/) in the contact form for submission checking, I thought there were some sort of hard working people continuously fill up the contact forms from the web sites, until I saw this promotion email one day:


[IMAGE]

It seems there are some tools specificly for site contact form spams! And they could blast the huge amount of spam emails every day (just check out the promotion discount).


We also tried to use some other WP plugins to stop the spams, but it turned out they not only block the spams, but also normal contact form requests. Since the contact form is the most important way for users to send out the feedbacks to us, such false positives on spam detection are obviously not acceptable.

Finally we tried to look into the alternative of reCaptcha: **hCaptcha**. The reason this directly popped into my mind is because I once saw a [related article](https://news.ycombinator.com/item?id=25212541) in hacker news, mentioning hCaptha captured 15% of market share, and unlike reCaptcha, they did not sell the data to others.  


The experience of hCaptcha is both easy and hard, here are the brief steps:
1. [Sign up for a hcaptcha account](https://www.hcaptcha.com/)
2. find out the secret key under your account, and copy out to any text editor (e.g. notepad or word).\
[IMAGE]
3. create a new site in hcaptcha, and copy out the site key\
[IMAGE]
3. Install [WP plugin](https://wordpress.org/plugins/hcaptcha-for-forms-and-more/)
4. In `settings` -> `hCaptcha` of wordpress admin page, input the site key and secret key:\
[IMAGE]
5. Activate plugin for contact form 7, and save the changes.\
[IMAGE]

==

And that's it. I think the most confusing part is, ironically, the easiness. After the plugin is activated, I expect to set up something for the final integration with my contact forms, and I cannot find any instructions about that. It turns out you need not (and cannot) do anything further, after the set up is finished, it would magically appear at the bottom of contact form.


Here is the result:

[IMAGE]


# Effectiveness

After I switched to hCaptcha plugin, I did NOT get another spam email from my contact forms. Not sure what's the difference between this and reCaptcha technically, but it seems to be working really well.
