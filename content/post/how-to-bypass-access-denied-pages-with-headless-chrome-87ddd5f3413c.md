+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/5627/1*AlWWNFwUOT0hce2g-H__tA.jpeg"
date = "2019-03-26T17:06:16.799Z"
title = "How to bypass “Access Denied” pages with Headless Chrome"
categories = [ ]
+++




<span class=subtitle>Some websites block Headless Chrome, here’s how to get around it.</span>


<!--more-->

Troubleshooting is key in all aspects of computers and programming — this article starts with how to figure this problem out on your own. If you don’t care, jump to the TL;DR at the end.


If you’re having trouble with headless mode, remember to take a screenshot with page.screenshot() so you can see what’s going on. At the least it lets you know if you’re dealing with the same visible content you have with headed mode and you’re not stuck at a broken script without understanding what you’re working with.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/1824/1*f2oeJayq4nWevzNSgkw-gA.png">

In this example the server didn’t even respond with the proper web page itself. The initial response is an “Access Denied” page and that’s all we can get when running Chrome in headless mode. This doesn’t happen at all in headed mode.


When troubleshooting it’s important to identify what we know and what we don’t know. Without this step it’s impossible to pursue a course of action that targets the unknown and isn’t redundant. This may sound basic but, unless you understand why, it’s non-intuitive how to get there. Troubleshooting is sometimes seen as running through a checklist but that only works if you have encountered the problem before.


What do we know? We know that the browser made a single request and we received a response that already said access denied. The original page wasn’t rendered and the browser made no other requests. This means that a server somewhere made a call based strictly on what we sent for that first request and our block has nothing to do with page content. That rules out troubleshooting anything after the page render and limits our scope to the request alone. The request itself is a bunch of bits and bytes sent over the internet and accepted by a server.


## Comparing HTTP Request headers


Because there is (supposed to be) little difference between Chrome when run in headless vs headed mode it’s a reasonable assumption that the core network stack is the same and there are no differences in how the browser transmits requests at the packet level. This points us to the content of the request alone. We can use a service that echos back our HTTP requests to inspect the differences between a request made from headless and headed Chrome. The following script uses http://scooterlabs.com/echo.json to get a JSON response that represents the request the server received.

<script src="https://gist.github.com/jsoverson/d419b945c480ecbfc71d3bc016c9d666.js"></script>

By running this in both headless (the default) and headed mode (by changing the launch properties to include headless:false) we can diff the output to see what, if any, differences there are.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/3544/1*qQNeyjMAMqgDO4mXKaqmKw.png">

time_utc is the time we made the request. It differs but is unlikely to be the single source of the block unless the site blocks all requests at certain parts of the day.


The Accept-Language header is missing altogether from headless mode. This is actually a good signal that someone is using a non-standard browser (or browser-mode) and is something the website could be using to block us. It would be my first guess if we didn’t also have the final differing header, theUser-Agent header.


User-Agent is a clear standout. The diff cuts off the important part, but headless Chrome is making itself known via this header:

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/3544/1*znR39fFfhDJlzwr7z4J1JA.png">

The header for headed Chrome is mostly the same minus the “Headless”. The User-Agent has long been a basic, naive way of blocking unwanted traffic. This is a good first place to start to see if we get what we need.


Blocking on User-Agent is naive and rarely used as a countermeasure nowadays because of how simple it is to bypass. It actually provides more value to a website to not block with it and use it to identify unwanted traffic because visibility is better than being blind.


## TL;DR: The solution


The solution is as easy as changing the User-Agent header which you can override on a page-by-page level with the method page.setUserAgent(). You can set the user agent to headed Chrome which, at the time of this writing, is “Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.75 Safari/537.36”.


That’s it. That’s why the method of troubleshooting is more important than the solution. These sorts of hurdles pop up all the time when trying to automate websites and, often times, you’re not going to find clean googlable answers so you’ll need to figure out how to solve it yourself. Good luck and feel free to reach out with any questions!


[Share this on Medium](https://medium.com/@jsoverson/how-to-bypass-access-denied-pages-with-headless-chrome-87ddd5f3413c)
