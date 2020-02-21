+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/1355/1*qYpAjaxStLTqThkj7bYteA.jpeg"
date = "2020-01-22T15:53:01.244Z"
title = "How I hacked the vote at Chrome Dev Summit"
categories = [ ]
+++




<span class=subtitle>Puppeteering for fun and outerwear</span>


<!--more-->

I wouldn’t say I have a problem. I have an inclination. I like to take things apart and change how they work. As a kid I’d stay on the computer all night poking at bits in memory trying to change a program’s behavior. Most programs would just break. Sometimes you’d hit the right bit and be rewarded with infinite cash in a computer game.


Fast forward a few decades and this inclination led to a career in software development and web security. Websites are perfect for the curious. You can view source code, inspect every request, and tweak an app live via the dev tools. As an application developer, it’s a nightmare. But that’s a different post.


Last November, Google hosted its annual Chrome Dev Summit, a conference by web developers for web developers. It’s a beautiful event put on by brilliant people. Google’s top developer advocates emceed the event and kept the audience engaged between talks.

<iframe width="560" height="315" src="https://www.youtube.com/embed/gUteNZ0IvrE?start=2118&end=2136" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The conference celebrated web features released over the last year and emerging tech that everyone could look forward to. The emcees embraced that theme with an interactive game, the Big Web Quiz, that pitted each feature up against another in a battle of Ultimate Web Tech. Between every talk, the audience got to vote on their favorite features by using a simple web app.


Can you see where this is headed?


Online voting is easy to manipulate and this was an opportunity to see the effect live. Is it wrong? Well, it’s not “right.” But I was at a conference full of developers and unwanted, automated manipulation is a problem they aren’t paying enough attention to. That was enough for me. Let’s get at it then.


Here’s the kickoff for the quiz to get a feel for how it worked.

<iframe width="560" height="315" src="https://www.youtube.com/embed/gUteNZ0IvrE?start=5998&end=6121" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The speakers took turns presenting the candidates for each matchup before turning votes over to the audience. Here’s one of the actual matchups, take note of how long the voting period lasts.

<iframe width="560" height="315" src="https://www.youtube.com/embed/gUteNZ0IvrE?start=6384&end=6415" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The audience can interact with the app for a brief period between the time voting starts and closes. That was less than 20 seconds for this matchup. Others were even shorter. There were fourteen matchups per day over two days. That left twenty-eight windows of less than half a minute each, at forty-five minute intervals, to complete the task. That’s best case. I didn’t start thinking about it until the end of day one.


There was a second problem. I could only see the results projected on stage. There was no feedback in the app. The only way I could confirm a script worked was by skewing enough votes to make the impact obvious, live, during the voting window. I had to have a script working in advance of the final matchups so I could fix bugs before it was over.


The app communicated via websockets so I turned to Firefox’s websocket debugger to inspect the traffic. Firefox makes it easy to see incoming and outgoing messages. Intercepting and simulating network traffic is the fastest way to control an app without diving into its core logic.


Firefox’s devtools allow developers to save local modifications to a page’s JavaScript. It’s useful for debugging live sites. One additional line of code, like window.someIdentifier = targetVariable, is all it takes to expose deeply scoped variables to the global namespace. Tossing variables onto the global makes them accessible on every refresh without dealing with breakpoints. I used this technique with the websocket instance variable to test requests and responses and see how the app responded.


Keep in mind I had to inspect, debug, and iterate in twenty second chunks. Each time the poll ended I closed my laptop and moved on for forty-five minutes.


I did find out how to trigger the voting-state by either simulating a websocket response or setting the app state directly. This extended the hacking window by letting me inspect app behavior outside of voting.


You can still visit bigwebquiz.com today and play around. You can break on line 128 of the prettified source…

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/974/1*DC2Ka6mkDl0XINOfoXByig.png">

…and set your own state like below…

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/557/1*k04g-J7Yzhco6iI39IQAlg.png">

After re-starting javascript execution the app will transition into the voting state:

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/974/1*JrwNMZGpnT3CojXqSSuf6g.png">

You can then submit your response and inspect the websocket messages using Firefox.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/611/1*ciZW1Icgs5t2PJMe-I8fpg.png">

