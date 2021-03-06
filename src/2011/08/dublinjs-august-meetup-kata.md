---
published: 2011-08-14T16:26:03+00:00
tags: dublinjs, javascript, webbie stuff
---

# DublinJS August meetup kata

<p>I’m doing a kata for <a href="http://www.meetup.com/Javascript-Dublin/events/27369271/">this month’s</a> meetup of <a href="https://groups.google.com/group/dublinjs">Javascript Dublin</a> group and my choice is <a href="http://codingdojo.org/cgi-bin/wiki.pl?KataRomanNumerals"><strong>Roman Numerals</strong></a>. It’s simple enough and it also demos some interesting transformations of the code during the whole TDD process (if you stick to the mantra of “write the simplest possible thing”). I found that I could also put some of the new ES5 features into practice: <code>Object.keys()</code>, <code>Array.prototype.forEach()</code> and <code>Array.prototype.reduce()</code>.</p>
<p>The Coding Dojo page for this kata also has a <a href="http://vimeo.com/15104374">video of it performed in Ruby</a>. There’s also a link to a video of it in Excel, but as much as it sounds good, it’s just building a VB macro…</p>
<p>You can find <a href="https://github.com/dymonaz/dublinjs">my code on GitHub</a>. I have also prepared a <a href="https://github.com/dymonaz/dublinjs/blob/master/roman_numbers.walkthrough.txt">walk through</a> on how I arrived at <a href="https://github.com/dymonaz/dublinjs/tree/master/20110814.roman_numbers">my solution</a> (txt is the new ppt!)</p>
<p>The previous kata sessions used Jasmine – and it works just fine – but I chose to do things with YUI Test. If you feel like it – I prepared a <a href="https://github.com/dymonaz/dublinjs/tree/master/yui-test-harness">skeleton for the project</a>. Note that it loads YUI from Yahoo’s CDN, so make sure you’re online (or update the harness.html).</p>