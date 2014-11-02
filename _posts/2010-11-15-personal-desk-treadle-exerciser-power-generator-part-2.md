---
title: Personal Desk Treadle Exerciser and Power Generator – Part 2
author: eliot
layout: post
permalink: /11/15/personal-desk-treadle-exerciser-power-generator-part-2/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Blog
---
In [Part 1][1] I <del>rambled on</del> wrote about the lead-up to building the treadle-based exerciser and power generator. Now on to the actual mechanics!

I decided fairly early on that the double bass pedal I bought was going to be conducive for modifying and that it&#8217;d be best to build the device from scratch. Here is a shot of a recent iteration:

<div class="shashin_image" style="width: 410px;">
  <a href="http://lh4.ggpht.com/_LYO5Bj1T__g/TLz60qlBYmI/AAAAAAAABuM/rkFZ3OszX6Y/CIMG1779.JPG?imgmax=640" class="highslide" id="shashin_thumb_link_1" onclick="return hs.expand(this)"><img src="http://lh4.ggpht.com/_LYO5Bj1T__g/TLz60qlBYmI/AAAAAAAABuM/rkFZ3OszX6Y/CIMG1779.JPG?imgmax=400" alt="I realized after setting it up like this and then testing it that the force from the chain on the drill chuck caused the plastic drill body to bend so I had to modify the setup by laying th drill horizontally and attaching it to the base with large hose clamps" width="400" height="300" id="shashin_thumb_image_1" title="I realized after setting it up like this and then testing it that the force from the chain on the drill chuck caused the plastic drill body to bend so I had to modify the setup by laying th drill horizontally and attaching it to the base with large hose clamps" /></a> <div class="highslide-caption">
    I realized after setting it up like this and then testing it that the force from the chain on the drill chuck caused the plastic drill body to bend so I had to modify the setup by laying th drill horizontally and attaching it to the base with large hose clamps
  </div>
</div>

With the drill attached to the base standing up by its base, I discovered that the force of the chain on the drill chuck would bend the plastic drill body and thus create too much slack between the drill chuck and the wheel cog. So I&#8217;m now laying the drill on it&#8217;s side and clamping it to the base with hose clamps:

<div class="shashin_image" style="width: 410px;">
  <a href="http://lh3.ggpht.com/_LYO5Bj1T__g/TOG4Gvi78hI/AAAAAAAABtQ/fm79P6GZpg8/CIMG1786.JPG?imgmax=640" class="highslide" id="shashin_thumb_link_2" onclick="return hs.expand(this)"><img src="http://lh3.ggpht.com/_LYO5Bj1T__g/TOG4Gvi78hI/AAAAAAAABtQ/fm79P6GZpg8/CIMG1786.JPG?imgmax=400" alt="New setup with drill lying on it's side and securely attached to the base with hose clamps. No more flex!" width="400" height="300" id="shashin_thumb_image_2" title="New setup with drill lying on it's side and securely attached to the base with hose clamps. No more flex!" /></a> <div class="highslide-caption">
    New setup with drill lying on it&#8217;s side and securely attached to the base with hose clamps. No more flex!
  </div>
</div>

It&#8217;s now *very* sturdy.

### How it Works

1.  User starts spinning the flywheel (pink wheel) by hand to get the motion going
2.  Then the user starts pushing the wooden pedal down as it&#8217;s traveling up and down to maintain the speed of the spinning wheel. The linkage between the wheel and the wooden pedal converts the radial motion of the spinning wheel into the linear motion that causes the pedal to travel up and down.
3.  As the wheel spins, the sprocket on the wheel also spins and that rotates the sprocket at the head of the drill chuck via the connecting chain
4.  The regular 18v cordless drill that I&#8217;m using acts as a DC generator when it&#8217;s driven in reverse (a force driving the chuck as opposed to the drill motor driving the chuck) and electricity is produced which can be harvested at the motor connection terminals (the terminals which in normal use would be connected to the drill battery).
5.  The motor terminals are then connected to the DC input of a battery pack to store the juice. I&#8217;m using the [Electromate 400][2]:  
    <img class="alignnone size-thumbnail wp-image-194" title="electromate-400" src="http://www.eliotk.net/wp-content/uploads/2010/11/electromate-400-150x150.jpg" alt="" width="150" height="150" />  
    The neat thing about the Electromate 400 or something similar is that is a has A/C conversion and output built in. But if you were using straight batteries you could rig up (or buy) a rectifier to convert the DC energy to AC.
