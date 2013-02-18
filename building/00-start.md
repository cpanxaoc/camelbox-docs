#summary Introduction to building Camelbox
#labels Phase-Implementation,Featured

[http://code.google.com/p/camelbox CamelBox Home Page] ::
[BuildStart Build Start] ::
[BuildSetup Build Setup] ::
[BuildPerl Building Perl] ::
[BuildCoreGtk Building Core GTK Libs] ::
[BuildExtraGtk Building Extra GTK Libs] ::
[BuildExternalApps Building External Gtk2-Perl Apps] ::
[Gtk2PerlLinks Gtk2-Perl Links Page] ::
[Credits Camelbox Credits]

===Prerequisites===
 * [http://www.cpan.org/src/README.html Perl source]
 * (Optional) [http://sourceforge.net/project/platformdownload.php?group_id=9328 Unix Utilities for Windows]; this package has a lot of the external utilities you will need when you run the CPAN shell or tools on Windows
  * Install to `C:\camelbox\`
  * You'll have to rename some of the !UnxUtilties binaries so they don't conflict with the Windows equivalents ([RenamedUnxUtilities renamed UnxUtilities])
 * MinGW; the MinGW software is now installed from a centralized installer, from which you can install extra packages if you wish (mostly compilers and `make`)
  * Camelbox only needs the "MinGW base tools" and "g++ compiler" packages
  * [http://sourceforge.net/project/showfiles.php?group_id=2435&package_id=240780 MinGW Installer downloads]
  * Install to `C:\camelbox\`
 * `dmake`, [http://search.cpan.org/dist/dmake/ downloadable from CPAN]
  * Install to `C:\camelbox\`
  * The `dmake.exe` file and `startup` folder should be placed in the `C:\camelbox\bin` folder.
  * Make sure the paths to `gcc.exe`, and `dmake.exe` (and it's subdirectories) are set on the machine using the Environment Variables button from the My Computer properties dialog (see the section titled [CamelBox#RunningPreZipped Running a pre-zipped Camelbox package] on the [CamelBox Camelbox Wiki Home Page] for step-by-step instructions on how to change the `%PATH%` environment variable in Windows)

===Build Order===
See also the BuildSetup page, which describes how to unpack the binary zipfiles in order to repackage them for distribution using the Camelbox installer.  After performing each of these steps in order, run the following:

  # a `ufind` on the `camelbox` directory in order to create a snapshot of what files were installed
  # a `diff -u` on the file you just created and the file that was created in the previous step of the build process; the first file obviously will have nothing to `diff` against, but subsequent `diff`s will show how the contents change over time.

  # !UnxUtils, dmake
    * `ufind /camelbox | sed -e '{/^\/camelbox$/d; s/\/camelbox[\\]*//;}' | tee 00-base-unxutils_dmake.txt`
  # MinGW
  # Perl, with simple CPAN config (remember to set `HOME` prior to running CPAN for the first time)
  # Perl YAML module
  # Perl LWP module
  # After copying over the GTK binaries
  # After installing core Gtk2-Perl
  # After any extra Gtk2-Perl modules
    # snapshot the tree after installing the C libraries
    # then snapshot the tree again after installing the Perl modules and libraries
  # (Optional) LZMA and 7zip

===Misc. Commands===
*Note:* the filelist should not contain any bare directories, unless you want
the contents of those directories archived as well; `tar` apparently is
greedy.  Also, `tar` does not like lines that end with `CR/NL` (MS-DOS), it
just likes *NIX-style line endings (`LF` only).

The GNU `tar` on Windows expects forward slashes in it's filelists:
{{{
tar -cvf - -Tperl-5.10.0.txt > test.list.tar
}}}

`perl-5.10.0.txt` looks like this:
{{{
bin/a2p.exe
bin/c2ph.bat
bin/config_data.bat
bin/corelist.bat
bin/cpan.bat
}}}

====find====
Generate filelists with:
{{{
xfind /camelbox | sed -e '{/^\/camelbox$/d; s/\/camelbox[\\]*//;}'
}}}
Windows MS-DOS Box version:
{{{
xfind /camelbox | sed -e "{/^\/camelbox$/d; s/\/camelbox[\\]*//;}"
}}}

Generate lists of the packages_dir with:
{{{
xfind . | sed '{/^\.$/d; s/^\.\\//; s/\\/\//g;}' > /temp/_package_dirs.txt
}}}

====LZMA====
Create a LZMA compressed tarball:
{{{
 lzma e /path/to/input/tarball.tar /path/to/output/file.tar.lzma
}}}


Create an LZMA compressed tarball using a list of files
{{{
 cd C:\camelbox
 tar -cvf - -Tfilelist.txt | lzma e -si /path/to/output/file.tar.lzma
}}}

Create an LZMA compressed tarball using a list of files, with comments
filtered out
{{{
 cd C:\camelbox
 grep -v "#" /path/to/package_list.txt | tar -cv -T - \
 | lzma e -si /path/to/output/file.tar.lzma
}}}


Unpack a LZMA compressed tarball
{{{
 lzma d -so demo.tar.lzma | tar -xvf -
}}}



Next: [BuildSetup Setting up files to be placed into archives]

<wiki:comment>
vi: set filetype=googlecodewiki shiftwidth=2 tabstop=2 paste:
</wiki:comment>
