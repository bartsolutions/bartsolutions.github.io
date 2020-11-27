---
layout: post
title: Simple Gmail Notes Chrome Extension
date: 2015-08-28
summary: For a long time, I wanted a browser extension that allows me simply add notes to the Gmail. 
---

For a long time, I wanted a browser extension that allows me simply **add notes to the Gmail**. It is because I need some easy way to mark down the comments on the resumes of candidates, Sometimes they would send the resumes across a long time span. Of course I could mark down the notes on evernote, but it's time-consuming and difficult to have an organized list of comments overall candidates, most of which I would not review for the second time.

There **was** a useful plugin called [Notes-For-Gmail](https://chrome.google.com/webstore/detail/notes-for-gmail/mhjceedeiokhkokngbljcgkbfcpnodag). Yet it stopped functioning months ago, and I have no way to contact the author.

Finally I decided my own one, as I **really** need this. And it seems to be a good chance to learn the Google chrome extension writing as well.

Final Product
-------------

Here is the URL for Google chrome extension:

[https://chrome.google.com/webstore/detail/simple-gmail-notes/jfjkcbkgjohminidbpendlodpfacgmlm](https://chrome.google.com/webstore/detail/simple-gmail-notes/jfjkcbkgjohminidbpendlodpfacgmlm)

Some screenshots:

![sgn-chrome-screen2](https://blog.walty8.com/wp-content/uploads/2015/08/sgn-chrome-screen2.jpg)

![sgn-chrome-screen3](https://blog.walty8.com/wp-content/uploads/2015/08/sgn-chrome-screen3.jpg)

And here is the full source code:

[https://github.com/walty8/simple-gmail-notes.chrome](https://github.com/walty8/simple-gmail-notes.chrome)

It's released under [GPLv3](https://www.gnu.org/licenses/gpl-3.0.en.html).

Things I learned
----------------

It's verbose to tell the whole story, so here I just mark down what I have learned:

#### 1\. Basic structure:

![Chrome JS Interactions - New Page](https://blog.walty8.com/wp-content/uploads/2015/08/Chrome-JS-Interactions-New-Page.png)

There are three types of scripts involved during development Google chrome extension. The naming could be arbitrary, here I used the convention inside the Google documentation.

*   background.js: An invisible background page lives as [singleton](https://en.wikipedia.org/wiki/Singleton_pattern). It exists during the life cycle of the extension, i.e., the initialization is called when the extension is installed, or when the browser is launched. All tabs of browser share the same background.js script. It means it would not hold the state of the page specific content. It has the full access of a special `chrome` object, which exposes some special API provided by chrome, e.g. `launchWebAuthflow`). It could not touch the DOM of the pages.
    
*   content.js: This js is tab specific. For each new tab, a new `content.js` would be initialized. It could also modify the DOM of the page. However, it's in a different javascript space from the actual web page. For example, if there is a line of 'var test1 = '123' in the web page, you could not get the value of `test1` in the content.js. It has only partial access of the `chrome` object.
    
*   page.js This is the same javascript space as the web page, whatever exists in the page, you could access that as well. But you can't access any chrome extension API, it's just the part of JS on the web page. Sometimes you don't need this, but for my case, I need to use \[gmail.js\][https://github.com/KartikTalwar/gmail.js/tree/master](https://github.com/KartikTalwar/gmail.js/tree/master), which has to be injected into page.js. There is a special mechanism to inject that, it's almost like hacking.
    

{% highlight javascript %}
var j = document.createElement('script');
j.src = chrome.extension.getURL('jquery-1.10.2.min.js');
(document.head || document.documentElement).appendChild(j);
var g = document.createElement('script');
g.src = chrome.extension.getURL('gmail.js');
(document.head || document.documentElement).appendChild(g);
var s = document.createElement('script');
s.src = chrome.extension.getURL('main.js');
(document.head || document.documentElement).appendChild(s);
{% endhighlight %}
 

#### 2\. Communication

There are many different ways for the [communication](https://developer.chrome.com/extensions/messaging), here are the list of ways I preferred more:

![Chrome Extension JS Structure - New Page](https://blog.walty8.com/wp-content/uploads/2015/08/Chrome-Extension-JS-Structure-New-Page.png)

#### 3\. Debug _(Very convenient)_

Use `console.log` for the message logging.

Go to chrome extensions page (<chrome://extensions/>), check `Developer mode`, under the item, click `Inspect View: backgroudn page`, and you would see the messages for the `background.js` and `content.js`.

#### 4\. OAuth

Google provides some [simple ways](https://developer.chrome.com/extensions/tut_oauth) to do OAuth from Chrome, yet it's less flexible, and requires login of Google Chrome browser. Finally I decided to use [launchWebAuthFlow](https://developer.chrome.com/apps/identity#method-launchWebAuthFlow) for the authentication. It's mainly used for 3rd party OAuth application, but it also supports the OAuth of Google itself. After all Google OAuth also complies to the standard OAuth protocol.

Some parameters are extremely hard to be found. But missing of which has severe consequence, it would actually try to cache some outdated tokens and make the whole authentication problematic. Here are the final version of queries

{% highlight javascript %}
chrome.identity.launchWebAuthFlow(
    {"url": "https://accounts.google.com/o/oauth2/auth?" +
      $.param({"client\_id":"38131814991-p4u809qrr5ee1bsehregd4os69jf2n7i.apps.googleusercontent.com",
          "scope":"https://www.googleapis.com/auth/drive.file",
          "redirect\_uri":"https://" + 
            chrome.runtime.id + ".chromiumapp.org/provider\_cb",
          "response\_type":"code",
          "access\_type":"offline",
          "login\_hint":email,
          "prompt":"consent"
      }), 
     "interactive": true
    },

{% endhighlight %}

Note that `login_hint` and `prompt` are OAuth standard parameters, and could **not** be found from the Google documentation.

**Offline Token**

By default, the tokens collected from Google OAuth would last for only 30 minutes. That means the user would need to log in every 30 minutes if they want to continue to use. In reality, the things would be probably better since there is caching, yet the prompt would still appear from time to time.

So, we need to get an offline token, which could be used for a long time (no limit of time).

The mechanism is a little bit complicated.

We need to use `launchWebAuthFlow` get a `code` first, and then use the `code` to get an `offline token` and an `access token`, and finally we use the `offline token` to renew the `access token` after 30 minutes. Note that only the `access token` could be used for the final access.

#### 5\. Google Drive API

Google chrome extension does not provide direct API to access the Google drive. However, since all Google Drive API and REST API, we could actually use jQuery ajax to send requests and interact with Google Drive.

The documentation is a little bit tricky, they provide the [Http Request](https://developers.google.com/drive/v2/reference/files/get) documentation, and a lot of samples of programming calls (Python, PHP, java, etc..), but there is no direct ajax call sample.

And if you follow the sample of Http Request directly, there are could still be problems. For example, they did not mention where to put the tokens during the access.

After some googling, and read multiple documentations, I finally tried out the correct full HTTP request of access. Here is one sample

{% highlight javascript %}
$.ajax({
        type:"GET",
        headers: {
                "Authorization": "Bearer " + getStorage(email, "access\_token")
        },
        url: "https://www.googleapis.com/drive/v2/files/" + gdriveNoteId + "?alt=media",
        success: function(data) {
            sendMessage({action:"update\_content", content:data});
            sendMessage({action:"enable\_edit", gdriveEmail:getStorage(email, "gdrive\_email")});  
        },
        error: function(data){
            sendMessage({action:"show\_error", 
                        message:"Faild load message, error: " + JSON.stringify(data)});
        }
    });
{% endhighlight %}

As one could see, there is a header of `"Authorization": "Bearer <access_token>"`, which is not mentioned by anywhere Google Drive API. My guess is it should be part of OAuth protocol.

More details of other Google Drive API access could be found in the [source code](https://github.com/walty8/simple-gmail-notes.chrome).

Publish
-------

Publish flow on Google Chrome store is smooth in general. (Need to pay 5 dollars for the initial set up though).

The only part that frustrated me is the icon looks very bad inside the listing page (search result page) of chrome extension. Instead of using the promotion image I provided, they actually just used the app icon (16x16) and enlarge it. One may imagine how bad could that be.

And it turns out that the promotion image needs to be manually approved before it could be seen on the listing page. You can't check the review status from the site, but you could send the email to [cws-assets@google.com](mailto:cws-assets@google.com) for the query.

Another problem with Google Chrome store is that they sort the result based on historical order. One week after my app was uploaded to chrome store, when I search the keywords 'Gmail Notes' in the store, the first two extensions failed to work at all, and the third one is a malware (as mentioned in the latest comments).

However, since those apps **used to** have a good user base, they still have a very high ranking despite enormous bad comments in the last few months. And apparently there is not much you can do with that.

Github
------

Right after I launched the app, I also published the source code to [github](github.com) (the app is under GPLv3). It turns out the GitHub could import source code from [subversion](https://subversion.apache.org/), and keep the commit history. But one thing surprised me, when I do further commit and push to the git repository, GitHub uses on the system configuration of `user.email` and `user.name` for the author identity, instead of my GitHub login information, though I need to provide the authentication every time I try to push. That means people could actually push the code on behalf of some others?
