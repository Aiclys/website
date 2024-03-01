+++
title = 'A thing or two about software minimalism'
date = 2024-01-21T19:02:35+01:00
author = 'Nyrs'
tags = ["software", "web", "minimalism"]
+++

## Why I dislike bloated software
#### Something I strongly dislike is bloat. A piece of software can be described as being bloated if it is full of unnecessary or even unwanted features. A perfect example would be the modern internet. Everything is full of malicious javascript code that intends to steal your data, which is then sold to the highest bidder. The simplest, most basic sites like recipe sites are full of javascript, which greatly increases the attack surface and is completely redundant considering the use of the website. Why does every site need to connect to ten different Cloudflare or Google domains? This also leads to a poor experience on the users end, which is kind of hypocritical, because everything is much slower than it needs to be. Bloat is also very prevalent in other applications. Take PowerPoint for example: Does it need to have a million of other features that nobody uses and that only complicate the use of it? Same thing with Thunderbird. Why does it try to be everything in one app? It's never going to happen and it just slows it down, enlargens the attack surface and phones home to several other services, who in turn harvest your data.
&nbsp;
&nbsp;
## What is the cause of modern bloat?
#### This all gets even worse once you realize that there is a simple way to avoid all of this bloat. Developers just have to create something simple that fulfills its purpose efficiently instead of trying to make their app be good at everything. That's all it takes. The problem is that no company wants that. Every company is trying to trap you into their own ecosystem so that you need to rely on one company to provide for all of your consumer needs. No company actually wants you to truly enjoy their product, they want to make as much money as possible with the least amount of work possible. Basically every company wants to achieve the same thing Apple excells in: Creating a walled garden and basically turning your userbase into a cult.

#### This isn't the only cause of modern bloat though. One thing I realized when I tried to learn javascript about 2 years ago is that when doing web dev, you aren't actually coding in vanilla js, you are much rather using some popular framework like React.js, Node.js etc. This is great for the dev as he has a more pleasant development experience but it makes a pretty noticable sacrifice on the end of the user: performance. You don't have to be a genius or a javascript wizard to come to this conclusion. It should be common sense that a website will be considerably slower if it connects to 10 different domains at the same time while being written in a very resource heavy js framework.
&nbsp;
&nbsp;
## But what can I do about it?
#### On the surface it seems like you can't do anything to combat the bloat, but there are alot of things you can do. First of all, use a content blocker when browsing the web. Not an adblocker but a content blocker. They are two different things. Content blockers also block ads but they also block a lot more. For example they can block paywall pop-ups, newsletter pop-ups, certain images, scripts etc. This way you don't need to see all of the ads and you will also notice an increase in performance when browsing the web as your computer won't have to load in that many scripts, ads etc. The best content blocker is uMatrix but for not so advanced users and the ease of use I would recommend uBlock Origin as uMatrix requires alot of tweaking to set it up and get it to work properly.

#### Another thing you can do to reduce the bloat you come across is to use less bloated frontends. If you don't know what an alternative frontend is, it's basically a different looking version of a popular service/website. Take Youtube for example. There are alot of alternative frontends but the most famous and probably the best one is [Invidious](https://invidious.io/). It removes all of Youtubes
