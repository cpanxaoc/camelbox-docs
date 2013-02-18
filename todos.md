# Camelbox Todos #

- Automate building via Jenkins
- Relocatable
- Figure out what you want to do with the batch files; do you want to call
  wperl, do you want to un-batch-file them, or ??? (example: prove.bat and the
  prove script)
- Figure out how to get podviewer to use a default directory when searching
  for other POD files than what it was opened with
- An applications guide, describing each application packaged with Camelbox
  along with screenshots.
- A developer's guide
  - installer naming conventions
  - group the Build documents in one place and explain their purpose
  - how to use the hump.sh/nsh_builder.pl scripts, when to use them, and why
    they do what they do
- Set up a script to sync the `Camelbox` directory to lagrange and/or the USB
  thumbdrive WORKDISK.
- Add a time measurement thingy to the installer; start the timer before
  downloading the first file, stop the timer after the last file installs.
- Create a standalone PAR/perl script for manually unpacking a base/complete
  install of Camelbox.
  - `unpack_base.sh` - Unpacks a base Camelbox install from packages.  Checks
    for existing Camelbox directories before unpacking.

## Packages to Add ##
- GStreamer
- Installer for DBD::Oracle, which downloads Oracle, unpacks it, and performs
  an install.
- Source code installer
- Developer tools installer (vim, SQL Manager, winroll, etc.)
- DBD::DB2?
  - [DB2 Express-C Tools/Clients page](http://www-01.ibm.com/software/data/db2/express/additional-downloads.html)
  - [IBM Data Server Runtime Clients License](http://www14.software.ibm.com/cgi-bin/weblap/lap.pl?la_formnum=&li_formnum=L-BTHU-75GKQS&title=IBM+Data+Server+Runtime+Clients&l=en) 
- screenshots on how to set up an ODBC data source; try for the following drivers:
  - CSV
  - SQL Server
  - MySQL
  - SQLite
- Locale::gettext (part of the 'gettext' package, needed for Gtk2::Ex::PodViewer)
- cdrtools? (http://fy.chalmers.se/~appro/linux/DVD+RW/tools/win32/, http://smithii.com/cdrtools)


## Building ##
Glib test fail message:

    t/64bit....................NOK 2/12#   Failed test at t/64bit.t line 25.

More of the same, run `dmake test` to see the errors.

## Installer ##
- run a http HEAD request prior to trying to download any/all of the files;
  this will detect missing files or an outdated installer
- Add a setup for running console windows with ANSI.SYS
  - [http://www.bribes.org/perl/wANSIConsole.html Win32::Console::ANSI ], a
    perl module that does the ANSI stuff
  - [http://www.geocities.com/jadoxa/ Jason Hood's homepage] has an application called ANSICON, which runs in 32-bit consoles (cmd.exe)
  - [http://www.xs4all.nl/~robw/files/ansi.zip ANSI.COM], meant to be run prior to running anything else
  - [http://www.windowsnetworking.com/kbase/WindowsTips/Windows2000/UserTips/Miscellaneous/CommandInterpreterAnsiSupport.html ANSI.SYS setup for Windows XP]
  - [http://academic.evergreen.edu/projects/biophysics/technotes/program/ansi_esc.htm ANSI setup and escape sequences]
  - [http://enterprise.aacc.cc.md.us/~rhs/ansi.html Guide to ANSI.SYS]
  - [http://support.microsoft.com/kb/q101875/ Microsoft KnowledgeBase article]
- How do you duplicate/replicate the perllocal.pod page.  perllocal.pod lists
  all of the extra modules installed after Perl has been installed on the
  system
- Re-do the demos packages
  - split the demos up into individual demo packages (Gtk2, Glib/Cairo, Gtk2::GladeXML, Gnome2::Canvas)
  - add extras like LWP, YAML, Moose, XML::Parser

## Testing ##
Moved to the [testing guide page](https://github.com/cpanxaoc/camelbox-docs/blob/master/dev/testing_guide.md).

## Running ##
- How do you change GTK themes?  
  - `gtk-chtheme`
  - Change the default GTK theme to the Windows theme?
- What happens when you use sh.exe in CPAN.pm's shell specification?
- Create a package manager, which would allow adding packages after the
  initial install
- Write a demo_runner script, it detects which Gtk2 modules are installed,
  which demos are installed, and offers the user a list of demos that can be
  run
- demo_runner - verifies that...
  - Perl loads correctly and 
  - only the demos for which the corresponding libraries are installed are
    displayed to the user
- Document setting up Perl with FastCGI under IIS 6/7
  - [http://www.iis.net/downloads/default.aspx?tabid=34&g=6&i=1521 FastCGI extension for IIS 6] 
  - [http://learn.iis.net/page.aspx/246/using-fastcgi-to-host-php-applications-on-iis7/ Using FastCGI on IIS 7]

## superhump.pl ##
Create lists of files beforehand.  When you go to run `superhump.pl`, the
filelists get read in by `superhump.pl` when it comes time to detect new
files; any files left over after all of the filelists have been read in and
matched belong to the new package.  Filelists can also now be listed as
`file:md5sum` instead of just the filename only.

This way, you can build things in any order you want, and you only
have to save/store one set of filelists.  These new package lists (with the
MD5 checksum) can also be used to audit an installed system.

## Misc. Utilities ##
* Perl equivalent to the Python uploader script for Google Code

## Creating Stand-alone Programs with PAR ==

    C:\camelbox\bin>pp --gui --icon C:/camelbox/bin/wperl.exe -l libCairoPerl.dll -l libgthread-2.0-0.dll -o C:\temp\asciio.exe -l C:\camelbox\site\lib\auto\Cairo\Cairo.dll -l C:\camelbox\site\lib\auto\Glib\Glib.dll -l C:\camelbox\site\lib\auto\Gtk2\Gtk2.dll -M Win32::Console -M Tie::Hash::NamedCapture -M Gtk2 asciio
	
More PAR links:

- http://www.nntp.perl.org/group/perl.par/2008/01/msg3361.html
- https://rt.cpan.org/Public/Bug/Display.html?id=13508
- http://grokbase.com/topic/2007/07/01/failure-with-packing-gtk/NLJXX2CP8OWvgE3IRkZ9X0ISmd8
  
Use `local::lib` with PAR to bootstrap a GTK-specific PAR module; the
bootloader PAR class sets up the GTK PAR class and then runs it.

## Done Todos ##

### Fixing Missing libraries problem ###

Fixed May 2009 courtesy of Ari Jolma's patches.

ExtUtils::Liblist::Kid does not search for libraries that end in `*.lib`, it
only uses `$Config{_a}` (`$Config{lib_ext}` in the code, which is an alias to
`$Config{_a}`).  A patch was created that causes the Windows function in
!ExtUtils::Liblist::Kid to go back and look again with the new file extension,
which usually causes that module to find the library it was looking for.

File Extensions to Search For:
- `dll`
- `a`
- `lib`

### Demos ###
- redo all of the packages from the latest source (May 2009)

### Shortcuts ###
- shortcut to wperl? (17Jun2009)
  - shortcuts with URLs to docs and recommended tutorials
  - group related shortcuts, i.e. the Glade folder will have a shortcut to
    Glade and all of the Gtk2::GladeXML demos
- Finish the shortcuts NSH builder (09Jun2009)
- create a program group with shortcuts to different perl binaries and
  examples that are included with Camelbox (17Jun2009)

### Installer ###
- create a couple of different installers
  - small installer, no perl modules, meant to be used with a package manager
    of some kind
  - large installer, has a complete list of Perl modules 
  - silent installer, for enterprise installs, no install options

### hump.pl ###
- write a script that generates lists of files;
  - difflist - list of files in C:\camelbox used for diffing 
  - package filelist - install a module from CPAN, running the difflist before
    and after the install
  - camelbox_packages.nsh - list of archive files to be used to build the
    camelbox_packages.nsh script
  - md5sum-<release>.txt - list of archive files with checksums for posting
    with releases
- files have the following metadata read from a JSON file:
  - package filename/short name
  - package description
- groups have the following metadata read from a JSON file:
  - group description
  - group members in list order

### Misc ###
- Move all of the Antlinux wiki pages to the Google Code Project wiki
- create a script that performs before/after snapshots of the Camelbox
  directory, to be used to install new Perl modules.  Capture the changes and
  package them up for re-distribution
- packaging glade
- a putty profile that can be used to tunnel database tests

### Packages ###
- XML::Parser (reqires expat package from http://www.sf.net/projects/expat)
- DBD::mysql
- DBD::Sqlite
- DBD::ODBC/Win32::ODBC/DBI::ODBC
- Log::Log4perl
- DBD::Pg
- DBD::ODBC
- Goo::Canvas - Windows binaries at [the GooCanvas Sourceforge page](https://sourceforge.net/project/showfiles.php?group_id=173653)

vim: filetype=markdown shiftwidth=2 tabstop=2
