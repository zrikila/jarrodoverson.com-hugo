+++
showonlyimage = false
draft = false
image = "https://cdn-images-1.medium.com/max/1351/1*Hq0v_xmSWwc43KrOLLvWlA.jpeg"
date = "2019-07-22T15:24:27.471Z"
title = "How Two Malicious NPM Packages Targeted & Sabotaged One Other."
categories = [ ]
+++




<span class=subtitle>An attacker allegedly gained access to an npm user account and published modules that broke dependents. But why?</span>


<!--more-->

On July 12th Harry Garrood posted a personal blog entry outlining deliberate sabotage aimed at the PureScript installer. Two separate dependencies, both owned by a user who goes by @shinnn, targeted the npm package purescript-installer with malicious code using techniques that I've seen in exploits by other attackers. Shinnn claims his account was compromised and that these packages were published without his knowledge.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/840/1*hJkhP-v3yNxbzvbQCOpjqw.png">

These attacks differ from most in that there is no obvious value in sabotaging an obscure compile-to-JavaScript language. There’s no bitcoin theft, no crypto mining, no data exfiltration nor any backdoors. This is a pure attack on another project for no value and without value there is no obvious motive. @shinnn has maintainer rights to over 400 popular npm packages. If an attacker gained access to @shinnn’s account there are much better targets than PureScript.


What actually happened?


## Background


If you haven’t discovered it yet, PureScript is a functional programming language like Haskell that compiles down to JavaScript, similar to how people use CoffeeScript or TypeScript. It is not a widely used language and it being targeted raises eyebrows on its own.


@shinnn is a developer who has contributed to hundreds of packages and is part of many notable GitHub organizations like babel, node.js, and postcss. Most of these have been set to private since June.


In early June there was a falling out between the PureScript core team and @shinnn due to differing styles of communication and collaboration.


## Timeline


Some timeline details from Harry’s account reproduced here for continuity.


5 June — @hdgarrood emails @shinnn thanking him for the work on the install-purescript-cli package but cites conflict and @shinnn's sole ownership as being a concern for the future. In the email @hdgarrood requests that @shinnn transfer the project to the PureScript core team. After a tense back-and-forth on a since-deleted GitHub issue, the PureScript core team adopts the source code in a new project and @shinnn deletes or makes private the original repository.


8 June — The PureScript team publishes purescript-installer, a rebranded version of shinn’sinstall-purescript-cli. The difference in names will become important later.


5 July, around 1300 UTC — @hdgarrood publishes version 0.13.2 of purescript which depends on purescript-installer.


8 hours later an attacker published load-from-cwd-or-npm version 3.0.2 with code that causes purescript-installer to hang by returning an object that performs no action but is designed not to throw an error. Npm has since removed version 3.0.2.


6 July — @develop7 opens a GitHub issue on purescript-installer outlining the problem.


9 July, around 0100 UTC — @doolse identifies load-from-cwd-or-npm@3.0.2 as the cause.


@doolse opens an issue on load-from-cwd-or-npm describing the problem, assumed it is a legitimate bug. @shinnn deletes the issue. He explains this here saying it was a knee-jerk reaction stemming from being upset about the original discussion on the project transfer.


9 July, around 0500 UTC — @shinnn publishes load-from-cwd-or-npm version 3.0.4which does not contain any malicious code.


9 July, around 0800 UTC — An attacker publishes rate-mapversion 1.0.3 which contains the same targeting logic but a different payload. This payload modifies a separate dependency, dl-tar, to produce unintended behavior and then rewrites itself locally to remove traces of the malicious code. NPM has since deleted this package.


9 July, around 1100 UTC — @hdgarrood, assuming the issue is due to a legitimate bug, publishes a new version of the PureScript installer that bypasses load-from-cwd-or-npm. This does not fix new issues due to the now compromised rate-map.


9 July, around 1130 UTC — @hdgarrood discovers the malicious code in rate-mapand reports it to npm's support email. @hdgarrood then publishes a new version of the PureScript installer with all of @shinnn’s dependencies removed.


15 July — When asked for comments, Npm responded that they consider the issue resolved with the removal of those packages despite issuing no security advisories at the time of request. Npm states that @shinnn’s account had been compromised and subsequently restored but declined to comment with any details about what, if anything, was actually restored.


17 July — Npm posts two security advisories, security advisory 1082 & security advisory 1083.


