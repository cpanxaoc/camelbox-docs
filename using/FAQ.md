#summary Frequently Questioned Answers
#labels Featured,Phase-Support

= General Info =
*Q:* Where does all of the software that makes up Camelbox come from?

*A:* See the [Credits Credits] page for download locations and license
details.

*Q:* Who is responsible for all of this?

*A:* Nobody and everybody.  Bathe in the rampant anarchy!

= Troubleshooting =

Before you post to [mailto:camelbox@googlegroups.com the mailing list] and/or [http://code.google.com/p/camelbox/issues/list file an issue] here on Google Code with an issue related to Camelbox, verify that you are actually having a problem with Camelbox, instead of a configuration issue on the your system.

== Before Installing ==

=== Setting up an HTTP proxy for installation ===
The NSIS Installer (which Camelbox uses) uses the native HTTP proxy functionality built into Windows.  

To set up an HTTP proxy outside of Internet Explorer:

*Start* -> *Settings* -> *Control Panel* -> *Internet Options* -> *Connections* -> *LAN Settings*.


To set up an HTTP proxy in Internet Explorer 8 on Windows XP:

  # Open Internet Explorer (if it's not already open)
  # Click Tools
  # Click Internet Options
  # Click the Connections tab
  # Click on the LAN Settings button
  # Click the check the box that starts with "Use a proxy server"
  # Enter in the IP/hostname and port of your proxy server

== After Installing ==

=== Check the Perl binary ===
Verify the Camelbox Perl binary is the only Perl binary in your path
  * `set | sort` in a Command Prompt (MS-DOS) window, look for any Path/PATH statements that belong to a different Perl distribution; multiple Perl binaries can co-exist on your system, but Camelbox paths must be *FIRST* before any other Perl binaries if you want to use Camelbox (see the below section *Check the support libraries* for more info on why this is so).
  * `which perl` in a zsh window (!UnxUtilities needs to be installed), verify that the Perl binary it finds is actually the Camelbox binary you're expecting it to find (hint: the path should start with `C:\camelbox`

=== Run Perl and/or some examples ===
  * Run Perl: `C:\camelbox\bin\perl -V` or `C:\camelbox\bin\perl -v` for more verbose and less verbose version output respectively
  * Run a demo: `C:\camelbox\bin\wperl C:\camelbox\examples\gyroscope.pl`

=== Check the support libraries (Gtk/Glib/Pango/Cairo) ===
If you get errors complaining about old versions of Gtk/Glib/Pango/Cairo and friends, check your `%PATH%` environment variables.  Example error message:

{{{
*** This build of Glib was compiled with glib 2.20.0, but is currently running 
with 2.18.2, which is too old.  We'll continue, but expect problems! 
}}}

In this case, there were multiple copies of Glib on this machine, and Camelbox is using the first `libglib` binary that was found in the user's `%PATH%`, which was an older version of `libglib`, not the one that comes with Camelbox.  Possible culprits for other copies of `libglib` on Windows include [http://www.gimp.org GIMP] and [http://www.pidgin.im Pidgin], both popular programs on Windows.  

The directory Camelbox installs into needs to be the *FIRST* path checked for Gtk/Glib/Pango/Cairo binaries, however Camelbox appends it's directory to the *END* of the user's `%PATH%` environment variable; this is by design.  

Since you can't have multiple versions of the same library file in the same directory on Windows due to filename conflicts, *you* need to manage your %PATH% statement so that applications you write with Camelbox can find the libraries that they are looking for.  This is a limitation of the operating system, not of Camelbox.  Your options as far as fixing this problem are to:
  # write a wrapper .bat file around your script that properly sets up the %PATH% environment variable, or
  # Change your system and user %PATH% variables so that Camelbox's path shows up first (the furthest to the left) in the list of directories in the %PATH% environment variables for both the system and the user.


= Running Perl/Gtk2-Perl =

==Camelbox Binaries with other Perl Distributions==
*Q:* Can I use the compiled Camelbox binaries for Gtk2-Perl with another distribution of Perl?

*A:* It depends.  The only distribution of Perl that the binaries compiled for
Camelbox are guaranteed to run on is Camelbox.  Perl distributions that are
similar to Camelbox, like [http://strawberryperl.com/ Strawberry Perl] for
example, should also work if you tell Strawberry Perl about the extra library
paths.  Distributions of Perl like !ActiveState may work, however, extensive
tweaking may be required in order to get !ActiveState to see the new library
files added from the Camelbox distribution.  Also, since !ActiveState is
compiled with Microsoft's C compiler, there may be issues with Camelbox
libraries/modules, as they're compiled with GNU's C compiler (GCC).  See the
"Which Toolchain to Use?" section of the
[http://www.gtk.org/download-windows.html GTK Download for Windows page] on
the [http://www.gtk.org GTK website], as well as the
[http://search.cpan.org/src/MJEVANS/DBD-ODBC-1.16/README.windows README.windows file for the DBD::ODBC module] for more info.

In order for things to work, your Perl distribution needs to find the Perl
Modules that come with Camelbox.  You would do this by tweaking one of the
following:

  * `@INC=<path to Camelbox Libraries/Modules>` in your code
  * `use lib <path to Camelbox Libraries/Modules>` in your code
  * `set PERL5LIB=<path to Camelbox Libraries/Modules>` in your environment

*Q:* Okay, so !ActiveState is not directly supported by Camelbox.  Are there any plans to build the same software that comes with Camelbox for !ActiveState?

*A:* There are already Gtk2-Perl add-ons for !ActiveState.  A [http://www.google.com Google search] for `"perl gtk activestate"` should turn up more than a few.

==Running Perl without the Command Prompt Window==
*Q:* How do I run a Perl script that uses Gtk2-Perl, but without having a Command Prompt window pop up while the Gtk2-Perl application is running.

*A:* Use the `wperl.exe` binary, normally located in `C:\camelbox\bin`.  This binary is compiled to *not* use the Command Prompt windows when it runs.  You can set up a Windows shortcut that says something like this for the target: `C:\camelbox\bin\wperl.exe C:\path\to\your\script.pl`.

==Slashes (/), Backslashes (\), and Spaces ( ) with Perl on Windows==
*Q:* What slashes can I use where in Perl on Windows?

*A:* This depends a lot on whether or not you are using single-quoted strings or double-quoted strings, and whether or not your filenames have spaces in them.  Here are some examples:

{{{
'C:\boot.ini' # works
'C:/boot.ini' # ditto
q(C:\boot.ini) # works, a wee bit more readable
q(C:/boot.ini) # same deal
"C:/boot.ini" # works
"C:\boot.ini" # fails, the backslash is interpolated by Perl
"C:\\boot.ini" # works, backslash is escaped from Perl
qq(C:/boot.ini) # works
qq(C:\boot.ini) # fails, the backslash is interpolated by Perl
qq(C:\\boot.ini) # works, backslash is escaped from Perl
}}}

As far as spaces go, here are some basic rules:

  # If you quote the filename containing spaces with double-quotes, it will work in the Windows command shell (cmd.exe), as well as most *NIX shells.
  # Double-quoted filenames with spaces will also work in Perl.
  # Single-quoted filenames will not work in the Windows commmand shell like they do in *NIX
  # But Perl handles single-quoted filenames with spaces fine.

If you work with filenames that have spaces in them (C:\Program Files for
example), expect some problems.  Not all Perl modules were written to play nice
on Windows (i.e. they were written on `*NIX` machines), so you'll see problems
if you use filenames with spaces in them.

The [http://perldoc.perl.org/perlwin32.html Perl under Windows POD Page] goes into much more detail on this.

==Compiling XS Modules on Windows==
*Q:* I have a Perl module that uses XS to link to external libraries.  The module is not compiling, it can't find the libraries it needs.  How can I get my module to compile?

*A:* There are three things you can check...
  # Some Perl modules look for files in specific places on Windows.  Verify that the `Makefile.PL` has no `-X` tests for files in specific locations.
  # See what external library is being linked against, and then find a `*.dll*` (Windows library file) for that external library.  You will most likely need the header files (`*.h*`) that come with the external library as well.  Place library files (`*.dll`) in `C:\camelbox\bin` and header files (`*.h`) in `C:\camelbox\include`
  # Verify the external library file is listed in the `Makefile` that actually compiles the `*.xs` file.  Inside of the `Makefile` that compiles the `*.xs` file are two environment variables, `EXTRALIBS` and `LDLOADLIBS`.  Add the full path to your external library file (`C:\camelbox\bin\libdemo.dll` for example) to the `EXTRALIBS` and `LDLOADLIBS` lines in the `Makefile` that compiles the `*.xs` code, then issue the `dmake` command in the module's toplevel source directory to build the module.

==Default CPAN Mirrors point to servers in the United States==
*Q:* The CPAN mirrors that come with [http://code.google.com/p/camelbox Camelbox] are all located in the United States.  How can I change the mirrors to point to servers that are closer to my location?

*A:* You have two options here; 1) Run the CPAN module, and re-configure the server list, or  2) hand-hack the CPAN `Config.pm` file and add/change the servers by hand.

Option #1:
{{{ 
HOSTNAME# perl -MCPAN -e shell
Terminal does not support AddHistory.

cpan shell -- CPAN exploration and modules installation (v1.9205)
ReadLine support available (maybe install Bundle::CPAN or Bundle::CPANxxl?)

cpan[1]> o conf init urllist
Found C:\camelbox\.cpan\sources\MIRRORED.BY as of Sat Mar 29 02:03:49 2008

I'd use that as a database of CPAN sites. If that is OK for you,
please answer 'y', but if you want me to get a new database now,
please answer 'n' to the following question.

Shall I use the local database in C:\camelbox\.cpan\sources\MIRRORED.BY? [y]

[ much snippage of CPAN output ]

(1) Africa
(2) Asia
(3) Central America
(4) Europe
(5) North America
(6) Oceania
(7) South America
(8) (edit previous picks)
Select your continent (or several nearby continents) [8]
}}}

Option #2: Use Wordpad (or another editor that supports `*NIX` text files, i.e. with newlines only) to edit the file `C:\camelbox\lib\CPAN\Config.pm`, and edit the `urllist` line:

{{{
'urllist' => [ q[http://server1.test/pub/CPAN], q[http://server2.test/pub/CPAN/] ],
}}}

<wiki:comment>
vi: set filetype=googlecodewiki shiftwidth=2 tabstop=2 paste:
</wiki:comment>
