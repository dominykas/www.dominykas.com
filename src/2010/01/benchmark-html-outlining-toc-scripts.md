---
published: 2010-01-18T22:09:12+00:00
tags: benchmark, html, javascript, webbie stuff
---

# Benchmark: HTML outlining/TOC scripts

<p>A bit over a week ago <a href="http://www.wait-till-i.com/2010/01/06/the-table-of-contents-script-my-old-nemesis/">Chris Heilmann published a post on table of contents generators</a>, where he listed a couple of JavaScript methods to do that. It’s been always in the plans to optimize the performance of <a href="https://github.com/h5o">my own implementation of the HTML5 outlining routine</a> – and what better way to measure it, than to compare it with some other approaches while I’m at it. To no surprise, I lost. Big time.<br>
<span id="more-68"></span></p>
<h2>Results</h2>
<ol>
<li>Chris Heilmann’s <a href="http://isithackday.com/demos/tocit/toc_yui3.html">YUI based approach</a> (136ms)</li>
<li>Chris Heilmann’s <a href="http://isithackday.com/demos/tocit/toc_dom.html">DOM based approach</a> (247ms)</li>
<li>Stuart Langridge’s <a href="http://www.kryogenix.org/code/browser/generated-toc/">generated-toc</a> (258ms)</li>
<li><a href="http://github.com/joshwnj/toc">Josh Johnston’s solution</a> with jQuery (781ms)</li>
<li>My own <a href="https://github.com/h5o">HTML5 Outliner</a> (3099ms)</li>
<li>Chris Heilmann’s <a href="http://isithackday.com/demos/tocit/toc_js.html">RegExp based approach</a> (4440ms)</li>
<li><a href="http://lab.diogovincenzi.com/blog/view/table-contents-jquery">Diogo Vincenzi’s solution</a> with jQuery (9334ms)</li>
</ol>
<h3>Methodology</h3>
<p>The numbers above are based on an 1.5Mb file, which has some 200 headings to use for the TOC table. The actual file, was created out of HTML4 specification part on forms, to reflect a more natural usage. The results were a bit different, when I used my own generated file, which had a lot more headings, and a lot less text.</p>
<p>The test runner itself would create an <code>iframe</code>, load the test document inside, inject the required script and call it. The <a href="https://github.com/h5osource/browse/trunk/benchmark">source is available</a> on Google Code (though be aware, that you will need to procure and hack the dependencies yourself).</p>
<p>I ran it on a decent 2.2Ghz laptop, using a vanilla version of Portable Firefox 3.5. With some exceptions (see below), the results were comparable and not unexpected in other browsers.</p>
<h2>Insights</h2>
<ul>
<li>The RegExp based approach was a non-contender from the start, as it doesn’t really work under any browser, other than Firefox.</li>
<li>Diogio’s solution scored so low because it’s querying the DOM twice inside every loop iteration (I think).</li>
<li>I am impressed at how well YUI3 performed – on every browser (incl. IE8), except Opera. I seriously need to follow up on the Opera thing…</li>
<li>Speaking of YUI3 – one needs to go through extra hoops to measure performance, due to YUI loader’s <code>setTimeout()</code>. And make sure that you have all dependencies in on file, to avoid calls to the Yahoo’s CDN.</li>
<li>IE8 didn’t like 2Mb documents inside an <code>iframe</code> (hence 1.5Mb)</li>
<li>I have plenty of space for improvement – it will be fun!</li>
</ul>