## Attack details


Visit Harry Garrood’s post for a line by line walkthrough on the malicious code. Here I’ll go over significant points.


## load-from-cwd-or-npm


Diff of versions 3.0.1 and 3.0.2


The purescript-installer package depended on load-from-cwd-or-npm by way of dl-tar.

```
purescript-installer
└─┬ dl-tar
  └─┬ load-request-from-cwd-or-npm
    └── load-from-cwd-or-npm  <<<<<<< compromised package
```

load-request-from-cwd-or-npm uses load-from-cwd-or-npm to load the request module either locally or from the npm registry. dl-tar uses request in a streaming API so any substituted stream would adhere to the same API. These relationships will be important.


The targeting code recursively looks at the parent module's name or directory structure to determine if it should activate its payload. If load-from-cwd-or-npm encounters a parent whose package name ends in "cli" or if the parent includes a directory named .git then the library will work as normal. This allows @shinnn's own install-purescript-cli to continue working and also prevents this from being reproducible in a common development environment. If a package other than @shinnn's own installer is using load-from-cwd-or-npm then load-from-cwd-or-npm will return a PassThrough stream instead. Stream.PassThrough is an implementation of a node.js stream that does nothing but pass bytes through unchanged.


The end result is that the PureScript core team’s installer downloads nothing because what should have been a request object ends up being a stream that does nothing. No errors are surfaced and the process does not continue.


## rate-map


Diff of versions 1.0.2 and 1.0.3


rate-map@1.0.3 contains the exact same mechanism of payload activation. The payload searches for a local dependency, dl-tar again, by way of the obfuscated code on line 26 and then rewrites dl-tar's source to remove callbacks with a specific signature. This causes similar behavior in the previous attack and results in a broken installer.


This version also goes out of its way to delete itself locally after it has run which makes the malicious intent far more clear.


## So what happened?


There is no direct evidence that @shinnn did this himself. Motive exists, @shinnn felt slighted by the PureScript team trying to take over his tool which resulted in hard truths surfacing about their relationships. The malicious payloads were both designed to protect @shinnn’s packages while sabotaging the PureScript team’s installer. @shinnn also requested the PureScript team enable 2FA as a condition of transfer yet claims he did not have 2FA enabled himself which is a critical part of the account compromise story.


This malicious code was also designed to do minimal damage and extract nothing of value. This is not representative of the vast majority of attacks. There is zero point to these attacks unless you have a personal problem with PureScript.


So @shinnn may not have done this, but someone with similar motivations as @shinnn and access to @shinnn’s npm account did.


## Why it matters.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/268/1*Jfb4Z_g8P9qp8sVimNF6ug.png">

@shinnn is a prolific developer maintaining hundreds of packages. He is a member of respected organizations (nodejs, babel, postcss and others), and submits code to high-profile projects. At best this is a user who has poor account security practices, at worst this is a user who crafted malicious code to explicitly sabotage a project out of spite. Either way trust was abused.


@shinnn’s repositories are his and any use of them is subject to his whim. The packages are open source under a very permissive license and when someone puts packages out in the wild it means they might be used by people they don’t like. There are much better ways at handling conflict than resorting to attacker tactics to sabotage others.


Npm inc’s response is disappointing. They did not issue security advisories until I asked them if there would be a post on this. They did not offer any transparency around the resolution and were not interested in exposing information that would help the community get a better understanding of what happened. I understand that Npm can’t spend time investigating every malicious package but there are basic capabilities that would enable the public to perform a better job on their own. As of this post the npm website doesn’t even list that a malicious version ever existed when you view the version details of a package. This is true for most packages that have been seen such problems.

<img style='max-width:100%;' src="https://cdn-images-1.medium.com/max/1132/1*VPN9ANqp6e1IZoxhq06uvg.png">

The npm registry should start exposing public metadata on whether a package was published through an MFA flow and this should be reported by npm audit. Depending on packages that have maintainers without MFA set up is liability. MFA is not a silver bullet but it would be a data point towards accountability. It would enable systems to ensure they are built only from packages that have been published with such safeguards in place.


Security surrounding node.js and the million plus npm packages in the registry is improving but trust is waning and much more still needs to be done.


[Share this on Medium](https://medium.com/@jsoverson/how-two-malicious-npm-packages-targeted-sabotaged-one-other-fed7199099c8)
