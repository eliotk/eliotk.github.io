---
title: Exim Mail Queue Alert Script in Python
author: eliot
layout: post
permalink: /04/22/exim-mail-queue-alert-script-in-python/
aktt_notify_twitter:
  - no
js:
  - '<script src="https://gist.github.com/eliotk/5339281.js"></script>'
  - '<script src="https://gist.github.com/eliotk/5339281.js"></script>'
  - '<script src="https://gist.github.com/eliotk/5339281.js"></script>'
  - '<script src="https://gist.github.com/eliotk/5339281.js"></script>'
  - '<script src="https://gist.github.com/eliotk/5339281.js"></script>'
categories:
  - Blog
  - Code
tags:
  - alert
  - exim
  - script
  - sysadmin
---
If you run a mail server using Exim then you&#8217;ll want to know when there is an above average amount of emails in the mail queue. This could be caused by a legitimate user using the server improperly (e.g. sending a newsletter or other mass email without any throttling or with a poor recipient list) or, more seriously, a jeopardized (i.e. hacked) account being used for sending spam.

I&#8217;ve created a simple script that retrieves the current number of emails in the mail queue and, if that number is greater than a certain threshold, emails an alert to the admin.

Here is the script:



Set the To and From email addresses and you also may need to change the path to Exim.

Instead of `['/usr/sbin/exim','-bpc']`, you may be able to use `['exim','-bpc']`. If neither of those work, locate where the exim executable is on your server and use the appropriate path.

Change the threshold number to be higher than the normal amount of queued messages that will be in the system at any given time so you don&#8217;t receive alerts that are false positives.

Once you have the script in on your server, make sure it&#8217;s executable:

`chmod +x /path/to/exim_alerts.py`

Then add a cron entry. I set mine to run the script every five minutes:

`*/5 * * * * python /root/exim_alerts.py`