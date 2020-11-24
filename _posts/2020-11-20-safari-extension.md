---
layout: post
title: Convert Safari Extension
date: 2020-11-20 19:22
summary: How to convert safari extension
categories: jekyll pixyll
---

## HOW TO CONVERT A CHROME EXTENSION INTO A SAFARI WEB EXTENSION, AND UPLOAD TO MAC APP STORE

Original Article: [https://www.bart.com.hk/convert-chrome-extension-safari-web-extension-upload-mac-app-store/](https://www.bart.com.hk/convert-chrome-extension-safari-web-extension-upload-mac-app-store/)

**Part A: Safari Web Extension Development**

Here we use [Simple Gmail Notes](https://www.bart.com.hk/simple-gmail-notes/) ([Source Code](https://github.com/bartsolutions/simple-gmail-notes.chrome)) for the example.

1. Make sure you have Safari 14 and Xcode 12 installed

2. In the terminal, use Xcode command for the conversion\
 \
 `xcrun safari-web-extension-converter <your extension folder>`\
 \
 (click Yes for default options)  
 \
 ![](/images/safari-extension/1__CBbsbXl6SQMT0XwsqSVhg.png)

3. A brand new Xcode project folder will be created, and Xcode will be automatically launched to open the new project.\
 \
 **The Xcode project will be linked to the source web extension folder**, so you need to make sure both source and generated folder exist and have a consistent relative path.\
 \
 ![](/images/safari-extension/1_nyn86xrO3GAPmaCbqsi3MQ.png)

4. Without doing anything further in Xcode, just click run to launch the extension

![](/images/safari-extension/1_DosAhhL5NhDF9HXMob1ctw.png)

5. Safari will be opened, yet extension will not appear at first sight. You need to do the following steps first:

5a: safari -> preferences -> enable development menu

![](/images/safari-extension/1_jj8e5xo5pbIEo3fWPf07uw.png)

5b: safari -> develop menu -> click allow unsigned extension (need to do this every time safari is restarted)

![](/images/safari-extension/1_IEtQu72j26N8jIO5Wx2SUA.png)

5c: safari -> preferences -> extensions tab -> click the extension

![](/images/safari-extension/1_emZPRoHUXbdc2ElGMje-Fw.png)

5d: open the web site, click the icon near the address bar, and allow the access

![](/images/safari-extension/1_RuDTgJkiWzWglW68oE3zYw.png)

6. Now the extension should be able to be launched, and you could see the content script in the Safari debug console.

![](/images/safari-extension/1_OQ5OSpAwrW1CBTYUD5hX_w.png)

7. To check the background script, in the Safari, click Develop -> Web Extension Background Pages

![](/images/safari-extension/1_Q-PT2K0Syj9RgapsyptoNA.png)

**Part B: Distribute Safari Web Extension to App Store**

1. Go to App Store Connect, create an identity:

[https://developer.apple.com/account/resources/identifiers/list/bundleId](https://developer.apple.com/account/resources/identifiers/list/bundleId)

![](/images/safari-extension/1_xwzbX2Ny1ZtPB-z0i94F5w.png)

2. In App store connect, create an app of ‘macApp’

[https://appstoreconnect.apple.com/apps](https://appstoreconnect.apple.com/apps)

In the bundle ID drop down, just select the one newly created

![](/images/safari-extension/1_bVO2qsEulT_G44DXd2KH1g.png)

![](/images/safari-extension/1_MVOM6H0RD4je_nNrIk_Ajg.png)

3. Go to Xcode, click Project -> target -> app target, update app category and bundle identifier (use the one in the appstore)

![](/images/safari-extension/1_NQJEH-Km9X9crvuTT0-TjA.png)

4. Click extension target of project, update bundle identifier.

Note the the project identifier should prefix the extension identifier. E.g. if project identifier is ‘hk.com.bart.simplegmailnotes’, then extension identifier should be something like ‘hk.com.bart.simplegmailnotes.extension’

![](/images/safari-extension/1_LGUVUhVz3WD2KDVVHyQK6g.png)

5. In Xcode -> assets -> make sure all icons are provided

![](/images/safari-extension/1_JfhkvwLcgxES-2aX9i4PEA.png)

5. In Xcode click Product -> Archive

6. Distribute window should automatically appear after the archive action. (If not, click Window -> Organize -> Distribute App)

![](/images/safari-extension/1_iAcgMEl4ThfgutKtFKqsxg.png)

7. Select App Store Connect

![](/images/safari-extension/1_bdtXGyYhWTdgOoDVMNF2bg.png)

8. Open a browser, go to App store connect, click the app, and now you should be able to select the build

![](/images/safari-extension/1_1Dv4lovtS5m5Ck67AqLfGg.png)

![](/images/safari-extension/1_pyl8mgUqkzlEsM53D-eDVg.png)

(If the build is not available, check your App Store email and see if there are any error reports.)

9. Upload all the screenshots and add descriptions to App Store Connect

10. You are now good to start a review process.
