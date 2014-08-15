#!/usr/bin/perl
##########################################################
# rk_report version 0.0.1                                #
# By Andrew Taylor ataylor [at] phr3ak [dot] com         #
##########################################################
#  Executes rkhunter and chkrootkit then scans the       #
#  output and emails any positive results to the admin   #
##########################################################

use strict;
use Sys::Hostname;
use Socket;

my $file_data;
my $status;
my $host = hostname;
my($address)=inet_ntoa((gethostbyname(hostname))[4]);

my $uptime = qx(uptime);
my $users = qx(users);

############### EDIT SETTINGS ###################
my $rkhunter = "/usr/bin/rkhunter";
my $rkhunter_log = "/var/log/rkhunter.log";
my $chkrootkit = "/usr/sbin/chkrootkit";
my $sendmail = "/usr/lib/sendmail";
my $tmp_file = "/tmp/rk_report.txt";
my $string = "INFECTED";
my $email_admin = "root\@localhost"; # Email address of admin
my $subject = "ROOTKIT DETECTED on $host";
###################################################

#### Execute rkhunter and chkrootkit to ensure recent results
print "Executing rkhunter...\n";
qx($rkhunter --cronjob --report-warnings-only);
qx(cp $rkhunter_log $tmp_file);
print "Executing chkrootkit...\n";
qx($chkrootkit >> $tmp_file);

#### Place file contents into an array ####
open (RESULTS, $tmp_file) or die "Unable to open file: $tmp_file\n$!";
my @file_data;
@file_data = <RESULTS>;
close(RESULTS);

### Delete temporary file containg scan results
qx(rm $tmp_file);

#### Search the array for the Infection string ####
foreach $file_data(@file_data) {
    if (index($file_data,$string) ge 0) {
	$status = 1;
	print "INFECTION FOUND!\n";
    }
}

if ($status eq 1) {
#### SEND EMAIL ####
    print "Sending email to $email_admin\n";
open(SENDMAIL, "|$sendmail -oi -t") or die "Cannot open $sendmail: $!"; 
print SENDMAIL "From: no-reply\@$host\n";
print SENDMAIL "To: $email_admin\n";
print SENDMAIL "Subject: $subject\n\n";
print SENDMAIL "POSSIBLE ROOT KIT DETECTED on $host\n\n";
print SENDMAIL "IP Address: $address\n";
print SENDMAIL "Host Uptime: $uptime";
print SENDMAIL "Logged In Users: $users\n";
#print SENDMAIL "@file_data\n";	# Send complete scan results
close(SENDMAIL);
exit 0;

} else {
    print "No Infection Found!\n";
    exit 0;
}

exit 1;
