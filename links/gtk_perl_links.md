#summary Links to Gtk2-Perl Software
#labels Featured,Phase-Support

[http://code.google.com/p/camelbox CamelBox Home Page] ::
[BuildStart Build Start] ::
[BuildSetup Build Setup] ::
[BuildPerl Building Perl] ::
[BuildCoreGtk Building Core GTK Libs] ::
[BuildExtraGtk Building Extra GTK Libs] ::
[BuildExternalApps Building External Gtk2-Perl Apps] ::
[Gtk2PerlLinks Gtk2-Perl Links Page] ::
[Credits Camelbox Credits]

See also the [Credits Credits] page for links and licensing details.

=== Other Windows Perl Distributions ===
[http://strawberryperl.com/ Strawberry Perl]
  * [http://www.mail-archive.com/win32-vanilla@perl.org/ Mailing list]

=== GTK+ Libraries for Windows ===
  * A GTK for Windows page at [http://www.gtk.org/download-windows.html gtk.org], which includes all of the software needed as well as links to dependencies and some background information on using GTK in Windows.  Updated regularly.
  * [http://ftp.acc.umu.se/pub/gnome/binaries/win32 GTK+ and friends pre-compiled binaries for Windows (gnome.org)], file archive
  * [http://ftp.acc.umu.se/pub/gnome/binaries/win32/dependencies/ Dependencies that may be required to build various Gtk2-Perl modules] (Gtk2::GladeXML, Gnome2::Canvas, etc.), file archive

=== Gtk2-Perl ===
  * [http://gtk2-perl.sourceforge.net/ Gtk2-Perl homepage (Sourceforge)]
   * [http://gtk2-perl.sourceforge.net/win32/ Gtk2-Perl Win32 page]

=== Windows GTK Applications ===
  * [http://sourceforge.net/project/showfiles.php?group_id=98754 gladewin32], a port of the Glade GUI creation tool for Windows
  * [http://www.redhat.com/docs/manuals/enterprise/RHEL-4-Manual/gnu-binutils/dlltool.html dlltool], a tool that creates `.dll` files on platforms that need them.

==External Gtk2-Perl Applications==
A lot of these external applications come from the `Gtk2::Ex` branch in CPAN.  You can perform a [http://search.cpan.org/search?m=all&q=Gtk2%3A%3AEx&s=1&n=100 search of CPAN for Gtk2::Ex] to see a complete list of applications that are available.

- [http://search.cpan.org/perldoc?App::Asciio Asciio], an ASCII-art drawing
  tool (formerly `gpad`)
  * [http://entropy.homelinux.org/axis/installation.html Axis], a suite of Perl modules that provide an alternative to RAD design tools for database access.
  * [http://sprog.sourceforge.net/index.html Sprog], a graphical tool which anyone can use to build programs by plugging parts together. In Sprog jargon, the parts are known as 'gears' and they are assembled to make a 'machine'.
  * [http://www.gcstar.org/ GCstar], a manager for collections of information such as books, CD's, DVD's, games, and more.
- http://frood.sourceforge.net/ - Frood - LDAP client

== Compiling Software on Windows: Libraries and Import Libraries ==
  * [http://mirrors.zoreil.com/webclub.kcom.ne.jp/ma/colinp/win32/tools/dlltool.html The DLL Import Library Tool]
  * [http://www.mingw.org/MinGWiki/index.php/CreateImportLibraries MinGW: Create Import Libraries]
  * [http://209.85.141.104/search?q=cache:FAJjMH-iZGEJ:www.mingw.org/MinGWiki/index.php/CreateImportLibraries+windows+import+library&hl=en&ct=clnk&cd=17&gl=us&client=firefox-a MinGW: Create Import Libraries] (Cached copy)
  * [http://osdir.com/ml/gnu.libtool.general/2004-04/msg00049.html Mailing list post] on the libtool mailing list about linking against import libraries.
  * [http://docs.python.org/ext/dynamic-linking.html Differences between Unix and Windows] from python.org.
  * [http://sourceware.org/binutils/docs/binutils/index.html#Top binutils Manual Page]
    * [http://sourceware.org/binutils/docs/binutils/objdump.html#objdump objdump]
    * [http://sourceware.org/binutils/docs/binutils/dlltool.html#dlltool dlltool]
    * [http://sourceware.org/binutils/docs/ld/Options.html#index-g_t_002d_002dexport_002dall_002dsymbols-263 --export-all-symbols] option to ''ld''; this may fix having to build import library files
    * [http://www.redhat.com/docs/manuals/enterprise/RHEL-4-Manual/gnu-linker/win32.html ld and Win32] page from Red Hat's website

<wiki:comment>
vi: set filetype=googlecodewiki shiftwidth=2 tabstop=2 paste:
</wiki:comment>
