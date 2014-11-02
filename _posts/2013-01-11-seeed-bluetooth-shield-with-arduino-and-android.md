---
title: Arduino Seeed Bluetooth Shield With Amarino and Android
author: eliot
layout: post
permalink: /01/11/seeed-bluetooth-shield-with-arduino-and-android/
aktt_notify_twitter:
  - yes
aktt_tweeted:
  - 1
categories:
  - Blog
---
I&#8217;m working on a new iteration of the [OpenExo][1] project. The problem is is that the microcontroller and project box is going to be located underneath the device. Running wires to a control is going to be cumbersome and also get in the way of the operation of the device so I thought that communicating wirelessly with the Arduino would be the best approach. And I can use my Android phone (or any Android phone) running an App to as the remote!

I&#8217;m using the Seeed Bluetooth Shield [available here on Amazon][2]. You can also find it sometimes at RadioShack.

The nice thing about using the shield as opposed to something like the [Bluesmirf][3] bluetooth module is that you don&#8217;t have to bother with lashing it to the Arduino and then working it into a proto board. The shield just sits nicely and securely on the Arduino.

### SoftwareSerial vs. Hardware Serial

The Seeed shield has jumpers that join any of digital pins 0-7 to the RX and TX serial lines that the Bluetooth module uses for communication to and from the Arduino.

<div id="attachment_419" style="width: 310px" class="wp-caption alignnone">
  <a href="http://www.eliotk.net/wp-content/uploads/2013/01/2013-01-11-11.17.08.jpg"><img class="size-medium wp-image-419" title="2013-01-11 11.17.08" src="http://www.eliotk.net/wp-content/uploads/2013/01/2013-01-11-11.17.08-300x225.jpg" alt="Seeed Bluetooth Shield Serial Selection Jumpers" width="300" height="225" /></a><p class="wp-caption-text">
    Here are the jumpers for selecting which pins to use for the Serial Bluetooth communication
  </p>
</div>

If you choose to use pins 2-7 then you&#8217;ll be need to use the SoftwareSerial (or NewSoftSerial if you&#8217;re in the Arduino environment < version 1) Arduino library to talk to the shield. If you use pins 0 and 1 then you can just use the Serial commands (the same as you&#8217;d use w/ the Serial monitor) to communicate with the shield.

The downside of using the hardware serial pins (0 and 1) is that, since the Bluetooth shield is basically hijacking the same line of communication that the Arduino uses to communicate to and from the computer then you can no longer use the serial monitor and also you&#8217;ll need to remove the shield each time you want to upload new code to the Arduino.

The upside of using the hardware serial pins is that a lot of libraries that you may want to use with Bluetooth are setup to work over the default Serial implementation. So in using SoftwareSerial, you may need to tweak these libraries like I had to in order to use Amarino with SoftwareSerial.

One curious issue I found was that I simply could not get the shield and code to work when I was using the default jumper positions that the shield came with (pins 6 and 7). I&#8217;m not sure if it&#8217;s a problem with my Arduino in particular or a broader issue pertaining to all Unos but everything worked correctly once I changed the jumpers to pins 2 and 3.

### Initializing Bluetooth Shield, Making it Pairable

In order to allow the Bluetooth shield to connect with other devices (making it pairable), it&#8217;s necessary to send initialization code every time the Bluetooth shield is powered up. Unlike setting the baud rate, the pairable configuration is reset to the default of not being pairable each time the board is reset.

This initialization code is available in the [Seeed Bluetooth Library][4]. Once you install the library in the libraries directory of your Arduino installation (/Applications/Arduino.app/Contents/Resources/Java/libraries/ for me on OSX), you&#8217;ll be able to open the &#8220;Slave&#8221; demo in the examples dropdown in your Arduino environment.

