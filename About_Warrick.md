# About Warrick #

"My old web hosting company lost my site in its entirety (duh!) when a hard drive died on them. Needless to say that I was peeved, but I do notice that it is available to browse on the wayback machine...Does anyone have any ideas if I can download my full site?" - A request for help at archive.org


Warrick is a utility for reconstructing or recovering a website when a back-up is not available. Warrick uses Memento TimeMaps to discover archived copies of resources. Such resources may exist at the Internet Archive, Google, or another archival organization. Warrick will download the pages and images and will save them to your filesystem. Warrick can be run through our website or as a command-line utility (directions for downloading, installing, and running are given below).

Since Warrick uses the Memento framework to assist in the recovery process, load balancing on your system is important. Memento queries the archives and search engine caches for mementos (archived resources). Since these archives and resources expect a certain amount of politeness, query limits are put into place. Running Warrick multiple times over a period of several days or weeks can increase the number of recovered files because the availability of content in the archives fluctuates. Internet Archive's repository is at least 6-12 months out of date, and therefore you will only find content from them if your website has been around at least that long. If they do not have your website archived, you might want to run Warrick again in 6-12 months.

Warrick is named after a fictional forensic scientist with a penchant for gambling. It was built as part of a research project in 2005 by Frank McCown, a Ph.D. student at Old Dominion University. In 2011, Justin F. Brunelle, another Ph.D. student from ODU, began working to adapt Warrick to utilize Memento instead of operating independently. A full release of the command-line and web interface products is expected in early 2012. You can read about the original Warrick and our experiments reconstructing websites at http://www.cs.odu.edu/~fmccown/research/lazy/. Future publications are expected to outline experimentation and the work done with the new version of Warrick that utilizes Memento.

If you would like to cite Warrick in your academic publication, please cite the following:

Frank McCown, Joan A. Smith, Michael L. Nelson, and Johan Bollen, Lazy Preservation: Reconstructing Websites by Crawling the Crawlers, Proceedings of the 8th ACM International Workshop on Web Information and Data Management (WIDM 2006), p. 67-74, 2006.

**Warrick currently does not work on Windows. A Windows version is currently being developed.**


# How It Works #

Warrick interacts with Memento TimeMaps to recover resources from archives. Memento has knowledge of the mementos available at a variety of archives, and Warrick asks Memento for a list of the archived copies of a resource. Warrick chooses the best version of the resource and downloads it to the host machine's hard drive using mcurl. mcurl is a wrapper for the cURL command.

Earlier versions of Warrick did use the Google API and lister site of the IA, but since APIs are not constant over time, Warrick has been designed to allow Memento to handle the responsibility of interacting with the archives. This allows Warrick to evolve independently of the archives and work more consistently over time.

