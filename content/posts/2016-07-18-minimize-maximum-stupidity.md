---
title: Minimize Maximum Stupidity
date: 2016-07-18T15:00:00Z
tags: management
---

TL;DR scaling a dev team + code base has more to do with minimizing stupidity than with maximizing brilliance.

I've worked with some amount of C, C++, Java, Ruby, Python, Bourne Shell, PHP, HTML, Objective-C, Haskell, and Javascript, among others. I've come to imagine that the range of code quality, of an average line of code by an average engineer, using C as a sort of baseline, looks something like this:

![3]

Sure you have your exceptions with folks that tend more the top or bottom of the range, but it seems that over time, most people and most projects encounter the full range for their language...I think it was John Carmack that said: if the compiler will let you do it, it will end up in your codebase. That.

I've seen plenty of code that was intended to be a throw away prototype but turned into production code. And plenty of projects under time pressure where corners were cut to meet a deadline, and the cleanup never seemed to be the highest ROI opportunity. And even when it all went right otherwise, requirement changes might still blow big holes in the technical design leading to tough choices between moving the product forward faster in the short-term or pausing product progress in order to refactor and avoid a bunch of tech debt. The point is, shit happens, its not primarily a lack of skill or some character defect that leads to the low end of the scale being used.

Put that another way--the problem is not that there are a bunch of lazy, undisciplined idiots writing OpenSSL code (or insert your favorite punching bag project here). I'm amazed at how much time and love people put into code, be it freely given away for the good of all humanity like OpenSSL (thank you!!), or be it work for hire. No, the problem is that the low end of the range is too easy to use and its consequences are too costly...much more costly than the high end of the range is cost-savings-y, in my experience. I mean, after a few million deaths in car accidents, you start to realize that blaming the drivers only gets you so far, and maybe adding [seatbelts][1], airbags, speed limits, and other safety features is a more promising approach to saving lives.

I'm less excited about dynamic languages than I used to be, because they expand both sides of the range, which is a net negative on large teams and/or codebases. We don't need more brilliance, we need less stupidity. And we're all stupid at times--I don't mean that in a character defect sort of way, I mean that we all make regrettable decisions, for whatever reason. That's why tests, CI, linters, [static code analysis,][2] code coverage tools, etc. are important. They help add friction to the low end of the range. Languages like Haskell and Rust make it harder to screw up, which means less screwing up. If the path of least resistance (on a team/codebase) is also the path to greater code quality, code quality will go up.

[1]: https://en.wikipedia.org/wiki/Unsafe_at_Any_Speed
[2]: http://www.gamasutra.com/view/news/128836/InDepth_Static_Code_Analysis.php
[3]: https://ggr_com.s3.amazonaws.com/images/language-scale.jpg "ranges of brilliance and stupidity by language"
