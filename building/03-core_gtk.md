#summary Building the core Gtk2-Perl libraries/modules
#labels Phase-Implementation

[http://code.google.com/p/camelbox CamelBox Home Page] ::
[BuildStart Build Start] ::
[BuildSetup Build Setup] ::
[BuildPerl Building Perl] ::
[BuildCoreGtk Building Core GTK Libs] ::
[BuildExtraGtk Building Extra GTK Libs] ::
[BuildExternalApps Building External Gtk2-Perl Apps] ::
[Gtk2PerlLinks Gtk2-Perl Links Page] ::
[Credits Camelbox Credits]

===Installing the GTK packages/software===
Before you start building any of the Perl GTK modules, you need to unpack the GTK C binaries so that when the Perl modules are built, they can find their appropriate C library counterparts.
 * Download all of the GTK packages from the [http://ftp.gnome.org/pub/gnome/binaries/win32/ GTK website].  There is a [http://www.gtk.org/download-windows.html Windows download page] that mentions what packages are needed to get GTK working on Windows (top of the page, under the heading *Packages*).  Also, the dependency packages that are needed for running GTK apps in Windows are marked with a 'checkbox' to the right of each package under the section titled *Third Party Dependencies*.  To compile Gtk2-Perl, you'll need the following:
  * zlib
  * GNU libiconv
  * gettext-runtime
  * libpng
  * libjpeg
  * libtiff
  * pkg-config
 * For any of the Gnome2::Canvas modules, you will also need:
  * Freetype
  * Fontconfig
  * libexpat
 * Unpack all of the GTK packages into a single directory.  The GTK packages were all zipped into Unix-style directory trees (`/bin, /etc, /shared, etc.`)
 *  Using Windows Explorer, take all of the GTK/support file directories that were unpacked, and move them into the Perl directory that was created when Perl was installed (you can do it from the command line too if you're feeling lucky). Windows Explorer will warn about copying over files in existing folders, but there shouldn't be any file conflicts, so you don't have to worry about that message.

If you're using the pre-built package directories, copy the contents of the
following directories into the Camelbox directory
  * gtk-core-bin
  * gtk-core-dev
  * gtk-support-bin
  * gtk-support-dev
  * imagelibs-bin
  * imagelibs-dev

===Testing pkg-config===
`pkg-config` is a tool that sets up the environment for a given package so that other software can be compiled against it.  You should verify that `pkg-config` works prior to trying to compile something, since all of the Gtk2-Perl apps will end up using it.  To test it:
 # Set up the `PKG_CONFIG_PATH` environment variable
  * `export PKG_CONFIG_PATH="C:/camelbox/lib/pkgconfig"`
 # Then run the `pkg-config` command
{{{
pkg-config --modversion <some library name>
pkg-config --modversion gtk+-2.0
}}}

===List of Gtk2-Perl modules in the order you should build them in===
Grab the modules from CPAN, as they're usually the lateѕt and greatest.  Use
the CPAN shell to install them from the network.

Required Modules (in dependency order):
 # !ExtUtils::Depends
 # !ExtUtils::!PkgConfig 
  * Make sure the GTK binaries are installed and `PKG_CONFIG_PATH` is set before installing this; the Perl module looks for the `pkg-config` binary
 # Test::Number::Delta
 # Cairo
 # Glib
 # Pango
 # Gtk2

Optional Modules:
 # Gtk2::GladeXML
 # Gnome2::Canvas
 # Gnome2::Print
 # Gnome2::GConf
 # Gnome2::Rsvg

All of the above required and optional modules can usually be built using:
{{{
# do this next line only once
export PKG_CONFIG_PATH=C:/path/to/pkgconfig/directory 
# do the rest of these every time
perl Makefile.PL
dmake
dmake test
dmake install
}}}

The `dmake` binary was the same one you used to build Perl in the first place.

Most of the steps below use something called
[http://www.redhat.com/docs/manuals/enterprise/RHEL-4-Manual/gnu-binutils/dlltool.html dlltool] in order to help build the `.dll` file on Windows.  The linked page better explains what `dlltool` does for the curious.

===Cairo Notes===
Add the following to the `Makefile` under `EXTRALIBS` and `LDLOADLIBS`:
{{{
C:\camelbox\bin\libcairo-2.dll
}}}

Add this line to the `Makefile` prior to `$(CHMOD) $(PERM_RWX) $@` (will be used when compiling `Gtk2`):
{{{
dlltool --input-def Cairo.def --dllname Cairo.dll \
   --output-lib libCairoPerl.a
$(CP) libCairoPerl.a C:/camelbox/lib
}}}

Run `dmake/dmake install`, which will copy `libCairoPerl.a` to `C:\camelbox\lib`

===Glib Notes===
Added to `EXTRALIBS` and `LDLOADLIBS`:
{{{
C:\camelbox\bin\libglib-2.0-0.dll
C:\camelbox\bin\libgobject-2.0-0.dll
C:\camelbox\bin\libgthread-2.0-0.dll
}}}

Add this line to the `Makefile` prior to `$(CHMOD) $(PERM_RWX) $@` (will be used when compiling `Gtk2`):
{{{
dlltool --input-def Glib.def --dllname Glib.dll \
     --output-lib libGlibPerl.a
$(CP) libGlibPerl.a C:/camelbox/lib
}}}

Run `dmake/dmake install`, which will copy `libGlibPerl.a` to `C:\camelbox\lib`

===Pango Notes===
Added to `EXTRALIBS` and `LDLOADLIBS`:
{{{
C:\camelbox\bin\libgtk-win32-2.0-0.dll 
C:\camelbox\bin\libgdk-win32-2.0-0.dll 
C:\camelbox\bin\libatk-1.0-0.dll 
C:\camelbox\bin\libgdk_pixbuf-2.0-0.dll
C:\camelbox\bin\libpangowin32-1.0-0.dll
C:\camelbox\bin\libpangocairo-1.0-0.dll 
C:\camelbox\bin\libpango-1.0-0.dll 
C:\camelbox\bin\libcairo-2.dll 
C:\camelbox\bin\libgobject-2.0-0.dll 
C:\camelbox\bin\libgmodule-2.0-0.dll 
C:\camelbox\bin\libglib-2.0-0.dll 
C:\camelbox\bin\libgthread-2.0-0.dll
C:\camelbox\lib\libCairoPerl.a
C:\camelbox\lib\libGlibPerl.a
}}}

Run `dmake/dmake install`, which will copy `libPangoPerl.a` to `C:\camelbox\lib`

Add this line to the `Makefile` prior to `$(CHMOD) $(PERM_RWX) $@` (will be used when compiling `Gtk2`):
{{{
dlltool --input-def Pango.def --dllname Pango.dll \
     --output-lib libPangoPerl.a
$(CP) libGlibPerl.a C:/camelbox/lib
}}}

===Gtk Notes===
Added the following to the `Makefile` under `EXTRALIBS` and `LDLOADLIBS`:
{{{
C:\camelbox\bin\libgtk-win32-2.0-0.dll 
C:\camelbox\bin\libgdk-win32-2.0-0.dll 
C:\camelbox\bin\libatk-1.0-0.dll 
C:\camelbox\bin\libgdk_pixbuf-2.0-0.dll
C:\camelbox\bin\libpangowin32-1.0-0.dll
C:\camelbox\bin\libpangocairo-1.0-0.dll 
C:\camelbox\bin\libpango-1.0-0.dll 
C:\camelbox\bin\libcairo-2.dll 
C:\camelbox\bin\libgobject-2.0-0.dll 
C:\camelbox\bin\libgmodule-2.0-0.dll 
C:\camelbox\bin\libglib-2.0-0.dll 
C:\camelbox\bin\libgthread-2.0-0.dll
C:\camelbox\lib\libCairoPerl.a
C:\camelbox\lib\libGlibPerl.a
C:\camelbox\lib\libPangoPerl.a
}}}

Add this line to the `Makefile` prior to `$(CHMOD) $(PERM_RWX) $@` (will be used when compiling modules that need to link against `Gtk2`):
{{{
dlltool --input-def Gtk2.def --dllname Gtk2.dll \
     --output-lib libGtk2Perl.a
$(CP) libGtk2Perl.a C:/camelbox/lib
}}}

Run `dmake/dmake install`, which will copy `libGtk2Perl.a` to `C:\camelbox\lib`

Next: [BuildExtraGtk Building Extra GTK Modules]

<wiki:comment>
vi: set filetype=googlecodewiki shiftwidth=2 tabstop=2 paste:
</wiki:comment>
