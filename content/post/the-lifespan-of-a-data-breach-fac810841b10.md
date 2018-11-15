+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/1514/1*ZsB_Lef8PR3aKrmnsqsMLg.png"
date = "2018-09-05T20:08:29.492Z"
title = "The Lifespan of a Data Breach & the Attack Lifecycle"
categories = [ ]
+++




<span class=subtitle>How a Data Breach gets passed around</span>


<!--more-->

I’ve been giving talks on credential stuffing and data breaches for a few years now and talking about the attack lifecycle and the ecosystems that support these attacks is one of my favorite things. It’s fascinating how much of a community and business has been built up around data breaches and credential spills and talking about it in public never fails to get met with disbelief, surprise, and skepticism.


### Tiers of Attacker Sophistication


In my last session I talked more about the tiers of attackers than I usually do which helps to tell a better story from the day of a breach to the downstream damage to, eventually, the records ending up on a site like haveibeenpwned.


This is a gradual process because breached data doesn’t get distributed across the world overnight. Credential spills, the class of breach that involves emails & passwords, are only as valuable as the freshness and the validity of the data. The first attacks are held close to the chest because the more this data is used the more it will trigger red flags to users and companies which then rapidly degrades the value.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/1514/1*ZsB_Lef8PR3aKrmnsqsMLg.png">

After the initial attacker(s) have gotten all the value out of the data they needed, they sell or share this data to their private network of associates who then proceed to do the same until they are done or after an agreed upon window of exclusivity closes. Once the first two tiers are done the data is resold on the dark web until someone there breaches the network of trust (or is exploited themselves) and the data makes its way to the public where anyone can grab it.


### Credential Spills gradually lose value

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/1856/1*UiHHyuru8uJXhrPSIrc-tg.png">

Credential spills naturally lose value over time because passwords have a habit of changing over time — they get reset after being forgotten, people get notified of breaches and all accounts are reset, or maybe they see scary emails calling out failed login attempts, anything. Passwords change for many reasons. Once a spill is publicly reported, though, the data in that spill loses value quickly, everyone gets notified at the same time and passwords are reset all around. It’s becoming less and less common to see spill data in the public eye before the breach is reported for (at least) two reasons: Troy Hunt has built his own free breach reporting service to help keep companies accountable and companies themselves have started scouring the dark web to see whether or not their own data is purchasable anywhere.


What I’m seeing as part of my research at Shape is spill data being locked away in the Tier 1 and Tier 2 groups for longer precisely because of this increased public awareness. Keeping this data hidden for as long as possible helps retain the value longer. This is analogous to the bittorrent-centered piracy scene over the course of the early 2000s and 2010s — when sites like The Pirate Bay were relatively under the radar it was trivial to find high-value movies and software but, after years of crackdowns, many private groups have kept onto content longer and held untrusted users at bay. This lifecycle is the natural evolution for stolen digital property.


There’s a lot more behind the attacker ecosystem that I’ll get into at a later point but if there’s one thing you can take away from this is that attacks are not performed by lone individuals, they aren’t straightforward, and they are backed up by more sophistication than most are aware of. You can’t patch your way out of being vulnerable to attacks that stem from data breaches.


I gave a talk on this somewhat recently and you can check out the slides on slideshare here if you’re interested, thanks!


[Share this on Medium](https://medium.com/@jsoverson/the-lifespan-of-a-data-breach-fac810841b10)
