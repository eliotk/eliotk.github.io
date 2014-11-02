---
title: MyTracks KML files to one CSV with summary data
author: eliot
layout: post
permalink: /12/02/mytracks-kml-files-to-csv-summary-data/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Blog
---
The goal:

Visualize multiple tracks together (e.g. total distance, average moving speed) in a time series display. I want to be able to see if I&#8217;m improving (or not!)

There isn&#8217;t a way to do this in the app. And all of the export options export each track individually into a KML, GPX or CSV file.

So I created a Ruby script &#8211; embedded below &#8211; that iterates through all of the synced KML files (using the option to sync to Google Drive from within the app), extracts and parses the summary data, then stores each track&#8217;s info as a row in a CSV file which is output as mytracks.csv.

You can then import the CSV into Google Spreadsheets/Excel and create a chart. Or use a graphing library in your preferred language.

{% gist eliotk/7744806 %}

Here are some of my tracks visualized with a Google Spreadsheets time series chart:

[<img class="alignnone size-medium wp-image-463" title="Screenshot 2013-12-02 21.34.52" src="http://www.eliotk.net/wp-content/uploads/2013/12/Screenshot-2013-12-02-21.34.52.png" alt="" />][1]

 [1]: http://www.eliotk.net/wp-content/uploads/2013/12/Screenshot-2013-12-02-21.34.52.png