6.  I&#8217;ll also most likely need to add a blocking diode to the connection between the drill motor terminals and the battery pack in order to stop the juice from flowing back from the battery and into the drill putting a load on the drill motor.

### Parts Breakdown

Here is a list of the parts that I&#8217;ve used so far in the project:

*   Wood board for the base
*   Wood scrap for the pedal
*   Door frame hinge for the pedal to the base connection
*   Kid&#8217;s (Barbie?) 16&#8243; bicycle wheel that my Dad had picked up along the way
*   Bike chain
*   Additional used coaster hub sprocket to use on drill chuck
*   18v cordless drill (bought on Craigslist cheap because the battery wouldn&#8217;t hold a charge)

### Assembly

In general the assembly is pretty straightforward.

I took a brute force approach in converting the coaster brake hub of the bike wheel into a fixed gear in order to drive the sprocket from the spinning wheel and in turn drive the sprocket on the drill chuck. I used JB Weld to &#8220;fix&#8221; the sprocket fitting on the hub to the hub flange.

I also used JB Weld for attaching the spare coaster brake hub sprocket to the head of the drill chuck. I also considered JB Welding/arc welding the sprocket to a broken drill so that the bit could then be inserted and tightened into the chuck. This would allow the sprocket to be removed if need be. I ruled that approach out though because of the headaches of centering the sprocket with the bit base and also it not being as sturdy as the current setup.

While iterating, I realized that the flywheel was going to need to be a lot heavier in order to develop a sufficient momentum to keep it going with the treadle pedal. So I filled the wheel with concrete:

<div class="shashin_image" style="width: 410px;">
  <a href="http://lh6.ggpht.com/_LYO5Bj1T__g/TOHQvGikHQI/AAAAAAAABug/Nb83Kr1b86c/CIMG1794.JPG?imgmax=640" class="highslide" id="shashin_thumb_link_3" onclick="return hs.expand(this)"><img src="http://lh6.ggpht.com/_LYO5Bj1T__g/TOHQvGikHQI/AAAAAAAABug/Nb83Kr1b86c/CIMG1794.JPG?imgmax=400" alt="Ready to add the concrete!" width="400" height="300" id="shashin_thumb_image_3" title="Ready to add the concrete!" /></a> <div class="highslide-caption">
    Ready to add the concrete!
  </div>
</div>

<div class="shashin_image" style="width: 442px;">
  <a href="http://lh3.ggpht.com/_LYO5Bj1T__g/TOHQxP2pFzI/AAAAAAAABuo/rsVwZ7XCWdk/CIMG1795.JPG?imgmax=640" class="highslide" id="shashin_thumb_link_4" onclick="return hs.expand(this)"><img src="http://lh3.ggpht.com/_LYO5Bj1T__g/TOHQxP2pFzI/AAAAAAAABuo/rsVwZ7XCWdk/CIMG1795.JPG?imgmax=576" alt="Concrete in place. Now must be patient. For 5 days. :-)" width="432" height="576" id="shashin_thumb_image_4" title="Concrete in place. Now must be patient. For 5 days. :-)" /></a> <div class="highslide-caption">
    Concrete in place. Now must be patient. For 5 days. <img src="http://www.eliotk.net/wp-includes/images/smilies/icon_smile.gif" alt=":-)" class="wp-smiley" />
  </div>
</div>

I&#8217;m a concrete newbie and one thing I learned that for this purpose it would have been better to use straight portland cement as opposed to concrete. Concrete contains gravel and the larger pieces made it difficult to work the mix between the spokes and into the wheel whereas portland cement is purely the fine cement itself. It would have also been easier to mold the outside of the wheel which would make it more aesthetically pleasing.

Stay tuned as I should finally be generating juice in part 3!

 [1]: http://www.eliotk.net/10/23/personal-desk-treadle-exerciserpower-generator-part-1/ "Desk Exerciser Power Generator"
 [2]: http://www.amazon.com/gp/product/B000EJS9IM?ie=UTF8&tag=eliotk-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=B000EJS9IM