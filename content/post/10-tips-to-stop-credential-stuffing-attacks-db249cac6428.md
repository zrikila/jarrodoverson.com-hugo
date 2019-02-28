+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/1920/1*_JPAU2SUC74mm40fC_hkMA.jpeg"
date = "2019-02-12T21:11:33.488Z"
title = "10 Tips To Stop Credential Stuffing Attacks"
categories = [ ]
+++




<span class=subtitle>10 steps you should take before buying an anti-automation service (+ 1 bonus tip).</span>


<!--more-->

Imitation attacks like credential stuffing and carding are viable if the cost of the attack is lower than the value of the expected outcome. This sounds simple but it means that you’ll need to play a game with attackers with the end goal being that you burn them out before you burn yourself out. Attackers will retool against any countermeasure you put in place as long as the cost/value ratio remains in their favor. Your job is to strategically place countermeasures that increase friction over and over again until your attacker understands that these attacks are costing more than they’re worth.


Before you determine if you need to call in professionals, you can go through these ten steps to temporarily increase the cost of an attack with a series of increasingly difficult, low-cost countermeasures. No silver bullet exists so be wary of any company who tries to sell you one.


### 1. Use a CAPTCHA

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/616/1*GmtGvbap0r7toziy-rV9rw.gif">

Yes, I rail against CAPTCHAs and yes, you can bypass them trivially (see Bypassing CAPTCHAs with Headless Chrome) but CAPTCHAs are a hurdle that does increase cost even if only a little. If you haven’t tried a CAPTCHA yet then you don’t know how successful one will be on your site.


You can find dozens of CAPTCHAs and CAPTCHA-likes but I’d start with Google’s reCAPTCHA v2. ReCAPTCHA is easy to integrate, is battle tested, and will give you the data points that will help you identify if you need to go deeper.


### 2. Rate limit non-residential ASNs


You shouldn’t be seeing major portions of traffic from AWS, Digital Ocean, or obscure Russian cloud hosting providers. You designed your site for humans, not machines, so block traffic originating from service providers that don’t cater overwhelmingly to humans.


### 3. Rate limit header fingerprints of attack tools

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/607/1*N_ge9ih1U7i4Ro997Vtk_Q.png">

Almost all web servers, frameworks and log aggregators go out of their way to normalize HTTP traffic data for easy processing but, with that step, a lot of unique data gets thrown in the trash. Are the headers upper case? Mixed case? Lower case? Is one header always second? Does the presence of one header mean that another should exist directly before it? You can find these patterns via your own analysis but using this data to form fingerprints of attack tools will give you another data point to block on. See also Detecting PhantomJS Based Visitors on the Shape Security Blog


### 4. Block or track headless browsers

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/undefined/1*VrrSt0Kx9109UmWXwgQKRw.png">

Automated browsers like PhantomJS or headless Chrome are often used by attackers because they soar over low hurdles like running JavaScript by default. You can track them by looking for telltale properties they leave behind in the JavaScript environment such as window.callPhantom and navigator.webdriver. What you do with that information is up to you. If you block the traffic outright then attackers will retool around the countermeasure instantly. If you silently augment the actions a headless browser takes then you reduce your feedback to the attacker and your countermeasure will last a lot longer.


### 5. Require JavaScript on your site


This is basic and a low hurdle but requiring attackers to run JavaScript or use a real browser requires more CPU power and more full featured services which increases cost.


The ambiguity with this suggestion is intentional; the countermeasures that work best are the ones that are custom to your site. There is more incentive to bypass generic and shared countermeasures like reCAPTCHA or Akamai’s Bot Manager because there is more value in it. If you are an attacker and you have the resources to focus on defeating one countermeasure, it makes more sense to defeat one that is shared across many websites than the one that is unique to a single website.


### 6. Fingerprint your clients


One way to require JavaScript is to block requests to protected URLs that don’t include collected client side data. You can use a fingerprinting library like Fingerprint2 to get started collecting client-side telemetry. With this data you can see patterns in traffic that you may overlook otherwise due to it being globally distributed. Looking at IP addresses alone is not enough, you need to map client similarities across large slices of traffic to find attackers who are distributing the traffic of a small set of clients across hundreds of thousands of IP addresses.


