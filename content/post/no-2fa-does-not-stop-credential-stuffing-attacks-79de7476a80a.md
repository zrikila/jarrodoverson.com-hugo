+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/1260/1*DVARhgpvufS13BayFlMs1g.png"
date = "2019-05-21T21:26:09.913Z"
title = "No, 2FA Does Not Stop Credential Stuffing Attacks"
categories = [ ]
+++




<span class=subtitle>Credential Stuffing Myth debunked.</span>


<!--more-->

There’s a great post on the Google Security blog entitled “How effective is basic account hygiene at preventing hijacking.” The post provides insight into two-factor authentication and its effectiveness at Google scale. Unfortunately, it also has some phrasing that is causing people to believe that basic one-time passwords as a second factor stops 100% of all credential stuffing attacks. This is causing thought leaders to post exactly that:

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/607/1*KkPrkjGLEf8Htf-3xKk2Rg.png">
<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/607/1*7DiA50Nb-Af94mxp3VooSg.png">

To be 100% clear and unambiguous: Two Factor Authentication does not stop credential stuffing attacks. At all.


The Google Security blog does not contradict this but the confusion comes from this sentence:


> We found that an SMS code sent to a recovery phone number helped block 100% of automated bots, 96% of bulk phishing attacks, and 76% of targeted attacks.

This sentence is not wrong, but it is easy to misinterpret. Automated bots on login are heavily associated with credential stuffing but that is not what is being described here. The chart that follows the quote describes the results more precisely:

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/702/1*4j7AT40XVggFUQBi5oLjoA.png">

Two-factor authentication protects automated account takeovers by bots. Credential stuffing is not an account takeover and lumping them together misrepresents the point of credential stuffing attacks. The point of a credential stuffing attack is to boil a list of mostly-junk credentials into a list of valid accounts for a service. If a service presents its 2FA gate to the user after they have entered in a good username and password then a credential stuffing attack still results in a list of valid accounts. What it doesn’t lead to is an immediate account takeover. This is an important nuance and, without acknowledging it, the phrasing leaves people thinking that 2FA is a silver bullet and that a silver bullet exists at all.


2FA is an important, valuable defense that does add value but there are no silver bullets against account takeover attacks. Accounts for big-name services have so much value locked away that attackers will iterate until they find something that works.


## Cost vs Value

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/1260/1*DVARhgpvufS13BayFlMs1g.png">

Every decision by an attacker is a cost vs. value justification. If the value is high enough then the attack sophistication (cost) can rise in turn. 2FA is a defense that adds a lot of cost to the attack but this is not an insurmountable hurdle for motivated attackers. Credential stuffing attacks discover if value exists. They have zero value by default and need to be cheap to perform because of it. Once an attacker completes a credential stuffing attack and has a list of valid accounts the input to the cost/value equation changes. The potential return becomes a lot more concrete. Phishing, social engineering, or other, more costly tactics are now be on the table. Untargeted phishing has low returns, it needs to be cheap to perform just like credential stuffing. Targeted phishing (spear phishing) is more effective and the effectiveness increases the more you know about the target. I would bet a lot of money that someone who knew enough about security to have 2FA enabled but not enough to know you shouldn’t reuse passwords is exactly the type of person that a targeted phishing campaign will be effective against.


TL;DR: 2FA doesn’t stop credential stuffing, it adds a hurdle to account takeovers. Credential stuffing is worth stopping on its own because getting a list of valid accounts is still a threat to your site or business.


[Share this on Medium](https://medium.com/@jsoverson/no-2fa-does-not-stop-credential-stuffing-attacks-79de7476a80a)
