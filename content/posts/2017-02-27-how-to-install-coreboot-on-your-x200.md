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

2017-04-07 update: Guillaume Simon wrote in to report that the BBB doesn't have enough RAM to build, but 2GB on a different box worked. He also pointed out that *some* settings are needed when configuring coreboot, and that the flash tools from Libreboot are easier to use. I updated the post inline incorporating Guillaume's feedback.

2017-04-25 update: an anonymous writer said they got a blank screen until OpenBSD boots, and pointed out the fix. I updated the post incorporating their feedback.

  [1]: https://www.coreboot.org/Build_HOWTO
  [2]: https://iqlusion.org/index.php/2016/03/01/x200-libreboot/
  [3]: https://marc.info/?l=openbsd-misc&m=147490313431099&w=2
  [4]: http://www.ebay.com/sch/i.html?_nkw=Pomona%205250%20SOIC%20Test%20Clip,%208%20Pin&clk_rvr_id=1174744441332&mfe=search
  [5]: http://www.ebay.com/sch/i.html?_odkw=Pomona+5250+SOIC+Test+Clip%2C+8+Pin&mfe=search&clk_rvr_id=1174744441332&_osacat=0&_from=R40&_trksid=p2045573.m570.l1313.TR0.TRC0.H0.X120pcs+Dupont+Wire+Male+to+Male+%2B+Male+to+Female+%2B+Female+to+Female+Jumper+Cabl.TRS0&_nkw=120pcs+Dupont+Wire+Male+to+Male+%2B+Male+to+Female+%2B+Female+to+Female+Jumper+Cable&_sacat=0
  [6]: http://www.ebay.com/sch/i.html?_nkw=GeauxRobot%20BeagleBone%20Black%20Compact%20Case%20Black&clk_rvr_id=1174767169717&mfe=search
  [7]: http://www.ebay.com/sch/i.html?_odkw=GeauxRobot+BeagleBone+Black+Compact+Case+Black&mfe=search&clk_rvr_id=1174767169717&_osacat=0&_from=R40&_trksid=p2045573.m570.l1313.TR0.TRC0.A0.H0.XMicro+HDMI+Type+D+Male+to+HDMI+Type+A+Female+Adapter+Converter+Connector+1080P.TRS1&_nkw=Micro+HDMI+Type+D+Male+to+HDMI+Type+A+Female+Adapter+Converter+Connector+1080P&_sacat=0
  [8]: http://www.ebay.com/sch/i.html?_odkw=Micro+HDMI+Type+D+Male+to+HDMI+Type+A+Female+Adapter+Converter+Connector+1080P&_osacat=0&_from=R40&_trksid=p2045573.m570.l1313.TR0.TRC0.H0.XBeagleBone+Black+Rev+C+1GHz+ARM+Cortex-A8+Mini+PC+BB-BBLK-000.TRS0&_nkw=BeagleBone+Black+Rev+C+1GHz+ARM+Cortex-A8+Mini+PC+BB-BBLK-000&_sacat=0
  [9]: http://www.ebay.com/sch/i.html?_odkw=BeagleBone+Black+Rev+C+1GHz+ARM+Cortex-A8+Mini+PC+BB-BBLK-000&_osacat=0&_from=R40&_trksid=p2045573.m570.l1313.TR12.TRC2.A0.H0.X3.3V%2F5V+MB102+Breadboard+Power+Supply+Module+For+Arduino+Board.TRS0&_nkw=3.3V%2F5V+MB102+Breadboard+Power+Supply+Module+For+Arduino+Board&_sacat=0
  [10]: http://www.ebay.com/sch/i.html?_odkw=usb+male+to+male&_osacat=0&_from=R40&_trksid=p2045573.m570.l1313.TR0.TRC0.H1.Xusb+type+a+male+to+male.TRS0&_nkw=usb+type+a+male+to+male&_sacat=0
