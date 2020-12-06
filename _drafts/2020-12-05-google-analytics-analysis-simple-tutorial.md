---
layout: post
title: A Simple Tutorial for Reading Google Analytics Data
summary: So after the tracking code is planted for a while, and you got a bunch of data, how to actually start reading the data?
---


# Introduction
This article aims to provide some quick jump-in tips to Google Analytics (GA) beginners, for those who want a complete step-by-step tutorial, you may want to check out the [official GA beginner course](https://analytics.google.com/analytics/academy/course/6).

Like many other Google tools, GA is extremely powerful, and yet the UI is not most trivial to get started with. That may explain why they even build a course for that. But once you got *some* sweet spot of GA, you could explore the remaining features yourself with relative ease.

To learn GA, or any other data mining tool, there are two basic prerequisites that allow people kick start:

1. You need a bunch of data for you to play around
2. You need a bunch of real data so it makes the whole thing more interesting

For 1, fortunately GA provides a bunch of demo data for every new GA account

Item 2 is actually most difficult part, this means unlike learn a new programming language, you actually need some *real* data to start making something userful in the real world.


Put a GA tracking code into a website is out of scope of this tutorial, but there are a [bunch of tutorials](https://www.google.com/search?q=how+to+add+a+google+analtycis+tracking+code) outside, it's extremely easy to plant one into your site. If you use a WP site, all it takes is to simply install a [wordpress plugin](https://www.google.com/search?q=wordpress+google+analytics), click a link and do a Google login.

# Main Sections

There are four main sections of GA:

1. Real time data
2. Audience
3. Acquisition
4. Behaviour
5. Conversions

[IMAGE]

# Quick Takeaway 1
- Overview of each section shows a consolidation of each section details
- The dashboard is a further consolidation of all section overviews
- You could always change the date range by clicking the top right corner of screen

The four sections are more or less related, and directly related to marketing concepts. For easier understanding, the sections could be ordered into this way:

1. Real time data - which page of your site has been visited since 30 minutes ago, this is the most direct indication of how busy your server is right now. It's also useful to verify if the tracking code is correctly planted into the system. You just don't wait for 24 hours and see if everything is correct :)\
 [IMAGE]
2. Acquisition - how people actually get started to visit your site? Is it refererred from another site, organic search or campaigns?\
 [IMAGE]
3. Behaviour - Where do the people visit after they entered your site? Do they exit immediately? Do they get lost?
 [IMAGE]
4. Audience - Who are those visitors? How many of them are new users and how many are returned users? You could learn more if you [enabled audience demographics](https://support.google.com/analytics/answer/2799357?hl=en). It's a bit aggresive, and they are never turned on in our [Simple CRM products](https://www.simplemobilecrm.com). But if you do, please make sure you notice the users beforehand, this is explictly required by Google.\
 [IMAGE]
5. Conversions - How do the visitors contibute to your revenue? You could set up some critical check points (goals) at different pages of your site, e.g. when user reached shopping card page,  check out page, payment succesful page, or sign up completion page.\
 [IMAGE]

Except section 1 (real time data), all sections allows an selection of time period at the top right corner of page. So, you could easily find out the new / returning users within 1 week, 1 month or 3 months.

[IMAGE]


In general the overview screen of each section is most useful for users.

[IMAGE]

In most cases this screen is carefully tuned by Google, and is supposed to provide most information to users, at a glance.


But in case that's not enough, you may try to deep a bit deeper yourself.

You could always finetune the tables and reports, and save them for future uses:

[IMAGE]

Here would show an example of pivot table. Apparently, this blog won't go into the details of all aspects, it aims to show a direction. And once you know a trick, it's easy to further explore other sides of GA.


# Pivot Tables #

The pivot tables is used for illustration because

We would use the demo data for the illustration here.

So we could see the following from the overview screen of behaviour:


[IMAGE]

By playing around the table, we could see different dimensions of data.

[IMAGE]

But, one day, we suddenly want to know, what countries are these people from, and what devices they used for the browsing, so I could tune my marketing more precise.

Apparently, it’s not possible with the simple table of front page, and this is where pivot table comes in handy.


In the devious page, click the right most icon

Select the xxx as primary dimension, yyy as second dimension.

Select zzz as pivot value

Then select bb and aa and pivot values.

The means for items  that divided as xxx, yyy, and ful filled zzz, how many values are that.

[IMAGE]

It’s like a table of 3 dimensions, with 2 values inside.


While you think xx, yy and zz are interchangeable, it’s not. The primary and secondary dimensions are more flexible in general, and will provide more choices, the pivot values, on the other hand, has more limits on the possible values

[IMAGE]


If u still think this is a headache, don’t worry. Just sent notice to us, we provide full stack solutions from project design to campaign information analysis.

