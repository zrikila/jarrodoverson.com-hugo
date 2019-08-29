+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/1292/1*ACtKxwthTY2662laLH803Q.png"
date = "2019-03-29T16:32:40.738Z"
title = "Stop asking users to enter good passwords"
categories = [ ]
+++




<span class=subtitle>You know the requirements. You know what makes a good password. Stop asking users to dance for you.</span>


<!--more-->

How often have you seen a registration form with a dozen different password requirements? Something like this?

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">What&#39;s this about, <a href="https://twitter.com/VirginAtlantic?ref_src=twsrc%5Etfw">@VirginAtlantic</a>? Your password restrictions seem silly and reduces security. /cc <a href="https://twitter.com/PWTooStrong?ref_src=twsrc%5Etfw">@PWTooStrong</a> <a href="https://t.co/N9kRaBiPgC">pic.twitter.com/N9kRaBiPgC</a></p>&mdash; JimDabell (@JimDabell) <a href="https://twitter.com/JimDabell/status/1111187568266084352?ref_src=twsrc%5Etfw">March 28, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Or maybe your product experience team thought that was too ugly so they opted to not even show the user what the requirements are.

<iframe width="560" height="315" src="https://www.youtube.com/embed/1xNxTesAKtE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Let’s get this straight, as a developer or product owner you know the following:

# Your unique requirements for passwords on your service.
# That users should pick a unique password for your service.
# That passwords should be reasonably complex to hinder cracking.

Why let the user pick the passwords at all? You’re forcing them to jump through hurdles to find something “good enough” — are you expecting them to pick a password that resonates with them? That makes them smile in a way that only that password can? No, they’re trying to use your site, password choice is a barrier.


## Generate passwords for your users.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/1231/1*BtXdc8tb7apWXs6K6G7eOQ.png">

This will help your users be better protected by default and it’s one less field to fill out which may positively impact the bounce rate on a registration flow.


Product and UX teams may need to rethink some user experience details and it may not be perfect but we’re talking about replacing an awful user experience that leads to poor security practices with a more flexible and potentially better user experience with better security implications.


Every major browser now has a capable password manager that also synchronizes across browsers and devices. We should ensure that password managers are managing good passwords, not awful ones.


## Why shouldn’t the user enter their own password?


A password should be a random string of characters. It shouldn’t be something that has meaning to any individual. Even with the password generators we already have, in browser and out, they still run afoul with arbitrary (and often poor) password requirements. Why not take that generation into your own hands and produce a better user experience?


We all know that weak passwords lead to cracked passwords (if you don’t, see: password security & password hashing algorithms). We all know that reused passwords, even if they are magnificent, leave users open to credential stuffing attacks (if you don’t, see: What is credential stuffing?). At Shape Security we see the resulting damage of bad password practices every single second of every single day. In the first 6 weeks of 2019 we saw over 2.3 billion (with a B) credentials leaked on the open web. In those same 6 weeks we recorded our biggest attack yet with 3 billion account takeover attempts in 7 days (and by the way, we just launched a self-service defense for smaller businesses, Shape Connect, if these sorts of attacks are sounding familiar to you).


We aren’t going to get rid of passwords completely in the near future but we can do a much better job at dealing with them.


[Share this on Medium](https://medium.com/@jsoverson/stop-asking-users-to-enter-good-passwords-b761685d05a)