The first step is to replay messages and see if they have the intended effect. I wrote the first attempt in the devtools console using a loop that sent requests via the now-global websocket instance. Low-level requests are always preferred, they execute the fastest. I could pump out thousands of requests in seconds. Thousands of requests should have a clear effect the next time voting opened. But they didn’t. There was no effect. I expected that but tried anyway. I closed my laptop and waited another forty-five minutes.


Refreshing the page didn’t reset the voting state but jumping into incognito mode would. I could try using Puppeteer to script Chrome and open up incognito windows before submitting votes. Using Puppeteer is much slower than making low level websocket requests. I had to parallelize Chrome instances to maximize the number of requests I could make in a voting window. Even still, we’re only talking hundreds of requests over a twenty second period.


The first attempt failed hard. I screwed up how I handled promises in a loop and brought down my computer. Turns out MacBook Pros can’t handle starting hundreds of Chrome instances at once. Another forty-five minutes down the drain.


By the end of the conference I was running out of chances. Incognito mode alone may have worked but I wasn’t sure if IP addresses played a role in limiting vote abuse. With the number of matchups dwindling I updated the script to proxy through Luminati, a service that hides the source of your traffic via proxies. The script wasn’t long. Here’s the lot of it, minus any Luminati account details.

<script src="https://gist.github.com/jsoverson/31fc33fe58ac4c7934ab318909852899.js"></script>

This should work. As if by divine intervention, a matchup with a clear winner was next. Even the hosts resigned themselves to the futility of the vote:

<iframe width="560" height="315" src="https://www.youtube.com/embed/gUteNZ0IvrE?start=21870&end=21905" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Audio device client was the clear underdog. Let’s see if our script was up to saving the poor feature.

<iframe width="560" height="315" src="https://www.youtube.com/embed/gUteNZ0IvrE?start=21996&end=22049" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Something happened! Maybe the audience really wanted Jake to win. Probably not. Who could vote against the combination of portals AND Paul Lewis. Only a soulless robot would do that.


What was I hoping to accomplish here, anyway? I forgot. Let’s do it again.

<iframe width="560" height="315" src="https://www.youtube.com/embed/gUteNZ0IvrE?start=22069&end=22205" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Looks like the bot was discovered. Props to Jake, Mariko, and Paul for handling this live on stage without missing a beat. I did feel guilty and confessed on Twitter right away. I’m not cut out for a life of crime.

<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Sorry <a href="https://twitter.com/aerotwist?ref_src=twsrc%5Etfw">@aerotwist</a> <a href="https://twitter.com/jaffathecake?ref_src=twsrc%5Etfw">@jaffathecake</a> 😂</p>&mdash; Jarrod Overson #Warren2020 (@jsoverson) <a href="https://twitter.com/jsoverson/status/1194399621184778240?ref_src=twsrc%5Etfw">November 12, 2019</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Here’s the response after my confession.

<iframe width="560" height="315" src="https://www.youtube.com/embed/gUteNZ0IvrE?start=23876&end=23921" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Paul looks more miffed than Jake and for that I felt bad. I’ve been on stage plenty and I should know better than to throw a wrench into someone else’s live show. Also, portals really should have won. Not cool on two counts.


Wait, I remember why I did this! It was to expose how bad actors can manipulate our apps in unwanted ways. Wait, no, it was fun. I did it because I have a problem. An inclination. The bad actors bit still fits though.


Much to my surprise (and eventual relief), Jake Archibald reached out via Twitter to see if I was available to receive a “prize” during the next intermission.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/517/1*76PnIPvS8XcjKYo4Uu4t2g.png">

Right. “Don’t worry it isn’t a trick” is exactly what I would expect to be told right before being tricked. I played along regardless. I told you I wasn’t cut out for this.

<iframe width="560" height="315" src="https://www.youtube.com/embed/gUteNZ0IvrE?start=27801&end=27852" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

And that’s how I became a failure at life.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/1355/1*qYpAjaxStLTqThkj7bYteA.jpeg">

What’s the moral of the story? Break stuff. You’ll either get a job or a T-Shirt out of it.


[Share this on Medium](https://medium.com/@jsoverson/how-i-hacked-the-vote-at-chrome-dev-summit-ba6cea7a468e)
