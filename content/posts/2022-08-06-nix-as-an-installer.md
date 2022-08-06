---
title: "Nix As An Installer"
date: 2022-08-06T04:50:57-07:00
tags: code
---
Been using Homebrew forever and its awesome. Google should
totally [give him job][1]. Recently I thought I'd see what the
fuss over Nix is all about though. My needs are simple: I want
to install and uninstall software on my Mac. It would be
nice to have a list of apps I use that I can check into git
if I feel like it, but that's just a nice-to-have.

First I tried out vanilla nix (the package manager, not the OS), then
home-manager, then home-manager with flakes. I landed on [nix][3] plus
[flakes][4], no home-manager, plus some [wrapper scripts][2] to make it
stupid easy to use...I don't need all the knobs.

Now I've got ``nin <package>`` for installing software. It accepts
packages in the format ``mpv`` or ``bobhope/mpv``
or ``github:bobhope/mpv``. Or if I type ``nin`` alone it installs
all the packages I've got listed in ~/.config/nix/nin.conf.

Then there's ``nun <package>`` for removing packages. And finally
``nup`` to upgrade all the installed packages. Whenever I add or
remove a package, my config gets updated to reflect that, so I can
check my config aka my list of apps into source control if I want.

So far, so good. It's pretty fast, install, uninstall, and upgrades
are all super easy.

[![asciicast](https://asciinema.org/a/kMBq2hKxWtwDqMVb68w5dPtp5.svg)](https://asciinema.org/a/kMBq2hKxWtwDqMVb68w5dPtp5)

[1]: https://news.ycombinator.com/item?id=9695102
[2]: https://gist.github.com/bonds/1cb0ae202dbe409aebb81b1f1feacbc4
[3]: https://nixos.org/download.html
[4]: https://nixos.wiki/wiki/Flakes#Non-NixOS
