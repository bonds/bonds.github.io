---
title: "Natural: a ruby gem for natural language search"
date: 2012-03-09T10:59:00Z
tags: code
---
<img alt="image" height="191" src="https://ggr_com.s3.amazonaws.com/images/natural_on_github.png" width="512" />
<br/>

When I started work on [DishFu.com][1] (one of my code playgrounds...its 
something like Yelp) a couple years ago I wanted to support natural 
language search so that, instead of clicking lots of checkboxes to 
search for the best burrito in my zip code, I could just ask "what is 
the best burrito near me" and get the answer. At the time (and even now) 
I didn't find a ruby library that made this easy to do, so I thought I'd 
take a stab at it.

[Natural][2] is the result of the aforementioned stab and its available 
on github. Checkout [Fantastical][3] and [Siri][4] for inspiration and 
two good examples of why natural language search is neat and how it 
enhances usability. Natural works by parsing the input text, looking for 
every possible match in its vocabulary, scoring all the possible 
combinations of matches, and choosing the highest scoring combination. 
One can achieve a similar effect (and faster) by enumerating a bunch of 
regular expressions and trying to match against the most complicated 
regular expression first and working your way down until you find a 
match, but I wanted a library that could also glean partial meanings and 
choose between different potential matches in a more flexible way. 
[Suggestions][5] and pull requests welcome.

 [1]: http://dishfu.com
 [2]: https://github.com/bonds/natural
 [3]: http://flexibits.com/
 [4]: http://www.apple.com/iphone/features/siri.html
 [5]: https://github.com/bonds/natural/issues
