[Camelbox Home Page](http://code.google.com/p/camelbox) ::
[Gtk2-Perl Links Page](https://github.com/cpanxaoc/camelbox-docs/blob/master/links/gtk_perl_links.md) ::
[Camelbox Credits](https://github.com/cpanxaoc/camelbox-docs/blob/master/about/credits.md) :: 
[Camelbox Docs Home](https://github.com/cpanxaoc/camelbox-docs)

-----

# What to install #
- There's a good list of tools to consider in the [Camelbox Tools Installer](https://github.com/cpanxaoc/camelbox/blob/master/installer/camelbox_tools.nsi) NSI file
- [Unix Utilities for Windows](http://sourceforge.net/project/platformdownload.php?group_id=9328);
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
  - LZMA and 7zip
    - See the [build start page](θttps://github.com/cpanxaoc/camelbox-docs/blob/master/building/00-start.md) for info on how to use lzma on the command line
  - wget & curl


-----

vim: set filetype=markdown shiftwidth=2 tabstop=2:
