---
title: How To Post Your Dynamic Internal IP To DynDNS From Your Windows Machine
date: 2009-10-09T12:37:00Z
tags: code
---
![2]

I looked around for an easier way to post an **internal** IP to DynDNS, 
but I didn't find one. Scripting to the rescue.

If you have a paid account at DynDNS (may work for free ones too, I'm 
not sure), you can update a DNS entry by hitting a URL like this:

> <div>
>   <p>
>     http://login:password@members.dyndns.org/nic/update?hostname=host.domain.com&myip=10.0.0.1&wildcard=NOCHG&mx=NOCHG&backmx=NOCHG
>   </p>
> </div>

So, to update your DNS entry, you just need to [get your IP alone in a 
variable][1] that a batch file can use, then setup a task to request 
that URL every so often. In more detail, the steps are:

1.  Install Cygwin including the 'curl' package. Curl allows you to make 
web requests from the command line.
2.  Create a batch file that gets your IP then makes the DynDNS update 
request (see below).
3.  Create a new scheduled task through the Windows Control Panel: setup 
multiple schedules so it runs the batch file you created in step #2 at 
startup, login, and when the machine is idle 60 minutes.

The batch file is like so, be sure to update the curl location, DynDNS 
login, password, and hostname info before you use it:

<pre>:: Script from: http://www.ericphelps.com/batch/samples/ip.txt
@echo off
cd %temp%
:: Make a line fragment "temp.txt"
echo e 100 "call temp2.bat "&gt; script
echo rcx&gt;&gt; script
echo f&gt;&gt; script
echo n temp.txt&gt;&gt; script
echo w&gt;&gt; script
echo q&gt;&gt;script
debug &lt; script &gt; junk
del script
:: Make the working file "temp2.bat"
echo shift&gt; temp2.bat
echo shift&gt;&gt; temp2.bat
echo shift&gt;&gt; temp2.bat
echo shift&gt;&gt; temp2.bat
echo shift&gt;&gt; temp2.bat
echo shift&gt;&gt; temp2.bat
echo set IP=%%9&gt;&gt; temp2.bat
:: Run the command that finds the IP and create "temp1.bat"
copy temp.txt temp1.bat &gt; junk
ipconfig.exe | find "IP Address" | find /v " 0.0.0.0" &gt;&gt; temp1.bat
:: Run the temp1.bat, which runs temp2.bat, which sets the IP variable
call temp1.bat
:: Remove temporary files
del temp1.bat
del temp2.bat
del temp.txt
del junk
:: Display the result
echo Your IP is %IP%
:: Send to DynDNS
c:\cygwin\bin\curl "http://login:password@members.dyndns.org/nic/update?hostname=host.domain.com&myip=10.0.0.1&wildcard=NOCHG&mx=NOCHG&backmx=NOCHG"
</pre>

 [1]: /how-to-get-your-ip-and-only-your-ip-in-windows.html
 [2]: https://ggr_com.s3.amazonaws.com/images/UpdateIP.bat-screenshot.jpg

