+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/1920/1*x9eeLbFbHabj68YTY0jG2w.jpeg"
date = "2019-01-17T16:44:29.091Z"
title = "Collection #1 and how Credential Stuffing works"
categories = [ ]
+++




<span class=subtitle>Troy Hunt just uploaded HaveIBeenPwned’s largest dataset yet, the “The 773 Million Record “Collection #1” Data Breach”, found on the…</span>


<!--more-->

Troy Hunt just uploaded HaveIBeenPwned’s largest dataset yet, the “The 773 Million Record “Collection #1” Data Breach”, found on the hosting service MEGA.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/2230/1*aIn_Mh40thwHSev-xCku4w.png">

I’ve already gotten a large number of questions as millions of people learn the term “credential stuffing” for the first time.


## So what is credential stuffing?


Credential stuffing, at the core, is just testing a username and a password across different sites to see where that combination has been reused.


It sounds simple because it is. Of course, testing random passwords isn’t going to result in much success but attackers don’t need to be random to be successful because users are predictably human— most users reuse passwords across many services. An attacker just needs to find your password once and they have a much higher chance of finding an account of yours that can be taken over.


Luckily for those attackers, Companies are doing a very poor job at 1) preventing their data from being breached and 2) securing the data in the first place in order to make a breach less valuable if it ever does happen.


## How does a data breach lead to credential stuffing?


A breach could be any data that gets stolen from a company. A class of data breach, a credential spill, is what we’re focusing on here. A credential spill is a data breach associated with, you guessed it, credentials like usernames and passwords.


Most companies don’t store passwords in their raw form, thankfully. They often hash passwords in a way that makes it easy to verify but difficult to reverse. The result of this hashing is what looks like a string of random characters.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/2654/1*2PlS4XMmAwRi1RX8lwpHbg.png">

This hashing process loses data, meaning you can’t go backwards from a hash to its input. The same input also results in the same hash every time.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/2654/1*Fq_xEKoIbHajAySbUCT57g.png">

It sounds like the perfect password solution! You can’t reverse it to get the password but as long as you have a password you can check to see if it’s the same one you’ve stored. Great! Many credential spills are exfiltrated in a form that has row after row of username plus its paired credential hash, e.g.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/2654/1*I9AXa8O_-BxeljLu3C776A.png">

The problem with these hashes is that many hashing algorithms can be run very, very quickly on everyday computers. Using free tools like hashcat combined with freely available databases like the top 1,000,000 passwords then your job becomes very manageable and cracking these hashes ends up being a trivial exercise.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/3028/1*PPaycvya2XKbF-DihMnOTw.png">

Now even if you use a completely unique password, if it is 8 characters or below then it is still quickly crackable. Each character you add increases the difficulty substantially.


So now you have a list of usernames and passwords, the next step is to test them. Testing them by hand is not feasible when you’re dealing with database the size of Collection #1. Testing 772,904,991 credential pairs, 1 every second, would take over 24 years. Luckily, we have computers!


## How to Credential Stuff


Just google for account checker. If you’re having a hard time then search on youtube for account checker tutorials.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/2290/1*AZTzwkm6uXw_KNkz_Zc8Xw.png">

Like I said, if it sounds simple it is because it is. Of course, the gradient of attackers who engage in credential stuffing campaigns is massive and it all depends on the cost vs value of the service being attacked. Services that are very attractive, like banks or other financial services, have better protection which necessitate better tools which require more sophisticated attackers. This leads into one of the other reasons why credential stuffing is such a problem, one simple defense can’t protect websites forever. The landscape changes, elevates, and becomes harder to manage over time.


What credential stuffing attacks boil down to though is a tool that is designed to make web requests over and over runs and amasses a list of working accounts for each service it is run against.


This known-good list is then used by the attacker for more targeted fraud. Maybe it’s emptying a gift card balance, or selling Fortnite accounts that have rare skins, whatever. After the fraud has been completed those lists are then resold on the dark web for more other attackers to use and engage in other form of fraud. These lists last forever and eventually make it into a dump like Collection #1.


## As a user, how can I protect myself?


Don’t reuse passwords. If you have (good) unique passwords everywhere then you are almost completely safe. That’s it. Managing unique passwords is hard so I recommend using 1Password or another password manager. If you don’t like that idea then use a notebook. Really. Your biggest threat is being caught in the wide net of credential stuffing attacks, not the people around you. Writing your passwords down and doing a good job keeping that book safe is better than reusing a 30 character password like “siFVpcd7i.3NgmjwUnHtVm,iz+jPbj” across all your services.


## As a company, how can I protect my site?


I’m working on a blog post and video on this topic specifically so please follow me on Medium or subscribe on YouTube if you want to be notified when it is out. Until that time I’m available for one-on-one discussions over the phone, on twitter, video, whatever. I also work for Shape Security, easily the leader in this industry and the company that coined the term “Credential Stuffing” in the first place — if you have a serious problem now then contact us for a more serious discussion ASAP.


Make sure to reach out on Twitter for any questions, quotes, or thoughts!


[Share this on Medium](https://medium.com/@jsoverson/collection-1-and-how-credential-stuffing-works-5429029f4c46)
