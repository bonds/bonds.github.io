---
title: My First Idris Program
date: 2017-08-15T19:05:00Z
tags: code
---
[Idris][1] is sort of 'Haskell 2.0', where the authors got to apply the lessons 
learned from the creation and evolution of Haskell, but leave behind all the 
baggage embedded in existing, in use libraries, since, you know, they don't have 
any of those yet. With the recent release of [the book][2] I was inspired to 
take Idris for a spin and see for myself just how lacking of ['production 
readiness'][3] it is.

One of my favorite ways to try a new language is to use it for scripting. I 
write and run small scripts a lot, and the combination of the scripts being 
small+simple and part of my day-to-day make them a great tool for learning in 
bite-sized increments all the time. Before I know it, I've got the hang of the 
new language...

Alright, enough talk, here's my first Idris program--it's a script for searching 
for an OpenBSD package by name:

````
#!/usr/bin/env runidris
-- vim:ft=idris:

import System

partial
main : IO ()
main = do
    args <- getArgs
    case args of
        (_::terms) => do
            let query = unwords terms
            ec <- system $
                    "/usr/local/bin/sqlite3 /usr/local/share/sqlports "
                  ++ "\"SELECT DISTINCT pkgname || ': ' || comment AS result "
                  ++ "FROM ports "
                  ++ "WHERE pkgname LIKE '%" ++ query ++ "%' "
                  ++ "OR comment LIKE '%" ++ query ++ "%' "
                  ++ "ORDER BY 1\""
                  ++ " | ag -i \"" ++ query ++ "\""
            pure ()
        _ => pure ()
````

````runidris```` is a recent addition to Idris, not yet tauted, and not yet 
installed for you, but you can find it in the [scripts][4] directory if you 
install Idris from source. You'll need to move it to a directory on your PATH 
and then you're ready to go. If you use Vim+[Ale][5] as your editor and linter 
combo, there's some basic support for flagging errors inline...doesn't work 
perfectly yet, but its a start.

[1]: http://www.idris-lang.org/
[2]: https://www.manning.com/books/type-driven-development-with-idris
[3]: https://www.idris-lang.org/idris-1-0-released/
[4]: https://github.com/idris-lang/Idris-dev/blob/master/scripts/runidris
[5]: https://github.com/w0rp/ale
