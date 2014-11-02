---
title: MySQL wait_timeout default is set too high!
author: eliot
layout: post
permalink: /12/21/mysql-wait_timeout-default-is-set-too-high/
aktt_notify_twitter:
  - yes
categories:
  - Blog
  - OK|Public
  - Tech
---
Recently an [OKPublic][1] server was experiencing fairly sporadic bouts of extreme CPU loads (upwards of 80!) every 6 to 12 hours or so. It was severely limiting the web server. As I was monitoring the running processes, I witnessed several of these bouts and noticed that MySQL processes were spawned repeatedly and in great number; about 3-5 new processes per second.

So I initially thought that these processes were the result of a popular account on the server, but digging through Apache domain logs, there didn&#8217;t seem to be any that corresponded with the timing of these events.

Also, looking at the time that processes had been alived, I noticed that the new processes weren&#8217;t new at all as some were 30 minutes to 3 hours old, so they were actually just coming out of sleeping.

Reading guides about MySQL optimization on the web, the wait\_timeout variable stood out to me as it represents the amount of time that MySQL will wait before killing an idle connection. What really shocked me was that the default wait\_timeout variable is <span>28800 seconds, of 8 hours. Why would anyone want to keep idle MySQL connections alive for 8 hours?</span>

So I changed the setting to 300 seconds (which is still probably more than necessary) and we haven&#8217;t experienced the problem since.

The only reason a wait_timeout as high as the default (<span>28800) </span>may make sense would be if there are lot of reoccurring visitors (or connections to the database through other means) and that the applications handling the connections are optimized for persistent connections, which most aren&#8217;t.

So the wait_timeout being set so high doesn&#8217;t act as a cache, but more of a pool of dead connections. And when MySQL goes into kill mode to wipe the idle connections clean (I&#8217;m not sure about the technicalities of this), it seems that the pool can become so large that it takes a lot of CPU usage and RAM to do it all at the same time.

It seems that a better way to save resources through MySQL configuration is to setup a thread\_cache and/or query\_cache.

 [1]: http://www.okpublic.com "OK Public Web Hosting"