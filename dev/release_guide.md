#summary List of steps followed for a Camelbox release
#labels Phase-Support

[http://code.google.com/p/camelbox CamelBox Home Page] ::
[Releases2008 2008 Camelbox Releases]

== Release Checklist ==
  * Unpack the binaries from the zipfiles
    * Use the checklist found on BuildSetup  
  * Build the software
    * BuildPerl
    * package the files for each application/libary/module that you build
  * run the app tests in the TestingGuide
  * upload the newly packaged files
  * build the installer
  * test the installer
  * run the app tests in the TestingGuide again
  * release
    * upload the installer
  * add the release info to the releases wiki page, including the text of the release e-mail 
  * tag SVN
  * email release info
    * long e-mail
      * release name, release date, which release series it belongs to
      * a link to the _versions.txt file
      * a link to the installer
      * upgrade recommendations
      * support info and feature suggestions go to the mailing list, include a link to the FAQ
    * shorter e-mails
      * link to google groups post 
      * more info, changes/upgrade recommendations/contact information
      * major changes include...
    * antlinux.com (long)
    * camelbox mailing list (long)
    * gtk2-perl mailing list (short)
    * sandiego.pm list (short)
    * dbi-users/dbi-announce (short)
    * gtkfiles.org (long)

=== Release E-mail ===
Subject: Release: Camelbox 200X.XXX.XXXXZ-xxx

Example: Release: Camelbox 2008.233.0533Z-odin

Body:

I'm pleased to announce a new release of Camelbox, 200X.XXX.XXXXZ
(XXXXXX XXth, 200X).  This is the second release in the 'odin'
(XXXX.x) release series.

What's new? 
[ new features added to this release; bugs fixed in this release]

You can download the new installer here:
[ link to installer]

Upgrade recommendation: Upgrading is recommended if you want to pick
up new features or applications.  Camelbox releases from
"200X.XXX.XXXXZ-nul" and older should be uninstalled before installing
this version.  If you have installed a previous Camelbox 'odin'
release, you can run this installer and just choose the new packages
to install them on top of your existing installation of Camelbox; see
the "Installing Missing Packages" section of the InstallingCamelbox
wiki page [2] for the particulars.

The installer comes with multiple install types; If you're not sure
which install types are which, check the InstallingCamelbox wiki page
[2] for a brief description of all of the install types and package
groups that are available in this release series.

For support with this software, feature requests, or complaints,
please send e-mail to the Camelbox mailing list at
camelbox@googlegroups.com.  Links to the Camelbox Homepage and
Camelbox Frequently Questioned Answers are at the bottom of this
e-mail.

Thanks,

Brian

For the statistically minded:
61 packages available in 10 groups
Unpacked size: 422960685
Archived size: 69318049
Compression Ratio: 0.16 

[ Links to things mentioned in the above message body ]

<wiki:comment>
vi: set filetype=googlecodewiki shiftwidth=2 tabstop=2 paste:
</wiki:comment>
