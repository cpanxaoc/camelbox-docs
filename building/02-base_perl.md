#summary Building Perl 5.10.0 on Windows
#labels Phase-Implementation

http://code.google.com/p/camelbox CamelBox Home Page ::
BuildStart Build Start ::
BuildSetup Build Setup ::
BuildPerl Building Perl ::
BuildCoreGtk Building Core GTK Libs ::
BuildExtraGtk Building Extra GTK Libs ::
BuildExternalApps Building External Gtk2-Perl Apps ::
Gtk2PerlLinks Gtk2-Perl Links Page ::
Credits Camelbox Credits

# Building Perl #
Use `dmake` to build Perl; [the Perl Win32 README file](http://http://perldoc.perl.org/perlwin32.html) is the source of the below instructions
- Verify your `PATH` contains both MinGW and the Windows `System32`
  directories

- Unpack your Perl source distribution
  - `tar -zxvf perl-5.10.0.tar.gz`
- Enter `$PERL_SRC/win32/` and edit the file called `makefile.mk`; you'll
  want to change the following makefile variables:
  - `INST_DRV` is the drive you want to install Perl to (`C:`)
  - `INST_TOP` is the directory on that drive to install Perl into
    (`$INST_DRV\camelbox`)
  - If you uncomment and use `INST_VER`, the Perl version will be tacked onto
    the `$INST_PATH` path (`$INST_DRV/$INST_PATH/$INST_VER`)
  - `CCHOME` needs to be set to the home directory for C compiler
    (`C:\camelbox`)
  - *OPTIONAL*: Replace the file `perlexe.ico` with a Windows Icon file of your
    own making.  If you are going to replace the icon, you need to pack it
    first
- Build under MinGW `bash`
  - Your path should look something like:
  - `/mingw/bin:/usr/bin:/usr/sbin:/c/Windows/System32`
- Run `dmake` with no arguments in the `$PERL_SRC/win32/` directory.  If
  the binaries from MinGW (above) are in the `%PATH%`, then `dmake` should
  start building Perl
- *Optional* After `dmake` builds Perl, you can run `dmake test` to run the
  tests that come with the Perl distribution.  All of the tests (about
  111,000 of them) pass for me except one, something about Math::!BigInt.
- Type `dmake install` in order to install Perl into the directory
  `$INST_DRV/$INST_TOP` or `$INST_DRV/$INST_TOP/$INST_VER` if you uncommented
  that makefile variable.
- *OPTIONAL*: Move/copy the file `prove.bat` to plain `prove`, so you can
  prove tests without opening a new shell window.
- Set up CPAN 
  - Ensure that you are on a network that has FTP open/available
  - Open a DOS/zsh window
    - DOS window: type `set HOME=C:\camelbox` (note backslash)
    - zsh window: type `export HOME=C:/camelbox` (note forward slash)
    - then type `perl -MCPAN -e shell` to start the CPAN shell
  - The CPAN module should now set itself up automatically... you can safely
    accept the defaults to all prompts
  - If CPAN prompts you for a CPAN URL to download files from, you can type 
    `o conf init urllist` to set up mirror servers
    - Use `o conf commit` to commit any changes to CPAN configuration
  - If you make a mistake, you can go back and edit
    `C:\camelbox\lib\CPAN\Config.pm` and change things in there to get them
    working again
  - Once you get into the shell, search for a random module to make sure that
    the CPAN module downloads all of it's metadata files
    - `m YAML`
  - Package everything up using `hump.sh`

## Build Modules Essential to Using CPAN ##
*NOTE*: No longer needed?  Maybe `cpanm` can take care of the below.

Install YAML and LWP, as it makes CPAN usage a bit easier, CPAN will complain
a lot less when you run it.

    perl -MCPAN -e shell
    install YAML

Package YAML module using `hump.sh`.

    perl -MCPAN -e shell
    install LWP

Package LWP module using `hump.sh`.

Next: BuildCoreGtk Building Core GTK Libs

##Creating The Windows Icon##
- Create the base image file in Gimp.  It should be 48x48 max; scale an image
  down if needed
- Create two other images, one 32x32 and 16x16 in new layers in Gimp.  The
  images should all be anchored in the upper left hand corner of the image
  window.  Like this:

http://camelbox.googlegroups.com/web/gimp_ico_image_layout.jpg
 
- Save the file as a Windows Icon in Gimp.  You'll get some choices for each
  image as far as color depth for each icon that gets saved in the `.ico` file
- Take the `.ico` file and run it through `uuenview`, stripping the `begin`
  and `end` tags


    uuenview -u perlexe-camelbox-logo.ico > perlexe-camelbox-logo.ico.packd

- use the `uupacktool.pl` script to pack/unpack the original image; packing
  the original image:


    GTK2PERL-BUILD# pwd
    C:/temp/perl-5.10.0-src/win32
    GTK2PERL-BUILD# ../miniperl.exe -I../lib ../uupacktool.pl -v -p perlexe.ico perlexe.ico.packd
    Writing perlexe.ico into perlexe.ico.packd

    GTK2PERL-BUILD# ../miniperl.exe -I../lib ../uupacktool.pl -v -u perlexe.ico.packd perlexe.ico
    Writing perlexe.ico.packd into perlexe.ico

vim: set filetype=markdown shiftwidth=2 tabstop=2:
