---
layout: post
title: One Web Extension for Both Chrome and Firefox
date: 2018-09-28
summary: How to Build One Web Extension for Both Chrome and Firefox
---

I wrote the first version of [Firefox extension of Simple Gmail Notes](https://walty8.com/simple-gmail-notes-firefox-addon/) about one and half year ago, and now I am forced to develop a new one using [WebExtension technology](https://developer.mozilla.org/en-US/Add-ons/WebExtensions), because the old jpm addons would be [fully disabled after Firefox 57](https://blog.mozilla.org/addons/2017/02/16/the-road-to-firefox-57-compatibility-milestones/).

That was quite a surprise, because when I started to develop the extension back then, jpm was the **most recommended** technology for Firefox addon development. And I suffered so much during the development.

Anyway, now the the extension already got some problems with new Firefox (FF 50+), especially with the [OAuth](https://github.com/mozilla/oauthorizer). So I am left no choice except starting on this ASAP.

It turned out that the Firefox WebExtension development was **MUCH** easier than I thought, it was ALMOST the same as chrome extension. There are some pitfalls, but in general it was very smooth. The debug process is much better than jpm development, and I could debug and reload the addon from the source code directly, without generating an new xpi file.

Eventually I merged extensions of Firefox and Chrome into **one single set of source code**. I believe my extension should be of medium complexity, but I got **almost** no pain during the migration.

[![FF & Chrome in One Code - Page 1 (2)](https://walty8.com/wp-content/uploads/2017/05/FF-Chrome-in-One-Code-Page-1-2-1-1024x673.png)](http://walty8.com/wp-content/uploads/2017/05/FF-Chrome-in-One-Code-Page-1-2-1.png)

Pitfalls
--------

There are still two pitfalls, however. But I believe they are mostly timing related, and I suppose they should not be major iusses later in the future.

**Catcha #1**

The API timing. Since the extension required access to Google Drive from Both Firefox and Chrome, an OAuth API is required. However, the API is [not ready until Firefox 53](https://discourse.mozilla-community.org/t/use-oauth-2-0-in-firefox-webextension/11984). That means I could use the developer edition for the extension development, but it could not be uploaded to the market until Firefox 53 is released to the public as stable version.

**Catcha #2**

Probably because of the hard deadline of Firefox 57, there is a huge queue for the Firefox addon review I have submitted my addon for almost 4 weeks now, and I am currenlty in the position of **103/210**. Apparently, it would need (at least) one more month to have my addon review got **started**. Fortunately, now Firefox introduced the new auto-sign mechanism, which means you could have a signed addon file (`.xpi`) **immediately** after you have passed the security check by Firefox. The main disadvantages are:

1.  Users could not see it in the Firefox market, you have to host the xpi yourself
2.  You have to deal with the upgrade yourself.

They are quite inconvenient indeed, but it does help when there are some existing users [got stuck with the legacy version](https://addons.mozilla.org/en-us/firefox/addon/simple-gmail-notes/).

Final Work
----------

Basically now I have one set of code for both Chrome and Firefoxes. I don't need to do **ANY** modification before I submit it to the two markets.

I place `if/else` in the code when differentiations of Chrome and Firefox are required in the logic. And the following list of spots implies all possible differentiations, regarding to this extension.

Let the code do the talk :)

{% highlight javascript %}
walty@ubuntu:/app/simple-gmail-notes.chrome$ grep -B3 -A5 -R 'SimpleGmailNotes.isChrome()' \*
--
common/shared-common.js-
common/shared-common.js-// \*\*\*\*\*\*\*\*\*\*\*\*\* for content script & background script \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
common/shared-common.js-SimpleGmailNotes.getBrowser = function(){
common/shared-common.js:  if(SimpleGmailNotes.isChrome())
common/shared-common.js-    return chrome;
common/shared-common.js-
common/shared-common.js-  //firefox
common/shared-common.js-  return browser;
common/shared-common.js-};
common/shared-common.js-
common/shared-common.js-SimpleGmailNotes.getIconBaseUrl = function(){
common/shared-common.js:  if(SimpleGmailNotes.isChrome())
common/shared-common.js-    return "chrome-extension://" + SimpleGmailNotes.getExtensionID() + "/image";
common/shared-common.js-
common/shared-common.js-  //firefox
common/shared-common.js-  return SimpleGmailNotes.getBrowser().extension.getURL("image");
common/shared-common.js-};
--
common/shared-common.js-
common/shared-common.js-SimpleGmailNotes.getSupportUrl = function(){
common/shared-common.js-  var url;
common/shared-common.js:  if(SimpleGmailNotes.isChrome())
common/shared-common.js-    url = "https://chrome.google.com/webstore/detail/simple-gmail-notes/jfjkcbkgjohminidbpendlodpfacgmlm/support?hl=en";
common/shared-common.js-  else
common/shared-common.js-    url = "https://addons.mozilla.org/en-US/firefox/addon/simple-gmail-notes/#reviews";
common/shared-common.js-
common/shared-common.js-  return url;
{% endhighlight %}

Four places in total:

*   `getBrowser()` : this the most important one. Chrome extension has a global object called `chrome` to do all the WebExtension specific tasks, and it's called `browser` in Firefox side. So I just set up a simple helper function for that, and in future I could call something like following without worrying about which platform is

getBrowser().runtime.sendMessage(message, function(response){
});

*   `getIconBaseUrl`: the way Chrome and Firefox used to get the icon URL is a bit different
*   `getSupportUrl`: not exactly program related, but it's probably not appropriate to lead the Firefox users to the supporting page of Chrome :P
*   (Not shown above) One last thing is, the manifest key for options page in chrome is called `options_page`, and it's called `options_ui` for Firefox. So I basically put something like this in the `manifest.json` file:

{% highlight javascript %}
"options\_page": "options.html",
"options\_ui": {"page": "options.html"},
{% endhighlight %}

And basically that's all.

You are welcome to view the full and latest source code from [here](https://github.com/walty8/simple-gmail-notes.chrome).