Warrick is first given a seed URL, the base URL (e.g., http://www.foo.edu/~joe/) for the website which should be reconstructed. This URL is added to the URL queue for recovery.

Warrick first makes queries to Memento to get the indexed/cached mementos for the particular site. Requests to the TimeMaps are cached to prevent unnecessary strain on the Memento Framework during future recoveries of the same resources. Please note that multiple resources may be required to get a canonical version of a site or even page. Such constituent resources could be CSS or image files and are necessary to provide an accurate recreation of the resource representation.

Each time an HTML resource is recovered, it is parsed for links to other resources, and the links are added to the URL queue. Only URLs that are in and beneath the seed URL are recovered. So if the seed URL is http://www.foo.edu/~joe/, only URLs matching http://www.foo.edu/~joe/ are recovered.

Warrick saves the recovered resources to disk. If a resource is found in more than one web repository, Warrick saves the resource with the most recent date. Some resources, especially images or PDFs, will not have a date associated with them. If the resource is a PDF, PostScript, Word document, or other non-HTML format, then Warrick will choose the IA (canonical) version over the HTML-version of the resource.

Several files are created as "byproducts" of the recovery process. A reconstruction summary file is created that lists the URLs that were successfully and unsuccessfully recovered. Unsuccessful recovery attempts are prepended with the text "FAILED::". Here's an example:


http://ahmedalsum.net/ => Location: http://api.wayback.archive.org/memento/20101228231547/http://ahmedalsum.net/ =>	 /home/jbrunelle/public\_html/wsdl/warrick/warrick/ahmed/index.html

http://ahmedalsum.net/images/Style.css =>	 Location: http://api.wayback.archive.org/memento/20101228231608/http://ahmedalsum.net/images/Style.css =>	 /home/jbrunelle/public\_html/wsdl/warrick/warrick/ahmed/images/Style.css
etc...

The name of the summary file depends on the URL you used to start the reconstruction, or the directory the recovered files are stored in. If you used http://www.foo.edu/~joe/, the file will be named www.foo.edu.joe\_reconstruct\_log.txt.

.save files are created upon successful completion of a recovery session. This file contains information about the recovery so that unfinished or suspended recovery jobs can be resumed later. This is handy for throttling purposes or even pausing the recovery process for any period of time. The files are stored as the process ID of the last recovery run, and the name of the machine in the following format: [ID](Process.md)_[name](Machine.md).save. The contents of the file will be XML._

A file called logfile.o will be created as a way for Warrick to self-monitor its progress recoverying a particular resource. This file can be disregarded as it is just a file for the Warrick process's use.

Notice in the summary file that the file names match the URLs of the resources. If using the Windows File Names options, special characters are not allowed in the recovered file names.

Warrick will continue to recover resources until the URL queue is empty or a maximum number of requests are made. Since the query limits are now controlled by Memento, it is the Warrick user's responsibility to monitor and throttle the recovery process for politeness purposes. When using Brass to perform the recovery, the politeness and throttling is handled on behalf of the user.

Note: Warrick cannot recover web pages that were never crawled and cached; therefore, pages that are not accessible to search engines (protected by robots.txt or passwords, pages residing in the deep web, or only accessable through Flash or JavaScript) are not accessible to Warrick. Also, Warrick cannot reconstruct the server-side components or logic (CGI programs, scripts, databases, etc.) of a website. That means if the bar.php resource is recovered, it will be the client's version of the page--not the file with the PHP code inside.

Warrick now uses caching when recovering pages. If Warrick determines that the page you need has been previously downloaded to your machine, it will get the local copy of a page, first, to reduce the load on the archives' servers.

# Downloading #

Warrick is available for download here:

> - http://warrick.googlecode.com/files/warrick_v2-2.tar.gz


NOTE: If you use Warrick to reconstruct a website that you have lost, please send me an email letting me know:
warrickrecovery@googlegroups.com

We are very interested in keeping a log of websites that have been recovered with Warrick for analysis and improvement purposes.

Warrick is licensed under the GNU General Public License. Warrick is under a lot of revision and will be updated periodically, so make sure you are always running the most recent version.


# Installing #

Unzip or untar the file in a directory, say or ~/warrick. You may then need to add warrick.pl to your path or just cd to the directory where you installed it.

Warrick has been tested on a Linux platform, but should work on any Unix or Linux system. A Windows version is in development. For a more automatic installation, please run the INSTALL file provided. It can be run from the command line with "sh ./INSTALL". To test the installation, run the TEST file as "sh ./TEST". This tester will try to recover a test page and make sure all of the constituent resources are present. Please note that it is possible that resources may change for this recovery. If you think this has happened, please contant Justin F. Brunelle at warrickrecovery@googlegroups.com. If you prefer to perform a custom installation or run into problems with the auto installer, pelase see below for software dependencies to be installed.
It was written in Perl, so you need Perl 5 installed. You may also need to install several Perl modules and the CPAN module if it's not already installed.

The following need to be installed:

> - curl

> - python

> - perl

> - HTML::TagParser

> - HTML::LinkExtractor

> - HTTP::Cookies

> - HTTP::Status

> - URI

> - HTTP::Date

> - Getopt::Long


If, for some reason, the install script isn't working properly, please use cpan (http://perl.about.com/od/packagesmodules/qt/perlcpan.htm) to install the missing modules. An example of installing the HTML::TagParser library is shown below:

perl -MCPAN -e 'install HTML::TagParser'

## OSX ##
Although Warrick has not been formally or thoroughly tested in operating systems other than Linux, other Warrick users have reported success using Warrick in OSX. Additional Perl modules (other than those installed with the INSTALL file) may have to be installed, such as "Bundle::LWP". Users should contact the Warrick Google Group (warrickrecovery@googlegroups.com) for additional questions or reports of success in other operating systems.

Paul R. Alexander from Stanford University provided the following feedback:
"I ran Warrick under OSX. It worked great with the exception of some missing Perl functionality. In additional to the CPAN modules from the INSTALL file, I had to run this command:
sudo perl -MCPAN -e 'install Bundle::LWP'"

More detailed instruction has been provided by Peter Bending: http://code.google.com/p/warrick/wiki/iOS_Installation

# Usage #

Usage: warrick [OPTION](OPTION.md)... [URL](URL.md)

OPTIONS:

-dr	| --date-recover=DATE	Recover resource closest to given date (YYYY-MM-DD)

-d	| --debug	Turn on debugging output

-D	| --target-directory=D	Store recovered resources in directory D

-h	| --help	Display the help message

-E	| --html-extension	Save non-web formats as HTML

-ic	| --ignore-case	Make all URIs lower-case (may be useful when recovering files from Windows servers)

-i	| --input-file=F	Recover links listed in file F

-k	| --convert-links	Convert links to relative

-l	| --limit-dir=L	limit the depth of the recover to the provided directory depth L

-n	| --number-download=N	limit the number of resources recovered to N

-nv	| --no-verbose	Turn off verbose output (verbose is the default)

-nc	| --no-clobber	Don't download files already recovered

-xc	| --no-cache	Don't use cached timemaps in the recovery
process

-o	| --output-file=F	Log all output to the file F

-nr	| --non-recursive	Don't download additional resources listed as links in the downloaded resources. Effectively downloads a single resource.

-V	| --version	Display information on this version of Warrick

-w	| --wait=W	Wait for W seconds between URLs being recovered.

-R	| --resume=F	Resume a previously started and suspended recovery job from file F
-B  			Keep the branding or headers from the archives from which the memento was recovered.
-nB			Remove the branding from the archives (this is the default)
-a | --archive=ia|wc|ai|loc|uk|eu|bl|b|g|y|aweu|nara|cdlib|diigo|can|wikia|wiki]
> Specify the archive to recover resources from. Specify	a single archive. Options are [Archive|Web Citation|Archive-It|Library of Congress|National Archives of UK|ArcheifWeb|British Library|Bing|Google|Yahoo|Archiefweb|nara|CDLib|Diigo|Canadian Archives|Wikia|Wiki](Internet.md)

