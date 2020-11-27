---
layout: post
title: Mobile Apps - Native, Hybrid, and HTML5 - A More Comprehensive Review
summary: Say, your own a small team of capable programmers, and you need to build an an mobile app across two platforms (iOS and Android), what would be your best bet?
---

Say, your own a small team of capable programmers, and you need to build an an mobile app across two platforms (iOS and Android), what would be your best bet?

Currently, there are a lot of different ways to do that, and that's exactly the biggest problem to many people. If we have no other choices, then we would simply build one iOS app and build one android app, without thinking too much. Unfortunately, that's not the case today. We have a lot of different choices now, in fact, we have **too many** choices.

According to the [most popular way of classification](https://developer.salesforce.com/page/Native,_HTML5,_or_Hybrid:_Understanding_Your_Mobile_Application_Development_Options), there are 3 main approaches when building the mobile app:

1.  Native: You build the iOS app using Xcode, and android app from Android Studio.
    
2.  HTML5: You basically just build a website, the user need to start a browser to view your content.
    
3.  Hybrid: You write some HTML, but (somehow) it appears as native/half-native app in the device.
    

Here we make a more detailed classification for those approaches **nowadays**, in the increasing order of **'nativeness**':

1.  **Pure Website**
    
2.  **Webview Hybrid**
    
3.  **JS Engine Hybrid**
    
4.  **Cross Linkage Native**
    
5.  **Pure Native**
    

[![mobile-application-technology-review-architecture](https://walty8.com/wp-content/uploads/2017/01/Mobile-Application-Technology-Review-Architecture-1024x585.png)](https://walty8.com/wp-content/uploads/2017/01/Mobile-Application-Technology-Review-Architecture.png)

Under each category, there are actually a bunch of technologies that could be used with, this diagram briefly illustrate the general picture. (It does not include ALL available technologies since there are too many of them, I just list out the most popular ones).

Pure Website
============

[![mobile-application-technology-review-pure-website-1](https://walty8.com/wp-content/uploads/2017/01/Mobile-Application-Technology-Review-Pure-Website-1.png)](https://walty8.com/wp-content/uploads/2017/01/Mobile-Application-Technology-Review-Pure-Website-1.png)

When using this technology, you basically build a regular website, using HTML + CSS + JS + backend language (Java, .NET, PHP, Python, Node.js or whatever). The user needs to be open a browser in order to view your content. While it's (very) unlikely to ask the user to type a long address in the mobile browser, you could provide some links in the email or ask the user to scan a QR code to access the URL.

People may put the website as a homepage icon in the device, if they want. But not many people would **actually** do that, unless your site is exceptionally attractive or they have no choices (e.g. required by the company policy).

There are a number of ways to make the web site look better in the mobile device, however.

### Traditional Website:

*   **Adapt to screen**: Since the mobile device normally has much smaller screen size than PC and notebook, the mobile website needs to be designed in a way that the layout makes more sense to the user. For example, you may show a list of items instead of a very wide table in the UI. Technically speaking, it's not a technology, just a minimum requirement for a page to be shown in a sensible way.
    
*   **Responsive**: If the site is meant to be seen for both desktop and mobile users, you could use [CSS media queries](http://www.w3schools.com/cssref/css3_pr_mediaquery.asp). It allows different sets of CSS to be applied to the content, when a different screen size is detected. So the web site may look differently on a desktop and a mobile device, though the underlying HTML source code is not changed.
    

### Single Page Application (SPA) Website:

It's still a website actually, however it uses some new technologies and frameworks, which are complicated enough to have it separated from the traditional website. The biggest difference is that, the web page will not be refreshed during the entire navigation. The website URL basically would not change except the hashtag (#) part.

One famous example of SPA is the Gmail, whenever you click links in the page, the page is not reloaded, you are just fetched with the new content.

There are a number of SPA frameworks outside, here are the most famous ones:

*   [React.js](https://facebook.github.io/react/tutorial/tutorial.html) (Supported by Facebook)
    
*   [Angular JS](https://angular.io/) (Supported by Google)
    
*   [Vue.js](https://vuejs.org/)
    

This article won't go into much details about the framework comparison, but my gut feeling is Vue.js might be a good one to stick with simply because the syntax of this framework looks more explicit and simpler ([Zen of python](https://www.python.org/dev/peps/pep-0020/) #2 & #3). There are a lot of related [comparison articles](https://www.google.com.hk/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#safe=strict&q=vue+react+angular+comparison) in Google.

### Mobile UI:

Strictly speaking, this is not another approach, it's just another technique you could add on. There are some mobile UI frameworks outside that could make your website looks more like mobile devices. The buttons, rows and combo boxes would look more \*\*like \*\*native devices.

It's a pure cosmetic thing, and it could be used along with either traditional website or SPA. [Bootstrap](http://getbootstrap.com/) is one of the most famous UI framework, and it's supported by Twitter.

### Websocket:

Again, this is not a framework, it's just another tool you could use and leverage. [Websocket](https://en.wikipedia.org/wiki/WebSocket) means you could continuously update your website without keep sending backend requests. For example, you want to set up a page that would show the stock prices in real time, if using traditional way, you may need to send ajax request to backend at a regular time interval. With websocket, you could pull the data from the website continuously using **one** long lived connection, and the data will be kept updated. You may find the actual demo [here](http://developer.kaazing.com/portfolio/foreign-exchange-dashboard/).

Like the UI framework, you may use this in conjunction with traditional website or SPA.

### Pros & Cons

**Advantages**:

1.  Normally, it's much easier to hire website engineers than mobile developers. In the extreme cases, you may only need to set up a decent wordpress page via drag and drop to accomplish a demonstration website without any coding. (SPA programming is not that trivial, however.)
    
2.  You could have the content updated at live time, without going through the app approval process.
    
3.  No need to worry about [app rejection](https://developer.apple.com/app-store/review/rejections/), you could put anything on the website. In fact, this is probably the only way to get rid of app approval process.
    
4.  Some app stores has strict regulations about payment and transactions, and you could get away from that too.
    
5.  You don't need to build two apps for two platforms.
    

**Disadvantages**:

1.  You can't promote you application from the app store. It's a big deal.
    
2.  Without the app icon, people will actually use it much less (except it's required by company regulations.)
    
3.  Low performance. Though JS engine is much powerful now, it's still much weak than the native UI. Also, one should note that even the Chrome app on iOS devices does not use JS engine V8.
    
4.  A lot of limitations exist in HTML5. For example, you can't have push notification for your website on any iPhone.
    

Webview (Embedded Browser) Hybrid
=================================

[![mobile-application-technology-review-webview-hybrid](https://walty8.com/wp-content/uploads/2017/01/Mobile-Application-Technology-Review-Webview-Hybrid.png)](https://walty8.com/wp-content/uploads/2017/01/Mobile-Application-Technology-Review-Webview-Hybrid.png)

This technology means you are still writing a website using HTML + JS + CSS. However, the website is wrapped into the **skeleton** of an app. It looks like an app from outside, so your app would still be uploaded to app store and appear as an app icon in the device. When the app is opened, actually it would open an internal browser, and your content will be displayed from that browser.

Since it still uses HTML technology, \*\*it means you could basically use all the techniques of the previous section. \*\*For example, you could show a SPA site inside the internal browser. Here you are going to see how the various technologies are interlinked together.

### Cordova:

[Cordova](https://cordova.apache.org/) is an Apache foundation project [started from 2011](https://en.wikipedia.org/wiki/Apache_Cordova), which aims to provide a framework for this hybrid approach. In addition to providing a simple skeleton for the website, it also provides some useful utilities:

1.  You could (and you should) put some local HTML content in the app, so not all contents are served from the website, most of the media and JS could be served locally
    
2.  You could build native custom plugins if necessary.
    
3.  It supports PC platforms like OSX and Windows. Would be a big bonus if you happened to want those too.
    

Cordova is actually the foundation of a big eco-system, and people tend to build frameworks upon it:

1.  [ionic](https://ionicframework.com/): it provides mobile like UI for the website, so eventually you are will have **a mobile like website inside a mobile skeleton**. It depends on Angular JS. That means, in order to use ionic, you need to have knowledge of Angular JS + Cordova + ionic.
    
2.  [Intel XDK](https://software.intel.com/en-us/xdk/docs/using-the-cordova-for-android-ios-etc-build-option): This is just a development toolkit so that you could write the cordova project more easily.
    
3.  [Phone Gap](http://phonegap.com/): Supported by Adobe
    
4.  [Chrome Mobile App](https://github.com/MobileChromeApps/mobile-chrome-apps): Supported by Google
    

### Pros & Cons:

**Advantages**:

1.  You could still get some level of dynamic content, because some of the HTML could be served from web server. Therefore you may update partial content without going through app store process
    
2.  You could have the desktop apps using the same source code.
    
3.  You could still have native API calls (like push notifications) inside the app.
    

**Disadvantages**:

1.  Performance is a major problem. Eventually the UI is built from the browser instead of native device API. If the app is a simple master-detail application, then it should be fine. But 99% of case you app is going to be more than that (though I bet most clients will claim it's going to be a \*\*simple \*\*app at the beginning.) When the app goes more complicated, and particularly when animations are involved, the performance is going be a problem.
    
2.  You may try to use native plugins for those tricky parts, but those native plugins are unlikely to be cross platform, so you are going to build two sets. When you try to add more and more plugins, you would probably find that it might be easier to start as native from beginning.
    
3.  It just not looks right. In most cases, the UI looks a bit odd, and people can still tell if it's a **real** native app or not. It's a problem if UI is really important.
    
4.  IDE is another big problem. IDE was never easy to accomplish, most the IDE for the hybrid technologies depend on some existing tools, so you got double dependencies and your IDE problems could be doubled.
    
5.  Saved time? **Theoretically**, the development time of hybrid app is faster than building from native, because you only need to write one set of codes. Also you would save a lot of time because you don't need to learn the native API.However, that based on the assumption that your development using cordova would be very smooth, which is unlikely. **Everyone** will get stuck on something as the development goes on. In my experience, sometimes you need to spend days or even weeks to solve a problem, which totally compensate the man days you saved using a HTML code. Honestly, the native development is not so difficult nowadays, and it should not be regarded as a major problem. The calculation is more subtle than you thought, we would further discuss about this in the last section of the blog.
    

JS Engine Hybrid
================

[![mobile-application-technology-review-js-engine-hybrid](https://walty8.com/wp-content/uploads/2017/01/Mobile-Application-Technology-Review-JS-Engine-Hybrid.png)](https://walty8.com/wp-content/uploads/2017/01/Mobile-Application-Technology-Review-JS-Engine-Hybrid.png)

This is another interesting hybrid model, that means you still uses HTML + JS to write the application. However, for those technologies in this category, **they did not embed a web browser inside.**

**The engines rendered the native UI based on the realtime Javascript object states**. That means, when the app is started, the JS scripts are executed, and another set of native UI widgets are created and rendered based on the status of realtime JS objects. The JS objects are never actually displayed in the webpage.

This is actually quite similar to what happened during SPA page rendering, so without much surprise, many of them are related with some SPA technologies.

1.  [Appcelerator](http://www.appcelerator.com/): This company has longest history on this field. They used a self-created language system for the mapping.
    
2.  [React Native](https://facebook.github.io/react-native/): Based on React.js, and naturally it's supported by Facebook.
    
3.  [Weex](https://weex-project.io/): Based on the model of Vue.js, and it's created by the team of [Tabao](https://en.wikipedia.org/wiki/Taobao), which is the biggest e-commercial site in China.
    

### Pros & Cons

**Advantages:**

1.  Like webview hybrid, you could still have some dynamic content there
    
2.  You even have native UI. Since all widgets rendered are native, users cannot see the difference between the two.
    
3.  Since native widgets are created, the performance is much better than the webview hybrid.
    
4.  You use HTML to write the app for two sides, so theoretically you still have one set of code for two platforms.
    

**Disadvantages:**

1.  Like the webview hybrid, you may possibly get into the pitfalls during the development. But this time you may get into be even worse ones. In most cases, the engines are either not open sourced (Appcelerator) or the source code is just too complicated to understand and compile by yourself. If you got some engine related bug or limitation, there is [not much you could do](https://www.quora.com/What-is-your-review-of-Appcelerator-Titanium) except asking the developer to fix it faster, which is unlikely to happen actually.
    
2.  Neither of the 3 frameworks are that popular now, so you may not find the corresponding solutions from the stackoverflow easily. If you get stuck, you are likely need to get a workaround with the client at the end.
    
3.  According to the model of this technology, the native UI are created on the fly, based on the JS code (not HTML). And this leads to a fundamental problem, the UI architecture of iOS and Android SDK are actually different. The difference is not huge, but still significant. For example the UIVIewController in iOS could not be fully mapped to Activity in Android, and also the back button display of the two platforms varies in a subtle way. So when the JS object (or whatever else) is mapped to two platforms, there are always **compromise decisions**. And these subtle compromises will make you slowly lose a full control of the UI.
    
4.  Like the case of Cordova, the SDK could be a big problem.
    

Cross Platform Linkage Native
=============================

[![mobile-application-technology-review-cross-linkage](https://walty8.com/wp-content/uploads/2017/01/Mobile-Application-Technology-Review-Cross-Linkage.png)](https://walty8.com/wp-content/uploads/2017/01/Mobile-Application-Technology-Review-Cross-Linkage.png)

This is probably the most bizarre approach among the 5 technologies. The user is required to write a mobile app in a neutral language (non-objective C and non-java), and the project would then be compiled to a native of app of iOS and a native app of Android.

When the final built app is executed, it just run as a normal app, it does not require any JS engine or webview. It just run like a native one.

It's extremely hard to accomplish the trick, and hence very few companies provide this technology. Currently [Xamarin](https://www.xamarin.com/) is the most famous (and probably the only one) company that provides this service. Users only need to write C# for the mobile app development of both iOS and Android. The magic seems to happen in the [low level API](https://www.quora.com/How-does-Xamarin-work), where the linkage from .NET to iOS/Java library happens.

### Pros & Cons

**Advantages:**

1.  Very fast, the compiled product is extremely close to a native one. Unlike the webview hybrid and JS engine hybrid, there is no runtime UI interpretation and patching.
    
2.  You could use the .NET framework and tools (e.g. [linq](https://msdn.microsoft.com/en-us/library/bb308959.aspx)), during mobile development.
    
3.  You could use Visual Studio for the app development. To be fair, visual studio is a much better than IDE than many others.
    

**Disadvantages:**

1.  Like the JS engine hybrid, you could still get stuck on the pitfalls, which you may need to [turn to workarounds](http://www.estaun.net/blog/some-thoughts-after-almost-a-year-of-real-xamarin-use/) at the end.
    
2.  Eventually, the .NET language is mapped to two frameworks. That means **compromise decisions** would still need to be done. You can't get the 100% dedicated UI on both platforms using the one source code file, you just can't. It's not the problem of technology, but a problem for any platform that tries to struggle for 'write once, run anywhere.'
    

Pure Native
===========

[![mobile-application-technology-review-pure-native](https://walty8.com/wp-content/uploads/2017/01/Mobile-Application-Technology-Review-Pure-Native.png)](https://walty8.com/wp-content/uploads/2017/01/Mobile-Application-Technology-Review-Pure-Native.png)

This is the most old fashioned approach to write apps. But in many cases, if your applications are enough complicated, this is actually the most safe way.

You just write an iOS app using xcode, and write an Android app using Android studio. In my own experience, once you have finished the iOS app, writing a counterpart in Android is not that difficult (and vice versa). In most cases you could **re-use architecture, design patterns and backend API**.

### Frameworks:

There are some other tools to help reduce your duplicate work, even if you are trying to develop in the native way:

1.  Game Engine:one could use [3rd party scripting languages](http://stackoverflow.com/questions/6171128/ios-android-cross-platform-development) for the game engines like [unity3D](https://unity3d.com/) (JS/C#) and [corona](https://coronalabs.com/) (Lua)
    
2.  Scripting Engine: one could simply embed the scripting engine inside the app for some dynamic and high level logic, and do all the remaining using native UI. Some popular choices are [Lua](https://www.lua.org/) and [Python](https://www.python.org/).
    
3.  Dual Platform Framework/Libraries: some frameworks provided the API for both platforms, so you could hold your app structure very consistent even if you write every thing from the scratch in the two platforms. One famous example is [cocos2D](http://www.cocos2d-x.org/).
    

### Pros & Cons

**Advantages:**

1.  Totally flexible. If you build the app in the native way, than you should have all the capability you could possibly get to build the app. In other words, if you can't accomplish one feature using the native way, then you can't do it in **any** other approach.
    
2.  High performance. Other hybrid models might also do some optimizations, but they are all implicit work. In this approach, you could tune the app memory with tools using the most standard and explicit ways.
    
3.  Community: the most old fashioned way actually owns the biggest community, as a matter of fact this is the way MOST developers do the apps. One could easily verify this by checking the tagged questions in the stackoverflow.
    
4.  Less pitfalls: there might still be pitfalls using the native SDK, but in general it's much less than other technologies, because it's the ground foundation of everything else.
    
5.  IDE: Android studio is good and Xcode is just great.
    

**Disadvantages:**

1.  Team: As mentioned before, the time and cost is not a major problem actually. But it's difficult to maintain a diversified team in long term. If the company focused on app development then it's fine. But in many cases, the company got an IT team of web developers and only develop the mobile apps occasionally, then it would be question to maintain a skillful mobile development team in the long term.
    
2.  Desktop App: a number of hybrid solutions gives extra benefit over the desktop apps, which means in future you could get the desktop app with relative ease as well. But if you build the native apps one by one, you are unlikely to get a desktop app with the previous source code.
    
3.  API & Device variation: The SDK of both android and iOS changes rapidly, so the developers need to keep an eye on the API changes of both sides. If the app aims to work on some older devices, the backward compatibility is another headache to maintain. Also, during the testing and optimizations, the developers need to handle a lot of subtle differences for various devices. However, with the help of a middle layer technologies, many of such minor issues would be tackled by the engine instead of developer.
    

Conclusion
==========

In summary, pure website is easiest to implement but with biggest limitation. Pure native is most flexible, but with big cost of maintenance. However, both approaches gives a more reliable schedule during project management, you are less likely to get stuck for weeks for a mysterious and program unrelated bug.

The other three technologies: webview hybrid, JS engine hybrid and cross-language linkage are all tricky approaches. You could be very happy at first, and totally painful at the end. Or you could be happy all along the way, depend on the complexity of the apps and the \*\*luck \*\*of your team.

So, let back to the first question, if you need to select a technology to develop a mobile app, what would be your best bet? That really depends on a number of factors, like app complexity, app schedule and available budget. However, I believe the following two factors are the most important among all:

1.  Does the UI detail matter? If the app is for high end customers, and the pixel level UI is wanted. Just forget about all other alternatives, and build the app from scratch!
    
2.  Team. It's seldom brought up by other articles, but I believe it should be the second most important factor to think about. Normally, the composition of a team depend a lot of non-technical factors. For example, what's the expertise of existing team? how diversified a team we would (or want to) maintain? Is it easy to hire mobile developers or web developers? These are objective limitations, and could give you an important hint about your best choice. For example, if your company already has a team of .NET developers, and would like to build a cross platform enterprise app (which means UI is not a big concern), then it makes a lot of sense to use Xamarin rather than Cordova.
    

Finally, here is the table that shows the pros and cons of all the discussed technologies:


<table>
  <tr>
    <td>
    </td>
    
    <td>
      Pure Webview
    </td>
    
    <td>
      Webview Hybrid
    </td>
    
    <td>
      JS Engine Hybrid
    </td>
    
    <td>
      Cross Linkage Native
    </td>
    
    <td>
      Pure Native
    </td>
  </tr>
  
  <tr>
    <td>
      Appstore Approval Process
    </td>
    
    <td>
      N
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      Y
    </td>
  </tr>
  
  <tr>
    <td>
      UI Change after Uploaded to App Store
    </td>
    
    <td>
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      N
    </td>
    
    <td>
      N
    </td>
  </tr>
  
  <tr>
    <td>
      One Set of Code for Two Platforms
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      N
    </td>
  </tr>
  
  <tr>
    <td>
      High Performance
    </td>
    
    <td>
      N
    </td>
    
    <td>
      N
    </td>
    
    <td>
      Medium
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      Y
    </td>
  </tr>
  
  <tr>
    <td>
      Full Native API Access
    </td>
    
    <td>
      N
    </td>
    
    <td>
      Y (need plugin)
    </td>
    
    <td>
      Y (need plugin)
    </td>
    
    <td>
      Y (need plugin)
    </td>
    
    <td>
      Y
    </td>
  </tr>
  
  <tr>
    <td>
      Suitable for App Complexity
    </td>
    
    <td>
      H
    </td>
    
    <td>
      M
    </td>
    
    <td>
      L
    </td>
    
    <td>
      M
    </td>
    
    <td>
      H
    </td>
  </tr>
  
  <tr>
    <td>
      Engineer Knowledge Requirement
    </td>
    
    <td>
      HTML + JS + CSS + Backend
    </td>
    
    <td>
      HTML + JS + CSS, hybrid engine
    </td>
    
    <td>
      HTML + JS, hybrid engine
    </td>
    
    <td>
      C#
    </td>
    
    <td>
      Objective-C, Java
    </td>
  </tr>
  
  <tr>
    <td>
      Big Pitfalls Ahead
    </td>
    
    <td>
      N
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      N
    </td>
  </tr>
  
  <tr>
    <td>
      IDE Stability
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      N
    </td>
    
    <td>
      N
    </td>
    
    <td>
      N
    </td>
    
    <td>
      Y
    </td>
  </tr>
  
  <tr>
    <td>
      High UI Flexibility
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      N
    </td>
    
    <td>
      N
    </td>
    
    <td>
      N
    </td>
    
    <td>
      Y
    </td>
  </tr>
  
  <tr>
    <td>
      Native Look and Feel
    </td>
    
    <td>
      N
    </td>
    
    <td>
      N
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      Y
    </td>
  </tr>
  
  <tr>
    <td>
      Easy to Troubleshoot via Google
    </td>
    
    <td>
      Y
    </td>
    
    <td>
      N
    </td>
    
    <td>
      N
    </td>
    
    <td>
      N
    </td>
    
    <td>
      Y
    </td>
  </tr>
</table>

