+++
showonlyimage = false
draft = false
image = "img/portfolio/Jarrod_Data_Breach_Cred_stuff.jpg"
date = "2018-07-19T12:23:01-07:00"
title = "3 Misunderstandings about Credential Stuffing attacks"
categories = [ "Security" ]
+++

Another day, another report of a [data breach](http://www.documentcloud.org/documents/4585869-Macys-Breach-Letter.html). The description in Macy’s announcement, though, is noticeably different than most — there was no reference to internal systems being accessed beyond the web application and no data extracted en masse.

<!--more-->

Instead, the accounts were individually accessed with legitimate usernames and passwords and exploited via the same user experience you or I might go through when logging in. This is certainly a “data breach” in the literal sense but, unlike most, this breach is not directly related to something that the victim company did or didn’t do — the vulnerability stems from the fact that a substantial number of users (by some estimates, the vast majority) reuse passwords across multiple sites and that other companies have had more traditional data breaches which have leaked usernames and passwords that are also used at sites like Macy’s. This is the classic aftermath of a credential stuffing attack.

## 1) Every company is vulnerable even if they are 100% secured.

No quick fix will protect any company forever. It’s an arms race that requires daily attention and iteration to keep up with and surpass attackers. I’ve spent the last four years building Shape’s protection systems and can attest that it requires a tremendous amount of ongoing research and development alongside fully staffed SOC and Tactical Security teams in order to stay ahead of the attacks. Anyone who promises easy answers is lying.

## 2) The cause is the same across all companies, even if the symptoms are different.

Credential stuffing is defined as large-scale automation of login flows fed by previously discovered username and password pairs. This differs from what is generally considered a “data breach” in that the attack travels through flows that are publicly available rather than the attacker gaining access to internal systems via a software exploit or social engineering attempt like phishing. Credential stuffing, unlike credential cracking, makes no attempts to guess or brute force passwords for any individual user — it merely runs through massive lists of credential pairs and saves what it finds has logged in successfully. Once that list of successful logins per website is generated, then targeted attacks occur per business. There are many ways an account can be exploited, many of which are not intuitive at all and this is where yet another major part of the problem lies. Many businesses consider their particular flavor of exploitation entirely unique to them and it doesn’t even occur to them to seek out protection from outside vendors — it’s just another type of loss that is chalked up under the fraud umbrella. We’ve seen everything from fraudsters making personalized phone calls to your hotel room right after checkin to large scale money laundering by way of cheese. It’s entirely reasonable to assume these are unique problems without generalizable solutions.

## 3) You don’t need to be targeted outright to be vulnerable.

> “I don’t worry too much about my data being stolen. I’m not interesting enough to target.”

I’ve heard this take many times and this is the biggest boon that ensures credential stuffing will be an attack vector for years to come. These attacks target no one in particular, they target anyone and everyone. This wide-net approach means that everyone is vulnerable and will become increasingly more vulnerable with every new breach that is reported. How many times do you think the average user changes their passwords? Every breach is 5–10 future years of pain for the average person and business.

## How can you protect yourself?

First and foremost, change each password on the following classes of sites to something unique and never before used. Enable multi-factor authentication where possible.

- Banks (including aggregators)
- Email
- Social networks
- Internet/Cellular providers

> “But I can’t remember a different password for every site.”

Password managers exist for this reason but, I know, they can be cumbersome and difficult to manage across many devices. I use 1Password and find it manageable.

If you simply can’t be convinced that it is worth it to use a password manager then you can use this following trick to give yourself some chance at managing this via memory.

1. Think of three short, 4–6 letter words, e.g. “pencil,” “card,” and “paper”.
2. Pick an order that you find easy to type and remember and then pick a “blank” spot in the order, e.g. “pencil ______ paper card”
3. Every time you need a password, substitute the name of the site in the blank, e.g. “pencil facebook paper card”

> “But anyone who knows my pattern knows my password everywhere!”

That may be true, but you are much less likely to be personally targeted than you are to be one more faceless line item in a long list of usernames and passwords being used in a credential stuffing attack.

Stay safe!
 
[Share this on Medium](https://medium.com/@jsoverson/3-misunderstandings-about-credential-stuffing-attacks-3526c618a8d6)
