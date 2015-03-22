# But it’s easy…

<p>Here’s a sample of how your “it’s easy” and my “sure, probably half an hour” becomes “half a day”:</p>
<ol start="0">
<li>You want me to make the Thing clickable?</li>
<li>Is just the Thing clickable or the whole line?
<ol>
<li style="list-style-type: lower-alpha;">Just the Thing – introduces technicalities (below)</li>
<li style="list-style-type: lower-alpha;">Whole line – quirky on small screens in portrait</li>
</ol>
</li>
<li>When you move your mouse over – how does it change to indicate it is clickable?</li>
<li>How shall we give it an affordance (make it look clickable)?
<ol>
<li style="list-style-type: lower-alpha;">The heading nearby is the same color as our standard link color. If we are to use our standard link color for the Thing, we must make all headings dark blue, which results in disbalance.</li>
<li style="list-style-type: lower-alpha;">Add an icon – we’ll introduce clutter, plus the icon is not always visible on smaller screens, let alone it’s harder to implement</li>
<li style="list-style-type: lower-alpha;">We can reduce icon clutter by increasing line height, but then Other Things no longer align and the Whole Thing looks disbalanced</li>
</ol>
</li>
<li>The Thing sometimes displays in gray. How do we make THAT Thing clickable?</li>
<li>Oh, and we’ll need to test pretty much every variation on PC, iPhone and Android and then when finally happy-ish – double check on all Internet Explorers.</li>
</ol>
<p>All this just to make one thing clickable, that wasn’t ever really meant to be clickable.</p>
<p>Ah, here’s another one:</p>
<ol start="-1">
<li>Let’s have a chat facility…</li>
<li>Let’s show user’s online status…</li>
<li>How do we know they are logged in?</li>
<li>What if they have the chat open multiple tabs?</li>
<li>What if they log out in one of these tabs?</li>
<li>Oh, let’s just see when they last loaded the page?</li>
<li>What if they leave a tab open for 30 minutes, but don’t do anything?</li>
<li>What if they have us as their homepage, therefore they visit often, but usually don’t even look at the chat?</li>
<li>What if they go to another tab and browse Facebook?</li>
<li>What if they have two tabs and go to another tab and don’t browse Facebook?</li>
<li>What if they leave the page open and go home?</li>
<li>What if they leave the chat open and go to the toilet for 30 minutes and then spend 30 minutes in Excel?</li>
</ol>
<p>Oh, so we should have a state where they are “online”, but “idle”? Congratulations, you just doubled the complexity.</p>
<p>Some changes are easier. Some are even trickier. I can’t recall the last time I said “sure, it’s trivial”, and it really was…</p>
<p>☑ Write a blog post this year.</p>