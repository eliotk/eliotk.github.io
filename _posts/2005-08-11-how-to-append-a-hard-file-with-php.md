---
title: How to append a hard file with PHP
author: eliot
layout: post
permalink: /08/11/how-to-append-a-hard-file-with-php/
aktt_notify_twitter:
  - yes
categories:
  - Blog
  - Code
  - Tech
---
At work I needed the following feature for a site:

A user can submit his/her email address via a form and, upon doing so, the email would be stored in a file with the email addresses of all of the other users that submitted their emails. The company wanted it&#8217;s visitors to be able to recieve a notification when the new site was launched.

I started by making the form, which ended up looking like this. I decided to echo the form info through PHP, so once the user submitted his/her email address, they would recieve a confirmation message. You&#8217;ll see what I mean as we go along.

So here&#8217;s the form, echoed:

`$out= "Our new and more comprehensive site will be launched shortly.`

Please submit your email address if you would like to be notified when it is launched.

&#8220;;

Notice I posted to self (sometimes I&#8217;m lazy and just drop in the page instead of the PHP server request self page call) and the name of the form and submit is &#8220;addemail&#8221;.

Next I setup an if command in the page to look for the form submission:

`//check to see if email address was submitted`

if ($_POST["addemail"]) {

If the email address was submitted, we want to grab with the REQUEST call. We also want to append it with a line breaks to put it on the next line, hence the &#8220;\r\n&#8221;:

`//get the emailaddress`

$emailaddress = $_REQUEST["emailaddress"] . &#8220;\r\n&#8221;;

//open file (in this case called &#8220;emails.txt&#8221;) to write email to it.

$myFile = &#8220;emails.txt&#8221;;

//first read the content so we can append  
$fR = fopen($myFile, &#8216;r&#8217;) or die(&#8220;can&#8217;t open file&#8221;);  
$fcontent = fread($fR, filesize(&#8220;emails.txt&#8221;));

//output new content with appended email address  
$newcontent = $fcontent . $emailaddress;

$fh = fopen($myFile, &#8216;w&#8217;) or die(&#8220;can&#8217;t open file&#8221;);

fwrite($fh, &#8220;$newcontent&#8221;);  
fclose($fh);

//send message to let them know their email address has been added

$out = &#8220;Thank you for your interest. You will be contacted in the coming weeks when the new site launches.&#8221;;

} else {

//if there was nothing posted, we prepare default display for output.

$out= &#8220;Our new and more comprehensive site will be launched shortly.  
Please submit your email address if you would like to be notified when it is launched.

&#8220;;

}

Then all we have to do is place the content somewhere within the page with this code:

`<br />
`

<div id="underconstruction">
  < ?php echo &#8220;$out&#8221;; ?>
</div>

Done!