---
title: How to Market Genode
date: 2018-09-11 15:45 UTC
tags: marketing
---
Following updates from [Genode][1] and [Haiku][2] highlighting their progress 
towards becoming broadly useful operating systems, I installed them on some real 
hardware, took them for a spin, and thought about what it would take for them to 
take over the world...what market [position][3] is available and accessible to a 
potential, future, Genode based OS?

So. Would you be interesting in an OS that can say *this* (with a straight 
face)?:

Uncrashable. Genode will never crash, ever, when run on properly functioning 
hardware. Go ahead and try, we dare you. For good measure there's a formal proof 
of Genode's uncrashability and it matches experience of real users--Genode is 
the most stable, reliable, general purpose operating system available, open 
source or proprietary, bar none. In fact, its able to detect and recover from 
many *hardware* bugs, to the point that Genode is the tool of choice by 
integrators trying to track down bad hardware.

Unstoppable. If you can play a video or music on your Genode machine, without 
skipping under light load, adding heavy load at 100% CPU won't cause it to skip 
nor will the UI become *any* less responsive than it was when you weren't 
running any apps. With Genode you get many of the benefits and guarantees of a 
realtime OS without the downsides--you get a great UI, a mainstream API, *and* 
reliable performance.

Unhackable. Genode trusts nothing. Not the CPU, not the RAM, not the devices, 
not the software. Genode protects against malicious hardware, drivers, and 
software in all categories, taking care to limit the data leaked and privileges 
accessed by a bug or a sophisticated attacker that controls one or more 
components. Genode uses encryption, separation, compartmentalization, and other 
techniques in a formally verified design that makes it provably impossible to 
use side-channel or direct attacks on the tech--you're left only with phishing 
and other social engineer attacks if you want to break into a Genode system.

Multilingual. Runs Linux, Windows, OSX, Android, iOS, and retro console binaries 
including office suites, system utilities, developer tools, and games. On all 
architectures known to man. And a pony.

Ok, I got carried away and it gets more ridiculous as I go, but at least some of 
the first two benefits are possible, interesting, and differentiated. Those 
would make for a pretty interesting OS.

P.S. Genode is not an OS, rather, its an OS framework that you use to make an OS 
by assembling a bunch of pieces (i.e. kernel, drivers, apps). 'Sculpt' is the 
name of the OS the Genode team makes to show off what Genode can do.
Nonetheless, Genode is the name most people might know, so I'm exercising a bit 
of creative license here, not unlike shortening GNU/Linux to Linux or referring 
to Linux as an OS when its really a kernel while Debian is the name of a proper 
(Linux-based) OS.

P.P.S. It is of course up to the people investing blood, sweat, and cash in 
Genode to decide where to take it next. I am not one of those, I have the much 
easier and safer task of hurling remarks from the peanut gallery.

P.P.P.S. Yes, yes, some of these ideas are impossible or at least highly 
impractical, but I can dream, can't I? :) Tablet computers probably seemed 
impossible when they were making the film 2001, but now we have them. Sometimes 
a bit of dreaming can bring the future closer.

[1]: https://genode.org/news/sculpt-for-the-curious
[2]: https://www.haiku-os.org/blog/waddlesplash/2018-08-19_r1beta1_release_plans_-_at_last/
[3]: https://www.amazon.com/Positioning-Battle-Your-Al-Ries/dp/0071373586