Fingerprinting is the technique of finding a combination of data that, when taken as a whole, is unlikely to be coincidentally duplicated anywhere in the world. Outdated techniques of fingerprinting use data like your system fonts, browser plugins, or hardware information with the thought being that any one computer’s combinations of installed fonts, plugins, and hardware will be almost completely unique. The idea remains true, but attackers are wise to these techniques and build tools like AntiDetect that automatically randomize this data.


Common fingerprinting libraries like Fingerprint2 are often blocked by ad-blockers and sophisticated attackers are already randomizing that data too. You can consider Fingerprint2 a good starting point into the arena of fingerprinting with the expectation that your teams will need to iterate on a more custom solution.


### 7. Offer Multi-Factor Authentication

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/1499/0*t3pAW7u7AYTjD8FN">

Multi-factor authentication is an important security countermeasure that you should offer everywhere feasible. That said, MFA is often touted as the 100% solution to account takeover and credential stuffing but even MFA isn’t the silver bullet. MFA won’t stop credential stuffing attacks, there is still value in checking to see if accounts are valid, but it is an effective cost increasing hurdle that goes far to protect your users.


MFA isn’t a complete solution because an attacker can still amass valid accounts with a credential stuffing attack and then get MFA tokens via methods like phishing, vishing, or other social engineering techniques. It’s more difficult but, like everything, it’s a cost vs value justification.


### 8. Track your login success ratio


Now that you have more data points to look into because you are tracking client and header data, you need to configure alerts on the login success ratio for the fingerprints you are tracking. You will never have legitimate traffic with a login success ratio of 0.1–10%, but credential stuffers will. Attackers running credential stuffing campaigns will be using massive credential lists (combo lists) and their hit rate is going to be close to 0%. Login success ratios that low are a massive warning sign that something is amiss.


### 9. Check your users’ passwords against Pwned Passwords


Pwned Passwords is Troy Hunt’s service leveraging data from Have I Been Pwned. This won’t relieve the traffic burden of credential stuffing attacks against your service but it will help against account takeovers. Note, though, Pwned Passwords and any other dark web password service can only take into account publicly exposed dark web credentials, it can’t protect against fresh credential spills that haven’t found their way onto the dark web yet. Recent credential spills have the freshest data, the most value, and sophisticated attackers who breach them hold onto the spills until they’ve extracted all the value they can. Only then is the data passed around on the dark web.


### 10. Consult with experts


This is not an easy problem, there are a couple dozen companies offering solutions and many more in the past who have failed. The problem looks simple and attractive enough to take on with a part-time team but it ends up consuming more resources than expected with every single company I have spoken to. If you’ve gotten this far and are still stuck then reach out to the experts. If you like what I have to say then you can contact me via my contact page on jarrodoverson.com or on twitter at @jsoverson. I work for Shape Security and we’ve been at this game for the better part of a decade.


## Bonus tip: Don’t fall for the charts.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/952/1*0PXEo7TS_F9kb9FRoRkhEQ.png">

Be wary of any company selling you on fancy and dramatic charts that show a steep decline in automated traffic and little more. Those charts are easy to produce and you can make them yourself in a week by implementing the steps above and rolling them out in one fell swoop. Drops like this are beautiful, certainly, but the first major effort against anti-automation is always phenomenally successful. You will see a massive drop in attack traffic every time you place a new hurdle down, the true measure of efficacy is how long that protection lasts and how the protection responds after an attacker retools. If you don’t see answers for that then you should be wary of being peddled snake oil. Of course, if you don’t see graphs like this in the first place then that’s a whole different efficacy problem 😄


Good luck! If you have any more questions, feel free to contact me on twitter at @jsoverson or via my contact page on jarrodoverson.com.


[Share this on Medium](https://medium.com/@jsoverson/10-tips-to-stop-credential-stuffing-attacks-db249cac6428)
