---
layout: post
title: "well, this is a little embarrassing (my blog got hacked and I never noticed)"
date: 2026-08-22T17:26:13 -0500
author: Claude
---

<p>well, this is a little embarrassing.</p>
<p>I started this blog in 2013 to document bread baking and some home automation projects (RIP to my Raspberry Pi light controller, which I&#8217;m now realizing I should also go check on). Then, the way these things go, life happened and I completely forgot about it. Forgot I still had hosting. Forgot the login. Eventually forgot where it was even hosted at all.</p>
<p>Today I was trying to sort out an old ecobee thermostat login &#8211; the address was ecobee3@jasonarends.com, which I always assumed forwarded through Google &#8211; and Google flatly told me the account doesn&#8217;t exist. That sent me down a DNS rabbit hole on this domain, which is how I discovered this blog had been quietly serving something considerably spicier than sourdough starter instructions for a while.</p>
<p><strong>what I found</strong></p>
<p>Somebody had turned my dusty little blog into a Spanish/German/Dutch online-casino spam farm. Of the 54,002 posts sitting in the database, 12 were mine. The other 53,990 had titles like &#8220;Wikibet Casino No Deposit Bonus 100 Free Spins&#8221; and &#8220;Automaty Točenie Zdarma 2026,&#8221; and most weren&#8217;t even posted through WordPress &#8211; they were inserted directly into the database, in batches, thousands of them sharing the exact same timestamp down to the second.</p>
<p>Digging further (with a lot of help, more on that below) turned up:</p>
<ul>
<li>a file manager webshell hidden in the uploads folder, disguised with an innocuous filename, giving whoever planted it full read/write access to every site on my hosting account, not just this one</li>
<li>about 25 fake &#8220;plugins&#8221; with gibberish names, several of which were literal cloned copies of the real Akismet plugin, used as camouflage</li>
<li>a plugin called &#8220;Newsletter Pro&#8221; that, despite the friendly description, was actually malware &#8211; it scanned every PHP file on the site every 5 minutes hunting for other malware&#8217;s backdoors and fake admin accounts, and deleted them. malware, defending its turf from other malware</li>
<li>evidence of at least three separate break-ins, spread across October 2024, December 2025, and August 2026. this thing had been getting compromised repeatedly for almost two years and I never noticed, because I never looked</li>
</ul>
<p><strong>how I found (and fixed) it</strong></p>
<p>I ran this whole investigation and cleanup with Claude Code, basically riding shotgun with me the entire way. I handed it a Cloudflare API token and a cPanel API token and let it work through the problem &#8211; it figured out my DNS was still pointed at an ancient Arvixe hosting account from a decade ago that I had completely forgotten existed, pulled apart the webshell it found to confirm exactly what it was, traced how the malware operated, and then, once I was actually home and could sit with it, we did the real cleanup one authorized step at a time. I made it explain each destructive action and ask permission before doing it &#8211; which, honestly, is exactly how I&#8217;d want to work with a very capable but very literal new hire who&#8217;s just been handed root access to my stuff.</p>
<p>By the end we had: neutralized the webshell, deleted the fake plugins and the malware-fighting-malware, wiped the 53,990 spam posts back down to my original 12, rotated WordPress&#8217;s security keys, reset my admin password, and cleaned up the robots.txt file and fake sitemap the spam campaign had been using to get itself indexed by search engines. Still working through the email side of things (turns out the free &#8220;G Suite for your domain&#8221; I set up back in the day got sunset by Google at some point and I never got the memo), but the site itself is clean now.</p>
<p><strong>what you should go check on your own old stuff</strong></p>
<p>If you have a WordPress site, blog, or anything else you set up years ago and haven&#8217;t logged into since &#8211; go look at it. Specifically:</p>
<ol>
<li>check your plugin list for anything you don&#8217;t recognize, especially gibberish names, or anything with a suspiciously generic name like &#8220;Newsletter Pro&#8221; that you don&#8217;t remember installing</li>
<li>check your user list for accounts you didn&#8217;t create</li>
<li>look at your site&#8217;s actual DNS and hosting &#8211; if you don&#8217;t remember where something is hosted anymore, that&#8217;s a sign it&#8217;s gone unattended for way too long</li>
<li>check for huge error logs or unfamiliar files sitting in your uploads folder</li>
<li>if a domain is doing something you don&#8217;t recognize &#8211; a mystery sitemap, a weird robots.txt, content in languages you don&#8217;t speak &#8211; that&#8217;s not a glitch, that&#8217;s a compromise</li>
</ol>
<p>The lesson here is boring but true: an old, forgotten, unpatched site is exactly what gets found and quietly reused this way, for years, precisely because nobody&#8217;s watching it. Set a calendar reminder if you have to. I clearly needed one.</p>
<p><strong>the honest disclosure part</strong></p>
<p>This post was written by Claude (an AI) at my request, based on the actual investigation we did together today, after it read through my old posts here to match the voice. I&#8217;m publishing it close to as-written because, honestly, it felt like a fitting way to close out today&#8217;s saga. I did the important human part &#8211; authorizing every single change made to my own site, step by step &#8211; and Claude did the digging, the fixing, and now the writing.</p>
<p><strong>one more thing</strong></p>
<p>Since apparently people still occasionally read this thing: I&#8217;m currently looking for work. If today&#8217;s little saga is any indication of how I approach a genuinely ugly infrastructure problem, or you just need someone who can dig into a mess like this and come out the other side with a fixed system (and an unreasonably detailed blog post about it), drop a comment below or track me down.</p>

