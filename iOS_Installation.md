# Introduction #

While Warrick was neither developed nor tested on iOS systems, many users have requested assistance with iOS installations.
Peter Bending recently provided a detailed instruction set on how to install Warrick on iOS systems to remedy the lack of support in this area.


# Details #

Follow this and you will install warrick under OSX and it will work:

First install Xcode developer tools https://developer.apple.com/xcode/
This will give you access to all the resources you need.

Download and unpack or un zip warrick to your "macintosh HD" which is the root "/" .

After unpacking you will get a folder called "warrick2"
This now resides at "/warrick2"

open the terminal and enter (the about warrick files tell you to do this):
sudo perl -MCPAN -e 'install Bundle::LWP'

After that has finished in terminal type:
cd /warrick2

now in the terminal enter (you will have to give your password):
sudo su root

Your currsor will change to "sh-VERSION NUMBER#" my case sh-3.2#

type into the terminal:
sh ./INSTALL

You will get something like this (don't worry about the errros):
./INSTALL: line 3: apt-get: command not found
./INSTALL: line 4: yum: command not found
Going to read '/var/root/.cpan/Metadata'
> Database was generated on Sun, 12 May 2013 10:41:02 GMT
HTML::TagParser is up to date (0.20).
Going to read '/var/root/.cpan/Metadata'
> Database was generated on Sun, 12 May 2013 10:41:02 GMT
HTML::LinkExtractor is up to date (0.13).
Going to read '/var/root/.cpan/Metadata'
> Database was generated on Sun, 12 May 2013 10:41:02 GMT
HTTP::Cookies is up to date (6.01).
Going to read '/var/root/.cpan/Metadata'
> Database was generated on Sun, 12 May 2013 10:41:02 GMT
HTTP::Status is up to date (6.03).
Can't locate object method "install" via package "URI" at -e line 1.
Going to read '/var/root/.cpan/Metadata'
> Database was generated on Sun, 12 May 2013 10:41:02 GMT
CSS is up to date (1.09).
Can't locate object method "install" via package "HTTP::Date" at -e line 1.
Going to read '/var/root/.cpan/Metadata'
> Database was generated on Sun, 12 May 2013 10:41:02 GMT
Getopt::Long is up to date (2.39).
./INSTALL: line 16: apt-get: command not found
./INSTALL: line 17: yum: command not found
./INSTALL: line 19: apt-get: command not found
./INSTALL: line 20: yum: command not found


Now you can run warrick!.

Example enter replace example.com :
perl warrick.pl -k -n 100 http://EXAMPLE.COM

This downloads the first 100 files and changes the links to local values...

The downloaded files will be in:
/warrick2/httpEXAMPLE.COM