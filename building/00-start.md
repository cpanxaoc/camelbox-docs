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

-----

### Prerequisites ###
- Perl source
  - http://www.cpan.org/src/README.html
- (Optional)
  [Unix Utilities for Windows](http://sourceforge.net/project/platformdownload.php?group_id=9328);
  this package has a lot of the external utilities you will need when you run
  the CPAN shell or tools on Windows
  - Install to `C:\camelbox\``
  - You'll have to rename some of the `UnxUtilties` binaries so they don't
    conflict with the Windows equivalents ([list of renamed
    UnxUtilities](https://github.com/cpanxaoc/camelbox-docs/blob/master/using/renamed_nix_utilities.md))
  - Or use https://sourceforge.net/projects/gnuwin32?
  - Or build a custom version of the \*NIX tools?
- MinGW
  - The MinGW software is now installed from a centralized installer, from
    which you can install extra packages if you wish (mostly compilers and
    `make`)
  - Camelbox only needs the "MinGW base tools" and "g++ compiler" packages
  - [MinGW Installer downloads](http://sourceforge.net/project/showfiles.php?group_id=2435&package_id=240780)
  - Install to `C:\camelbox\ `
- `dmake`
  - [downloadable from CPAN](http://search.cpan.org/dist/dmake/)
  - Install to `C:\camelbox\ `
  - The `dmake.exe` file and `startup` folder should be placed in the
    `C:\camelbox\bin` folder
  - Make sure the paths to `gcc.exe`, and `dmake.exe` (and it's
    subdirectories) are set in the system's environment
    - Windows 7:
      - Right click on `Computer`
      - Choose `Properties`
      - Click on `Advanced System Settings`
      - Click on the `Advanced` tab
      - Click the `Environment Variables` button
      - In the `System variables` box, scroll down until you get to the `PATH`
        environment variable, then double click to edit it, and add the path
        to `gcc.exe` and `dmake.exe` to the end of that line
        - Use semicolons to separate path components, and quote characters to
          quote any paths with space in them

### Build Order ###
See also the [build
setup](https://github.com/cpanxaoc/camelbox-docs/blob/master/building/01-setup.md)
page, which describes how to unpack the binary zipfiles in order to repackage
them for distribution using the Camelbox installer.  After performing each of
these steps in order, run the following:

- a `xfind` on the `camelbox` directory in order to create a snapshot of what
  files were installed
- a `diff -u` on the file you just created and the file that was created in
  the previous step of the build process; the first file obviously will have
  nothing to `diff` against, but subsequent `diff`s will show how the contents
  change over time.

Points at which you need to run a checkpoint `xfind/diff`:
- After dropping UnxUtils and `dmake`
  - `xfind /camelbox | sed -e '{/^\/camelbox$/d; s/\/camelbox[\\]*//;}' | tee 00-base-unxutils_dmake.txt`
  - MinGW
  - Perl, with simple CPAN config (remember to set `HOME` prior to running CPAN for the first time)
  - Perl YAML module
  - Perl LWP module
  - After copying over the GTK binaries
  - After installing core Gtk2-Perl
  - After any extra Gtk2-Perl modules
  - (Optional) LZMA and 7zip

### Misc. Commands ###
*Note:* the filelist should not contain any bare directories, unless you want
the contents of those directories archived as well; `tar` apparently is
greedy.  Also, `tar` does not like lines that end with `CR/NL` (MS-DOS), it
just likes \*NIX-style line endings (`LF` only).

The GNU `tar` on Windows expects forward slashes in it's filelists:

    tar -cvf - -Tperl-5.10.0.txt > test.list.tar

`perl-5.10.0.txt` looks like this:

    bin/a2p.exe
    bin/c2ph.bat
    bin/config_data.bat
    bin/corelist.bat
    bin/cpan.bat

#### xfind ####
Generate filelists with (`zsh.exe`)

    xfind /camelbox | sed -e '{/^\/camelbox$/d; s/\/camelbox[\\]*//;}'

Windows MS-DOS Box version:

    xfind /camelbox | sed -e "{/^\/camelbox$/d; s/\/camelbox[\\]*//;}"

Generate lists of the packages_dir with:

    xfind . | sed '{/^\.$/d; s/^\.\\//; s/\\/\//g;}' > /temp/_package_dirs.txt

#### LZMA ####
Create a LZMA compressed tarball:

    lzma e /path/to/input/tarball.tar /path/to/output/file.tar.lzma


Create an LZMA compressed tarball using a list of files

    cd C:\camelbox
    tar -cvf - -Tfilelist.txt | lzma e -si /path/to/output/file.tar.lzma

Create an LZMA compressed tarball using a list of files, with comments
filtered out

    cd C:\camelbox
    grep -v "#" /path/to/package_list.txt | tar -cv -T - \
    | lzma e -si /path/to/output/file.tar.lzma


Unpack a LZMA compressed tarball

    lzma d -so demo.tar.lzma | tar -xvf -

-----

Next step: [Setting up files to be placed into archives](https://github.com/cpanxaoc/camelbox-docs/blob/master/building/01-setup.md)

vim: set filetype=markdown shiftwidth=2 tabstop=2:
