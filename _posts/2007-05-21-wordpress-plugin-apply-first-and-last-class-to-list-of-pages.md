---
title: 'WordPress Plugin: Add first and last class to list of pages'
author: eliot
layout: post
permalink: /05/21/wordpress-plugin-apply-first-and-last-class-to-list-of-pages/
categories:
  - Code
  - Open Source
  - WordPress Plugins
---
<center>
  <img src='http://www.eliotk.net/wp-content/uploads/2007/05/wordpress-logo.jpg' alt='WordPress Logo' />
</center>

I wrote this plugin because there was no easy way to define a first and last class to the list of pages generated in WordPress with wp\_list\_pages. These classes are useful for tweaking the visual formatting of the page list with CSS. 

I&#8217;ve tested this with WordPress 2.2 and it should behave nicely with other plugins as well as earlier versions. Though let me know if you find something buggy.

As always, I am not responsible if this plugin blows up your computer.

***WHY WOULD I WANT THIS? ***

Let&#8217;s say you want to create a horizontal list of your pages in the footer of your page with pipes separating the page links.

The css might look something like this:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="css" style="font-family:monospace;"><span style="color: #cc00cc;">#footer</span> ul <span style="color: #00AA00;">&#123;</span>
	<span style="color: #000000; font-weight: bold;">list-style-type</span><span style="color: #00AA00;">:</span> <span style="color: #993333;">none</span><span style="color: #00AA00;">;</span> 
	<span style="color: #000000; font-weight: bold;">margin-left</span><span style="color: #00AA00;">:</span> <span style="color: #933;">0px</span><span style="color: #00AA00;">;</span>
	<span style="color: #000000; font-weight: bold;">padding-left</span><span style="color: #00AA00;">:</span> <span style="color: #933;">0px</span><span style="color: #00AA00;">;</span>
<span style="color: #00AA00;">&#125;</span>
<span style="color: #cc00cc;">#footer</span> li <span style="color: #00AA00;">&#123;</span>
	<span style="color: #000000; font-weight: bold;">float</span><span style="color: #00AA00;">:</span> <span style="color: #000000; font-weight: bold;">left</span><span style="color: #00AA00;">;</span>
	<span style="color: #000000; font-weight: bold;">padding</span><span style="color: #00AA00;">:</span> <span style="color: #933;">0px</span><span style="color: #00AA00;">;</span>
	<span style="color: #000000; font-weight: bold;">margin</span><span style="color: #00AA00;">:</span> <span style="color: #933;">0px</span><span style="color: #00AA00;">;</span>
<span style="color: #00AA00;">&#125;</span>
<span style="color: #cc00cc;">#footer</span> li a
<span style="color: #00AA00;">&#123;</span>
	<span style="color: #000000; font-weight: bold;">border-right</span><span style="color: #00AA00;">:</span> <span style="color: #933;">1px</span> <span style="color: #993333;">solid</span> <span style="color: #cc00cc;">#CCC</span><span style="color: #00AA00;">;</span>
	<span style="color: #000000; font-weight: bold;">display</span><span style="color: #00AA00;">:</span> <span style="color: #993333;">block</span><span style="color: #00AA00;">;</span>
	<span style="color: #000000; font-weight: bold;">padding-top</span><span style="color: #00AA00;">:</span> <span style="color: #933;">0px</span><span style="color: #00AA00;">;</span>
	<span style="color: #000000; font-weight: bold;">padding-left</span><span style="color: #00AA00;">:</span> <span style="color: #933;">10px</span><span style="color: #00AA00;">;</span>
	<span style="color: #000000; font-weight: bold;">padding-right</span><span style="color: #00AA00;">:</span> <span style="color: #933;">10px</span><span style="color: #00AA00;">;</span>
	<span style="color: #000000; font-weight: bold;">text-align</span><span style="color: #00AA00;">:</span> <span style="color: #993333;">center</span><span style="color: #00AA00;">;</span>
<span style="color: #00AA00;">&#125;</span></pre>
      </td>
    </tr>
  </table>
</div>

The border-right applied to the link css sets a gray &#8216;pipe&#8217; that separates out the page links.

The code in your WordPress theme file &#8216;footer.php&#8217; might look like this:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="php" style="font-family:monospace;">&lt;div id="footer"&gt;
	&lt;ul&gt;
		<span style="color: #000000; font-weight: bold;">&lt;?php</span> wp_list_pages<span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'sort_column=menu_order&title_li='</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span> <span style="color: #000000; font-weight: bold;">?&gt;</span>
	&lt;/ul&gt;
&lt;/div&gt;</pre>
      </td>
    </tr>
  </table>
</div>

So right now this would output in the browser as:

![List Pages Plugin Before][1]

See that last pipe following &#8220;Contact&#8221;? We don&#8217;t want that. 

But since we now have a separate class for that last list item, we can add this to the css, which will remove that last &#8216;pipe&#8217;:

<div class="wp_syntax">
  <table>
    <tr>
      <td class="code">
        <pre class="css" style="font-family:monospace;"><span style="color: #cc00cc;">#footer</span> <span style="color: #6666ff;">.last_item</span> a
<span style="color: #00AA00;">&#123;</span>	
	<span style="color: #000000; font-weight: bold;">border-right</span><span style="color: #00AA00;">:</span> <span style="color: #993333;">none</span><span style="color: #00AA00;">;</span>
<span style="color: #00AA00;">&#125;</span></pre>
      </td>
    </tr>
  </table>
</div>

And now our list of pages in the footer will look like this:

![List pages with correct css applied][2]

***HOW DO I INSTALL IT?***

<a href="http://www.eliotk.net/wp-content/code/pages-first-last/pages-first-last.phps" title="WordPress Plugin - First and Last Class" target="_blank">View/Download</a> the plugin file and place it in your /wordpress/wp-content/plugins/ folder. Then activate the plugin from your WordPress control panel.

***HOW DO I USE THE PLUGIN?***

When activated, the plugin will automatically apply the class &#8220;first\_item&#8221; to the first li (for the first page) as well as the class &#8220;last\_item&#8221; to the last li (for the last page) in the list that is generated with wp\_list\_pages.

 [1]: http://www.eliotk.net/wp-content/uploads/2007/05/llist-pages-plugin-before.jpg
 [2]: http://www.eliotk.net/wp-content/uploads/2007/05/llist-pages-plugin-after.jpg