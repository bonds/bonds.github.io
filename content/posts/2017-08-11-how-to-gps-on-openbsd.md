---
title: How to GPS on OpenBSD
date: 2017-08-11 15:35 UTC
tags: code
---

I've heard tell that the WWAN module lodged inside my laptop can give me my 
coordinates on planet Earth. I thought I'd see if it was true. Fortunately, a 
number of brave souls have blazed the path, I needed only to rediscover it.

### Funny side note

Did you know that your super modern WWAN module uses 1980s-era modem commands to 
control it? You know, AT...OK, blah blah blah. Who knew, right?

### Let's do this

1. Buy and install an Ericsson H5321 WWAN module in your Lenovo X200 running 
   coreboot. The X200 and coreboot part isn't strictly necessary, but neither is 
   OpenBSD nor life, yet all of the above are a good idea.
1. \# pkg_add gpsd gpsd-X11 socat jq
1. Download and run [gps_on][4].
1. Download and run [gps_location][5].
1. Wait 10 minutes while the WWAN module ponders life and acquires a GPS lock. 
   YMMV...it may take infinity minutes, depending on how your WWAN module and 
   the GPS satellites feel that day. But that's ok because the X200 is a 
   [hypercomputer][3], so it will go by fast.
1. Bask in the glory of your location.
1. Donate [$1 to GPSD][1] and [$1 to OpenBSD][2]. It's a good habit to get into 
   after you bask in glory.

[1]: https://www.patreon.com/esr
[2]: http://www.openbsdfoundation.org/donations.html
[3]: https://en.wikipedia.org/wiki/Hypercomputation
[4]: https://gist.github.com/bonds/dbeeea001e72da1cae084585ac1deaae
[5]: https://gist.github.com/bonds/b6fc2e4381b555df7d2d0bf0d3805664

