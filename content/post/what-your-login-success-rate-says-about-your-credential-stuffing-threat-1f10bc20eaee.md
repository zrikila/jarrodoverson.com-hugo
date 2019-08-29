+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/1200/1*m7bFhTEnhq1_3Rovbgzkmw.jpeg"
date = "2019-05-10T18:22:32.903Z"
title = "What Your Login Success Rate Says About Your Credential Stuffing Threat"
categories = [ ]
+++




<span class=subtitle>One of the problems with imitation attacks such as sophisticated credential stuffing is that they are designed to blend in with legitimate…</span>


<!--more-->

One of the problems with imitation attacks such as sophisticated credential stuffing is that they are designed to blend in with legitimate traffic. How can you measure something that you can’t detect? Fear-mongering marketing compounds this problem and makes everything sound like a snake-oil solution for a problem people don’t think they have.


Imitation attacks against your services and APIs leverage inherent functionality in your system. In other words, they can be successful even when you have patched, firewalled, and done everything perfectly from an application security standpoint. Blocking basic credential stuffing attacks generated from naive bots is straightforward but, as attackers evolve, they develop more sophisticated tools to launch attacks that blend in with legitimate traffic better. They use machine learning to emulate user behavior like mouse movements and keystrokes. They generate or harvest digital fingerprints to distribute across a botnet to make each node appear more “real.” They proxy requests through residential IP addresses to give the traffic the appearance of originating from known-good home networks. Googles themselves make tools like Puppeteer & headless Chrome to automate and script the world’s most common browser which is exactly what you would use if you were trying to blend in with legitimate users. This is a problem that is getting harder, not easier.


Imitation attacks like advanced credential stuffing do have one thing in common, though — they send millions of requests hoping that a fraction of a percentage end up successful and result in an account takeover, a valid credit card, an account number with a loyalty balance, anything. This success/failure ratio is observable with data you have now. What we’ve found at Shape, is that similar companies have similar success ratios for similar user experience flows.


> If you’re debating if you have a credential stuffing problem, then take a long look at your login success ratio.

## What is your average login success ratio?


The average login success ratio drops dramatically during periods of credential stuffing attacks. These attacks use combolists with millions of usernames and passwords and of course the majority of these credentials aren’t valid on your site. Shape sees credential stuffing success rates between .2 and 2%, typically — attackers don’t need a very high success rate as long as the attack is cheap to perform. These attacks push the login success rate for your site down well below normal numbers. Some Shape customers have seen login success ratios lower than 5% before enabling countermeasures. Success ratios that low are abnormal and should be immediately investigated. Below are average login success ratios for one month of traffic across three major industries:

- Financial institutions: 79%
- Travel industry: 73%
- Retailers: 62%

Individual companies deviate from this average as much as 10% — the sites where customers log in more frequently tend to have a higher login success ratio. The users at these sites are more likely to remember their passwords and are also more likely to have stored their credentials in their devices or web browsers. Banks and financial institutions only keep users logged in for 15 minutes leading to more successful logins than retailers or social media sites that keep users logged in for longer periods of time. This results in much higher login success rates for banks than for retailers.


Users also have access to few bank accounts and do not change them often, as a result they are more likely to remember their login credentials. Users however regularly shop at multiple retailers and it is easy to create a retail account. This results in lower login success rates for such sites, reflecting a higher rate of users who may be visiting for the first time in months or even years. Infrequent visitors naturally forget their passwords more regularly.


> Companies should expect to see 60–85% login success rates. Anything higher or lower is suspect.

No matter the industry, companies should expect to see 60–85% login success rates. Anything higher or lower is suspect. Spikes in traffic can temporarily affect the login success ratio but those should be explainable by commonly understood events like promotions or viral marketing. If there are spikes that have nothing in common then you should look deeper, that traffic is probably a credential stuffing attack that you need to stop as soon as possible.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/613/1*EwiSI_lX-ouZDzCRldV7xQ.png">

## One caveat


Some industries like banks and other financial institutions are frequently targets for aggregators, services like Mint and Plaid that act as delegates with user permission to log in and gather data across many companies and present it in one unified interface. Aggregators use legitimate credentials and log in multiple times a day, unnaturally inflating the login success rate. You can look for evidence of aggregators by querying for successful logins across multiple users from the same IP addresses, especially if the IP addresses are from cloud or hosting providers. This is not a foolproof method of detection but you will see traces that will help you get a better understanding of your true login success ratio. If you see login success rates in the high 80s or 90s, that is abnormally high and indicative of low credential stuffing threat but high aggregator traffic. Whether or not to consider aggregators a threat is different for every business.


## Where to go from here?


What do you do if you find a login success ratio that is concerning? Like with any threat, you need visibility into the attack before you can think about mitigation. Start with free options before committing to a vendor. Tying yourself up with a vendor too early can spin you in the wrong direction and end up wasting months of time. I’ve written an article on 10 things you can do to stop credential stuffing attacks which goes over some free detection methods as well as some mitigation strategies. This should be enough to get you started understanding your problem and, once you understand the scope of your issue, then you can have better conversations with security vendors. Of course we at Shape Security are available to answer questions any time of day and you can feel free to reach out to me personally on twitter.


This article originally posted on Shape Security’s engineering blog.


[Share this on Medium](https://medium.com/@jsoverson/what-your-login-success-rate-says-about-your-credential-stuffing-threat-1f10bc20eaee)