Here is the Slave sketch code:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="c" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">/*
BluetoothShield Demo Code Slave.pde. This sketch could be used with
Master.pde to establish connection between two Arduino. It can also
be used for one slave bluetooth connected by the device(PC/Smart Phone)
with bluetooth function.
2011 Copyright (c) Seeed Technology Inc.  All right reserved.
&nbsp;
Author: Steve Chang
&nbsp;
This demo code is free software; you can redistribute it and/or
modify it under the terms of the GNU Lesser General Public
License as published by the Free Software Foundation; either
version 2.1 of the License, or (at your option) any later version.
&nbsp;
This library is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
Lesser General Public License for more details.
&nbsp;
You should have received a copy of the GNU Lesser General Public
License along with this library; if not, write to the Free Software
Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301  USA
&nbsp;
For more details about the product please check http://www.seeedstudio.com/depot/
&nbsp;
*/</span>
&nbsp;
<span style="color: #808080; font-style: italic;">/* Upload this sketch into Seeeduino and press reset*/</span>
&nbsp;
<span style="color: #339933;">#include &lt;SoftwareSerial.h&gt; //Software Serial Port</span>
<span style="color: #339933;">#define RxD 6</span>
<span style="color: #339933;">#define TxD 7</span>
&nbsp;
<span style="color: #339933;">#define DEBUG_ENABLED  1</span>
&nbsp;
NewSoftSerial blueToothSerial<span style="color: #009900;">&#40;</span>RxD<span style="color: #339933;">,</span>TxD<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
<span style="color: #993333;">void</span> setup<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#123;</span>
  Serial.<span style="color: #202020;">begin</span><span style="color: #009900;">&#40;</span><span style="color: #0000dd;">9600</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
  pinMode<span style="color: #009900;">&#40;</span>RxD<span style="color: #339933;">,</span> INPUT<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
  pinMode<span style="color: #009900;">&#40;</span>TxD<span style="color: #339933;">,</span> OUTPUT<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
  setupBlueToothConnection<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
<span style="color: #009900;">&#125;</span> 
&nbsp;
<span style="color: #993333;">void</span> loop<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#123;</span>
  <span style="color: #993333;">char</span> recvChar<span style="color: #339933;">;</span>
  <span style="color: #b1b100;">while</span><span style="color: #009900;">&#40;</span><span style="color: #0000dd;">1</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span>blueToothSerial.<span style="color: #202020;">available</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span><span style="color: #666666; font-style: italic;">//check if there's any data sent from the remote bluetooth shield</span>
      recvChar <span style="color: #339933;">=</span> blueToothSerial.<span style="color: #202020;">read</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      Serial.<span style="color: #202020;">print</span><span style="color: #009900;">&#40;</span>recvChar<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span>Serial.<span style="color: #202020;">available</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span><span style="color: #666666; font-style: italic;">//check if there's any data sent from the local serial terminal, you can add the other applications here</span>
      recvChar  <span style="color: #339933;">=</span> Serial.<span style="color: #202020;">read</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
      blueToothSerial.<span style="color: #202020;">print</span><span style="color: #009900;">&#40;</span>recvChar<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
  <span style="color: #009900;">&#125;</span>
<span style="color: #009900;">&#125;</span> 
&nbsp;
<span style="color: #993333;">void</span> setupBlueToothConnection<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#123;</span>
  blueToothSerial.<span style="color: #202020;">begin</span><span style="color: #009900;">&#40;</span><span style="color: #0000dd;">38400</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//Set BluetoothBee BaudRate to default baud rate 38400</span>
  blueToothSerial.<span style="color: #202020;">print</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>+STWMOD=0<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//set the bluetooth work in slave mode</span>
  blueToothSerial.<span style="color: #202020;">print</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>+STNA=SeeedBTSlave<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//set the bluetooth name as "SeeedBTSlave"</span>
  blueToothSerial.<span style="color: #202020;">print</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>+STOAUT=1<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// Permit Paired device to connect me</span>
  blueToothSerial.<span style="color: #202020;">print</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>+STAUTO=0<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// Auto-connection should be forbidden here</span>
  delay<span style="color: #009900;">&#40;</span><span style="color: #0000dd;">2000</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// This delay is required.</span>
  blueToothSerial.<span style="color: #202020;">print</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>+INQ=1<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//make the slave bluetooth inquirable</span>
  Serial.<span style="color: #202020;">println</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"The slave bluetooth is inquirable!"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
  delay<span style="color: #009900;">&#40;</span><span style="color: #0000dd;">2000</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// This delay is required.</span>
  blueToothSerial.<span style="color: #202020;">flush</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span></pre>
      </td>
    </tr>
  </table>
</div>

The first few lines need to be changed:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="c" style="font-family:monospace;"><span style="color: #339933;">#include &lt;SoftwareSerial.h&gt;    //Software Serial Port</span>
<span style="color: #339933;">#define RxD 6</span>
<span style="color: #339933;">#define TxD 7</span></pre>
      </td>
    </tr>
  </table>
