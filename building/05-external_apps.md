#summary Building External Gtk2-Perl Applications
#labels Phase-Implementation

[http://code.google.com/p/camelbox CamelBox Home Page] ::
[BuildStart Build Start] ::
[BuildSetup Build Setup] ::
[BuildPerl Building Perl] ::
[BuildCoreGtk Building Core GTK Libs] ::
[BuildExtraGtk Building Extra GTK Libs] ::
[BuildExternalApps Building External Gtk2-Perl Apps] ::
[Gtk2PerlLinks Gtk2-Perl Links Page]

The URLs to all of these applications can be found on the [Gtk2PerlLinks] page.

=== Misc. notes ===
  * `objdump` can be used to view what functions are compiled into a library;
  * see the [http://www.mingw.org/docs.shtml MinGW docs page] for more on the below command:
{{{
 objdump -p file.dll > dll.fil
}}}

 MinGW Wiki Links that fixed problems with linking to `.dll` files:
  * [http://mingw.sourceforge.net/MinGWiki/index.php/FAQ MinGW FAQ Wikipage]
  * [http://mingw.sourceforge.net/MinGWiki/index.php/CreateImportLibraries Create Import Libraries]

== MSYS ==
=== Installing ===
Download the MSYS installer from
[https://sourceforge.net/project/showfiles.php?group_id=2435 the MinGW
Sourceforge] site;
  * click on 'MSYS Base System'
  * Current Release (at the bottom of the page)
  * `MSYS-1.0.X.exe`

Edit the `/etc/profile` file in the MSYS distribution; make sure the MSYS
binary directories are listed first in the PATH statement in that file.

MSYS versions newer than 1.0.11 do not come with an installer.  Use the [http://crosswire.org/~jmarsden/setup-mingw.bat setup-mingw.bat] script from http://crosswire.org/~jmarsden/setup-mingw.html to perform an install instead.

== Perl Modules ==


=== gettext Perl Module ===

This is used with Gtk::Ex::!PodViewer.  Requires `gtk-support-dev` package
(`libintl.h`), as well as `Gtk2::Ex::Simple::List` module.  In the `Makefile.PL` for the `gettext` module, add the following line where the `system()` call is for compiling library tests:
{{{
system($cc . " -o conftest " . $libs . " conftest.c C:\\camelbox\\bin\\intl.dll");
}}}

(taken from
[http://mirrors.zoreil.com/webclub.kcom.ne.jp/ma/colinp/win32/tools/link.html a mirror of a MinGW tutorial]; [http://www.spacejack.org/games/mingw/ another
reference] for compiling MinGW applications)

*Note*: Make sure you add `C:/camelbox/bin/intl.dll` to the end of the
`LDLOADLIBS` variable in the `Makefile`.

=== Gtk2::Ex::PodViewer ===
Requires Locale::gettext, IO::Scalar, Gtk2::Ex::Simple::List

=== DBI ===

Run CPAN, `install DBI`.  Module should install with no issues.

=== DBD::mysql ===

Requirements:
  * libmysql.dll library (add to $CAMELBOX/bin)
  * all MySQL headers (add to $CAMELBOX/include)
  * libmysql.lib library (add to $CAMELBOX/lib)

The `Makefile.PL` for `DBD::mysql` will want to know the location of the
`mysql.h` header file.  So if you try to install `DBD::mysql` via CPAN, it
will bomb out.  Once it does, type the following lines to start compiling DBD::mysql.  Note that you'll need to use forward slashes, the backslashes are interprited by the build tools.

{{{
look DBD::mysql
perl Makefile.PL --cflags=-IC:/camelbox/include --libs=-LC:/camelbox/lib

}}}

Add the following library to `EXTRALIBS`/`LDLOADLIBS` in the `Makefile`:
  * `C:\camelbox\lib\libmysql.lib`

{{{
dmake
dmake install
}}}

=== XML::Parser ===
Tweaking the Makefile in the $XML_PARSER_SOURCE/Expat directory
(mine is C:\camelbox\.cpan\build\XML-Parser-2.36-XXXXXX\Expat).
Inside that Makefile there are two environment variables that are set
during the build, EXTRALIBS and LDLOADLIBS.  If you add the the full
path to libexpat.dll (C:\camelbox\bin\libexpat.dll) to the end of the
line for both of those environment variables, and then issue 'dmake'
from the top of the unpacked XML::Parser source directory, it should
then build without errors... 

{{{
perl Makefile.PL EXPATLIBPATH=C:\camelbox\bin EXPATINCPATH=C:\camelbox\include
cd Expat
vi Makefile
<add C:\camelbox\bin\libexpat-1.dll to EXTRALIBS, LDLOADLIBS>
dmake
dmake install
}}}

=== DBD::Pg ===
Copy over the postgresql-bin and postgresql-dev packages (postgresql-client is optional but recommended), then use CPAN to install DBD::Pg.

How it was done in Strawberry Perl:

http://www.nntp.perl.org/group/perl.dbd.pg/2008/02/msg240.html

=== DBD::SQLite ===

Run CPAN, do a `force install` (some of the test fail on Windows).  You don't
even need to install the SQLite libraries, as the DBD driver comes with them.

=== DBD::ODBC ===

Run CPAN, `install DBI`.  Module should install with no issues.

=== Net::SSH::Perl===
Requires Math::GMP.  You can download a pre-built copy of the GMP library compiled for Windows at the [http://www.cs.nyu.edu/exact/core/gmp/ Core library] website. Make sure you download the dynamic library.  `dmake`/`dmake install` will work as usual once you add the `.dll` file to the `Makefile`.

== Perl Applications ==

=== Asciio ===
The package now contains a `Makefile.PL` file, which means it can be built with dmake and Perl.

Forced modules (run with `force install`):
  * Test::Block
  * Eval::Context
  * Test::Dependencies

During module installation, you may have to hit the <Return> key on the keyboard if it looks like a test has hung.  Mostly in the 'Perl Critic' tests.

=== Axis ===

== External Applications ==

Links:
  * http://www.mingw.org/node/18
  * http://wiki.enlightenment.org/index.php/EFL_Windows_XP

Download and unpack the following MSYS packages:
  * MSYS-1.0.11-20080710-dll.tar.gz 
  * MSYS-1.0.10.exe
  * bison-2.3-MSYS-1.0.11-1.tar.bz2 (from Supplementary tools directory; Postgresql)
  * zlib-1.2.3-MSYS-1.0.11-1.tar.bz2 (from Supplementary tools directory; Postgresql)

[http://sourceforge.net/project/showfiles.php?group_id=2435&package_id=24963&release_id=46827 MSYS Base System]

[http://sourceforge.net/project/showfiles.php?group_id=2435&package_id=67879 MSYS Supplementary Tools]

You will need to move/remove any other paths from the %PATH% environment
variable that might have binaries with the same names as the MSYS binaries.

=== OpenSSL ===
  * Homepage: http://www.openssl.org/
  * Source: http://www.openssl.org/source/
  * Win32 Install Instructions: http://cvs.openssl.org/fileview?f=openssl/INSTALL.W32

{{{
gunzip -c openssl-0.9.8?.tar.gz | tar -xv 
cd openssl-0.9.8?
# create the symlinks that didn't get created when unpacking the tarball
cd include/openssl
find ../../crypto/ -name "*.h" -exec ln -s '{}' \;
./config --prefix=/stow/openssl-0.9.8?
time make 
time make install
time make test # (optional)
}}}

=== PostreSQL ===

  * Homepage: http://www.postgresql.org/ 
  * Source: http://www.postgresql.org/ftp/source/
  * [http://www.postgresql.org/docs/8.3/interactive/reference-client.html List of client apps]
  * [https://sourceforge.net/project/showfiles.php?group_id=2435&package_id=67879 MSYS Supplementary Tools ] - needed for the `bison`, `flex`, and `regex` packages

and unpack it somewhere under `C:\msys\1.0`.  Note that compiling with OpenSSL
currently doesn't work (14May2009).

Open the MSYS shell (icon on the desktop) and type the following: 
{{{
# add the MSYS path to the PATH environment variable
export PATH=/bin:$PATH
# go to your PostgreSQL source directory
cd /path/to/postgresql/source
CFLAGS="-LC:\apps\msys\1.0\bin -LC:\apps\msys\1.0\lib \
-LC:/msys/1.0/bin -LC:/msys/1.0/lib" \
./configure --prefix=/home/stow/postgresql-8.3.?
time make
make install
}}}

You should now have a complete binary install of PostgreSQL in `C:\msys\1.0\stow\postgresql-8.3.3`.

=== SQLite ===
{{{
cd /path/to/sqlite/source
./configure --prefix=/home/stow/sqlite-1.3.X
time make
make install
}}}

Copy the binaries into the package_dirs directory

=== Tk ===
  # Download the source, run `perl Makefile.PL'
  # Add the file `C:\camelbox\lib\libjpeg.dll.a` to `$TK_SRC/JPEG/Makefile` in the `EXTRALIBS` and `LDLOADLIBS` variables.
  # `dmake && dmake install`
  # demo is the `widget.bat` file

=== GMP math libraries (for Net::SSH::Perl) ===
http://www.cs.nyu.edu/exact/core/gmp/
http://progressive-living.com/opensource/gmp/gmp.html

<wiki:comment>
vi: set filetype=googlecodewiki shiftwidth=2 tabstop=2 paste:
</wiki:comment>
