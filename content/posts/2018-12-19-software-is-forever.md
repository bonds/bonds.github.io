---
title: Calculate the Full Price of That New Tech
date: 2018-12-19T19:52:00Z
tags: leadership
---
Next time you get the urge to try out some new tech in production please 
remember this: 5 years from now, long after you got bored with it, some poor sap 
is going to be stuck fixing bugs in that new tech code you committed, because no 
one ever took the time to rip it out, and something in production depends on it.  You've just introduce tech debt that will most likely be wasting someone's time 
for many years to come.

I'm not saying never try new tech, I'm just saying, pay for it: write the new 
feature in the old tech FIRST, to keep yourself honest, then in the new tech, 
and deploy and maintain each of them on 50% of the servers. If the old tech 
wins, you up the capacity on the old tech servers, turn off the new ones, rip 
out the new code, and you've got no tech debt--experiment paid for in full. If 
you don't do that you're Trojan horsing it in--it sounds innocent enough to just 
upgrade one service to try out the new tech, but then what?

If the new tech 'wins', hold on a second and make sure you've thought through 
the implications...if the new tech wins does that mean you're committed to 
porting 10M lines of code in the old tech to the new tech? What will that cost?  What benefits will you get? Or are you instead committing to slowly port things 
over taking 10 years while maintaining +1 stacks increasing the cost of new 
feature development, maintenance, infrastructure, recruiting, training, bug 
fixes, troubleshooting, etc. Is it worth it? Really? $10M invested across 10 
years in porting and +1 stack costs to achieve a 10% productivity boost once 
you're done?  If the math doesn't work, maybe its not a good idea. And maybe do 
the math before starting the project.