</div>

If you&#8217;re in the Arduino environment greater than version 1, then you can use this SoftwareSerial library inclusion:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="c" style="font-family:monospace;"><span style="color: #339933;">#include &lt;SoftwareSerial.h&gt;</span></pre>
      </td>
    </tr>
  </table>
</div>

For versions less than 1, you need to get the NewSoftSerial library and put it in your Arduino libraries directory and include it like this:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="c" style="font-family:monospace;"><span style="color: #339933;">#include &lt;NewSoftSerial.h&gt;</span></pre>
      </td>
    </tr>
  </table>
</div>

The other thing that needs changing is the Rx and Tx pin configuration. The default in the Slave sketch should work with the default of the shield but, like I mentioned, I needed to change the jumpers and the config to pins 2 and 3 like this:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="c" style="font-family:monospace;"><span style="color: #339933;">#include &lt;SoftwareSerial.h&gt; //Software Serial Port</span>
<span style="color: #339933;">#define RxD 3</span>
<span style="color: #339933;">#define TxD 2</span></pre>
      </td>
    </tr>
  </table>
</div>

Then you can run the Slave code and you should see the board LEDs go to blinking between red and green instead of just the green LED blinking in two pulses. This means that the Bluetooth module is initialized and it is able to be paired with a device.

### Changing the Baud Rate

Another thing you might need to do is change the Baud rate of the Bluetooth shield which basically determines how fast it communicates with the paired device. There are different recommended Baud rates for different applications. For using Amarino and Android, one of the recommended Baud rates is 57600.

So to change the Baud rate, you can insert this line into the Slave sketch:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="c" style="font-family:monospace;">blueToothSerial.<span style="color: #202020;">print</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>+STBD=57600<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span></pre>
      </td>
    </tr>
  </table>
</div>

Changing the Baud rate on the shield is permanent so you&#8217;ll need to connect to it using that Baud rate once the change is made. You can of course change it again using the command above but it will keep the latest Baud rate even if you power down the board.

### Connecting Android and Arduino using Bluetooth

You can follow these installation instructions to get Amarino setup both on your Android device as well as for the Arduino development:

<http://www.amarino-toolkit.net/index.php/download.html>

Next, you can test that you can get communication going between the Android and Arduino by using the SoftwareSerialExample sketch included with Arduino. You&#8217;ll need to edit that though in order to the initialization routine for the Bluetooth shield.

Here&#8217;s what mine looks like after adding it in:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="c" style="font-family:monospace;"><span style="color: #808080; font-style: italic;">/*
  Software serial multple serial test
&nbsp;
 Receives from the hardware serial, sends to software serial.
 Receives from software serial, sends to hardware serial.
&nbsp;
 The circuit:
 * RX is digital pin 10 (connect to TX of other device)
 * TX is digital pin 11 (connect to RX of other device)
&nbsp;
 Note:
 Not all pins on the Mega and Mega 2560 support change interrupts,
 so only the following can be used for RX:
 10, 11, 12, 13, 50, 51, 52, 53, 62, 63, 64, 65, 66, 67, 68, 69
&nbsp;
 Not all pins on the Leonardo support change interrupts,
 so only the following can be used for RX:
 8, 9, 10, 11, 14 (MISO), 15 (SCK), 16 (MOSI).
&nbsp;
 created back in the mists of time
 modified 25 May 2012
 by Tom Igoe
 based on Mikal Hart's example
&nbsp;
 This example code is in the public domain.
&nbsp;
 */</span>
<span style="color: #339933;">#include &lt;SoftwareSerial.h&gt;</span>
&nbsp;
SoftwareSerial blueToothSerial<span style="color: #009900;">&#40;</span><span style="color: #0000dd;">3</span><span style="color: #339933;">,</span><span style="color: #0000dd;">2</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// RX, TX</span>
&nbsp;
<span style="color: #993333;">void</span> setup<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>
<span style="color: #009900;">&#123;</span>
  <span style="color: #666666; font-style: italic;">// Open serial communications and wait for port to open:</span>
  Serial.<span style="color: #202020;">begin</span><span style="color: #009900;">&#40;</span><span style="color: #0000dd;">38400</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
  <span style="color: #b1b100;">while</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span>Serial<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
    <span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// wait for serial port to connect. Needed for Leonardo only</span>
  <span style="color: #009900;">&#125;</span>
