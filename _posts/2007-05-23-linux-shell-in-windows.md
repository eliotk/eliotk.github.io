---
title: Linux Shell in Windows
author: eliot
layout: post
permalink: /05/23/linux-shell-in-windows/
categories:
  - Open Source
  - Utilities
---
<center>
  <img src='http://www.eliotk.net/wp-content/uploads/2007/05/cygwin.png' alt='Linux-Shell-Windows' />
</center>

[Cygwin][1] is a clever environment for Windows that emulates features of Unix.

My computer is setup to dual-boot, which let&#8217;s me load either Windows XP or Ubuntu Linux upon startup. Today though, while I was in Windows, I was itching to run some commands on the hard drive and first started with DOS commands. But it&#8217;s just not the same as running BASH commands (and also I have a lot less experience with Windows commands).

Enter Cygwin. With it I was up and running with a Linux shell in no time. It works by using POSIX (Portable Operating System Interface) calls. POSIX is a collection of standards, which were setup in order to allow for software compatibility between Unix variants. Max OS X and Windows OS&#8217;s fully comply with POSIX. 

I just have the Cygwin shell running now, but the neat thing is that you can extend Cygwin to run most Linux open source software, including gnome, x windows, and even a Linux version of apache. I&#8217;m not sure why someone would want to setup a Linux server environment within Windows, but it&#8217;s a neat concept nonetheless.

 [1]: http://www.cygwin.com/