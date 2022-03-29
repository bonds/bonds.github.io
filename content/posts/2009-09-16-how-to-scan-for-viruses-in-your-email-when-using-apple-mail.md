---
title: How To Scan For Viruses in Your Email When Using Apple Mail
date: 2009-09-16T14:10:00Z
tags: code
---
![9]

There's more than way to go about it, but I prefer using the open source 
ClamAV and a script that runs to scan each email as it comes in.

**Setup ClamAV**

1.  Install [ClamAV][1]. I used [MacPorts][2] to install it: 
`sudo port install clamav`
2.  Make sure all the ClamAV binaries are in your PATH. Chances are 
if you're using MacPorts, you've already taken care of that.
3.  Configure freshclam and clamd. Since I used MacPorts to install 
ClamAV, this consisted of...
4.  rename the example conf files in /opt/local/etc: `mv 
example-freshclam.conf freshclam.conf;` `mv example-clamd.conf 
clamd.conf`
5.  read the conf files and edit them as appropriate, then add the line 
`NotifyClamd /opt/local/etc/clamd.conf (`substituting the full path to 
your clamd.conf file) to the end of freshclam.conf so that clamd knows 
about it when freshclam has updated the virus definitions
6.  run freshclam to see if it works
7.  notice that it doesn't work because it needs permissions to certain 
directories; `sudo chown -R <clamav user> <directory>`...the directory 
you need to update will be clear based on the error message, the user 
that freshclam and clamd run under is configured in the conf files. In 
the MacPorts case its 'clamav'.
8.  rinse and repeat until freshclam works
9.  run clamd to see if it works
10. fix its permissions too
11. run clamdscan to check that it can scan some files using clamdscan
12. Create [launchd][3] items for freshclam and clamd. Freshclam 
should run every 168 hours or so. Clamd should run all the time.
I recommend using [Lingon][4] to configure your launchd items.
13. Reboot. Check to see that clamd is running. Fix it if its 
not.

**Setup Growl**

1.  Install [Growl][5].
2.  Install GrowlNotify. It's in the Extras folder of the Growl 
installer.
3.  Make sure GrowlNotify is in your PATH.

**Setup Mpack**

1.  Install Mpack. With MacPorts its: `sudo port install mpack`
2.  Make sure Mpack is in your PATH.

**Setup the antivirus script**

1.  Download the [antivirus script][6] I updated (fixed it to work with 
Snow Leopard, added Growl support, removed Stuffit support). A big 
thank you to the [original authors][7]!
2.  Move the script to your ~/Library/Scripts directory.
3.  Edit the script, updating the configuration options at the top of 
the file.
4.  Create a local mail folder called 'Infected' in Apple Mail.
5.  Create a rule in Apple Mail that runs the script on all email 
messages.
6.  Try emailing yourself a [test virus][8] and verify that your 
antivirus script sends a Growl alert and moves the message to the 
infected folder.

 [1]: http://www.clamav.net/
 [2]: http://www.macports.org/
 [3]: http://developer.apple.com/macosx/launchd.html
 [4]: http://sourceforge.net/projects/lingon/files/
 [5]: http://growl.info/
 [6]: http://ggr_com.s3.amazonaws.com/VirusChecker.scpt
 [7]: http://creativeeyes.at/tools/clamav
 [8]: http://www.eicar.org/anti_virus_test_file.htm
 [9]: https://ggr_com.s3.amazonaws.com/images/apple-mail-antivirus-rule.jpg
