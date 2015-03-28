---
published: 2012-04-12T13:42:53+00:00
tags: responsive-design, webbie-stuff
---

# OMG OMG Nielsen is wrong, let’s all, like, build responsive sites

<p>Two days ago Jakob Nielsen published a new Alertbox column: <a href="http://www.useit.com/alertbox/mobile-vs-full-sites.html">Mobile Site vs. Full Site</a>, which seems to have caused some uproar in the web community, <a href="https://twitter.com/karenmcgrane/status/189816427795062784">openly mocking his ideas</a>:</p>
<blockquote><p>Jakob Nielsen’s April Fools Day piece on mobile is HILARIOUS. So boneheadedly wrong. But why April 10? (<a href="https://twitter.com/karenmcgrane">@karenmcgrane</a>)</p>
</blockquote>
<p><span id="more-147"></span><br>
Honestly, I’m not sure I see the contradiction between what Nielsen says and Responsive Design. He’s just stating that “well designed mobile specific sites” work better for the users. Is there anything to argue about that?</p>
<p>Now, some are trying to say, that <a href="http://www.lucentwebdesign.co.uk/index.php/blog/entry/on_not_quite_agreeing_with_jakob_nielsen">this is also pushing the expensive option</a>. But how is that a problem? If you can’t afford it – well, you don’t have it! And Responsive Web Design is the cheaper option, even if not as optimal as a completely separate site.</p>
<p>IMHO, RWD is purely a technical solution to achieve the same result – optimize the layout and content for mobile. It’s not like Nielsen is saying “Don’t use CSS – use font tags and tables for layout”.  And that’s what media queries really are – just a simpler technical way of using different CSS for the same markup.</p>
<p>From the designers perspective (as in “graphical bit”) <strong>RWD is still about making multiple designs</strong> (especially if done in Photoshop). RWD only places an additional constraint – the content must be pretty much the same. However, the “design” itself, while consistent, is still different. IMHO RWD is more similar to Nielsen’s “two sites” idea, than different.</p>
<p>The only place where Nielsen is more wrong than not in that article is about the “&lt;..&gt; penalty imposed on desktop users when you give them a design that’s suboptimal for bigger screens” – but I believe that’s just the mis-interpretation of “mobile first”, because “mobile first” is not “mobile only”. Neither is responsive design.</p>
<p><strong>Update:</strong> Jakob Nielsen <a href="http://www.netmagazine.com/interviews/nielsen-responds-mobile-criticism">responded to critique</a>. I find this bit to be saying exactly what I tried to say with this post:</p>
<blockquote>
<p>There are at least three different ways of implementing different user interfaces for different devices:</p>
<ol>
<li>Each version lives at a different URL.</li>
<li>The same URL serves up different versions, depending on the device used to request the page.</li>
<li>The same code is transmitted to all devices, and the client side transforms this into the different designs, using responsive design.</li>
</ol>
<p>As long as each user sees the appropriate design, the choice between these implementation options should be an engineering decision and not a usability decision.</p>
</blockquote>