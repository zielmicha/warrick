Warrick Version 2.0 "The website reconstructor"

# Introduction #

Created by Frank McCown at Old Dominion University - 2006

Modified by Justin F. Brunelle at Old Dominion University - 2011
warrickrecovery@googlegroups.com



# Details #

Running ./INSTALL at the command line should install these dependencies.
To test the installation, run ./TEST. This will recover a web
page and compare it to a master copy.

For information on running Warrick, run at your command line:
> `perl warrick.pl --help`

This version of Warrick has been redesigned to reconstruct lost
websites from the Web Infrastructure using Memento. For more
information on Memento, please visit http://www.mementoweb.org/.

# Help improve Warrick #

We want to know if you have if you have used Warrick to
reconstruct your lost website.  Please e-mail me at jbrunelle@cs.odu.edu

# Recovery Byproducts #

This program creates several files that provide information or
log data about the recovery. For a given recovery RECO\_NAME, we
will create a RECO\_NAME\_recoveryLog.out, PID\_SERVERNAME.save,
and logfile.o. These are created for every recovery job.
RECO\_NAME\_recoveryLog.out is created in the home warrick
directory, and contains a report of every URI recovered,
the location of the recovered archived copy (the memento), and
the location the file was saved to on the local machine in the
following format:
ORIGINAL URI => MEMENTO URI => LOCAL FILE
Lines pre-pended with "FAILED" indicate a failed recovery of
ORIGINAL URI
PID\_SERVERNAME.save is the saved status file. This file is
stored in the recovery directory and contains the information
for resuming a suspended recovery job as well as the stats
for the recovery, such as the number of resources failed
to be recovered, the number from different archives, etc.
logfile.o is a temporary file that can be regarded as junk.
It contains the headers for the last recovered resource.

If you would like to assist the development team in refining
and improving Warrick, please provide each of these files to
the development team by emailing them to warrickrecovery@googlegroups.com.

Thank you for your help.