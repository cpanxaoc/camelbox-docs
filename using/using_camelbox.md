#summary Things you can do once Camelbox is installed
#labels Featured,Phase-Deploy

== Perl Version ==

First, you may want to make sure things are working.  Open up a Command Prompt (Start -> 
Programs -> Accessories -> Command Prompt in Windows XP).  Type in the following command in the window:

{{{
C:\>perl -v

This is perl, v5.10.0 built for MSWin32-x86-multi-thread

Copyright 1987-2007, Larry Wall

Perl may be copied only under the terms of either the Artistic License or the
GNU General Public License, which may be found in the Perl 5 source kit.

Complete documentation for Perl, including FAQ lists, should be found on
this system using "man perl" or "perldoc perl".  If you have access to the
Internet, point your browser at http://www.perl.org/, the Perl Home Page.
}}}

You can use `perl -V` (capital 'V') to get more verbose output.

== Run a simple Perl script ==

The following examples assume that you installed the *gtk2-perl-examples* package.  Inside that package are a bunch of Perl/Gtk2-Perl scripts.  The first example that will be run is called `perl_swiss_army_knife.pl`, a basic script that prints environment variables and installed Perl modules.  Run the following commands at the Command Prompt:

{{{
perl C:\camelbox\examples\perl_swiss_army_knife.pl | less
}}}

In the command above, the output of `perl_swiss_army_knife.pl` is piped into the `less` command, part of the !UnxUtilities package.  Use the `q` key on the keyboard to exit the `less` command.  If you did not install the !UnxUtilities package, try this instead:

{{{
perl C:\camelbox\examples\perl_swiss_army_knife.pl | more
}}}

Again, the `q` key exits the `more` command.

== Run an actual Gtk2-Perl script ==

There is a script called `gyroscope.pl` in the `C:\camelbox\examples` directory.  It is an HTML color picker, you pick a color, then copy the HTML code from a text box.  To run the script:

{{{
perl C:\camelbox\examples\gyroscope.pl
}}}

A window should pop up with a large green square, and a text box underneath that has the text `#00ff00` inside.  The window may take a few seconds (between 5-7 seconds) before it pops up; this is normal the first time the program is run.  Subsequent runs of the same script will be faster.  Click on the `X` in the upper right hand corner of the window to close the window and stop the script from running.  Pressing `Ctrl-C` in the Command Prompt window also will stop the script.

== More Examples ==

Here is a list of examples that you can run using the same command syntax as the previous step:

 * For the `C:\camelbox\examples\Gtk2` directory: 
   * `scribble.pl`, `calendar.pl`, `colorlist.pl`, `layout.pl`, and `simplelist.pl`
 * For the `C:\camelbox\examples\Gtk2-Demo` directory: 
   * `program1.pl`
 * For the `C:\camelbox\examples\Gnome2-Canvas` directory (requires that the `Gnome2::Canvas` Perl module be installed): 
   * `canvas.pl`
 * For the `C:\camelbox\examples\Gtk2-GladeXML` directory (requires that the `Gtk2::GladeXML` Perl module be installed): 
   * `hello-world.pl` and `scribble.pl`

<wiki:comment>
vi: set filetype=googlecodewiki shiftwidth=2 tabstop=2 paste:
</wiki:comment>
