---
title: NixOS Is Great
date: 2024-06-05T00:22:00-07:00
tags: misc
---
Finally got around to trying out NixOS. This is the way. :) 

I've used Chef, Ansible, shell scripts, manually cowboy sysadmin knob twiddling, CloudFormation, Terraform and other means of wrangling the computers and software I manage and code > manual but NixOS takes it to the next level with a declarative > imperative approach to configuring a Linux box.

It's not all roses. I'm going to have to invest real time before I'll have wrapped my head around the Nix language...and without that I'm groping around in the dark at times. I've already bruised my head on Haskell, another functional language, so hopefully it's not too bad. A lot has changed over the years and plenty of example configs and ideas and docs that were right before are outdated now, so...more groping.

But being able to build my workstation image and roll back and forward is a revelation. Access to the [hugest library][1] of high quality, well maintained packages in the world of Linux/Unix, bar none, is awesome (yay I have Dwarf Fortress working!). Putting my config in source control with a real hope of being able to build a new workstation with everything ready to go, with minimal manual config for Gnome, Firefox, the apps to install, and my rotated monitors promised to save from me lots of grief going forward.

[1]: https://repology.org/repositories/graphs
