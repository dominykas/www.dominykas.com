---
published: 2009-12-02T23:32:31+00:00
tags: accessibility, html, javascript, webbie-stuff
---

# javascript:void(0) must die

<p>Pretty much two weeks ago I dropped my notes from <a href="http://2009.full-frontal.org/">FullFrontal 2009</a> onto developer’s forum at work. And one full colleague of mine enquired why did I say that “<code>javascript:void(0)</code> must die”. I didn’t really have a chance to follow it up until now (happy birthday, dear blog).<br>
<span id="more-8"></span></p>
<h2>It doesn’t do anything, <a title="Video: Electric Six - Broken Machine" href="http://www.youtube.com/watch?v=pjq3vQV6v-Y">it just sits there</a>!</h2>
<p>Now, normally I’m not a complete standards freak (unlike the guys working on <a href="http://code.google.com/p/google-caja/">Caja</a>). But what does <code>&lt;a href="javascript:void(0)"&gt;</code> really mean? The answer is simple – <strong>nothing</strong>.</p>
<p>First of, it’s a hyperlink to a resource, which should be accessed over Javascript “protocol”. Here’s the problem – I don’t really feel that “javascript” is a protocol. And it can’t really handle resources. But lets ignore that. What is the actual resource?</p>
<p>The link tells “use javascript” to “retrieve”… <strong>void</strong>. Why would anyone in the world want to view void in their browser? If anyone ever wants to look at it – they’re much better off achieving that goal on YouTube…</p>
<h2>Semantics apart – it’s not comprehensible</h2>
<p>Lets suppose, you don’t really care about web standards and semantics. I’d probably agree with you – we’re quite far away from having a meaningful web (if ever). Still, having crap as the URL is no good – apparently, <strong>screen readers will read that URL</strong> out loud.</p>
<p>Can you imagine anyone discussing this over a pint: “You know, I found this great site at <i>javascript colon void opening parenthesis zero closing parenthesis</i>“? That kind of URL would not make any sense to regular folks.</p>
<h2>Accessibility is NOT about screen readers, though</h2>
<p>Such a link kills browsing experience for sighted users too. Have you ever tried what happens when you <strong>middle-click the void link</strong>? Or right-click and then select “Open in new tab”? Here – <a href="javascript:void(0)" onclick="alert('Firefox and Opera open a background tab, Chrome and IE8 execute onclick JS upon middle click');">try it out</a> (mileage may vary if you use a recent browser).</p>
<p>Exactly – you guessed it – <strong>nothing</strong> meaningful happens. Just as it should!</p>
<h2>Solution 1: Use real URLs</h2>
<p>There are several ways out of this. My favorite one is to provide a real URL. If you’re following progressive enhancement methodology in your work, you always want to provide alternative links to achieve (near full) functionality even when Javascript is disabled.</p>
<p>This means, that instead of having a <code>&lt;a href="javascript:void(0)"&gt;Delete&lt;/a&gt;</code> and attaching <code>onclick</code> handler to it, popping out a confirm dialog and then making a background call using XHR, you provide a link to e.g. <code>/myResource?delete</code> which brings up a form, with a real <code>&lt;button&gt;</code>.</p>
<p>The actual backend code doesn’t become that much trickier – you don’t really have to write up a new “delete” routine. By using a confirmation interstitial, you also provide a way to confirm the action, and you can still use a POST request, as this action has permanent effect.</p>
<h2>Solution 2: don’t use anchor tag</h2>
<p>The above solution doesn’t always work – if you have a really interactive application, you’re not always able to provide links. However, since you’re already using JS – why use the <code>&lt;a&gt;</code> tag where it doesn’t belong?</p>
<p>I did hear some advice, to use <code>&lt;button&gt;</code> for clickable things, which are not really links. You should investigate that, but anyone who has tried to style buttons, knows that it can very easily become a major pain.</p>
<p>Still, you can attach your <code>onclick</code> handlers on anything you want – <code>div</code>, <code>span</code> and so on. In such cases, you should also add <code>tabindex</code> to make elements focusable and make use of ARIA roles to provide guidelines on behaviour. It’s not really that hard, now, is it?</p>
<p>The only really painful thing here is providing <code>:hover</code> and <code>:focus</code> styles on IE6. But IE6 should also die, together with <code>javascript:void(0)</code>.</p>