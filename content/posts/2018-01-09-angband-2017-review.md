---
title: Angband 2017 Review
date: 2018-01-09T16:32:00Z
tags: games
---

![Angband screenshot](https://quisquous.s3.amazonaws.com/angband.png)

A couple months ago my wife got locked out of Steam while trying to remember her 
password and we had to give up on a rare chance to play some Don't Starve 
Together, um, together. It got me thinking...DRM is a pain in the butt 
sometimes. I wonder what FOSS games are out there.

Turns out there are some rather good ones available, unless your aim is showing 
off how much you can spend on a game system. That's not my aim--a while ago I 
realized that the best gameplay is not coming out of the game industry's big 
budget blockbuster hit machines, but from indies plying their art as best they 
can.

Which brings me to [Angband][1], an old, and I mean old, roguelike. Turns out 
there's a package for an older version on OpenBSD, the latest builds ok on 
OpenBSD too, and its a lot of fun. Seeing as its under continuous-ish 
development, and seeing as its 2018, it seemed like a good time to write a 
review of the game as of 2017 for my 5 loyal, non-bot readers. Hi readers!

In Angband, as with other roguelikes and other games inspired by D&D and/or
Tolkien, you start by creating a character and then you enter a dungeon full of
10x10 rooms with orcs guarding treasures. Ok, most of the rooms aren't 10x10,
but there are orcs and treasures. And if you die you have to start completely
over.

Anyhow, in Angband you're trying to defeat Morgoth. He's on the 100th floor and
its said he's pretty tough. I'm not sure what he's doing down there--maybe
watching Netflix. I started on the 0th floor, in town, where I had just figured
out how to walk using the arrow keys when I tried to walk past a dog and
quickly found myself staring at a gravestone and various stats on my pitiful
state, having just died. Reminded me of my first outing in Ultima Online, where
my newly minted, ultimate badass warrior get offed by a bunny right outside of
town. Morale of the story: stay away from the animal life when starting games, 
especially near town.

On my 10th life or so I started to get the hang of staying away from dogs in 
town, going down the stairs, and fighting the less powerful beasts that roam 
level 1 of the dungeon. Skimming the help game me an idea for what keys to 
press, and I soon figured out how to zap wands, use staves, and upgrade my armor 
and weapons. By my 20th life I managed to level up a bit and go as far as the 
10th floor. Feeling cocky I started diving a lot deeper using scrolls of Deep 
Descent, got my ass handed to me, pondered my sins, and went back to grinding 
for equipment and experience so I could survive the lower levels.

This game, in a nutshell, uses the classic game loop of: fight, level up, unlock 
new abilities through experience and equipment, fight tougher things, repeat. At 
first combat is very basic. Then magical creatures start freezing you, and you 
need a resistant to that before you can safely progress. Then they start 
poisoning you, and you need a resistance to that, etc. Just when you think 
that's all there is to it, you get rooms full of monsters that are *way* too 
tough for you (aka vaults), and you learn about the importance of stealth, 
teleporting away, and all those spells, wands, and abilities you never had any 
use for before. Its a lot of fun uncovering each new puzzle, but its a bit of a 
grind when you die to level all the way back up to facing something new again.  
I'm told there are ways to cheat if you don't like that sort of gameplay, and 
heck, its FOSS so you can modify the game however you want, but there no 
bragging rights for cheaters, so there.

First I played v3.3.2 because there's a package for it on OpenBSD 6.2. Then I 
[compiled v4.1.2 from source][2]...the maintainer has filed tickets against some 
[OpenBSD compiling challenges][3], but I was ok with the basic text version, and 
that compiled and ran fine.

I noticed a lot of differences between the versions. In 3 I spent a fair amount 
of time grinding for money in order to buy upgraded equipment...more than half 
the wands and staves I found I never used because I wanted the money instead. In 
4 items have no monetary value (if you use the default starting options) and the 
stores have less cool stuff to buy, so I spent less time running back and forth 
to town and more time in the dungeon. I also used a lot more of the equipment I 
found instead of getting rid of it. Magical items switched from a seemingly 
fixed list of item powers to a more flexible 'rune' based system where item 
powers can be mixed in infinite ways.

The cosmetics got an upgrade too--spells animate, with dragons breathing ASCII 
fire at you and wands sending out dashes of death towards molds sleeping on the 
floor nearby. Town is no longer rectangle shaped, and many of the dungeon rooms 
have more interesting shapes as well.

I really like the turn-based nature of the game. Its easy to put down and 
pickup. I have kids now, so being able to drop my game at a moment's notice to 
pay attention to the evening's crisis is a big advantage over most games that I 
would otherwise tend to play (e.g. TF2, Don't Starve Together). The text UI took 
a little getting used to, but its nice how fast it runs on my old laptop and 
there's something neat about filling in some details with my imagination instead 
of with polished graphics. I mean, the LoTR movies were great, but the books 
were great too, and they left a lot more room for my mind to bring the story to 
life in its own way.

My wife wonders why I haven't rage quit after dying 100 times, including the 
recent death of a level 30 high-elf mage (sad face)...and I do keep putting this 
game down, but then after a while I pick it up again. I guess that means its 
good. The hard part for me is being patient. Its not that hard a game, until I 
start blasting through stuff without paying enough attention and suddenly I'm 
dead and have to start over after 10 hours of leveling up a level 30 high elf 
mage.

Deep breath. One turn at a time. The fastest way to play is to play slow.

[1]: http://rephial.org/
[2]: http://trac.rephial.org/wiki/Compiling
[3]: http://trac.rephial.org/search?q=openbsd
