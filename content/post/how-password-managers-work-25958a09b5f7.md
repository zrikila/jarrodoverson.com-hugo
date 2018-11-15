+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/970/1*-Zat3NWY7MIaStAkvmyzzA.png"
date = "2018-09-04T19:25:51.043Z"
title = "How password managers work"
categories = [ ]
+++




<span class=subtitle>All passwords are not created equal</span>


<!--more-->

Since I’ve started speaking about password security and the risks it entails a I’ve gotten a wide range of questions from every angle depending on the audience. One recent question reminded me of an angle I had largely forgotten about.


> “Isn’t storing all your passwords in one place more dangerous?”

The short answer is no, read on for the long answer.


### What is a password?


A password is just a secret phrase that unlocks something. Passwords can be used for anything but there are two major classes of password that we encounter daily.


### Passwords for authentication


Passwords are most frequently used, alongside a username or email, as credentials for a website to determine whether or not you are who you claim to be. This enables the service to decide whether or not to unlock certain actions for you. For example, logging in with your email address and password to a retailer like Amazon lets Amazon trust that you are who you say you are and that you should be allowed to purchase items with any stored credit cards on the account. You can still purchase or buy without access to your account, but you won’t be able to rely on Amazon’s stored information for that account (like addresses or credit cards) or any linked subscriptions (like Amazon Prime).


These kinds of passwords are tied to you and a company like Amazon can reset your password by sending you an email because the password is just something secret that only you should know, just like your email account should be. It doesn’t matter what it is, as long as you’re the only one who knows it.


Passwords for authentication can be seen like the key to your house. It unlocks the front door and if you lose a key you can call a locksmith to have the door unlocked or the doorknob replaced. If someone breaks through a window then they have access to all your possessions regardless of whether or not they had access to a key.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/970/1*-Zat3NWY7MIaStAkvmyzzA.png">

### Passwords for encryption


Another type of password is used for encryption, or locking up data. You may have encountered passwords on things like PDFs, ZIP files, spreadsheets, or similar. These often don’t have a username associated with them and if you don’t have the password then you’re out of luck, there’s no “reset” service for them. Passwords like these are used to encrypt the data so that it is meaningless unless provided with the password that is used to decrypt it.


These kinds of passwords are tied to the data and, once lost, are unrecoverable. No one can reset your password because it was used only to encrypt the data and then it was thrown away. It’s not stored anywhere and it can’t be recovered.


Passwords for encryption can be seen like decoder rings or secret glasses that you might have used when you were a kid. Without them, what you’re looking at is (largely) meaningless but, with them, you can read the message your best friend sent to you. Obviously this is much more complex in computer cryptography but the fundamental idea is the same, hiding a message (data) that can only be unlocked with an agreed upon key (password).

<iframe height='265' scrolling='no' title='Drag to Make the Red Squiggles Disappear' src='//codepen.io/danwilson/embed/ZrGBVx/?height=265&theme-id=0&default-tab=result' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/danwilson/pen/ZrGBVx/'>Drag to Make the Red Squiggles Disappear</a> by Dan Wilson (<a href='https://codepen.io/danwilson'>@danwilson</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

Reputable password managers largely rely on the second type of password in order to protect your data. You may also have a username and password to log in to a service they provide, especially if its a paid service, but your stored password data is protected via encryption and what unlocks that is usually called something different, e.g. a “master password”. It’s confusing and muddies up what’s going on, but the important point to understand is that you have many more layers of protection in place when using a password manager.


### Password managers should be trusted!


Using a password manager to store your passwords enables you to use stronger, randomized passwords more often and makes it easier to have a unique password for every website. These two aspects alone protect you online more than anything else right now.


If you have any questions, please feel free to message me on twitter at @jsoverson!


[Share this on Medium](https://medium.com/@jsoverson/how-password-managers-work-25958a09b5f7)
