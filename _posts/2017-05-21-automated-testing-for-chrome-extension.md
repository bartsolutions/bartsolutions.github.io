---
layout: post
title: Automated Testing for Chrome Extension
summary: Since I have migrated the extension of Simple Gmail Notes as an official side project of the [new company](https://www.bart.com.hk) , I would like to keep a more rigid development process of this.
---

Since I have migrated the extension of [Simple Gmail Notes](https://www.simplegmailnotes.com) as an official side project of the [new company](https://www.bart.com.hk) , I would like to keep a more rigid development process of this.

Very soon, the extension would need to support 4 different environments, it would be run for:

1.  Chrome + Gmail
2.  Firefox + Gmail
3.  Chrome + Google Inbox
4.  Firefox + Google Inbox

The 4 combinations of environments, plus all kinds of configurations in the preferences page:

[![Screen Shot 2017-05-13 at 4.03.28 PM](https://walty8.com/wp-content/uploads/2017/05/Screen-Shot-2017-05-13-at-4.03.28-PM.png)](https://walty8.com/wp-content/uploads/2017/05/Screen-Shot-2017-05-13-at-4.03.28-PM.png)

It would be too _painful_ to do a fully test for every release. From the point of view of team management, time is one thing, but pain is actually another even bigger problem.

The good part of writing a Chrome extension is, you don’t need to worry about the browser compatibility. Apparently **all** users will use Chrome to run the extension. And most Chrome browsers would be auto-upgraded, so you don’t even need to worry about the version problems (much).

Since Chrome is such a popular and developer friendly browser, I previously thought finding an automated testing tool would be relatively easy, but it seems not the case. I have spent 1 full day for the research, and here are my research result so far:

1.  Selenium IDE in Chrome:
    *   Use the Selenium IDE in chrome and do all the recording, and then play back on Chrome. It will be the best options for me, because I am already familiar with IDE and got a bunch of tools on hand as well. The only problem is, such things does NOT exist. Consider the selenium IDE is not under active development for FF now, I don’t think it’s going to happen ever. [![selenium-ide](https://walty8.com/wp-content/uploads/2017/05/selenium-ide.gif)](https://walty8.com/wp-content/uploads/2017/05/selenium-ide.gif)
2.  [Selenium Webdriver](https://www.seleniumhq.org/projects/webdriver/)
    *   It’s **the** most recommended option in the industry (and stackoverflow). But the problem is the overhead of using webdriver is just too big for me. Since most browsers has native support for webdriver, there is almost no limitation at all when using it for the functional testing. Yet it’s just impractical to require engineers to set up all the testing flow. It’s not only expensive to maintain a such engineer team, but also very difficult keeps those engineers from being bored. It may not be a problem for Google, who created Webdriver (aka selenium v2) and use it to replace the user friendly selenium v1 and selenium IDE, but AFIAK, it’s not a feasible solution for many small consulting companies out there.
3.  [Wildfire](https://chrome.google.com/webstore/detail/wildfire/djhgeeodemlfdpmcccdekfalbhllcoim?hl=en)
    *   It uses a pixel based approach for the testing (like sikuli). But brief tests brought two major problems: a. you could not step over your test, you need to do all the tests again and again. (I mailed the company and confirmed this). b. the validation is not reliable, sometimes the page is not even there, but the verification result still gives True.
4.  [Ghost Inspector](https://chrome.google.com/webstore/detail/ghost-inspector-automated/aicdiabnghjnejfempeinmnphllefehc)
    *   It tries to record the tests and run it remotely in the cloud. So it brought one obvious problem when we started the testing, how do we actually test a browser extension? I just can’t. I also emailed the company and got confirmed on this.
5.  [Chromium Browser Automation](https://chrome.google.com/webstore/detail/chromium-browser-automati/jmbmjnojfkcohdpkpjmeeijckfbebbon?hl=en)
    *   It allows you to run the tests. But you [cannot do any kind of assertion](https://chrome-automation.com/actions), which is really weird.
6.  [UI Automation](https://chrome.google.com/webstore/detail/ui-automation/aacdhbhfmngpoiinjmphdcpalpdcmbpf)
    *   What it does is to help you set up the webdriver template file, so you could kick start the webdriver approach more easily in Chrome. This is useful if I go route 2, but not for now.
7.  [Screenster](https://screenster.io/):
    *   pixel based and cloud based, should be similar to ghost inspector. That means testing of chrome extension is also not possible
    *   Conclusion:

After a lot struggles, I finally decided to **go for route 1**. Of course, there is still a small problem, i.e. the IDE does not exist for Chrome. Therefore, I decided to **migrate the web extension from Chrome to Firefox** in order to use it for automatic testing. The previous FF extension is written in JPM, and is going to be outdated anyway. If the migration effort is small, then the reliability of Firefox addons imply the same quality for Chrome extension. And as it turned out, the latest conversion from Chrome to Firefox is actually VERY easy. In fact I could now use exactly **same set of source code** for the submission of both Chrome and FF extension. I would write a separate blog for this one.

Finally, there are two pitfalls when I tried to use selenium IDE for the FF testing of the extension:

**Pitfall One:** 1. I used the latest FF (FF 54) for the testing. It’s because the extension of SGN required OAuth, which in turn require FF 53+ to work properly 2. Gmail testing could not allow single window mode of selenium, because the policy of the web site 3. but selenium standalone server + multiple window mode + FF 54 seems not working together, a blank page will appear. 4. Solution: you need to [disable multiprocess firefox](https://www.ghacks.net/2016/07/22/multi-process-firefox/) in order for selenium standalone server to work with latest firefox

**Pitfall Two:** 1. After FF 57, it would be impossible to use the selenium IDE, because Firefox would only allow webextension addon since then. 2. I searched around for this, and it seems almost dead end. There is a company (or organisation) called [sideex](https://sideex.org/) developing the extended version of selenium. And I have asked the team if they would be able to support the webextension in future, and the result is affirmative. I was told they are actually working on this now, and hopefully have it ready before FF57. It’s a good news, though I got some doubts about this. 3. I suspect there are some underlying limitations of webextension make it difficult to work out an product with full capability as selenium IDE. But I guess even a half-powered tool will work for me too. And I am willing to contribute some source code if needed.

Finally, just for reference, here is an in-depth discussion thread about this topic in hacker news: [https://news.ycombinator.com/item?id=13586904](https://news.ycombinator.com/item?id=13586904)
