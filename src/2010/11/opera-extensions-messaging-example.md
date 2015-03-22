# Opera Extensions: messaging example

<p>I already <a href="http://twitter.com/dymonaz/status/29608503399">vented out</a> my <a href="http://dev.opera.com/forums/topic/793632">frustration with examples that have flaws</a>, so this one is more constructive and tries to actually explain and solve things. You’re welcome to skip all of that and just <a href="http://code.dominykas.com/opera-extensions/title_in_popup.oex">get the example code</a>.</p>
<p>It may not be 100% correct, it may have it’s own flaws, and obviously it may soon become obsolete, as Opera 11 is still in alpha, but I did create a more reliable example of how to communicate between the user scripts and popup windows.</p>
<p>This article assumes you already grok the <a href="http://dev.opera.com/articles/view/getting-started-with-opera-extensions/">introductory information on Opera extension</a>. In fact, knowledge of Chrome extension flows may also help.<br>
<span id="more-117"></span></p>
<h2>The flaws</h2>
<p>Let’s skip the ranting about lack of documentation (hint hint) and look at the fundamental flaws in the original <a href="http://dev.opera.com/articles/view/opera-extensions-messaging/#popup_injectedscript">Communicating between popup and injected script</a> example. You can download <a href="http://code.dominykas.com/opera-extensions/message_example3/message_example3_modified.oex">the modified version of it</a> that attempts to display the page title. I also documented the steps to <a href="http://code.dominykas.com/opera-extensions/message_example3/readme.txt">reproduce two bugs</a> in it.</p>
<ol>
<li>There is only one communication channel – and it’s always reset to the page which was loaded last.</li>
<li>The above means, that we may not be communicating with the focused tab.</li>
<li>The above also means that the channel is not re-established once a new popup opens – even if it’s on the same tab. I suspect that <code>if (port)</code> is supposed to check whether the channel is still active, but (potentially – due to a browser bug) it returns a truthy value, hence the new channel is not sent to the popup.</li>
<li>The check inside <code>onconnect</code> only validates that a communication channel was created – it never validates that the connecting script is actually a popup window</li>
</ol>
<h2>The solution</h2>
<p>In here, I have a couple of things that are merely assumptions on how things work, and how the API should respond – this is mostly due to lack of documentation (hint hint, again) and is based on experience with Chrome extensions.</p>
<p>The core point of the solution is to <strong>avoid storing the communication channel in the background script</strong> – instead – store a reference to the popup window. I feel that it is safe to do, since the popup window closes automatically, and it seems that all data associated with it gets destroyed.</p>
<p>The background script still plays an important role – it’s job is to pass the <code>MessagePort</code> from the user script to the popup, but it only does that when requested. As mentioned above, when the popup window closes, we also need to re-establish the connection, so the final flow becomes like this:</p>
<ol>
<li>Browser loads, background script is initialized</li>
<li>A page in a tab loads, user script gets initialized</li>
<li>User clicks on the toolbar icon for the popup</li>
<li>The popup loads</li>
<li>Background page receives an <code>onconnect</code> event</li>
<li>It then checks the event origin – all widget related files have URLs that start with <code>widget://</code></li>
<li>If the thing that just connected is a popup window, the background script determines the active tab, and sends a <code>getPorts</code> message to initiate messaging connection. It also stores the reference to the popup for future communication.</li>
<li>The user script receives the message and creates a new communication channel (it assumes that the previous channel is long dead)</li>
<li>It then sends that communication channel back to the background script using <code>establishConnection</code> message.</li>
<li>The background script forwards that message to the previously stored popup reference. I feel that it is safe enough to trust that, since the steps 5-9 should really be pretty much instantaneous without any user interaction possible in between.</li>
<li>The popup receives the communication channel – it is free to do with it whatever it likes, e.g. request information from the user script using <code>postMessage()</code> and receive that information using <code>onmessage</code>.
</li><li>Once the popup closes, we end up at point 2</li>
</ol>
<p><a href="http://code.dominykas.com/opera-extensions/title_in_popup.oex">Download example code</a> (I release it into public domain, without any guarantees)</p>
<h2>The gotchas, suggestions and pleas to the Opera team</h2>
<h3>Document <code>MessageChannel</code> and <code>MessagePort</code></h3>
<p>While this is an obvious request, I’d also like to mention that I find Chrome’s model of two way messaging much simpler – just pass around a callback function for each message.</p>
<h3>Rename <code>port1</code> and <code>port2</code> to something meaningful</h3>
<p>My initial response to these two properties was that one of them is for sending messages, the other is for receiving. As far as I understand that right now – one is to be used as a “local” communication port, and the other is for the use by “remote” script. They should be named accordingly. However, a much better approach would be to not expose them at all – same as the previous suggestion – it should be possible to just create a <code>MessageChannel</code> with <code>postMessage()</code> and <code>onmessage</code> – which are inversed once they change context.</p>
<h3>Clarify if objects are allowed as <code>event.data</code></h3>
<p>I’ll admit – I didn’t read the W3C spec. My example uses simple objects, but the <a href="http://labs.opera.com/extensions-api/">API documentation</a> says the message data has to be a <code>DOMString</code>. While it’s not a biggie, and I’m sure everyone is good friends with <code>JSON.stringify()</code> and <code>JSON.parse()</code>, it either should be documented as allowed or should throw errors when used.</p>
<h3>Create an easier way to determine who is the <code>event.origin</code></h3>
<p>At the moment, to check if the message was sent by a popup, I’m testing the URL in the <code>event.origin</code>, but I’d really like to see some methods, such as <code>isBackgroundScript()</code>, <code>isUserScript()</code> and <code>isPopup()</code> for simplicity.</p>
<h3>More graphical information</h3>
<p>I’m guilty here, since I probably should have included the flow diagram instead of an 11 point list in this blog, but I do find the <a href="http://labs.opera.com/extensions-api/visual-guide/index.htm">visual guide to the API</a> very useful. The <a href="http://dev.opera.com/">Dev.Opera</a> article about messaging inside extensions should have included some of that love.</p>
<h3>Explain best practices</h3>
<p>Having looked through most of the example extensions, I find certain things quite interesting – and they do raise a lot of “why” type questions:</p>
<ul>
<li>Why do we need to do stuff on <code>load</code> in the background scripts?</li>
<li>How does that make a difference as compared to just executing the code in the <code>&lt;script&gt;</code> tag?</li>
<li>Do we also have to do things on <code>load</code> in the popup scripts?</li>
<li>Why do some examples check for existence of <code>opera.extension</code>? When it might not be available?</li>
<li>What are the “dos” and “donts” for the background process? What are the limitations? Considering that it’s a page that’s always active, I’m sure there are plenty.</li>
</ul>
<p>I hope the time spent with frustration, figuring things out and writing up this article was worth it. I also hope that it’s useful for at least one other person. However, in case of the information in here is already published and the questions are already answered – please – drop me a link in the comments or <a href="http://twitter.com/dymonaz">on twitter @dymonaz</a>.</p>