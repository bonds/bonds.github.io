---
title: Winot and My OpenBSD Wifi Adventures
date: 2016-03-01T18:40:00Z
tags: code
---

I run OpenBSD on my main laptop. OpenBSD doesn't come with a Gnome-like Network
Manager...you are on your own to keep your laptop connected to the wifi network,
to manage your wifi passwords, etc. The OS makes it easy to connect to the
wireless network to be sure...it just doesn't automate away connecting to a
different network at work and home and such.

So I thought, I'll see if anyone has written a tool, and lo and behold,
[wiconfig][1] is a great start, written in Bourne Shell, so it has no
requirements besides OpenBSD itself. I used wiconfig for a while and was happy
with it.

But then I got to thinking, that I'd like to not only stay connected to wifi,
but also to VPN at all times, so that when on a wifi network, my traffic will be
routed through my VPN and be protected from the local snoops. I also wanted to
fallback to my cellular wwan connection when a familiar wifi was unavailable.
Thus [winot][2] was born. It started life in Ruby and did all the things I
needed, but it was plagued by dropped connections that it couldn't recover from.
Well, plagued may be an exaggeration--a couple times a day I had to manually
intervene...but for a tool like this it should be 0 times a day! I added more
logging and slowly worked through the edge cases including: wake from sleep, a
weak (but still connected) wifi signal, etc.

In the middle of this, I upgraded to a new release of OpenBSD. I always install
from scratch and use Ansible to setup my machine again, to avoid any unintended
cruft from my previous install. But this time, getting Ruby up and running again
proved more difficult than expected, and it got me thinking, maybe I should
switch to Bourne Shell. I had hitherto avoided doing much shell scripting in
Bourne, but I figured it would be a good excuse to learn it, and the stuff winot
does shouldn't be too hard to implement as a shell script.

So winot became Bourne Shell based, and that brings the story up to the present
day. Winot works pretty well, but there are a few challenges with it. I need to
add more logging to troubleshoot the existing issues. The CPU usage is way too
high. And there are, once again, conditions where it gets stuck I need to
manually intervene to get connected again.

Who knew staying connected to the wifi at home and work, always routing over an
SSH based VPN, falling back to WWAN when the VPN is down, all automagically,
would be so tricky? :)

So now I'm using this an excuse to learn (more) Haskell...all the locking,
reading files, awking, seding, tailing, cutting, and forking is probably much
less efficient than it needs to be, and a library that will help me with logging
levels and such would be really nice. Less portable to be sure, but I want to
learn Haskell and I've got only so much time available for my coding side
projects!

  [1]: https://github.com/devious/wiconfig
  [2]: https://github.com/bonds/winot
 
