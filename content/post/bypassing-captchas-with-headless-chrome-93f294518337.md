+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/1200/1*VrrSt0Kx9109UmWXwgQKRw.png"
date = "2018-12-03T18:23:46.074Z"
title = "Bypassing CAPTCHAs with Headless Chrome"
categories = [ ]
+++




<span class=subtitle>Using 2Captcha and Puppeteer to automate through CAPTCHAs</span>


<!--more-->

You’ve seen CAPTCHAs all over the internet for over a decade now. Those squiggly lines, words, or numbers that block your way when you try to log in, sign up, or post a comment anywhere.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/1006/1*oahXcpeA_ePC6gFP7XhWWw.png">

CAPTCHAs (or Completely Automated Public Turing tests to tell Computers and Humans Apart) are designed to be a gate that lets humans through and robots (programs) out. The squiggly lines and wiggly words are less common nowadays and they have been replaced by version 2 of Google’s reCAPTCHA. This is the CAPTCHA that gives you the green checkmark as long as your humanity quotient is deemed high enough.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/616/1*GmtGvbap0r7toziy-rV9rw.gif">

If you don’t score above Google’s human threshold then reCAPTCHA falls back to a puzzle-like picture challenge which, surprisingly enough, actually succeeds at being more annoying than deciphering a couple words.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/830/1*-l3OuRKcooLd5Y4OvBYSWQ.png">

As annoying as CAPTCHAs are for humans they could be tolerated if they at least did their job but it’s almost easier to automate them than it is to prove to them you are human.


## How 2Captcha works


2Captcha solves a number of different CAPTCHA styles all with mostly the same two API endpoints. The first request delivers the data necessary for the CAPTCHA to be solved and returns a request ID. In the case of an image-based CAPTCHA, the data would be a base64-ed image of the CAPTCHA itself.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/1682/1*Tsk1lK-VMi7tYgxdLPck8A.png">

Once you have the request ID then you will need to submit requests to the result endpoint, polling until the solution is ready.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/1680/1*RnL29oLlXWUBSHoEltNTsA.png">

For reCAPTCHA v2 the story is a little different. You’re still engaging in the same 2-step process as above but you’re sending different data. In this case you need to send the reCAPTCHA sitekey which can be found on the containing <div>, regardless of whether or not the iframe has loaded.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/2686/1*56EMzNr3YuWhD23YX55DBA.png">

The response you get is a token that needs to be submitted alongside the form and needs to be entered into a hidden text field with the ID of g-recaptcha-response. The image below shows where it is located and I’ve disabled the display: none css property just to shows it in the page. Having it editable makes it easy for you to test out the 2Captcha response by hand in order to reduce the variables of testing integration.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/2935/1*acvBNfUaTZ38fo2KkkU3ig.png">

For image-based CAPTCHAs the result is almost instantaneously available. For reCAPTCHA v2, it can take upwards of 15–30 seconds.


## Automating with Puppeteer


Before worrying about the CAPTCHA you need to get everything else taken care and before we can do that we need to choose our weapons. In this post we’re going to be using Google’s Chrome for 3 reasons:


(( Unhandled block ))


(( Unhandled block ))


(( Unhandled block ))


### Using Puppeteer


You don’t even need to install Chrome if you don’t want it, Puppeteer comes with everything you need including a Chromium install. You can use a local installation of Chrome if you want it, but that’s up to you.


(( Unhandled block ))


Make sure everything’s all wired up by taking it for a spin. For this exercise we’re going to be automating Reddit’s signup page simply because it was the first page I came across that used reCAPTCHA.


(( Unhandled block ))


(( Unhandled block ))


(( Unhandled block ))


In this code we’re specifying two configuration properties at launch, headless: false in order for us to be able to see what we’re doing and defaultViewport: null to account for an ugly visual glitch where the viewport doesn’t fill the window. Neither are important for headless operation — they just make it easier to see and, more importantly, take screenshots. Like this one:

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/2624/1*69bFrHEsbdH30YmR31RKmw.png">

That was easy! Now that we’re up and running the next step is to automate the signup as if there wasn’t a CAPTCHA in place. This is where having the ability to toggle headless off and on is helpful because we can drive the browser like a human when we need to. First we need to understand how to access the elements on the page that need to be manipulated. Get your browser running and inspect the loaded page via Chrome’s devtools (Shortcut: F12). Next, find the text fields we’ll need to manipulate (Shortcut: ⌘+Shift+C on Mac and Ctrl+Shift+C on Windows). In Reddit’s case we need to be able to directly access the username field, the 2 password fields, and the button. The email field is optional so we can ignore it. Typing in text fields is almost comically intuitive with the puppeteer API, you simply pass in selector that identifies the element and the desired string to the .type() method.


(( Unhandled block ))


Manipulating the button is just as intuitive except that the button in Reddit’s page doesn’t have an ID associated with it so we need to have a slightly more complicate selector. If you aren’t familiar with CSS Selectors, check out the Mozilla Developer Network for a quick rundown.


