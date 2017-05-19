Rootkit Reporter
===========
Andrew Taylor < ataylor@phr3ak.com >

rk_report is a perl script that scans the output of the 3rd party 
applications chkrootkit and rkhunter. If a rootkit or other infection 
is discovered rk_report will send an email alert.

CONFIGURATION:
===========
You should edit rk_report to match file locations on *YOUR* 
system. You must also provide a valid email address for the admin.


System Requirments
===========

chkrootkit - To scan system for rootkits<br />
rkhunter   - To scan system for rootkits<br />
perl       - To run the rk_report script<br />
sendmail   - To alert the admin via email<br />
