---
layout: post
title: A Simple Tutorial for Reading Google Analytics Data
summary: So after the tracking code is planted for a while, and you got a bunch of data, how to actually start reading the data?
---


This article aims to provide some quick jump-in tips of GA to beginners, for those who want a complete step-by-step tutorial, you are advised to follow the [official GA course](https://analytics.google.com/analytics/academy/course/6).

I believe most people will agree that, Google Analytics is a powerful analytics tool, which is natural as Google is one of most data dependent company. It’s probably safe to declare that Google is the top data expert company.

So to learn GA, or any data mining tool, there are two basic barriers that would stop the user.

1. You need a bunch of data for you to play around, fortunately GA provides a bunch of demo data for every user
2. You need a bunch of real data so it makes the whole thing more interesting
3. You need to learn some basic concepts about how it works.


The implantation of tracking code is out of scope of this tutorial, but there are a bunch of tutorials outside, it's general extremely easy to plant one into your site. If you use a WP site, all it takes is to simply install a <a>plugin</a>, click a link and do a google login.

So, there are 4 main sections of GA

1. Real time data
2. Audience
3. Acquisition
4. Behaviour
5. Conversions

[IMAGE]

The sections are more or less related, and directly related to the marketing concept. For easier understanding, I would  rearrange the section as following sequence:

1. Real time data - which page of your site is being visited in the last 30 minutes, this is the most direct observation about how busy your server is right now. It's also useful to verify if the tracking code is correctly planted into the system. Normally you just wait for 24 hours and see if everything is correct :)\
 [IMAGE]
2. Acquisition - how people actually get started to visit your site? (refererred from another site, organic search or campaigns?)\
 [IMAGE]
3. Behaviour - What did the people do AFTER they got into your site (did they exist immediately, did they get lost?)\
 [IMAGE]
4. Audience - How many are new users and how many are returned users? Who are all those users（user location down to city, browser model) You could learn more if you <a>enabled demographic models</a>. But make sure you are the users know beforehand.\
 [IMAGE]
5. Conversions - How did they visitor contibute to your revenue, exactly? It's normally done by set up some critical checkout points (goals), e.g. user reached shopping card page,  check out page and and finished payments, or just finished sign up process.\
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

