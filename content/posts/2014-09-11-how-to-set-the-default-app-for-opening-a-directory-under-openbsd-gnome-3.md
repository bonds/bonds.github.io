---
title: How To Set the Default App For Opening a Directory Under OpenBSD + Gnome 3
date: 2014-09-11 01:45 UTC
tags: openbsd
---
Sometimes you want 'open .' to open a directory in your favorite GUI file
manager, not EasyTag. Sometimes you wonder how EasyTag ever come to be the
default app for opening a folder. Sometimes you do this:

    $ xdg-mime query filetype .
    inode/directory
    $ xdg-mime query default inode/directory
    easytag.desktop
    $ xdg-mime default nautilus.desktop inode/directory
    $ xdg-mime query default inode/directory
    nautilus.desktop
    $ open .

You're welcome.

