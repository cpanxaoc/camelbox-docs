#summary Building External Gtk2-Perl Applications
#labels Phase-Implementation

[http://code.google.com/p/camelbox CamelBox Home Page] ::
[BuildStart Build Start] ::
[BuildPerl Building Perl] ::
[BuildCoreGTK Building Core GTK Libs] ::
[BuildExtraGtk Building Extra GTK Libs] ::
[BuildExternalApps Building External Gtk2-Perl Apps] ::
[Gtk2PerlLinks Gtk2-Perl Links Page]

== Renamed !UnxUtilties Binaries ==
The following is a list of files from the [http://unxutils.sourceforge.net/ UnxUtilities] package that have the same names as files that come with Windows
XP. It is recommended that the Windows versions of files with the same name be
seen first in the system; you can either copy/rename the
[http://unxutils.sourceforge.net/ UnxUtilities] commands, or call them with
absolute pathnames in order to use them.

(filename, what it's !UnxUtilities equivalent is, why it needs an equivalent)
  * bin/find.exe -> xfind.exe (Windows binary)
  * bin/sort.exe -> xsort.exe (Windows binary)
  * bin/head.exe -> xhead.exe (or rename the HEAD file that's installed from LWP)
FIXME the LWP version should be renamed, lwphead?
  * bin/date.exe -> xdate.exe (Windows cmd.exe shell builtin)

<wiki:comment>
vi: set filetype=googlecodewiki shiftwidth=2 tabstop=2 paste:
</wiki:comment>
