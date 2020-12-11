---
layout: post
title: A Simple Way to Use NPM Library in Browser
summary: Occasionally, we need to use a JS library in our browser side, yet it's only available from the NPM repository.
---

Occasionally, we need to use a JS library in our browser side, yet it's
only available from the NPM repository.

As usual, the [Google result](https://www.google.com/search?client=firefox-b-d&q=use+npm+library+in+browser)
of any NPM related questions will bring you more yes-and-no answers, and
leave you in further confusions and headaches.

Well, life better be simpler :)

Say, we are going to use the NPM library of `email-js-mime-parser` and
`buffer` in the browser, all we need to do is:

​1. install browserify tool
 {% highlight bash %}
 npm install -g browserify
 npm install emailjs-mime-parsernpm install buffer
{% endhighlight %}

​2. install npm libraries
 {% highlight bash %}
 npm install emailjs-mime-parsernpm install buffer
{% endhighlight %}

​3. create a new JS file, `main.js`
{% highlight javascript %}
var parse = require('emailjs-mime-parser').default
var Buffer = require('buffer').Buffer
global.window.parseEmail = parseglobal.window.Buffer = Buffer
{% endhighlight %}\
(Note that `default` is needed for `emailjs-mime-parser` because of
legacy export syntax.)

​4. compile the `main.js`:
{% highlight bash %}
browserify main.js -o bundle.js
{% endhighlight %}

​5. use `bundle.js` in normal webpage, and you could use `parseEmail` and `Buffer` in the browser side JS:
{% highlight html %}
{% raw %}
<html>
<head>
<script src='bundle.js'></script>
<script>
console.log(window.parseEmail);
console.log(window.Buffer);
</script>
</head>
<body></body>
</html>
{% endraw %}
{% endhighlight %}

 


 

And that's all :)

