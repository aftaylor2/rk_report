                           Rootkit Reporter

Andrew Taylor <ataylor> (at) phr3ak (dot) org (Developer)

rk_report is a perl script that scans the output of the 3rd party 
applications chkrootkit (http://www.chkrootkit.org/) and rkhunter.
If a rootkit or other infection is discovered rk_report will send 
an email alert.

CONFIGURATION:
You should edit rk_report to match file locations on *YOUR* 
system. You must also provide a valid email address for the admin.

 
---------------------------------------------------------------------

USAGE:
------

[user@host]# ./rk_report

Note: You may wish to add the script as a cronjob.

Package Contents
----------------

rk_report
README.md
LICENSE


System Requirments
------------------

chkrootkit - To scan system for rootkits<br />
rkhunter - To scan system for rootkits<br />
perl - To run the rk_report script<br />
sendmail - To alert the admin via email<br />

Acknowledgements
---------------


ChangeLog
---------


Upcoming Features
-----------------
SMS (Text Message) Notifications