&nbsp;
  Serial.<span style="color: #202020;">println</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"Goodnight moon!"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
  blueToothSerial.<span style="color: #202020;">begin</span><span style="color: #009900;">&#40;</span><span style="color: #0000dd;">57600</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
  blueToothSerial.<span style="color: #202020;">print</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>+STWMOD=0<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//set the bluetooth work in slave mode</span>
  blueToothSerial.<span style="color: #202020;">print</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>+STNA=SeeedBTSlave<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//set the bluetooth name as "SeeedBTSlave"</span>
  blueToothSerial.<span style="color: #202020;">print</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>+STOAUT=1<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// Permit Paired device to connect me</span>
  blueToothSerial.<span style="color: #202020;">print</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>+STAUTO=0<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// Auto-connection should be forbidden here</span>
  delay<span style="color: #009900;">&#40;</span><span style="color: #0000dd;">2000</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// This delay is required.</span>
  blueToothSerial.<span style="color: #202020;">print</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>+INQ=1<span style="color: #000099; font-weight: bold;">\r</span><span style="color: #000099; font-weight: bold;">\n</span>"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">//make the slave bluetooth inquirable</span>
  Serial.<span style="color: #202020;">println</span><span style="color: #009900;">&#40;</span><span style="color: #ff0000;">"The slave bluetooth is inquirable!"</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
  delay<span style="color: #009900;">&#40;</span><span style="color: #0000dd;">2000</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #666666; font-style: italic;">// This delay is required.</span>
  blueToothSerial.<span style="color: #202020;">flush</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #993333;">void</span> loop<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #666666; font-style: italic;">// run over and over</span>
<span style="color: #009900;">&#123;</span>
  <span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span>blueToothSerial.<span style="color: #202020;">available</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
    Serial.<span style="color: #202020;">write</span><span style="color: #009900;">&#40;</span>blueToothSerial.<span style="color: #202020;">read</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
  <span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span>Serial.<span style="color: #202020;">available</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span>
    blueToothSerial.<span style="color: #202020;">write</span><span style="color: #009900;">&#40;</span>Serial.<span style="color: #202020;">read</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span></pre>
      </td>
    </tr>
  </table>
</div>

Now, you can open the Amarino app in Android, connect to the device listed (should be there as &#8220;SeeedBTSlave&#8221;) and go to the monitoring tool inside the Amarino app. Then you should be able to send commands from the Amarino app to the Arduino serial monitor like I did in the video above.

### Using SoftwareSerial with the Amarino bridge and MeetAndroid Library

One other hangup when you actually start making your Android app and have it talk with Arduino is that the MeetAndroid Amarino libraries that use with Amarino are setup with the assumption that you&#8217;ll be using the hardware Serial, pins 0 and 1 for Bluetooth communication. So if you are using pins 0 and 1 with the shield, you are all set. But if you&#8217;re not, you&#8217;ll need to get a modified version of the MeetAndroid library.

Thankfully someone ran into this problem already and was kind enough to modify the libraries and put them up for download here:

<http://www.double-oops.org/mini-blog/amarinowithsoftwareserial>

So this is excellent. Except there is one other problem. When using the shield, you need to run that initialization code first. I tried doing this first by putting the initialization code right in the sketch after created the modified MeetAndroid connection like we&#8217;ve been doing in the sketches above. However, there was a conflict in that the MeetAndroid library takes control of the Bluetooth serial lines once it&#8217;s initialized and therefore trying to initialize the module inside the sketch doesn&#8217;t work.

So I modified the the library again, adding a new &#8220;send_plain&#8221; method which can be used to send Bluetooth configuration commands. This was necessary since the &#8220;send&#8221; command built into the library modifies the input string in order to communicate appropriately with the Amarino API on the Android side.

I put it up at Github:

[MeetAndroid SoftwareSerial Library With Bluetooth Configuration Command][5]

 [1]: http://www.openexo.com
 [2]: http://www.amazon.com/gp/product/B006YM5QWU/ref=as_li_ss_tl?ie=UTF8&tag=eliotk-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=B006YM5QWU"
 [3]: https://www.sparkfun.com/products/10269
 [4]: http://www.seeedstudio.com/wiki/images/3/30/BluetoothShieldDemoCode.zip
 [5]: https://github.com/eliotk/meetandroid-softserial