---
title: How To Run an Arch Linux (Qemu) Guest On an OpenBSD Host
date: 2014-09-30 20:03 UTC
tags: openbsd
---
The main stumbling block I had to overcome to get various flavors of Linux to
install as a guest OS on a Qemu instance, running on an OpenBSD source, was to
disable [APIC][1], not be confused with [ACPI][2].

With Arch Linux you do this:

1. boot the Arch Linux CD (in your Qemu guest)
1. press tab to config the boot command
1. add a space and then 'noapic' to the boot command
1. press Enter to boot
1. [install Arch Linux][3] on your Qemu guest hard drive
1. add the 'noapic' parameter to boot command in your boot config, e.g. /boot/syslinux/syslinux.cfg

  [1]: https://en.wikipedia.org/wiki/Advanced_Programmable_Interrupt_Controller
  [2]: https://en.wikipedia.org/wiki/Advanced_Configuration_and_Power_Interface
  [3]: https://wiki.archlinux.org/index.php/Beginners%27_Guide

