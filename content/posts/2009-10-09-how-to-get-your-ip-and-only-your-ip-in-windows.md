---
title: How To Get Your IP and ONLY Your IP in Windows
date: 2009-10-09T12:30:00Z
tags: code
---
<img alt="image" height="105" src="https://ggr_com.s3.amazonaws.com/images/getIP.bat-screenshot.jpg" width="512" />
<br/>

Sometimes you need to know your Windows machine's IP. For example, if 
you would like to [update your dynamic DNS entry from a script][1] file. 
Here's a hack that gets the job done.

This is from [someone good with windows scripts][2], updated with some 
extra 'shifts' to get it to work under XP. Check out the link for an 
explanation. Save this in a batch file, I call mine 'GetIP.bat':

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
pause
</pre>

 [1]: /how-to-post-your-dynamic-internal-ip-to-dyndns-from-your-windows-machine.html
 [2]: http://www.ericphelps.com/batch/samples/ip.txt