Recovering entire websites (recursive recovery) is the default Warrick operation. To limit the recovery to a single page, please use the -nr flag. Suppose the website foo.edu/~joe/ was suddenly lost. This is how to run Warrick to reconstruct the entire site using optional parameters -nv and -o (quotes around the URL are usually only neccessary when it contains the "&" character):

> - warrick.pl -nv -o warrick\_log\_foo.txt "http://foo.edu/~joe/"


-nv : Execute without verbose output

-o : Put all warrick output in a log file

A reconstruction summary file called foo.edu.joe\_reconstruct\_log.txt would be created listing the URLs that were recovered. Because Warrick could run for more than 24 hours, you may want to run it as a background process (adding a & to the end of the command in Linux/Unix). Also, you may want to break the recovery process into multiple sessions. For example

> - warrick.pl -nv -o warrick\_log\_foo.txt -n 100 "http://foo.edu/~joe/"


-nv : Execute without verbose output

-o : Put all warrick output in a log file

-n : Limits the program to 100 recovered files

This will stop the recovery after 100 files and store the state of the recovery as [ProcessID](ProcessID.md)_[ServerName](ServerName.md).save. To resume the recovery, you should use the -R flag:_

> - warrick.pl -R [ProcessID](ProcessID.md)_[ServerName](ServerName.md).save_


