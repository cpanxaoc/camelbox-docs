#summary Step-by-step instructions for installing Camelbox
#labels Phase-Deploy,Featured

== Download the Installer ==
http://camelbox.googlegroups.com/web/camelbox-featured_downloads.jpg

The most current installer is always available in the *Featured Downloads* section of the [http://code.google.com/p/camelbox/ Camelbox home page].  Click to download the installer using your web browser, save the installer to your hard drive, then run the installer by double-clicking on it in Windows Explorer.

== Run the Installer ==

Once you run the installer, the first screen you will see is the startup banner screen, showing you the Camelbox logo and the current release logo:

http://camelbox.googlegroups.com/web/camelbox-startup_banner-30Jul2008.jpg

The next screen you will see is the license screen:

http://camelbox.googlegroups.com/web/camelbox-license_screen-30Jul2008.jpg

If you agree to the license(s) shown on that screen, press the *I Agree* button to continue.  The next screen is the download mirror selection screen:

http://camelbox.googlegroups.com/web/camelbox-mirror_selection-30Jul2008.jpg

The repository for Camelbox packages is hosted on [http://code.google.com Google Code].  This is the URL shown in the screenshot.  

You could also create a local mirror of all of the Camelbox packages, in order
to perform multiple installs at your site or location.  In that case, you would
use this screen to point to your local server and the directory on your server
containing the downloaded packages.  You can easily create a local mirror by clicking on the "_Keep downloaded archive files after installer exits?_" checkbox.

Click the *Next >* button to continue on to the Package Selection screen.

http://camelbox.googlegroups.com/web/camelbox-package_selection-30Jul2008.jpg

This is the screen where you choose the actual packages you wish to install.

===Install Types Explained===
 # "The Starter" - A basic install with Perl, the GTK libraries, and the Perl DBI/DBD stack.  This is the default install.
 # "The Step Up" - All of the packages contained in "The Starter", as well as extra tools (database binaries for example), as well as Perl applications (App::Asciio and Gtk2::Ex::!PodViewer)
 # "The Developer" - All of the packages contained in "The Step Up", as well as development headers, import libraries, and documentation that can be used to compile new libraries.
 # "The Bloatware - The Whole Enchilada" - You want everything.  All of the Camelbox packages will be downloaded and installed.
 # "The Basics - Perl Only" - You just want Perl and that's it.
 # "The Basics - Perl with all Non-GTK Modules" - You just want Perl and the non-GTK modules (DBI/DBD, YAML, XML::Parser, etc.).
 # "The Basics - Perl with Database Support only" - Perl with DBD/DBD and some extra support modules and database tools binaries.
 # "Vapourware" - A placeholder used for testing and development.  Doesn't install any packages.

===Package Groups Explained===
 * *Core Gtk2-Perl Packages* are all of the packages that are needed to run applications written for the Gtk2-Perl GUI environment.
 * *Extra Gtk2-Perl Packages* are packages that are not *needed* to run Gtk2-Perl applications, but provide additional functionality above the core Gtk2-Perl installation.  Currently, the packages in this category include Gtk2::GladeXML and Gnome2::Canvas.
 * *Gtk2-Perl Applications* are applications written to use the Gtk2-Perl stack.
   * *App::Asciio* - an ASCII art drawing program; you can find out more information about App::Asciio by visiting it's [http://search.cpan.org/dist/App-Asciio/ CPAN description page], and there are also [http://www.youtube.com/watch?v=IiOHYNHo_Nw screencasts of Asciio] available on !YouTube.
   * *Gtk2::Ex::!PodViewer* - a Perl POD parser/reader written using GTK.
 * The *Extra Perl Modules* packages contains popular Perl modules that have been downloaded and installed from CPAN, the Comprehensive Perl Archive Network.  You could also download and install these CPAN modules by hand if you wish, they're just provided here for convenience.
 * The *Perl Database Support* group contains the Perl DBI (Database Independent Interface) module, as well as DBD (Database Driver) modules for MySQL, ODBC, PostgreSQL and SQLite.
 * The *Development Packages* contains packages that hold library files and header files for various packages in the Camelbox distribution.  If you plan on doing additional development or need to compile binaries for Camelbox, then you would need some or all of these packages in order to compile any additioanl software. The MinGW  and dmake packages are located here, as they are needed for compiling external programs/libraries.
 * *Database Tools Packages* contain binary programs that are used to interact with databases, for example the MySQL client _mysql.exe_, the PostgreSQL client _psql.exe_, and the SQLite binary _sqlite.exe_.  Extra MySQL packages are available for install, but are generally not installed by default (use the *Bloatware* install type to install them).
 * The *Extra Tools Packages* are packages that contain non-essential binaries; handy to have, but not needed for basic usage.  This package group includes the Glade GUI builder tool, !UnxUtilities for Windows, the LZMA archiver, the imagelibs utilities, the gettext utiltities and extra dmake files that are not needed on Windows.
 * The *Bloatware* group holds extra software that is generally not needed for most users, but is available for download and installation if you "Just Gotta Have It!"
 * The *Documentation and Examples* packages contain the HTML documentation for Perl, the HTML documentation for the GTK C API's, as well as all of the Gtk2-Perl examples.

The *Environment Variables* option allows you to add the path to the Camelbox binaries to your *%PATH%* environment variable in Windows.

== Installing Missing Packages ==

If you do not choose the *Bloatware* install type when you install Camelbox on your system, there is an easy way to add more packages after the initial install has completed.  Simply run the installer again, and choose the packages that you want to install, and let the installer do the work for you.  

The safest option as far as keeping your Camelbox install stable is to only
run the installer from the same release series that was used for the initial
install.  This way you will not get mismatches in library versions when you
add additional packages to your install.

== Creating a Local Camelbox Mirror ==

If you need to install Camelbox on a large number of machines, or want to
develop applications using Camelbox, but don't want to keep downloading the
archive files over again, then setting up a local mirror of the Camelbox
archives is just what you're looking for.

During the Camelbox install process, you can specify a mirror server to use
besides the default (http://camelbox.googlecode.com/files).  On the same
screen where you choose the download mirror, you can also specify to "Keep
downloaded archive files".  When this option is checked, the installer will
not delete the downloaded archive files after unpacking them.  This means that
you can move these archive files to a local mirror server for re-use at a
later time.

<wiki:comment>
vi: set filetype=googlecodewiki shiftwidth=2 tabstop=2 paste:
</wiki:comment>
