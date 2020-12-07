---
layout: post
title: A Simple Tutorial for Reading Google Analytics Data
summary: So after the tracking code is planted for a while, and you got a bunch of data, how to actually start reading the data?
---


## Introduction
This article aims to provide some quick jump-in tips to Google Analytics (GA) beginners, for those who want a complete step-by-step tutorial, you may want to check out the [official GA beginner course](https://analytics.google.com/analytics/academy/course/6).

Like many other Google tools, GA is extremely powerful, and yet the UI is a bit untrivial to beginners, to say the least. That may explain why Google even build a *course* for that. But once you got *some* sweet spot of GA, you could explore the remaining features yourself with relative ease.

To learn GA, or any other data mining tool, there are two basic prerequisites that help people kick start:

1. You need a bunch of data for you to play around
2. You need a bunch of real data so it makes your study *interesting*

For item 1, fortunately GA provides a bunch of demo data for every new GA account

Item 2 is actually the most difficult part, this means unlike learning a new programming language, you actually need some *real* data to start working out something useful.

Put a GA tracking code into a website is out of scope, but there are a [bunch of tutorials](https://www.google.com/search?q=how+to+add+a+google+analtycis+tracking+code) outside. It's extremely easy to plant one into your site. If you use a WP site, it's even simpler. All it takes is to simply install a [wordpress plugin](https://www.google.com/search?q=wordpress+google+analytics), and do a Google login, you don't even need to know the tracking code value.

## Main Sections

**Quick Takeaway**
- Overview of each section shows a consolidation of each section
- The dashboard is a further consolidation of all section overviews
- You could always change the date range by clicking the top right corner of screen

[IMAGE]

There are four main sections of GA:

1. Real time data
2. Audience
3. Acquisition
4. Behaviour
5. Conversions

The four sections are more or less related, and directly map to marketing concepts. For easier understanding, the sections could be re-ordered into this way:

1. Real time data - which page of your site has been visited since 30 minutes ago, this is the most direct indication of how busy your server is right now. It's also useful to verify if the tracking code is correctly planted into the system. Normally, you don't wait for 24 hours and see if if the tracking code is fine :)\
 [IMAGE]
2. Acquisition - how people actually start to visit your site? Are they introduced from another site (referral), organic search or marketing campaigns?\
 [IMAGE]
3. Behaviour - Where do the people visit after they entered your site? Do they exit immediately? Do they get lost?
 [IMAGE]
4. Audience - Who are those visitors? How many of them are new users and how many are returned ones? You could learn more if you [enabled audience demographics](https://support.google.com/analytics/answer/2799357?hl=en). It's a bit aggressive, and they are never turned on in our [Simple CRM products](https://www.simplemobilecrm.com). But if you do, please make sure you notice the users beforehand, this is explicitly required by Google.\
 [IMAGE]
5. Conversions - How do the visitors contribute to your revenue? You could set up some critical check points (goals) at different pages of your site, e.g. when user reached shopping card page,  check out page, payment successful page, or sign up completion page.\
 [IMAGE]

Except section 1 (real time data), all other sections allow an selection of time period at the top right corner of page. So, you could easily find out the new / returning users within 1 week, 1 month or 3 months.

[IMAGE]

In general the overview screen of each section is most useful for users.

[IMAGE]

In most cases this screen is carefully tuned by Google, and is supposed to provide most information to users, at a glance.

But in case that's not enough, you may try to deep a bit deeper yourself.


You could always finetune the tables and reports, and save them for future uses:

[IMAGE]

# Pivot Tables #

Here we would show an example of pivot table. This blog won't go into much details, it aims to show a direction and sweet spot. And once you know a trick, it's quite easy to further explore other aspects of GA.

We would use the demo data for the illustration here, here is the default behaviour overview screen:

[IMAGE]

By playing around the overview table, we could already see different dimensions of demo data.

[IMAGE]

Say, one day, we want to know what countries are these people from, *and* what devices did they for the browsing?

This can't be done via simply tuning the overview table, this is where pivot table comes in handy.

In the behaviour page, click the right most icon

[IMAGE]

Select the xxx as primary dimension, yyy as second dimension.

Select zzz as pivot value

Then select bb and aa and pivot values.

You would see the following as result:

[IMAGE]

The means for items that divided *simultaneously* fulfill  xxx, yyy, and zzz, what pivot values is that:

[IMAGE]

Basically it’s a table of 3 dimensions, with 2 values inside.

You may think xx, yy and zz are interchangeable, actually it’s not. The primary and secondary dimensions are more flexible, and have more choices. The pivot values, on the other hand, have more limits on the possible values

[IMAGE]

If you still think this is a headache, don’t worry. Just sent [notice to us](), we would provide full stack solutions from project design to product user analysis.

