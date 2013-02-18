#summary Building Extra Gtk2-Perl Libraries
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

=== Gtk2::GladeXML ===
Requires the following extra GTK+ packages:
 * `libglade` and `-dev`
 * `libxml2` and `-dev` 

`Gtk2::GladeXML` uses the same base libraries as `Gtk2`, but it also uses following additional libraries for `EXTRALIBS`/`LDLOADLIBS`:
{{{
C:\camelbox\lib\libGtk2Perl.a
C:\camelbox\lib\libGlibPerl.a
C:\camelbox\bin\libglade-2.0-0.dll
C:\camelbox\bin\zlib1.dll
C:\camelbox\bin\libxml2.dll
}}}

=== Gnome2::Canvas ===
Requires the following extra GTK+ packages:
 * `libgnomecanvas` and `-dev`
 * `libart` and `-dev` (listed as `libart_lgpl` on the  [http://ftp.acc.umu.se/pub/gnome/binaries/win32/ gnome.org FTP server]
 * `freetype` and `-dev` (2.3.5, in the `dependencies` directory)
 * `fontconfig` and `-dev` (2.4.2-tml, in the `dependencies` directory)
 * `expat`
 * `gail` and `-dev` used to be required, but they're packaged with the GTK libraries now

`Gnome2::Canvas` uses the same base libraries as `Gtk2`, but it also uses following additional libraries for `EXTRALIBS`/`LDLOADLIBS`:
{{{
C:\camelbox\lib\libGtk2Perl.a 
C:\camelbox\lib\libGlibPerl.a 
C:\camelbox\bin\libgnomecanvas-2-0.dll
C:\camelbox\bin\libart_lgpl_2-2.dll
}}}

=== Gnome2::Print ===
Requires the following extra GTK+ packages:
 * `gnomeprintui` and `-dev`
 * `gnomeprint` and `-dev`
 * `libxml2` and `-dev`
 * `zlib`
 * `libart_lgpl_2` and `-dev`

`Gnome2::Print` needs the following additional libraries for `EXTRALIBS`/`LDLOADLIBS`:
{{{
C:\perl\5.8.8\lib\libgtk-win32-2.0.dll.a
C:\perl\5.8.8\lib\libgdk-win32-2.0.dll.a
C:\perl\5.8.8\lib\libatk-1.0.dll.a
C:\perl\5.8.8\lib\libgdk_pixbuf-2.0.dll.a
C:\perl\5.8.8\lib\libpangowin32-1.0.dll.a
C:\perl\5.8.8\lib\libpangocairo-1.0.dll.a
C:\perl\5.8.8\lib\libpango-1.0.dll.a
C:\perl\5.8.8\lib\libcairo.dll.a
C:\perl\5.8.8\lib\libgobject-2.0.dll.a
C:\perl\5.8.8\lib\libgmodule-2.0.dll.a
C:\perl\5.8.8\lib\libglib-2.0.dll.a
C:\perl\5.8.8\lib\libgthread-2.0.dll.a
C:\perl\5.8.8\lib\libgnomecanvas-2.dll.a
C:\perl\5.8.8\lib\libgnomeprint-2-2.dll.a
C:\perl\5.8.8\lib\libgnomeprintui-2-2.dll.a
C:\perl\5.8.8\lib\libart_lgpl_2.dll.a
C:\perl\5.8.8\lib\libglade-2.0.dll.a
C:\perl\5.8.8\lib\libxml2.dll.a
C:\perl\5.8.8\lib\zlib1.dll.a
C:\perl\5.8.8\lib\libCairoPerl.a
C:\perl\5.8.8\lib\libGlibPerl.a
C:\perl\5.8.8\lib\libGtk2Perl.a 
}}}

=== Gtk2::SourceView ===
Along with the same requirements as `Gnome2::Print` above, this module requires the following extra GTK+ packages:
 * `gtksourceview` and `-dev`

`Gtk2::SourceView` uses the same base libraries as `Gnome2::Print`, but it also uses following additional libraries for `EXTRALIBS`/`LDLOADLIBS`:
{{{
 C:\perl\5.8.8\lib\libgtksourceview-1.0.dll.a
}}}

=== Gnome2::GConf ===
Requires the following extra GTK+ packages:
 * `GConf` and `GConf-dev`
 * `ORBit2` and `ORBit2-dev`

`Gnome2::GConf` uses following additional libraries for `EXTRALIBS`/`LDLOADLIBS`:
{{{
C:\perl\5.8.8\lib\libglib-2.0.dll.a
C:\perl\5.8.8\lib\libgobject-2.0.dll.a
C:\perl\5.8.8\lib\libgthread-2.0.dll.a
C:\perl\5.8.8\lib\libgconf-2.dll.a
C:\perl\5.8.8\lib\libORBit-2.dll.a
C:\perl\5.8.8\lib\libGlibPerl.dll.a
}}}

=== Gnome2::Rsvg ===
Requires the following extra GTK+ packages:
 * `librsvg` and `librsvg-dev`
 * `svg-gdk-pixbuf-loader`
 * `svg-gtk-engine`
 * `libcroco`
 * `libgsf`
 * `libbzip2` (in the `dependencies` directory)

Add the same libraries as above for `Gtk2`, but also add the following libraries:
{{{
C:\perl\5.8.8\lib\libGtk2Perl.dll.a
C:\perl\5.8.8\lib\librsvg-2.dll.a
}}}

=== Gnome2::VFS ===
Requires the following extra GTK+ packages:
 * `GConf` and `GConf-dev`
 * `ORBit2` and `ORBit2-dev`

Added to `EXTRALIBS` and `LDLOADLIBS`:
{{{
C:\perl\5.8.8\lib\libglib-2.0.dll.a
C:\perl\5.8.8\lib\libgobject-2.0.dll.a
C:\perl\5.8.8\lib\libgthread-2.0.dll.a
C:\perl\5.8.8\lib\libgconf-2.dll.a
C:\perl\5.8.8\lib\libORBit-2.dll.a
C:\perl\5.8.8\lib\libGlibPerl.dll.a
}}}

=== Gtk2::Html2 ===
*Note*: it looks like this module has not been updated in a while; it has dependencies against GTK 1.x.

Requires the following extra GTK+ packages:
 * `libgtk-html-3.x` and `libgtk-html-3.x`
 * `libgnomeui` and `libgnomeui-dev`
 * `libgnome` and `libgnome-dev`
 * `libbonobo` and `libbonobo-dev`

=== Gtk2::Spell ===
Requires the following extra libraries:
 * `aspell`
 * `gtkspell`
See http://developer.pidgin.im/wiki/BuildingWinPidgin for links to pre-built packages.

<wiki:comment>
vi: set filetype=googlecodewiki shiftwidth=2 tabstop=2 paste:
</wiki:comment>
