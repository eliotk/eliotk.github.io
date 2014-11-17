---
title: 'Monit logrotate configuration to avoid redundant alerts'
author: eliot
layout: post
permalink: /monit-logrotation
---

Here's the [default monit logrotation configuration](http://mmonit.com/wiki/Monit/ConfigurationExamples#logrotate):

    /var/log/monit {
        missingok
        notifempty
        size 100k
        create 0644 root root
        postrotate
            /bin/kill -HUP `cat /var/run/monit.pid 2>/dev/null` 2> /dev/null || true
        endscript
    }

The goal of the postrotate command is to trigger the Monit service to close and reopen the reference to its log file so that it will start writing to the main `/var/log/monit` file. Otherwise it will continue to write log messages to the rotated log file (e.g. `/var/log/monit.1`)

The problem is that the SIGHUP signal will force Monit to reinitialize itself and, in addition to reopening the log file, the state will be reset. So any alerts that have been triggered will be re-sent each time logrotate runs, usually on a daily basis.

Here's a better logrotate conf to avoid the state problem:

    /var/log/monit {
        copytruncate
        missingok
        notifempty
        size 100k
        create 0644 root root
    }

The copytruncate declaration prompts logrotate to copy the log file to a new "rotated" file and then truncates the original file. In turn, no postrotate command is necessary and there is no concern over repeated alerts.