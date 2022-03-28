---
title: How to Restart PostgreSQL While Developing a Rails App
date: 2012-01-13 11:24
tags: code
---
<img alt="image" height="153" src="/images/ran-out-of-connections.jpg" width="512" />
<br/>

While developing a Rails apps using PostgreSQL (unlike MySQL) I often 
run out of db connections and see errors like

> <div>
>   <p>
>     FATAL: remaining connection slots are reserved for non-replication superuser connections
>   </p>
> </div>

and when I do, my Rails app stops working. Restarting Postgres fixing 
the problem, but it was harder to restart postgres that I expected. 
Here's how I do it.

To restart PostgreSQL I added a function to my ~/.bash_profile file:

<pre>restart postgres pgr() { kill `ps -ef | grep postgres | grep -v | grep | awk '{print $2}'` }</pre>

After saving and restarting Terminal, running 'pgr' will find all the 
postgres process and kill them. Once launchd notices postgres is down it 
restarts it because I setup launchd to keep postgres running no matter 
what. If you don't have postgres setup to stay running, you would need 
to start postgres whatever way matches your setup. I tried a number of 
different solutions before I arrived at this one:

1. running 'pg_ctl -D <path to db> restart' would cause postgres to try 
and restart, but it would timeout unsuccessful
2. logging out then logging back in again works (since I'm running 
postgres as a 'personal' launch agent, it starts and stops with my login 
and logout) but that's terribly disruptive to my work
3. killall would kill some, but not all of the errant postgres 
processes

I'm running OSX Lion, PostgreSQL 9.1.2, Rails 3.1.3, Ruby 1.9.2-p290. I 
Googled the hive-mind for a better answer, after all, when developing a 
rails app using MySQL I had no such problem. It seems others have run 
into this, but I didn't find a better solution. I have a nagging feeling 
there's some setting I could add to my database.yml file to get 
PostgreSQL to behave well in my development environment and obviate the 
need for my PostgreSQL restarting shenanigans, but I've not yet 
discovered it.
