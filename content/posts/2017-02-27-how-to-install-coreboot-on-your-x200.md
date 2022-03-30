---
title: How To Install Coreboot Onto Your Lenovo Thinkpad X200 Laptop
date: 2017-02-27T22:59:00Z
tags: openbsd
---

I flashed a Lenovo x200 with Coreboot with Intel microcode enabled, ME removed, and the gigabit ethernet firmware from Libreboot. Everything seems to work with OpenBSD (my daily driver OS). Unlike with Libreboot, which comes with a Grub2 payload, Coreboot uses the SeaBIOS payload by default and it can boot an encrypted OpenBSD volume. I'm encountering what seems to be a random lockup every few days, haven't had a chance to troubleshoot it yet.

### Let's Do This

1. Buy stuff: [BeagleBone Black][8], [BBB case][6], [3.3v power source][9], [USB-A to USB-A cable][10] for the 3.3v power source, [micro-HDMI adapter][7], [test clip][4], [jumper cables][5], SD card with USB adapter.

1. [Build a Coreboot ROM][1] by following the normal instructions and using the default build settings. I used a Debian qemu VM to build with, but I suppose I could have used the Beaglebone. 2017-04-07 update: the BeagleBone Black doesn't have enough RAM to build coreboot...2 GB or more is a good idea. And you must at a minimum configure Mainboard vendor, Mainboard model, and ROM chip size. 2017-04-25 update: you must compile SeaBIOS with CONFIG_VGA_COREBOOT=y and 
compile coreboot with CONFIG_VGA_BIOS=y, CONFIG_VGA_BIOS_FILE="<path to the vgabios.bin>", CONFIG_MAINBOARD_DO_NATIVE_VGA_INIT, and comment out CONFIG_VGA_ROM_RUN and other options with default values except for those in the "Mainboard" category like vendor, model, device in order to see the SeaBIOS prompt (rather than a blank screen) until OpenBSD boots.

1. [Flash your x200][2] ...but use the Coreboot ROM that you made in the last step, instead of the Libreboot ROM, follow the rest of the steps unaltered, i.e. use the Libreboot GBE firmware, etc. 2017-04-07 update: I used the libreboot 'flashrom' utility for my actual flashing and it was easy. I'm told the coreboot one requires configuration, unlike the libreboot one, and may otherwise be more difficult to get working, so, use the libreboot one.

### So What

The upshot of using Coreboot or Libreboot is that I'm no longer restricted to using mini PCI-e cards that have been whitelisted by Lenovo. I can use the sweet, sweet umb cards for WWAN access, I can upgrade to the latest iwm driver with MIMO, etc. And for those that haven't experienced an x200 yet, and you're wondering why anyone would voluntarily use a 10 year old laptop: the x200 is only $50 before upgrades (I like iwm, umb, an SSD, new battery, new power adapter, USB3 expresscard), has a great keyboard, solid build quality, good portability, good expandability (3 internal mini pci-e, 1 external expresscard slot, 3 USB2 ports), and its relatively easy to repair.

Downsides are its limited to 8G of RAM and the CPU aren't as sprightly as the
latest+greatest (I've shifted by heavy lifting to servers so not a big issue for
me), extended battery only lasts about 3 hours (enough for how I roll, but I can
understand if you've been spoiled by an all-day battery on a different laptop), VGA out instead of HDMI (can be solved by an adapter), audio quality sucks (can be solved by an adapter).

I keep 3 x200s around right now...at $50 each, it doesn't break the bank to have some backups, and if one goes south its easy to just swap the hard drive and go. Harder to pull off if my laptop costs $2k. ;)

My original goal was to see what a maximally open source setup might be like and got as close as I'm likely to get (for now) with Libreboot+OpenBSD+ral, etc. It was pretty good--I'm excited to see what the future holds as more of the stack becomes more hacker friendly.

For those interested, here's a thread about my [prior attempts to get Libreboot working][3]. Libreboot mostly works too, but its a bit less stable (Intel microcode maybe?) and I didn't figure out how to boot a fully encrypted OpenBSD installation. I suspect if I could just swap in the SeaBIOS payload it would work, but I tried for a bit and wasn't able to get it across the finish line before I gave up and decided to try Coreboot instead.

*Updated on April 07, 2017*

Guillaume Simon wrote in to report that the BBB doesn't have enough RAM to build, but 2GB on a different box worked. He also pointed out that *some* settings are needed when configuring coreboot, and that the flash tools from Libreboot are easier to use. I updated the post inline incorporating Guillaume's feedback.

*Updated on April 25, 2017*

An anonymous writer said they got a blank screen until OpenBSD boots, and pointed out the fix. I updated the post incorporating their feedback.

*Updated on March 30, 2022*

Replaced broken links to eBay listings for stuff to buy, with working links at Amazon
instead.

[1]: https://www.coreboot.org/Build_HOWTO
[2]: https://www.chucknemeth.com/laptop/lenovo-x200/flash-lenovo-x200-libreboot
[3]: https://marc.info/?l=openbsd-misc&m=147490313431099&w=2
[4]: https://www.amazon.com/DGZZI-Black-SOIC8-Flash-Without/dp/B08R364SYM/ref=sr_1_4?crid=35ILWONNUGMVY&keywords=soic+test+clip&qid=1648663545&sprefix=soic+test+clip%2Caps%2C156&sr=8-4
[5]: https://www.amazon.com/EDGELEC-Breadboard-Optional-Assorted-Multicolored/dp/B07GD2BWPY/ref=sr_1_3?crid=E6S9EG65AANP&keywords=breadboard+jumper+wires&qid=1648663375&s=electronics&sprefix=breadboard+jumper+wires%2Celectronics%2C140&sr=1-3
[6]: https://www.amazon.com/GeauxRobot-BeagleBone-Black-Compact-Case/dp/B00JVD594E
[7]: https://www.amazon.com/UGREEN-Adapter-Compatible-Raspberry-ZenBook/dp/B00B2HORKE/ref=sr_1_6?crid=3AMBN5QW0G4VN&keywords=micro-hdmi&qid=1648663301&s=electronics&sprefix=micro-hdmi%2Celectronics%2C213&sr=1-6
[8]: https://beagleboard.org/black/
[9]: https://www.amazon.com/MakerSpot-Breadboard-Voltage-Solderless-Friendly/dp/B01IUYLVFK/ref=sr_1_9?crid=2FTW3RC2IKP3A&keywords=3.3v+power+supply+usb&qid=1648663079&s=electronics&sprefix=3.3v+power+supply%2Celectronics%2C136&sr=1-9
[10]: https://www.amazon.com/Monoprice-1-5ft-24AWG-Cable-Plated/dp/B009GUXG92/ref=sr_1_3?crid=2CP4ZKY6QE7BI&keywords=usb-a+to+usb-a&qid=1648663239&s=electronics&sprefix=usb-a+to+usb-a%2Celectronics%2C155&sr=1-3
