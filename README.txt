ezwinports -- MS-Windows ports of Unix and GNU software

Warning: all the ports produced since the year 2021 onwards depend on
the libgcc DLL, and some depend on libstdc++-6.dll, which are not
provided in the zip files.  For the reasons, see below.  If you don't
have these DLLs on your system, you can download them from this site:

  https://osdn.net/projects/mingw/releases

Specifically, download and install these two archives:

  https://osdn.net/projects/mingw/downloads/72215/libgcc-9.2.0-3-mingw32-dll-1.tar.xz/
  https://osdn.net/projects/mingw/downloads/72210/libstdc%2B%2B-9.2.0-3-mingw32-dll-6.tar.xz/

This project is a collection of ports to MS-Windows of GNU and Unix
software packages, which either don't have precompiled Windows
binaries available, or whose existing ports are buggy or broken or
outdated.  All the ports are built using the 32-bit MinGW development
environment, mostly with, but sometimes without, MSYS.  (MSYS is used
to run the `configure' scripts and the subsequent build with the Make
utility, where these make heavy use of Unix-isms.)

The ports are not necessarily of the "latest and greatest" versions
you can find upstream.  But they are well tested and "work for me" in
daily usage (on XP SP3, on Windows 7, and on Windows 10).

For each package, you will find here 2 compressed archives: a source
archive and a binary archive.

The binary archive includes all the executable programs, dynamic
libraries, header files, and all the documentation files -- in
general, everything that is installed by running "make install".  For
those of you who don't have Groff installed, I've included formatted
versions of man pages, so just a port of Less should be enough to
display them.  If the executable programs or libraries need additional
DLLs, they are also included, to make the zip archives self-contained.

To install a binary archive, simply unzip it, preserving the directory
structure recorded in it, and make sure the 'bin' directory is on your
Path.  If you already have a public 'bin' directory, unzip the binary
archive from that 'bin's parent directory.  The other directories,
like 'include', 'lib', and 'share', are populated with the rest of the
package; in particular, the man pages are in 'share/man', and the Info
docs in 'share/info'.  It is advisable to unpack all the archives you
download from this site into the same tree: this will ensure all the
packages work seamlessly together when needed.

The source archive includes everything needed to build the binaries;
in particular, the sources are already patched with all the changes
necessary for the Windows port to function correctly.  The source
archive also includes the results of configuring the package: the
generated Makefile's, the famous config.h header file, etc.  It is
possible that some of the generated files includes traces of my local
directory tree (e.g., I have a Unix-style directory hierarchy under
`D:\usr'), in which case you may need to edit those files to adapt
them to your machine.  In most case, but not always, there's one or
more "DIFFS" files somewhere that show the changes I made relative to
the original sources.

Most of the ports use a small number of DLLs for libraries, such as
libiconv or libintl, which I didn't build myself.  The GPL requires
that the sources of those libraries be available from this very site.
Therefore, I provide those sources in the Dependencies/ subdirectory
of this directory.  The file README.txt there explains how to find the
source distribution for the library you are interested in.

Starting from the year 2021, the ports use newer versions of the
libintl, libiconv, and some other libraries, which depend on the
libgcc DLL.  I cannot distribute the libgcc DLL without providing its
source, which is the humongous GCC source distribution; I'd also need
to update the GCC source distribution each time I upgrade the GCC
installation on my development machine.  Therefore, sadly, I'm forced
to make a step back from providing 100% self-contained binary
packages, and avoid including the libgcc DLL in the binary zips.  If
you don't have a GCC installation, you will need to download and
install the libgcc DLL from the MinGW download site:

   https://osdn.net/projects/mingw/releases

Here's a short description of each package you will find in this
collection:

RCS-5.7-1:

  This is a port of the official RCS v5.7.13 source to MS-Windows.  I
  did this port because the existing GnuWin32 port was broken: any RCS
  command that required running another program as a subprocess (e.g.,
  rcsdiff) would either crash or produce an error message, due to an
  unhandled problem in the Windows versions of the spawn* library
  functions.

flip-1.19

  This is a Windows port of the `flip' utility, which converts newline
  format between Unix LF and DOS/Windows CR-LF conventions.  Its home
  page is http://packages.debian.org/sid/flip.  I like this utility
  better than unix2dos/dos2unix, because (a) it's a single program,
  (b) it doesn't try to convert character sets, (c) it changes files
  in-place while keeping their time stamp intact, and (d) it keeps its
  claws off any binary files, so it's safe.

texinfo-4.13a-w32

  This is a Windows port of the GNU Texinfo package, version 4.13a.
  My reasons for making this port are (1) the makeinfo.exe available
  from GnuWin32 crashes for any non-trivial Texinfo source; and (2)
  info.exe refuses to work on Windows because no one bothered to make
  its terminal display code work on Windows.  This port solves both of
  these problems.

ministat-1.0-w32

  This is a Windows port of the ministat program, you can find the
  original sources here:

   http://packages.debian.org/sid/math/ministat

  AFAIK, there's no Windows port of this program anywhere.  The
  program is handy for computing statistics and significance testing
  of a series of measurements, e.g. running times of some program (for
  performance comparisons).

man-1.4

  A Unix `man' command for Windows.  Unlike all the other packages on
  this page, this one is not a port.  It is a clone of its Unix
  namesake, and has absolutely no code common with its cousins.  I
  wrote it originally as part of the DJGPP project
  (http://www.delorie.com/djgpp/), and later updated it to compile
  with MinGW and run on MS-Windows as a native Windows program.

  If you want to view unformatted man pages, you will have to install
  a port of Groff (it is available from this page, see below).

grep-2.10-w32

  A Windows port of GNU Grep.

  The latest port available from GnuWin32 is of version 2.5.4, which
  was released in Feb 2009, quite some time ago.  Also, it always
  annoyed me that color highlighting of Grep matches is not available
  on MS-Windows.  This port of the latest release 2.10 of Grep fixes
  that.

  To use Perl-style regular expression, Grep needs to be built with
  libpcre, so you have this as a bonus below.

pcre-8.21-w32

  Library of Perl-compatible regular expressions.  I needed this to
  build Grep capable of "grep -P" mode.  (A newer version is available
  below, but this one is still required for the ported Grep.)

gmp-5.0.2-w32
p11-kit-0.9-w32

  Windows ports of, respectively, GMP (the GNU Multiple Precision
  Arithmetic library), and p11-kit (a package to load and enumerate
  PKCS#11 cryptographic modules).  I needed them to build GnuTLS and
  wget, but they can be useful on their own right, so I provide them
  here.  Note that the latest versions of GnuTLS and wget no longer
  use p11-kit.

libxml2-2.7.8-w32

  A Windows build of libxml2 2.7.8.

  The available Windows ports are compiled with MSVC, which means they
  are not 100% compatible with MinGW.  The libxml2 sources include a
  JScript configuration script, suitable for running with cscript, and
  a bunch of Makefile's to go with it.  But it looks like this
  suffered some bitrot, and it doesn't support running the test suite,
  which was important for me to make sure the build is dependable.

  So instead of using this Windows-specific stuff, I configured the
  package with MSYS and built it using the Posix configury.  The
  result passed all the tests.

  To compile and link programs against libxml2, you will need to
  install libiconv, whose headers and import libraries need to be
  available to the compiler and linker.  You can find the MinGW port
  of libiconv on the MinGW site:

    http://sourceforge.net/projects/mingw/files/MinGW/Base/libiconv/

  (The libxml2 binaries found here were linked against the
  libiconv-1.13.1-1-mingw32-dev.tar.lzma tarball.)

which-2.20-2-w32

  A Windows port of GNU Which v2.20

  GnuWin32 does offer a port of this latest version of Which, but it
  has a few bugs.  This port improves on that one:

   . Under -a, it shows the executables in exactly the same order as
     the shell would look them up.
   . It behaves like on Unix when run by a privileged user.
   . Supports home directories both if pointed to by the HOME
     environment variable and (if HOME is not set) if pointed to by
     the USERPROFILE variable.
   . Is more consistent in its support for backslashes and forward
     slashes.
   . It fixes a couple of minor bugs.

  This second upload fixes a bug whereby 'which' would sometimes crash
  when invoked with the -a switch.

lzip-1.13-rc3

  A Windows port of Lzip, "a lossless data compressor based on the
  LZMA algorithm".

  The only port of Lzip I'm aware of is the one available from the
  Lzip download page, which is of version 1.11, quite old.  Here you
  have the latest version as of this writing.

xz-5.0.3-w32

  A Windows port of xz, lzma, and liblzma.

  With many GNU projects starting to use .tar.xz archive as their only
  format of tarballs, having this in your development toolbox is
  really a must.

bzip2-1.0.6-w32

  A Windows port of bzip2 and of libbz2.

  GnuWin32 has only a very old version.  MinGW does offer version
  1.0.6, but it was built in a way that makes the binaries dependent
  on the DLL version of libgcc.  This means that anyone redistributing
  these binaries would have to also provide the humongous 75-MB source
  tarball of GCC, to comply with the GPL license.  I think this is
  ridiculous, so I made my own port, which is free of this
  restriction.  While at that, I also fixed a couple of bugs in the
  existing ports (e.g., try "bunzip2 -c SOMETHING.bz2 > nul", which is
  important for measuring decompression speed, if for nothing else).

  Note that bzip2.exe in this port is statically linked with libbz2
  library, so it doesn't need the DLL to run -- another advantage.

mairix-0.22-w32

  A Windows port of mairix, a program for indexing and searching email
  messages (http://www.rpcurnow.force9.co.uk/mairix/).

  As far as I know, there are no native Windows ports of mairix
  available.  I needed it to be able to search my vast email archives
  using the Emacs mairix-el package.  I only tested this port with the
  mbox mail folders, which is all I have, so caveat emptor.

ncurses-5.9-w32

  A Windows port of ncurses 5.9.  I don't think there's a native
  Windows port of this available anywhere.  I needed it for Readline
  and for Gawk (below), but it should be useful for many other
  programs as well.  AFAIK, there was never a curses library for
  Windows, except for a very old port of PDCurses.

readline-6.2-w32

  A Windows port of the GNU Readline library.  The versions offered by
  GnuWin32 are very old.  This is the port of the latest release, and
  it is built with ncurses, so no Windows-specific hacks were necessary
  in the sources.

openssl-1.0.0g-w32

  A Windows port of the OpenSSL package.  I needed it for porting XAR
  (below), and the build offered by openssl.org seems to be compiled
  with MSVC and also it was unclear to me which of the various packages
  to install for my needs.  So I just built my own.

xar-1.5.2-w32

  A Windows port of XAR, the extensible archiver from
  http://code.google.com/p/xar/.  I'm not aware of any Windows ports of
  this available, and I'm not surprised: the code is full of stuff that
  is only available on latest Posix systems; porting that was quite a
  job.  The main reason why you'd be interested in the result is that
  it has full support for NTFS security, and can record and restore the
  entire NTFS security descriptor of each file, complete with its
  owner, primary group, and DACL.  (Caveat: use this feature and the
  associated -p command-line option with caution: if you don't know
  what you are doing, you can easily restore files in a way that will
  prevent you from modifying or deleting them.)

mpfr-3.1.0_p2012-03-12-w32

  This is a Windows build of the GNU MPFR library version 3.1.0 with
  the cumulative patches as of 12 Mar 2012 applied.  I needed this for
  building a development version of Gawk, but I understand many
  projects that use extended-precision calculations can use this
  (together with GMP, upon which MPFR is built).  MinGW, the only
  alternative, offers a relatively old port, which is at least partly
  dependent on the GCC runtime DLL.

autoconf-2.65-msys

  This is version 2.65 of GNU Autoconf configured for use with the MSYS
  environment.  The MSYS site does not offer a download of this
  version, which is needed for configuring GNU Emacs.  Unzip the
  archive from the root of the MSYS tree (_not_ the MinGW tree!).

automake-1.11.6-msys

  This is version 1.11.6 of Automake configured for use with the MSYS
  environment.  It is required for configuring and building GNU Emacs
  from its bzr repository.  Unzip the archive from the root of the MSYS
  tree (_not_ the MinGW tree!).

idutils-3.2.99-2-w32

  This is a Windows port of GNU ID Utils.  ID Utils and the
  corresponding Emacs front end is an essential part of my Emacs-based
  development tool-chain.  Without ID Utils, there's no easy way of
  finding your ways in a large and complex software project.

  Unfortunately, the port available from GnuWin32 is broken and does
  not work (mkid emits an error message and quits).  So I made my own
  Windows port of ID Utils version 3.2d (an interim version that was
  only available from alpha.gnu.org in the past, and now deleted even
  from alpha.gnu and not available anymore on any GNU site, although
  you can still find it on the net if you are persistent enough).
  That port was done in May 2005.  Later, I upgraded that port using
  the user-visible changes from ID Utils 4.5, because I needed ID
  Utils to support Java and Lisp, which was not available in v3.2d.

  If you wonder why not just port ID Utils 4.6, then you should know
  that I found out to my astonishment that 99% of the changes between
  4.6 and 3.2d have no user-visible effect.  The bulk of the changes
  were "portability enhancements".  As result of these "enhancements",
  the number of files imported from gnulib (in the lib/ subdirectory)
  went up from 38 to 143(!), the configury of the package became much
  more complex, but the net gain for users in terms of functionality
  was almost nil.  Needless to say, none of the real problems that
  made the Windows port buggy were fixed by these "enhancements"...

  So instead of porting ID Utils 4.6, I copied the few changes that
  actually contributed to user-visible functionality to the old 3.2d
  sources, added to lib/ 3 files that were required for those changes,
  fixed a couple more of Windows-related problems (e.g., that `sbrk' is
  not available, and therefore "mkid -s" would not display meaningful
  memory-usage statistics), and that's what I have now.  I call this
  version 3.2.99, because its source code base is still largely 3.2
  vintage.  The ChangeLog file in the top-level directory describes the
  Windows-related changes I made in more detail.  The file
  DIFFS-3.2d-3.2.99.dif shows all the diffs wrt version 3.2d, which
  include modifications copied from ID Utils 4.5.  I also modified the
  Copyright notices of all the old files, to have their years extended
  through 2011. 

  This 2nd upload fixes an upstream bug (only corrected in ID Utils
  4.6) whereby "lid -F" would mishandle open-ended ranges like
  2000.. or ..200.

findutils-4.2.30-5-w32

  This is a Windows port of GNU Findutils 4.2.30.  It includes all the
  binaries in the original distribution, even those, such as code.exe,
  frcode.exe, and bigram.exe that you are not supposed to need.  I
  made this port because the GnuWin32 port of v4.2.20 had several
  grave problems: find.exe was abysmally slow, xargs.exe didn't work
  at all, and neither did locate.exe.  This port includes updatedb.bat,
  which is a stripped-down replacement for the original updatedb Unix
  shell script.  Please note that xargs.exe in this distribution has
  some issues that cause it to fail sometimes.  But find.exe and
  locate.exe work flawlessly for me for several years.

  This fifth upload solves a bug whereby 'find' would sometimes
  infloop when some of the directories it traverses are symlinks to
  other directories.  The solution is to never descend into a
  directory that is a symlink (i.e., this port always behaves as if
  the -P option was specified).

  As an additional bonus, this port includes 64-bit binariesin a
  separate findutils-4.2.30-4-w64-bin zip file, prepared by Erwin
  Waterlander <waterlan@xs4all.nl>.  If you are running a 64-bit
  Windows version, you may wish to use these 64-bit executables, as
  they are about 5 times faster than the 32-bit ones.

zlib-1.2.8-2-w32

  This is a Windows build of the latest version 1.2.8 of the venerable
  zlib library.  MinGW provides this version also (under the name
  libz-1.dll), but it depends on GCC's libgcc_s_dw2-1.dll, which has
  the same problems as described under bzip2 above, and in addition
  tends to crash programs at exit (due to a grave bug in the libgcc
  DLL).  So I provide here a build that don't have this problem.

  You should be able to replace your older zlib1.dll with this
  version, as the latter is binary-compatible with the old one.

  This second upload fixes a problem with the zlib.pc file which would
  fail compilation and linking against zlib in packages that use
  pkg-config to determine the necessary compilation and link flags.

tiff-4.0.3-w32

  A Windows build of the latest version 4.0.3 of TIFF library and
  utilities.

  Available ports of this library are way outdated.

librsvg-2.40.1-2-w32

  This is a Windows build of the latest version 2.40.1 of librsvg, the
  library for manipulation, conversion, and viewing of SVG images.
  The only other existing port of librsvg that is known to me is from
  the GTK project, but is outdated, uses much more dependencies that
  is strictly needed on Windows, and also involves a small "DLL hell",
  since various dependencies need different versions of the same
  library (freetype and libpng).  By contrast, this port requires only
  the minimal set of dependencies (see below), and only one version of
  each dependency.

  This second upload fixes a problem with packaging the binary
  archive, which could result in librsvg not working unless installed
  in d:/usr.

pango-1.36.1-2-w32

  Pango is a library for laying out and rendering of text, with an
  emphasis on internationalization.  This is a Windows build of the
  latest version 1.36.1.  It is required for librsvg (see above).

  This second upload fixes a problem with packaging the binary
  archive, which could result in Pango not working unless installed in
  d:/usr.

cairo-1.12.16-w32

  This is a Windows build of the latest version 1.12.16 of Cairo, a 2D
  graphics library with support for multiple output devices.  This
  minimal build provides only the win32 back-end and a minimal set of
  "surfaces" (including SVG) which are are needed for librsvg (above).

pixman-0.32.4-w32

  A Windows build of the latest version 0.32.4 of Pixman, a library
  that provides low-level pixel manipulation features.  It is required
  for Cairo, and thus needed for librsvg (above).

libcroco-0.6.8-w32

  This is a Windows build of libcoroco, a standalone CSS2 parsing and
  manipulation library.  It is required by librsvg (above).

gdk-pixbuf-2.30.2-w32

  The Gdk Pixbuf is a toolkit for image loading and pixel buffer
  manipulation.  This is a Windows build of the latest version 2.30.2
  of Gdk Pixbuf.  It is needed for librsvg (above).

glib-2.38.2-w32

  A Windows build of the latest version 2.38.2 of Glib, a set of
  low-level libraries useful for providing data structure handling for
  C, portability wrappers and interfaces for such runtime
  functionality as an event loop, threads, dynamic loading and an
  object system.  It is required for librsvg (above).

lzo-2.06-w32

  LZO is a data compression library which is suitable for data
  decompression and compression in real-time.  This is a Windows build
  of its latest version 2.06.  This library is required for one of the
  components of Cairo (above).

git-merge-changelog-0.1-2-w32

  If you use git (msysGit) on Windows, you will have merge problems
  when merging from branches that modified ChangeLog files.  This
  merge driver solves those annoying problems, but msysGit
  distribution doesn't provide it for some reason, and there doesn't
  seem to be a build-ready source archive available anywhere.
  Building out of gnulib git repo, where the sources live, on a
  Windows system is not for the faint at heart.  So here you have the
  package, complete with sources and binaries.  See the file
  README.txt for installation and configuration instructions.

  This second upload fixes a bug whereby the merge would always
  produce a file with DOS-style CR-LF end-of-line (EOL) format, even
  if the original files used Unix EOLs.  This is an upstream bug,
  fixed in this port.

hunspell-1.3.2-3-w32

  This is a Windows port of Hunspell v1.3.2.  Hunspell
  (http://hunspell.sourceforge.net/) is a spell-checker with support
  for peculiarities of many languages and with Unicode character
  codepoints support out of the box.  To the best of my knowledge,
  there's no other Windows port of Hunspell.  In addition, this port
  includes fixes for bugs, both Windows-specific and
  platform-independent.  The result works well for me as the back-end
  of the spell-checking features in Emacs.  The interactive
  curses-based user interface also works, although (due to limitations
  of the ported ncurses) only characters in the current ANSI codepage
  are supported.

  The binary distribution includes dictionaries for US English and UK
  English.  You can find the dictionaries for other languages on the
  Internet; install them into share/hunspell sub-directory of your
  Hunspell installation directory.

  This third upload fixes a subtle issue with running Hunspell under
  Emacs 24.4 and later, whereby the default dictionary would not be
  set correctly during initialization.  All the previous bugfixes are
  also included, such as failure to rename the temporary file with the
  text corrected by spell-checking to the original name of the file
  submitted to the speller, and a couple of other minor bugs reported
  lately to the Hunspell bug tracker.

giflib-5.1.0-w32

  This is a Windows build of the latest version 5.1.0 of the giflib
  library.  Gnuwin32 has only an ancient version 4.1.4, and I didn't
  find any Windows port of the 5.x series.  (The 'lua-files' project
  seems to have a binary, but no sources.)  The few problems that I
  found and corrected while testing the previous port were accepted
  upstream, so this release builds with MinGW out of the box; thus no
  DIFFS here.

libpng-1.6.12-w32

  This is a Windows build of the latest version 1.6.12 of libpng, the
  official PNG image library.  It includes several important security
  and stability fixes, and is binary-compatible with the previous
  1.6.x releases, so you are well advised to upgrade.

  As GnuWin32 libpng ports are very old, and even the GTK site falls
  behind, there's a need to have the latest PNG library available for
  Windows.  So here you have that.

jpeg-v9a-w32

  This is a Windows build of the latest version 9a of jpegsrc, the
  IJG's library for JPEG image compression.

  Like with libpng, it's high time Windows users had the latest JPEG
  library available to them.

jpeg-v8d-w32

  This is a Windows build of an older version 8d of jpegsrc, the IJG's
  library for JPEG image compression.  It is here for those users who
  have binaries linked against this older version (since the MSYS2
  project doesn't yet offer v9a).

libcrypt-w32

  This is a small library to encrypt and decrypt a block of data.
  This is needed for Guile and GDB below.

gc-7.2f-w32

  This is a Windows build of the Boehm-Demers-Weiser garbage collector
  (a.k.a. "Boehm GC").  It is used by Guile below.  I'm not aware of
  any Windows binaries of this library.  The library was built with
  Win32 threads (_not_ pthreads!), so if you need to use it with a
  package that uses pthreads, these binaries are not for you.

libunistring-0.9.3-w32

  This is a Windows port of libunistring 0.9.3, a library that
  provides functions for manipulating Unicode-encoded strings, and for
  manipulating C strings according to the Unicode standard.  The MinGW
  site offers a binary distribution of the same version, but it is
  severely broken on Windows: it cannot be used after setting a
  non-default locale by calling 'setlocale'.  This port fixes the bugs
  which cause this breakage, and which render Guile (below) unusable
  for i18n features.

libffi-3.1-w32

  This is a Windows build of the latest version 3.1 of the libffi
  library, which provides a portable, high level programming interface
  to various calling conventions.  It is required for Guile below and
  also for librsvg above.

guile-2.0.11-2-w32

  This is a Windows port of the latest Guile 2.0.11.  It is heavily
  patched wrt the upstream sources, and supports all features that can
  be reasonably supported on MS-Windows.  One notable exception is
  threads: this port was configured without threading support, because
  Guile built with threads (using the Windows port of pthreads) is
  unusable: it hangs or crashes in many simple and trivial programs,
  and cannot even compile its own Scheme files.  The Guile binary and
  library in this distribution pass all the tests in the test suite.
  I'm not aware of any reliable Windows port of Guile anywhere.

  If you install this anywhere but d:/usr, you will need to set 2
  environment variables:

    set GUILE_LOAD_PATH=x:\foo\share\guile\2.0
    set GUILE_LOAD_COMPILED_PATH=x:\foo\lib\guile\2.0\ccache

  where "x:\foo" is the directory from which you unzipped the Guile
  binary zip file.

  This 2nd upload fixes a couple of minor problems in the code, and
  also includes DLL shared libraries in addition to static libraries.

libgsf-1.14.30-w32

  This is a Windows build of libgsf, the GNOME Structured File
  Library, a library for reading and writing structured file formats.
  It supports reading text, XML, compressed data, MS OLE2, metadata,
  and OASIS Open Document streams.  It is required by libpst, but can
  also be useful on its own, in particular for porting GNOME packages.

libpst-0.6.63-w32

  This is a Windows port of the latest release 0.6.63 of libpst, a
  library and a set of utilities to read and convert Outlook *.pst
  files.  It can convert email messages in the *.pst files to mbox or
  MH or KMail files, and Contacts to vcard or ldif formats.  (I only
  tested and used the conversion to mbox files, including their
  display in Emacs.)  The port includes a few Windows specific patches
  to fix display of non-ASCII characters on the Windows console.

  I'm not aware of any recent Windows port of this package.  It was
  useful for me, so I'm guessing it might be useful to others.

libtasn1-4.2-w32

  This is a Windows build of version 4.2 of the GNU ASN1 library.  A
  port of a newer version 4.9 is available here, but I'm keeping this
  because some packages here were linked against this older version.

nettle-2.7.1-w32

  A Windows build of version 2.7.1 of the Nettle library.  A port of a
  newer version 3.3 is available here, but I'm keeping this because
  some packages here were linked against this older version.

libidn-1.29-w32

  A Windows port of Libidn, a package designed for internationalized
  string handling based on the Stringprep, Punycode and IDNA
  specifications defined by the IETF Internationalized Domain Names
  (IDN) working group, and used for internationalized domain names.
  Used by Wget for correct handling of internationalized names of
  hosts and URLs.

gnutls-3.3.11-w32

  A Windows port of GnuTLS 3.2.11.  Needed to build wget (below), and
  is also useful for Emacs.  A port of a newer version 3.4.15 is
  available here, but I'm keeping this because some packages here
  (wget) were linked against this older version.

pcre-8.36-w32

  Version 8.36 of the library of Perl-compatible regular expressions.
  I needed this to build wget (below).

  The C++ bindings of this library is provided only as a static
  library, to avoid dependency on libstdc++ DLL.

libpsl-0.6.2-w32

  This is a C library for handling the Public Suffix List, a list of
  known domain suffixes, such as .com and .co.uk, under which Internet
  users can register domain names.  This library is used by wget
  (below) for checking cookies.  I'm not aware of a Windows port of
  this library.

wget-1.16.1-w32

  A Windows port of wget 1.16.1.

  The GnuWin32 port is of version 1.11.4, which was released a few
  years ago.  This is the latest released version, as of this writing
  (Dec 2014).  It was configured and built with as many optional
  features as practical on Windows.

pkg-config-0.28-w32

  This is a MinGW build of the latest version 0.28 of the pkg-config
  utility.  The GTK site, which previously offered a slightly outdated
  version 0.26, no longer does that, and I'm not aware of any other
  Windows port of pkg-config.  So here you have the latest version.

libXpm-3.5.11-2-w32

  This is a MinGW build of the latest version 3.5.11 of the libXpm-noX
  DLL.  The last version offered by GnuWin32 is the ancient v3.5.1,
  and later versions are not available in a single binary package that
  includes everything needed to build programs (like Emacs) against
  libXpm; instead, you need to collect files from various binary and
  source packages.  Here you have everything together, and as a bonus
  this includes a small program cxpm for checking validity of XPM
  files.

  This second upload fixes a few problems in the header files that go
  with the library.

libtasn1-4.9-w32

  This is a Windows build of version 4.9 of the GNU ASN1 library, a
  highly portable C library that encodes and decodes DER/BER data
  following an ASN.1 schema.  It is used by GnuTLS for reading
  certificate files.

nettle-3.3-w32

  A Windows build of the latest version 3.3 of the Nettle library, a
  low-level cryptographic library used by GnuTLS and other packages.

gnutls-3.4.15-w32

  A Windows port of GnuTLS 3.4.15, the latest stable release of
  GnuTLS.  Needed to build wget (below), and is also useful for Emacs.

  Unlike a previous port of GnuTLS 3.0.9, this port was built
  without the PKCS#11 library, because that one is only needed for
  authentication using smart cards, for which on Windows you will have
  to rebuild GnuTLS with the corresponding DLLs for hardware support.
  Therefore, there's no p11tool.exe in the binary distribution.

  Another change is that this version comes with Guile bindings, so if
  you have Guile installed, you will be able to use GnuTLS from Guile
  programs.

  The C++ bindings of GnuTLS are only provided as a static library,
  since a DLL built for that is dependent on the libstdc++ DLL, which
  will then require me to provide the whole GCC source tarball here,
  and might also get you into a DLL hell if your GCC version is
  different from mine.  Sorry.

zstd-1.1.1-w32

  This is a Windows build of Zstandard v1.1.1, a real-time compression
  algorithm, providing high compression ratios.  Included are a couple
  of programs to compress and uncompress files, and a library that
  allows including zstd compression capabilities in applications.

gperf-3.1-w32

  This is a Windows build of the latest version 3.1 of GNU 'gperf'
  perfect hash function generator utility.  The only other Windows
  port of 'gperf' is available from the GnuWin32 site, which offers an
  ancient version 3.0.1.

lz4-1.7.5-w32

  LZ4 is a fast, scalable, lossless compression algorithm.  This is a
  Windows port of the latest release 1.7.5 of LZ4.  It is needed for
  libarchive (below), but is also useful on its own right.  I'm not
  aware of any Windows port of this package.

libarchive-3.3.1-w32

  A Windows port of the latest release of libarchive and of bsdtar,
  bsdcpio, and bsdcat programs.  The latter is a relatively new
  addition to the package.

  GnuWin32 has an old version 2.4.12 released in 2008.  MinGW offers a
  newer version 2.8.3, but it is still old (7 years ago).  Even the
  MSYS2 project offers only v3.1.  This is the port of the latest
  release, and it fixes a few upstream bugs.

  This latest release of bsdtar is really wonderful: it supports most
  every format of compressed archives on Earth.  gzip, xz, lzma, zip,
  rar, 7-zip, pax, rpm, even CAB!  You name it, it supports that.
  More importantly, it does all compression and decompressing in
  memory, without invoking external programs, so it's faster (but
  still uses the same algorithms and code via the corresponding
  libraries it links against).  It also supports UTF-16 file names on
  Windows, therefore you can now unpack archives created in other
  Windows locales, and still have the files unpack under correct
  names.

  In general, the degree of Windows support is very good in this
  package, in stark contrast to GNU Tar, whose current maintainers are
  much less friendly to Windows support.

lcms2-2.8-w32

  This is a Windows build of the latest version 2.8 of Little CMS, a
  color management engine.  I needed it for Emacs, but it is useful on
  its own right.

jansson-2.10-w32

  This is a Windows build of the latest version 2.10 of Jansson, a C
  library for encoding, decoding and manipulating JSON data.  I needed
  it for Emacs, but it is useful on its own right.

grap-1.45-w32

  A Windows port of the latest version 1.45 of the Grap preprocessor.
  The GnuWin32 site offers only an outdated version 1.43, and I'm not
  aware of any other/later native Windows port.  Here you have the
  latest release that includes all the latest additions.

  The binary was configured to look for grap.defines in the
  d:/usr/share/grap/ directory, and if not found there, in the
  ../share/grap/ directory relative to where grap.exe lives.  If none
  of this fits the way you installed the binary distribution, you can
  set the GRAP_DEFINES environment variable to point to the correct
  directory.

uchardet-0.0.6-w32

  uchardet is an encoding detector library, which detects encoding of
  text by examining its bytestream.  I needed it for Groff, but it can
  also prove useful on its own right.  The binary package includes
  also a command-line tool which you can invoke on a file whose
  encoding you need to know.

groff-1.22.4-w32

  A Windows port of the latest release 1.22.4 of GNU Groff.

  GnuWin32 offers a rather old version 1.20.1 of Groff, released in
  Jan 2009.  The latest man pages emit more and more error messages
  with old versions of Groff, because they don't support several new
  roff features.  Here you have the latest released version with all
  the new stuff.

  Note: this distribution was built without Ghostscript being
  installed, so the HTML back-end (grohtml) and the PDF formatter
  (pdfroff) were not tested, and might even not work due to some
  missing file or font.

  The package was configured to be installed under d:/usr, but it
  should work even if you install it in a different place.  If you did
  install in a different place, and it doesn't work for some reason,
  set the GROFF_BIN_PATH to point o the place where you put the *.exe
  programs, and perhaps also set the other GROFF_*_PATH variables
  documented in the Groff man page.

boost_1_69_0-w32

  This is a MinGW build of version 1.69.0 of the Boost libraries.  The
  few available binary distributions out there are either very old or
  for the wrong compilers (MSVC and MinGW64), so I decided to build my
  own.

  The Boost Python libraries were built against Python 2.6.6, so if
  you need to use those components, you will need to install Python
  from https://www.python.org/download/releases/2.6.6/.

  Unlike all the other packages on this page, the source distribution
  is just a copy of the tarball downloaded from the Boost site.  This
  is because the distribution is so large that making a zip archive
  from it would produce a humongous large file.

source-highlight-1.3.8-w32

  This is a Windows build of GNU Source-highlight 3.1.8.  GnuWin32
  offers an outdated version 1.2.1, which also doesn't include the
  library against which applications could link (which was only
  introduced in v3.0 of the package).  Here you have a newer version.
  I also included the Boost headers which I think might be needed to
  compile applications that are linked against the
  libsource-highlight.a library.

  There's no DLL in the binary package, only a static library.  This
  is both because the build fails to produce a DLL (due to libtool
  snafu specific to Windows), and because a DLL would have probably
  depended on libstdc++ and libgcc DLLS, so I wouldn't be able to
  distributed it anyway.

freetype-2.10.0-w32

  A Windows build of the latest version 2.10.0 of Freetype, a software
  library to render fonts.  HarfBuzz (below) needs it.  GnuWin32
  offers only a very old version 2.3.5, and the Freetype site itself
  has only binaries built with Microsoft's Visual Studio.

graphite2-1.3.13-w32

  Graphite is a system to handle fonts for some rarely-used
  languages.  HarfBuzz (below) needs it to be able to render the
  Graphite fonts.  This is a Windows build of the latest release of
  Graphite2.  I'm not aware of any site that offers precompiled
  binaries for Windows.

harfbuzz-2.4.0-w32

  HarfBuzz is a modern text shaping engine supporting OpenType and
  TrueType fonts.  This is a Windows build of version 2.4.0 of
  HarfBuzz.  I needed it for Emacs.  Unlike some other Windows ports,
  this one was built with the minimal set of dependencies, basically
  just Graphite2 and Freetype.  All the other dependencies are
  optional, aren't needed for text shaping per se, and just bloat the
  library and make its future updates more complicated.  For this
  reason, the binary distribution doesn't include hb-view and other
  utility programs: they require more dependencies than are needed for
  text shaping.

source-highlight-1.3.9-w32

  This is a Windows build of GNU Source-highlight 3.1.9, the latest
  official version of that package.  GnuWin32 offers an outdated
  version 1.2.1, which also doesn't include the library against which
  applications could link (which was only introduced in v3.0 of the
  package).  Here you have a full latest version.  I also included the
  Boost headers which I think might be needed to compile applications
  that are linked against the libsource-highlight.a library.

  This is needed for recent ports of GDB.

gdb-11.1-w32

  A 32-bit Windows build of version 11.1 of GDB.  The MinGW
  site lags behind the official releases; here you have the latest
  release that supports both Python and Guile.  One caveat: you will
  have to download and install Python 2.6.6 from
  https://www.python.org/download/releases/2.6.6/; gdb.exe in this
  archive depends on the Python library and DLL, and will not run
  without it being available on your system.  (I don't want to
  distribute Python binaries, because then I would also need to
  provide the Python sources from this site, which is way too much.)

  The NEWS file in 'share/doc/gdb-VERSION/' describes all the new and
  improved features in this release.

  Starting with GDB 7.10, the data files in this port are installed
  into a version-specific directory 'share/gdb/VERSION/'.  This is so
  you could keep previous versions of GDB renamed as, say,
  gdb-x.y.z.exe, and still be able to invoke them and let them find
  their data files.  If this is the first GDB port you are installing
  that uses this structure, I suggest to move the data files of the
  previous version -- everything under share/gdb/ -- into a version
  specific subdirectory share/gdb/X.Y.Z/, where X.Y.Z is the version
  of GDB you had before this one.

  Guile dependencies are included in this binary distribution.
  If you install this anywhere but D:\usr, you will need to set 2
  environment variables:

    set GUILE_LOAD_PATH=x:\foo\share\guile\2.0
    set GUILE_LOAD_COMPILED_PATH=x:\foo\lib\guile\2.0\ccache

  where "x:\foo" is the top directory of the GDB installation, under
  which you have the tree of the unzipped files.  (If you used
  unzip.exe to unzip the distribution, the top directory is the one
  from which you ran unzip.exe.)  These variables are required for the
  Guile support in GDB to be able to initialize itself.

  If GDB complains at startup about being unable to load Python
  modules, you may need to set the PYTHONPATH environment variable to
  point to your Python 2.6.6 installation, like this:

    set PYTHONPATH=C:\Python26\DLLs;C:\Python26\Lib;C:\Python26\lib\plat-win;C:\Python26\Lib\lib-tk;C:\Python26;C:\Python26\Lib\site-packages

  (assuming you installed Python in C:\Python26).

  This port also supports TUI, the Text-mode User Interface; invoke
  GDB with the -tui command-line option to activate it.  Note that
  this mode should only be used when invoking GDB from the shell
  prompt, not, for example, when invoking GDB as a subprocess of
  Emacs.

  This port also supports source highlighting via the source-highlight
  library, and the new 'styling' feature of GDB, which together cause
  the GDB output to have nice colors.

file-5.41-w32

  A Windows port of the latest version 5.41 of the 'file' utility and
  its libmagic library.

  The latest GnuWin32 port is of version 5.03, released in May 2009.
  It has a subtle bug that breaks libtool, and also a few Windows
  specific gotcha's (e.g., try "file NUL" or "file -").  This port of
  the latest upstream release fixes those bugs, and includes support
  for looking inside compressed files.

sqlite3-3.37.0-w32

  A Windows build of version 3.37.0 of SQLite, a library that
  implements an SQL database engine.  I needed this for Emacs, but the
  library can be useful on its own.  This includes the sqlite3
  program, the sqldiff program (for comparing databases), and the full
  documentation of the SQLite library.  (The latter two parts were
  collected from sources other than the corresponding source
  archives.)  The documentation is just a verbatim copy of the
  separate sqlite-doc distribution you can find on the SQLite site,
  https://www.sqlite.org/download.html.  I just unzipped it into the
  share/doc/ subdirectory.

  Please note that the library was built without THREADSAFE support,
  as the Autoconf build doesn't directly support that (one needs to
  tweak the generated Makefile, which I didn't do).

emacs-28.2-2-w32

  A 32-bit Windows build of GNU Emacs version 28.2.  The MS-Windows
  binaries of Emacs available from the GNU FTP site include only a
  64-bit build, and cannot run on Windows before Windows 7.  This
  32-bit build runs on Windows XP and later, and is supposed to be
  able to run on Windows 9X as well (but was not actually tested
  there).

  This second upload fixes a packaging mistake whereby HarfBuzz was
  omitted from the original binary zip.

  The binary archive includes, in addition to Emacs itself, the
  minimal set of dependencies that I thought would present a
  reasonably feature-full Emacs.  The following optional features are
  included in this binary archive:

    . Complex text shaping (via HarfBuzz)
    . Display of XPM images (via libXpm)
    . Display of PNG images (via libpng)
    . TLS network connections (via GnuTLS)
    . Decompression of *.gz files (via zlib and gzip/gunzip)
    . HTML and XML parsing (via libxml2)
    . JSON parsing (via libjansson)

  To install the binary archive, unzip it and make sure the 'bin'
  directory created by unzipping is on your Path.

  You will also need the libgcc DLL, libgcc_s_dw2-1.dll.  I cannot
  distribute this DLL for legal reasons, but if you don't have it
  already, you can download it from the site mentioned at the very
  beginning of this README file.

  The following optional features were compiled into this build, but
  to be able to actually use them, you will need to download and
  install one or more of the following additional packages, all of
  them available from this site:

    . to display TIFF images install tiff-4.0.3-w32
    . to display JPEG images install jpeg-v8d-w32
    . to display GIF images install giflib-5.1.0-w32
    . to display SVG images install librsvg-2.40.1-2-w32
    . to get support for the LCMS2 functions install lcms2-2.8-w32

  To install any of the additional packages, use "unzip -u" from the
  same directory where you unzipped the Emacs binary archive.  The -u
  switch will make sure you don't overwrite newer files by older ones
  of the same name.

make-4.4.1-with-guile-w32
make-4.4.1-without-guile-w32

  This is a MinGW build of the latest version 4.4.1 of GNU Make.
  There are 2 different binary zip files here: with and without Guile
  support.  The zip without Guile is much smaller, so if you are sure
  you won't need Guile scripting in Makefiles any time soon, I
  recommend to install the "without-guile" version.  The sources for
  both these binary zips are in make-4.4.1-w32-src.zip.

  For the "with-guile" version, if you install it anywhere but d:/usr,
  you will need to set the following 2 environment variables:

    set GUILE_LOAD_PATH=x:\foo\share\guile\2.0
    set GUILE_LOAD_COMPILED_PATH=x:\foo\lib\guile\2.0\ccache

  where "x:\foo" is the top directory of the Make installation, under
  which you have the tree of the unzipped files.  (If you used
  unzip.exe to unzip the distribution, the top directory is the one
  from which you ran unzip.exe.)  These variables are required for the
  Guile support in Make to be able to initialize itself.

libwebp-1.3.0-w32

  This is a 32-bit MS-Windows build of the latest version 1.3.0 of
  Google's libwebp, the WebP image library (and a few related
  utilities).  I needed it for Emacs, but it can also be used for
  other projects.  The Google site provides only MSVC-compiled
  binaries, which include only static libraries, no DLLs, and only for
  64-bit systems, and MSYS2/MinGW64's 32-bit builds don't support XP
  and older systems.  Here you have a port that is free of those
  deficiencies.

texinfo-7.1-w32

  This is a Windows build of the latest version 7.1 of the GNU Texinfo
  package.  It includes a working stand-alone Info reader info.exe, as
  well as install-info.exe, and also makeinfo, pod2texi and texindex.
  The texi2pdf utility is provided only as a Unix shell script.

  Note that makeinfo was reimplemented in Perl starting from version 5.0,
  which made it about 18 times slower.  Starting with Texinfo version 6.4,
  Perl extensions in C can be used, which speed up makeinfo by 40% (70% if
  using TEXINFO_XS_PARSER), but these extensions make makeinfo dependent on
  a specific binary version of Perl you should have installed, and create
  licensing issues.  Therefore, the binary distribution of this port doesn't
  include the extensions, and you may wish keeping makeinfo.exe from version
  4.13 around for the time being.  If you do want to use this new makeinfo,
  you will need to install Perl and make sure it is on PATH.

gdb-14.1-w32

  A 32-bit Windows build of the latest version 14.1 of GDB.  The MinGW
  site lags behind the official releases; here you have the latest
  release that supports both Python and Guile.  One caveat: you will
  have to download and install Python 3.4.4 from the python.org site:

    https://www.python.org/downloads/release/python-344/
    https://www.python.org/ftp/python/3.4.4/python-3.4.4.msi

  gdb.exe in this archive depends on the Python library and DLL, and
  will not run without it being available on your system.  (I don't
  want to distribute Python binaries, because then I would also need to
  provide the Python sources from this site, which is way too much.)
  Starting from GDB 12.1, you will need Python 3, since GDB 13 and
  later will not support Python 2.x anymore.

  The NEWS file in 'share/doc/gdb-VERSION/' describes all the new and
  improved features in this release.

  Starting with GDB 7.10, the data files in this port are installed
  into a version-specific directory 'share/gdb/VERSION/'.  This is so
  you could keep previous versions of GDB renamed as, say,
  gdb-x.y.z.exe, and still be able to invoke them and let them find
  their data files.  If this is the first GDB port you are installing
  that uses this structure, I suggest to move the data files of the
  previous version -- everything under share/gdb/ -- into a version
  specific subdirectory share/gdb/X.Y.Z/, where X.Y.Z is the version
  of GDB you had before this one.

  Guile dependencies are included in this binary distribution.
  If you install this anywhere but D:\usr, you will need to set 2
  environment variables:

    set GUILE_LOAD_PATH=x:\foo\share\guile\2.0
    set GUILE_LOAD_COMPILED_PATH=x:\foo\lib\guile\2.0\ccache

  where "x:\foo" is the top directory of the GDB installation, under
  which you have the tree of the unzipped files.  (If you used
  unzip.exe to unzip the distribution, the top directory is the one
  from which you ran unzip.exe.)  These variables are required for the
  Guile support in GDB to be able to initialize itself.

  If you install GDB anywhere but D:\usr, you will also need to set
  the environment variable TERMINFO:

    set TERMINFO=x:\foo\share\terminfo

  otherwise, line-editing commands will not work as expected, and
  arrow keys, Ctrl-A, Backspace, etc. will not move cursor correctly.

  If GDB complains at startup about being unable to load Python
  modules, you may need to set the PYTHONPATH environment variable to
  point to your Python 3.4.4 installation, like this:

    set PYTHONPATH=C:\Python344\DLLs;C:\Python344\Lib;C:\Python344;C:\Python344\Lib\site-packages

  (assuming you installed Python in C:\Python344).

  This port also supports TUI, the Text-mode User Interface; invoke
  GDB with the -tui command-line option to activate it.  Note that
  this mode should only be used when invoking GDB from the shell
  prompt, not, for example, when invoking GDB as a subprocess of
  Emacs.

  This port also supports source highlighting via the source-highlight
  library, and the new 'styling' feature of GDB, which together cause
  the GDB output to have nice colors.

gawk-5.3.0-2-w32

  A Windows build of the latest version 5.3.0 of GNU Awk.  This was
  linked against Readline, and so has a fully functional command-line
  editing interface, including command history, when using the Gawk
  debugger.  Also, this port was linked against the MPFR library, and
  so supports arbitrary-precision floating-point arithmetics, when
  invoked with the -M or --bignum command-line options.  See the node
  "Gawk and MPFR" in the manual for the details.  The new dynamic
  extensions feature is also supported, see the node "Dynamic
  Extensions" in the manual.  Several ready-to-use extensions, in the
  form of DLL files, are bundled; you will find them in the
  lib/gawk/ext-4.0 directory of your Gawk installation.  If you have
  your own extensions compiled against Gawk versions older than 5.3.0,
  you will have to recompile them against the new gawkapi.h, as the
  API supported by this version of Gawk is binary-incompatible with
  the API of older Gawk.  Last, but not least, this version supports
  network and co-routines.

  The "persistent memory" feature is not supported in this port, as it
  currently only works in 64-bit executables.

  This second upload fixes an upstream bug in reading file names from
  directories using the readdir extension.

tree-sitter-0.20.8-w32
tree-sitter-lang-20240214-w32

  This is a MinGW build of the tree-sitter library v0.20.8 and of
  tree-sitter grammar libraries for several programming languages and
  formatted files.  I need this for Emacs, but they can also be useful
  on their own right.

  Many of the grammar libraries don't make versioned releases, so here
  you have their latest development versions directly from their
  corresponding repositories.

binutils-2.42-w32

  This is a Windows build of the latest version 2.42 of the GNU
  Binutils.  The Binutils versions offered by the MinGW site lag
  behind the upstream releases; here you have the latest one.  In
  addition to bringing the latest features, this build supports both
  the 32-bit i386 and the 64-bit x86_64 targets, even when running on
  a 32-bit OS.  This allows using these utilities with 64-bit binaries
  on 32-bit versions of Windows.  Note that binutils are built in a
  separate directory, build-binutils-X.YY, so if you are looking for
  the products of the build, like config.log and the Makefile's, in
  the source zip file, look in that directory, not in binutils-X.YY.
