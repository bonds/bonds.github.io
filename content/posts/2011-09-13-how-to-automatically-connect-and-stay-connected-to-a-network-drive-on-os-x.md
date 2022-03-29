---
title: How to Automatically Connect and Stay Connected to a Network Drive on OS X
date: 2011-09-13T18:39:00Z
tags: code
---
![8]

I keep my music and my photos on a server at home. Whenever I'm home I 
want all of my shares to be accessible automatically so I can launch 
iTunes and iPhoto without needing to do anything first (i.e. I don't 
want to click anything to mount the drives before I start listening to 
[Adagio for Tron][1]). Here's how I pulled it off.

The short version: I run a script that checks whether any mounts are 
missing and if possible it restores them. Here's the script:

<pre>#!/usr/bin/env ruby

require 'ruby-debug'
require 'dnssd'
require 'timeout'

login     = 'login'
password  = 'password'
host      = 'fileserver-computer'

shares = [
  'Music',
  'Photos'
]

def file_server_online?(host)
  begin
    service = DNSSD::Service.new
    timeout 3 do
      service.query_record "#{host}._afpovertcp._tcp.local", DNSSD::Record::SRV do |record|
        # FIXME: a valid record may be returned even when the server is missing, not sure...
        # I only saw timeouts in that case
        return true if record
        break
      end
    end
  rescue Timeout::Error
    return false
  end
end

shares_to_mount = shares - `mount`.scan(/on (.*) \(/).flatten.select {|a| a =~ /^\/Volumes\//}.map {|a| a.sub('/Volumes/','')}
if shares_to_mount.size &gt; 0 && file_server_online?(host)
  shares_to_mount.each do |share|
    Dir.mkdir("/Volumes/#{share}") if !File.exists?("/Volumes/#{share}")
    `mount_afp -s afp://#{login}:#{password}@#{host}.local/#{share} /Volumes/#{share}`
  end
end</pre>

I run it once a minute using [launchd][2] for which there's a [good 
GUI][3]; and here's[ a tip in case you're using RVM][4]. If you want to 
try this at home, you'll also need to install the gems 'required' at the 
top of the script. There are a number of other ways to achieve a similar 
effect, but I had trouble getting them to work:

1.  [Mount a share at login][5]. Judging by the number of discussions 
that reference this technique (and its cousins) it would seem popular, 
but it didn't quite do what I wanted--each time my machine woke up from 
sleep or my wifi connection was interrupted, I'd lose my mounts and 
would need to manually remount them (or logout and login again).
2.  <Use the automount feature of OSX>. This sure looked promising, but 
I found it to be unreliable in practice. Sometimes my mount would be 
there, sometimes it would not, sometimes it was there but no files 
appeared when I browsed...
3.  Detect when I connect to my home network, run a mounting script then 
(using [SideKick][6]). This solution got a bit closer--it reconnects my 
shares after I wake from sleep or my network connection was otherwise 
interrupted, but a loss of connection to my file server was not always 
proceeded by a loss of connection to the network, so there were plenty 
of times when I was still forced to manually connect to my drives.
4.  Use an app that does what my script does: detect when my file server 
is accessible and restore the connections to it as needed. 
[BonjourMounter][7] does just that, but I found it to be unreliable on 
Lion. A Lion compatible version is in the works, but after waiting a 
couple months, I decided to take matters into my own hands.

That's all folks, thanks for stopping by! 

**Updated on September 23, 2011: **

I'm finding Bonjour to be a bit flaky...there are plenty of 
times I can ping and mount my NAS, but it won't show up in a Bonjour search. 
In light of that, I changed file\_server\_online() to use ping:

<pre>def file_server_online?(host)
  ping_count = 1
  result = `ping -q -c #{ping_count} #{host}`
  if ($?.exitstatus == 0)
    return true
  else
    return false
  end
end</pre>

 [1]: http://www.amazon.com/Adagio-For-Tron/dp/B004EIAPXQ/ref=sr_1_1?ie=UTF8&qid=1315965192&sr=8-1
 [2]: http://en.wikipedia.org/wiki/Launchd
 [3]: http://itunes.apple.com/se/app/lingon-3/id450201424?ls=1&mt=12 "Lingon in the App Store"
 [4]: http://stackoverflow.com/questions/2398722/script-executes-successfully-in-commandline-but-not-as-a-cronjob
 [5]: http://www.ehow.com/how_4549984_mount-remote-volume-startup-mac.html
 [6]: http://oomphalot.com/sidekick/
 [7]: http://bonjourmounter.gestosoft.com/en/
 [8]: https://ggr_com.s3.amazonaws.com/images/automount_screenshot.jpg