-R : Resume recovery from the reference save file
If you want to run Warrick again on subsequent days to find additional files, you would use the "no clobber" option (-nc) so the files already recovered would not be downloaded again. The downloaded files would be re-processed and parsed for links to missing resources. This is how you might run Warrick using the no clobber option:

> - warrick.pl -D Joe\_Recovery -nc -o warrick\_log\_foo.txt "http://foo.edu/~joe/"


This would store the recovery in the local directory Joe\_Recovery



If you would like Warrick to ignore the case of the URLs it recovers, use the -ic (ignore-case) option. This is very useful when reconstructing websites that were housed on a Windows server. The Windows filesystem is case-insensitive, so the URL http://foo.org/bar and http://foo.org/BAR refer to the same resource on a Windows web server. Google may have this URL stored as one way and Yahoo another. Warrick will by default treat these as separate URLs although they really refer to the same resource. If the -ic option is used, Warrick will treat these URLs as one and the same. Example:

> - warrick.pl -nr -ic http://foo.edu/~joe/


To recover a resource at a specific date, use the -dr option and specify the begin and end dates (inclusive) in this format: yyyy-mm-dd separated by a colon. For example, to recover only resources archived closest to Feb 1, 2004

> - warrick.pl -dr 2004-02-01 http://www.cs.odu.edu/


Be careful when running Warrick: some archives may monitor traffic to enforce politeness and crawling. Google monitors traffic through www.google.com, and if they suspect you are making automated requests, they will "blacklist" your IP address and will not respond to queries for as long as 12 hours. If Warrick detects that it has been blacklisted, it will sleep for 12 hours and then pick up where it left off. In my experiments, Google has detected me after about 100-150 requests. We cannot be held responsible if Google or any other archive blacklists your IP address. To only recover from a single archive (in this case, the Internet Archive), please use the -a option:

> - warrick.pl -a ia http://www.cs.odu.edu

# Viewing Reconstructions #

After reconstructing a website, you may want to view the files that were recovered in your browser. You can open the files directly into your browser or double-click on them to launch the default application associated with the files. The default application is normally determined by the file's extension. If the file extension is .html, the browser is usually the default application. If the extension is .gif, a graphics application may be the default application.

In order to navigate the reconstructed website from your hard drive by clicking on links, you will likely need to convert absolute URLs to relative ones and rename some of the files. For example, if you are viewing a web page that has a link to http://foo.org/index.php?nav=1, clicking on the link will cause the browser to load the URL, not the index.php?nav=1 file on your hard drive. To view the actual file, the absolute link will need to be converted to a relative one, and the file extension may also need to be changed. Warrick can do this for you. Please note that Warrick does not handle relative link conversion of anchor tags written by JavaScript or any other client-side code.

The -k option will convert all absolute URLs to relative URLs (without changing any file names). For example, the URL pointing to "http://foo.edu/~joe/car.html" will be converted to point to the car.html file you just recovered (e.g., "../car.html").

Example:

> - warrick.pl -k http://foo.org/

# Donations #

If you are thankful for getting back your lost website and would like to make a donation (of any amount), please consider giving to the Internet Archive. They are a non-profit organization, so your donation is tax deductible. Plus it's easy to donate on-line using PayPal. If you do make a donation, please inform the Internet Archive that the dontain was prompted by your use of Warrick.

We also appreciate any feedback about your recovery experience. If you would like to provide credit to the project, please cite the project's many publications.


# Future Enhancements #

The following are enhancements I am planning on making to Warrick and Brass. I do not yet have a time frame to make the enhancements.

> - Detect soft 404s - Ignore pages that are cached in a search engine that appear to be soft 404s.

> - Work on a Windows command-line version