(( Unhandled block ))


There you have it! Test the script to make sure the login is being submitted. It won’t work, of course, because of the CAPTCHA, but we can test to see the hooks are working properly.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/2624/1*p3niwPN83-WyvuJojJh_xw.png">

Wait a second! We don’t even see a CAPTCHA and the JavaScript console is complaining of errors. What is happening here? When automating web pages there are numerous non-CAPTCHA hurdles that can get in your way and one of them is just going so fast that the page breaks. When browsers are automated they are manipulated many, many times faster than a normal human can operate and that often leads to code being executed in an order that developers had not tested (this is called a race condition).


Reddit’s page suffers from a race condition where Google’s reCAPTCHA is only being rendered after the second password field has been focused. Our script operates so quickly that focus occurs before the reCAPTCHA script is ready. There are many solutions to this but the easiest is to add the smallest delay necessary that gets around this race condition. We could add hooks and listeners to make sure we only operate after reCAPTCHA has been loaded but the Reddit developers themselves seem fine with this race condition so there’s no need for us to get too smart. There are many ways we can delay but Puppeteer’s browser launch options take in a “slowMo” value that globally delays all actions a set amount. This is a heavy handed approach since it slows down any Puppeteer action but it’s a good place to start.


(( Unhandled block ))


After adding that option we see the CAPTCHA and things are back on track. For a fun experiment you might as well try to solve the CAPTCHA right now and see what happens. Since we’re using the default Chromium instance that Puppeteer opens and we are controlling it via automated means then reCAPTCHA will try its damnedest to prove that we’re not human. You will likely go through multiple levels of the challenge even if you’re getting all the pictures right. When I tested this I had to go through 10 different iterations before I got the green checkmark.


Luckily we have a much easier way of doing this.


## Wiring up 2Captcha


2Captcha needs an API key which you get when you sign up. You’ll also need to deposit some funds because, well, nothing in life is free. And just for fun, of course, you’ll need to solve a CAPTCHA when signing up 😃

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/2222/1*SO3buG87yMQwVggpTg3snA.png">

2Captcha’s API works via a 2 step process where you submit CAPTCHA data in and then poll for results with the returned request ID. Since we’re dealing with reCAPTCHA v2 we’ll need to send the sitekey for Reddit which I outlined earlier. We also need to make sure we set the method to userrecaptcha and deliver the page URL that this reCAPTCHA is located on.


(( Unhandled block ))


(( Unhandled block ))


(( Unhandled block ))


After you make this call and get a request ID back, you need to poll the “res.php” URL with your API key and the request ID in order to get the response.


(( Unhandled block ))


If your CAPTCHA is not ready then you’ll receive a “CAPTCHA_NOT_READY” response which indicates you need to try again in a second or two. When it is ready the response will be the appropriate data for the method you sent. For an image based CAPTCHA it’s the solution, for reCAPTCHA v2 it’s the data that you will need to send with the form inputs.


For reCAPTCHA v2 the solution times can vary a bit — I’ve seen it as quick as 15 seconds and as long as 45 seconds. Below is an example polling mechanism but this is just a simple URL call that can be integrated in your app however you feel comfortable


(( Unhandled block ))


(( Unhandled block ))


(( Unhandled block ))


(( Unhandled block ))


After you have the response data you need to inject that result into the hidden g-recaptcha-response textarea in Reddit’s signup form. This isn’t as easy as using Puppeteer’s .type() method because the element isn’t visible and can’t receive focus. You can make it visible and then use .type() or you can use JavaScript in order to inject the value into the page. To inject JavaScript into a page using Puppeteer we have the .evaluate() method which takes either a function or a string (if you pass a function then it simply .toString()s it) and runs it in the page context.


(( Unhandled block ))


(( Unhandled block ))


Once we’ve injected that value then we are all set to complete our signup. It’s really as easy as that.

<iframe width="560" height="316" allowfullscreen="" frameborder="0" src="https://medium.com/media/22e8d98b7dbaaf52d65c1e47e5ee1c2e?postId=93f294518337"></iframe>

The full script is located below if you want to experiment with Puppeteer and/or 2Captcha.

<iframe width="560" height="316" allowfullscreen="" frameborder="0" src="https://medium.com/media/473779fad284f954ee604d9ff2b53e4b?postId=93f294518337"></iframe>

## What can you do now?


This post was written for two purposes:


1. Show you how much CAPTCHAs suck


and


2. Show you that CAPTCHAs don’t need to block you


CAPTCHAs are there usually to block bad actors manipulating content for fraudulent or malicious purposes in attack campaigns that run into the millions of requests. There are many legitimate reasons why you might want to programmatically control a website and if CAPTCHAs aren’t blocking the bad guys then they sure shouldn’t stop you.


Thanks for reading! As always feel free to reach out on twitter @jsoverson with questions or comments.


[Share this on Medium](https://medium.com/@jsoverson/bypassing-captchas-with-headless-chrome-93f294518337)
