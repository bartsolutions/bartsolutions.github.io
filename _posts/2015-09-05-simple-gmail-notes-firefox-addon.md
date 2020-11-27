---
layout: post
title: Simple Gmail Notes Firefox Addon
date: 2020-11-20 19:22
summary: One week after the Chrome extension of simple gmail notes was released, I started to plan on porting of extension to Firefox.

---

One week after the [Chrome extension of simple gmail notes](https://chrome.google.com/webstore/developer/edit/jfjkcbkgjohminidbpendlodpfacgmlm?hl=zh-CN&authuser=0) was released, I started to plan on porting of extension to Firefox.

There are 2 major incentives for this porting:

1.  I spent quite a lot of effort to work out the google API for the extension. Most of them are just [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer) HTTP API, which are supposed to work with Firefox extension right alway.
2.  During the implementation of Google extension, I tried to get way from most Chrome specific API (e.g. chrome sync). So _theoretically_ most code should work with Firefox extension.

Final Product
-------------

Here is the URL for Firefox extension:

[https://addons.mozilla.org/en-us/firefox/addon/simple-gmail-notes/](https://addons.mozilla.org/en-us/firefox/addon/simple-gmail-notes/)

Some screenshots:

![sgn-chrome-screen2](https://walty8.com/wp-content/uploads/2015/08/sgn-chrome-screen2.jpg)

![sgn-chrome-screen3](https://walty8.com/wp-content/uploads/2015/08/sgn-chrome-screen3.jpg)

And here is the full source code:

[https://github.com/walty8/simple-gmail-notes.firefox](https://github.com/walty8/simple-gmail-notes.firefox)

It's released under [GPLv3](https://www.gnu.org/licenses/gpl-3.0.en.html).

Frustration
-----------

The biggest problem to start the development of Firefox extension is, you cannot Google out the result easily. The most intuitve keywords for Google should be "[firefox extension tutorial](https://www.google.com/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=firefox%20extension%20tutorial)", or "[firefox extension development](https://www.google.com/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=firefox+extension+development)".

Yet, for both cases, the optimal / best result is not inside the first search two results. It's not a big problem for experienced developers, but if you are going to get **started** on this field, it's going to be a nightmare. Most of search results are from the same official site of [https://developer.mozilla.org](https://developer.mozilla.org), it seems they did not give a well structured SEO for the Google search. Some outdated pages got a even higher SEO ranking than those new ones.

Another depressing thing is, for the [first search result](https://developer.mozilla.org/en-US/docs/Building_an_Extension), the tutorial mentioned a [hello world sample](https://web.archive.org/web/20130627120158/https://mozilla.doslash.org/stuff/helloworld.zip), which is a dead link! That's really bad, When one started to learn something totally new, the worst thing that could ever happen is a surprise of frustration, no matter how small it is!

Actually, like most developers, I only want a simple list of instructions to get started. And if possible, I want to follow a step by step hello world tutorial, just like the [search results for Chrome extension](https://developer.chrome.com/extensions/getstarted) do.

SDK
---

After wasted a few days on the wrong paths, I finally got some basic understanding about the Firefox extension/addon development (extension is a subset of addon).

Historically, there were 3 different ways of development, plus 1 new way of future:

1.  [raw development](https://developer.mozilla.org/en-US/Add-ons/Overlay_Extensions/XUL_School/Getting_Started_with_Firefox_Extensions) - set up the file structure from scratch
2.  [cfx](https://developer.mozilla.org/en-US/Add-ons/SDK/Tools/cfx) - use python for development, replaced by jpm since Firefox 38.
3.  [jpm](https://developer.mozilla.org/en-US/Add-ons/SDK/Tutorials/Getting_Started_(jpm)) - latest addon SDK
4.  [chrome extension comptable SDK?](https://blog.mozilla.org/addons/2015/08/21/the-future-of-developing-firefox-add-ons/) - totally new API structure. And it's announced in the middle of development of my Firefox addon. Not sure how the jpm thing will evolve in the future.

Anyway, for now, the best option for Firefox extension development would be using **jpm** SDK.

Structure
---------

The structures of Chrome and Firefox extensions are actually quite similar. There are, however, subtle differences in the scope of Javascript.

![Firefox Addon Structure - New Page (1)](https://walty8.com/wp-content/uploads/2015/09/Firefox-Addon-Structure-New-Page-1.png)

Thanks for the [template project of firefox](https://github.com/rinkudas/gmail-firefox-addon-boilerplate) (though it's in cfx), it makes my development much more easier. After struggled a few days on the structural discrepancies between Chrome and Firefox extensions, the remaining change on source code is actually relatively small. It only took me two more (half) days to port the whole project.

Pitfalls
--------

One major difference of between Firefox and Chrome extensions is you **cannot** get the javascript object of `window` in the scope of background script, so you have no way to include the [jQuery](https://jquery.com/) inside the background script (`index.js`). Finally, I have to write a [custom ajax wrapper](https://github.com/walty8/simple-gmail-notes.firefox/blob/6537e81e270c9bb83e56f66de4f087b59268402e/index.js#L483) using the builtin [Request](https://developer.mozilla.org/en-US/Add-ons/SDK/High-Level_APIs/request) object of Firefox SDK to micmic the jQuery ajax.

function sendAjax(ajaxConfig) {
  var request = Request({
    url: ajaxConfig.url,
    contentType: ajaxConfig.contentType,
    content: ajaxConfig.data,
    headers: ajaxConfig.headers,
    onComplete: function(response){
      var data = response.json;
      if(!data)
        data = response.text;

      //debugLog("@205, ajax complete", response.status, ajaxConfig.url, response.text);

      if(ajaxConfig.complete){
        ajaxConfig.complete(data);

      }

      if(response.status >= 400){ //got error
        if(ajaxConfig.error){
          //debugLog("@205, ajax error", response.status, ajaxConfig.url, response.text);
          ajaxConfig.error(data);
        }
      }
      else{ //success
        if(ajaxConfig.success){
          //debugLog("@211, ajax success", ajaxConfig.url, response.text);
          ajaxConfig.success(data);
        }
      }

    }
      
  });

  switch(ajaxConfig.type){
    case "POST":
      request.post();
      break;
    case "PUT":
      request.put();
    case "DELETE":
      request.delete();
    default:
      request.get();
  }

}

Another problem I hit is I failed to import the [oauthorizer](https://github.com/mozilla/oauthorizer) library into the project. The instruction provided in the `README.md` did not work at all. And I checked [the sample code in github](https://github.com/search?l=javascript&q=require+oauthorizer&type=Code&utf8=%E2%9C%93), but still could not figure out how the import system really works. Finally, I copied the whole folder of oauthorizer into `<project_root>/lib`, and added the following line into the background script:

let {OAuthConsumer} = require("./lib/oauthorizer/lib/oauthconsumer");

Messaging
---------

Here is the messaging structure of Firefox Addon.

![Firefox Messaging - New Page](https://walty8.com/wp-content/uploads/2015/09/Firefox-Messaging-New-Page.png)

Firefox extension has some difficulties to find the currently active tab in the background script (unlike Chrome extension), so you better passing the `worker` object to the all the procedure calls, only the worker could reliably send the message back to the content script.

Debug Cycle
-----------

Firefox extension debugging is less smooth then Chrome extension. Yet it is still relatively easy using latest `jpm`.

The default execution command `jpm run` would start a new profile each time, which could be problematic if your site is web page related. For example, I have to log into the Gmail account every to debug the `Simple Gmail Notes`, and it's really painful.

Fortunately, you could reuse the same profile:

`jpm run --no-copy --profile <profile_folder>`

To reload the extension after the source code modification, use this command:

`jpm post --post-url https://localhost:8888/`

Yet, I still got one **most** painful expreince here. For **one time**, somehow the whole debugging system collapsed, all `console.log` failed. I have no idea what happened. No error message, no warning. All logs jsut disappeared, which makes further development impossible. I suspect there is something wrong with the configuration, or the early executed source code, or the Firefox profile, but I failed to dig out the root cause.

Finally, I have to redo the work again from the last SVN version, and this is really bad. Fortunately, it only happened for once.

Publishing
----------

### Manual Review

The publishing of Firefox extension is much slower than the Chrome extension in general. It took about 1 hour to be publish the extension in Chrome extension store. For the Firefox extension, however, it took about **4 days** to finish the publishing process.

It is because Mozilla actually did **manual checking** for each extension. And my extension was rejected for 3 times in total:

*   version 1.6: I put some .bak files and .bat files inside which are not used by the extension.
    *   solution: remove those redudant files
*   version 1.7: the [oauthorizer](https://github.com/mozilla/oauthorizer) checksum is not correct, because I modified a little bit of it.
    *   solution: instead of using `npm install`, I copied the files into the root directory, and explained to the reviewer my changes.
*   version 1.8: the minified jQuery did not match the checksum, and event monitoring of DOM is found:
    *   solution: Both are related with the imported library of [gmail.js](https://github.com/KartikTalwar/gmail.js/tree/master). I downloaded the _more_ original jQuery script, and further explained where the DOM monitoring happened.

As one could see, it's a much more strict reviewing process then the one of Chrome extension, for which I believe only minimal automatic checking is provided. My feeling is that Firefox is very cautious about the malware, that's why they explicitly require the matching of checksum against the minified code.

### Magical Queue Number

Each time the extension is rejected, I have to generate a new version (with new version number) in order to have the extension approved. Normally the waiting time is less than 24 hours. But one time is really fast, it took the reviewer less than 30 minutes to check and reject my app (version 1.7).

From the Google search, many people complain about the slowness of queue, but it's actually not that bad. But I don't really think it's a queue. The queue number moved extremely slow, it may move from 137/140 to 135/140 after two hours, and then fall back to 138/145 after another hour. The number goes forward and backward. But in general, if you _don't_ stare at the queue number, the review would get finished within 1 day (at least for my case).

### Users

Both Firefox and Chrome extensions basically got the exactly same UI and functionality, since the Firefox extension is merely a ported version. In general, the active users of Firfox extension is _fewer_ than the Chrome extension one, it's probably related with the difference of user base between the two browsers.
