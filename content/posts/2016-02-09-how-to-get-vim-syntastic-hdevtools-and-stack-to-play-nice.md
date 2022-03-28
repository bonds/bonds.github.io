---
title: How To Get Vim, Syntastic, Hdevtools, and Stack To Play Nice
date: 2016-02-09 16:51 UTC
tags: code
---
I was poking around some old Haskell code the other day, when I realized that,
since switching to Vim (from Atom) I hadn't setup the necessary plugins in Vim
to get syntax checking and such for Haskell.

Seeing as Stack is the new Haskell installer hotness, I installed it and used it
to install a bunch of 'global' packages for use with my runghc based scripts. I
installed ghc-mod and hlint, but I didn't see any error messages when I messed
up the syntax of my Haskell code. A bit of investigation revealed that Syntactic
dropped support for ghc-mod, but that hdevtools was supported. I installed that,
loaded my Haskell code into Vim, and this time I got errors about missing
libraries. I realized hdevtools was looking for the libraries in the system GHC
instead of using my global Stack based libraries. To get it to use the global
stack libraries instead I:

* created /home/scott/bin/hdevtools-stack which is a script that boils down to: "stack exec hdevtools -- $@"
* added "let g:syntastic_haskell_hdevtools_exec = '/home/scott/bin/hdevtools-stack'" to my vimrc
* pkill hdevtools
* launch Vim and load my Haskell code

Voila, it works.

**Updated on February 12, 2016:**

I decided to remove the vimrc syntastic config line and instead I wrote a
hdevtools script and made sure its higher priority in my PATH. This works for
ghc-mod, which, in combination with ghcmod-vim, makes it so I can do fancy stuff
like get the type of whatever my cursor is over. I'm using the --verbosity
silent option so my ghc-mod script works ok, with no stack warning to cause
problems for ghcmod-vim (without --silent ghcmod-vim chokes on the stack-ified
ghc-mod script I wrote). Here's my ghc-mod script (/home/scott/bin/ghc-mod):

    #!/bin/sh
    stack --verbosity silent exec ghc-mod -- $@
