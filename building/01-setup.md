[Camelbox Home Page](http://code.google.com/p/camelbox) ::
[Gtk2-Perl Links Page](https://github.com/cpanxaoc/camelbox-docs/blob/master/links/gtk_perl_links.md) ::
[Camelbox Credits](https://github.com/cpanxaoc/camelbox-docs/blob/master/about/credits.md) ::
[Camelbox Docs Home](https://github.com/cpanxaoc/camelbox-docs)

Building Camelbox: [Build Start](https://github.com/cpanxaoc/camelbox-docs/blob/master/building/00-start.md) ::
[Build Setup](https://github.com/cpanxaoc/camelbox-docs/blob/master/building/01-setup.md) ::
[Build Base Perl](https://github.com/cpanxaoc/camelbox-docs/blob/master/building/02-base_perl.md) ::
[Build Core GTK+](https://github.com/cpanxaoc/camelbox-docs/blob/master/building/03-core_gtk.md) ::
[Build Extra GTK+](https://github.com/cpanxaoc/camelbox-docs/blob/master/building/04-extra_gtk.md) ::
[Build External Apps](https://github.com/cpanxaoc/camelbox-docs/blob/master/building/05-external_apps)

These sections appear roughly in the order you should install them in.

## Camelbox Build Directory structure ##
- build - directory for building perl
- gtk-archives - tar/lzma'ed files
- gtk-tarballs - downloaded archives and support software
- gtk-binaries - directories containing unpacked binary archives
  - dmake
  - dmake-extra (unneeded files from dmake)
  - expat-bin
  - expat-dev
  - gettext-utils
  - glade-win32
  - gtk-core-bin
  - gtk-core-dev
  - gtk-core-doc
  - gtk-support-bin
  - gtk-support-dev
  - imagelibs-bin
  - imagelibs-dev
  - imagelibs-utils
  - libglade-bin
  - libglade-dev
  - libgnomecanvas-bin
  - libgnomecanvas-dev
	  * libgoocanvas-bin
	  * libgoocanvas-dev
  - lzma
  - unxutils

# Unpacking Binary Archives #

Unpack the binary distributions, then start installing things that have an
installer, like MinGW and NSIS.

## gtk-binaries preparation ##
- extract all of the non-dev archives to gtk-core-bin
- extract all of the -dev archives to gtk-core-dev
- move the contents of gtk-core-dev\share\gtk-doc\html from to
  gtk-core-doc\share\html 
- delete gtk-core-dev\share\gtk-doc

The gtk-binaries should be the only ones that you have to re-do for each
release; the other packages (below) won't change as often.

## gtk-support packages ##
gettext
- extract normal archive to gtk-support-bin
- extract -dev archive to gtk-support-dev
- extract gettext-tools archive to gettext-utils package

libiconv
- required by pkg-config to run
- move libiconv\bin and libiconv\share\locale to gtk-support-bin
- move contents of libiconv\share\doc\libiconv to
  gtk-support-dev\share\doc\libiconv
- move contents of libiconv\share\man to gtk-support-dev\share\man
- move libiconv\README.libiconv to gtk-support-dev\share\doc\libiconv

pkg-config
- extract pkg-config.exe and manifest\ directory to gtk-support-bin
- extract the rest to gtk-support-dev
  - move gtk-support-bin\make to gtk-support-bin\usr\share\doc\pkg-config

zlib
- extract zlib1.dll only to gtk-support-bin\bin
- extract files in the lib\ and include\ directories to gtk-support-dev
- extract the rest of the files to gtk-support-dev\usr\share\doc\zlib

## imagelibs packages ##
jpeg\*-bin
- extract bin\jpeg\*.dll and manifest\ to imagelibs-bin
- extract all of the rest of the \*.exe files in the bin\ directory to
  imagelibs-utils
- extract the man pages to imagelibs-utils\man\
- extract the rest of the archive (contrib) to imagelibs-dev\share\doc, and
  move the contrib\jpeg subdirectory into imagelibs-dev\share\doc and delete
  the unneeded directories

jpeg\*-lib
- extract all files to imagelibs-dev

libpng\*-bin
- extract libpng\*.dll and manifest\ to imagelibs-bin
- *NOTE*: The PNG utilities are no longer bundled with the current version of
  libpng.  Get them from an older version (1.2.8)

libpng\*-lib
- extract all files to imagelibs-dev
- move the src\ directory to share\doc\png

libtiff\*-bin
- extract libtiff\*.dll and manifest\ to imagelibs-bin
- extract all of the rest of the \*.exe files in the bin\ directory to
  imagelibs-utils
- extract the lib\ directory to imagelibs-dev\
- extract the rest of the archive (contrib) to imagelibs-dev\share\doc, and
  move the contrib\tiff subdirectory into imagelibs-dev\share\doc and delete
  the unneeded directories

libtiff\*-lib
- extract all files to imagelibs-dev

## UnxUtils ##
- *Can't use UnxUtils on Windows 7*
  - binaries are too old, they generally don't run without crashing
- move everything in unxutils\usr\local to unxutils\usr
- create unxutils\usr\share\doc\unxutils\
- move StdDisclaimer.html and UnxUtilsDist.html to unxutils\share\doc\unxutils\
- move the contents of unxutils\usr\local\share to unxutils\share\doc\unxutils\
- move unxutils\usr\md5sum to unxutils\share\doc\unxutils\
- move the contents of unxutils\usr\wbin to unxutils\bin
- delete unxutils\usr\wbin
- move unxutils\bin\libfl.[a|lib] to unxutils\usr\lib, overwrite existing files
- see the RenamedUnxUtilities page for a list of binaries to copy and rename

## dmake ##
for the dmake package:
- create a bin directory
  - *Optional* Add to MinGW bin directory
- move dmake.exe and support\win95 directories, as well as the files in the
  support directory to dmake\bin

for the dmake-extras package:
- create bin, usr, share\doc\dmake directories
- move support\\* directories to dmake-extra\bin
- move man\ to dmake-extra\usr\
- move all of the other files/directories to dmake-extra\share\doc\dmake
- move all of the unneeded directories in dmake-extra\bin\support to a
  dmake-extra package (only the win95 directory is needed on Windows XP).

## Installing MinGW ##
- Make sure you select g++
- Install to C:\camelbox
- move camelbox\COPYING\* and camelbox\MinGW shortcut to camelbox\doc
- move installed.ini, MinGW-5.1.4.exe and uninst.exe to camelbox\mingw32
- move camelbox\man to camelbox\usr\man
- move camelbox\info to camelbox\usr\info
- move camelbox\doc to camelbox\share\
- move all of the MinGW files in the camelbox\share\doc directory into the
  camelbox\share\doc\mingw-runtime directory 

# Perl #
You now have enough software installed to build Perl.  Unpack the source, and
use dmake to build.

- Change the path for the build shell so that only the MinGW binary
  directories and `C:\Windows\System32` are in the `%PATH%`
- make sure the Camelbox logo has been substituted for the perlexe.ico.packd
  file in Perl's win32 directory
- Run `dmake` in the `win32` directory to perform the build
- When you run `hump.sh` on the Camelbox directory, you'll get a list of files
  that includes Perl and the Perl HTML documentation.  You'll have to split
  this list by hand so that the html directory is packaged in a separate file
  from the Perl binaries, modules, support files and POD documentation.
- *MAKE SURE* to change the text file type to UNIX in vim for the html_docs
  filelist, GNU tar doesn't like Windows text file line endings


## Optional/Misc Packages ##
lzma 
- create lzma\bin, lzma\share\doc\lzma
- move lzma.exe to lzma\bin
- move lzma.txt, history.txt to lzma\share\doc\lzma

expat-bin and expat-dev
- Other Perl modules besides Gnome2::Canvas depend on expat-bin and expat-dev,
  so they get their own packages
- create expat-bin\bin
  - copy libexpat.dll and libexpatw.dll to expat-bin\bin
- create expat-dev
  - copy everything not copied into expat-bin into this folder
  - move man directory to share\man

## Gtk2-Perl Modules ##
requires 
- gtk-core-bin and gtk-core-dev (obviously)
- gtk-support-bin
- imagelibs-bin and imagelibs-dev package (contains pkg-config .pc files)
- build hints on the BuildCoreGtk page, including setting the PKG_CONFIG_PATH
  variable to the directory containing all of the pkg-config \*.pc files

## Gtk2::GladeXML Module ##
- libglade-bin and libglade-dev
- libxml2 and libxml2-dev

optional
- glade-win32

## Gnome2::Canvas ##
See the BuildExtraGtk page for updated requirements; requires
- libart_lgpl and libart_lgpl-dev
- libgnomecanvas-bin and libgnomecanvas-dev
- fontconfig and fontconfig-dev
- freetype and freetype-dev
- MOVED 06May2009 - Other Perl modules depend on expat and expat-dev, so they
  get their own packages
- NOT NEEDED 22Apr2009 - gail and gail-dev - both are provided in the GTK+
  packages

##MySQL##

Create the following package directories:
- mysql-bin (libmysql.dll,mysql.exe)
- mysql-debug (.pdb files used for debugging)
- mysql-dev (header files, libraries and .def files)
- mysql-docs (.chm help file)
- mysql-server (all of the mysqld binaries)
- mysql-utils (mysqladmin, myisam\*, all other utilties)

- copy $MYSQL\*.ini, COPYING and EXCEPTIONS to mysql-utils\share\mysql
- copy $MYSQL\Docs\ChangeLog and INSTALL to mysql-utils\share\mysql
- copy $MYSQL\lib\opt\libmysql.dll to mysql-bin\bin
- copy $MYSQL\lib\opt\\*.lib to mysql-dev\lib 
- copy $MYSQL\bin\\*.exe except for mysqld\* and mysql.exe to mysql-utils\bin
- copy $MYSQL\share\<language> to mysql-bin\share
- copy $MYSQL\share\<other files> to mysql-utils\share\mysql
- copy $MYSQL\scripts folder to mysql-utils\share\mysql
- copy $MYSQL\Docs\manual.chm to mysql-docs\share\mysql
- copy $MYSQL\mysql.exe to mysql-client\bin
- copy $MYSQL\\*.map and \*.pdb files to mysql-debug\share\mysql\debug
- copy $MYSQL\include\\*.lib to mysql-dev\include
- copy $MYSQL\data to mysql-server\share\mysql
- copy $MYSQL\bin\mysqld\* to mysql-server\bin

## PostgreSQL ##
Create the following package directories:
- postgresql-bin
- postgresql-client
- postgresql-dev
- postgresql-docs
- postgresql-server

- copy $PGSQL\bin\libpq.dll to postgresql-bin\bin
- copy $PGSQL\bin\psql.exe to postgresql-client\bin
- copy $PGSQL\bin\pg_config.exe to postgresql-dev\bin
- copy $PGSQL\doc\html to postgresql-doc\share\html\postgresql-version
- copy $PGSQL\include to postgresql-dev\include
- copy $PGSQL\lib to postgresql-dev\lib
- copy $PGSQL\man to postgresql-doc
- copy the files in $PGSQL\share to
  postgresql-server\share\doc\postgresql-version
- copy the directories timezone, timezonesets and tsearch_data in $PGSQL\share
  to postgresql-server\share

Next: [BuildPerl Building Perl]

vim: set filetype=markdown shiftwidth=2 tabstop=2:
