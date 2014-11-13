## Building

### Source Code

EECS' source code is located at
`http://mancubus.net/svn/hosted/eternity/branches/client-server`. On Windows
you can use TortoiseSVN; Linux users are encouraged to use their distribution's
package management to install the Subversion binaries. The command-line to
checkout the code is:

    svn co http://mancubus.net/svn/hosted/eternity/branches/client-server

Once you've successfully checked out the source code from the Subversion
repository, create an `eedeps` folder inside of it.

### Dependencies

EECS has pre-built dependencies for Windows and Linux located
[here](http://static.totaltrash.org/eedeps). If you are using Code::Blocks on
Windows you should use the MinGW distribution, but if you are using MSVC on
Windows you should use the MSVC distribution. 32-bit Linux users should use the
Linux32 distribution, and 64-bit Linux users should use the Linux64
distribution. It is also possible to build EECS using packages installed on
your machine. Here is a list of EECS' dependencies:

  * ENet 1.3.x
  * libarchive 2.8.x
    * bzip2
    * zlib
    * xz
  * curl
    * c-ares-1.7.4 (Linux only)
    * gnutls-2.8.x
    * libgcrypt-1.5.x
    * libgpg-error-1.10
    * libidn-1.22
  * SDL
  * SDL\_net
  * SDL\_mixer
    * flac-1.2.x
    * libmad-0.15.1b
    * libmikmod-3.1.11
    * libogg-1.2.x
    * libvorbis-1.3.x

#### OpenSSL

Please be aware that while OpenSSL may be substituted for GnuTLS and its myriad
dependencies, binaries built against OpenSSL may not be distributed because of
a licensing conflict between its license and EECS' license (GPLv2). They are OK
for personal use however.

#### MP3

MP3 support is on sketchy legal ground due to patents covering MP3 technology.
Use at your own risk. We strongly encourage mappers and modders to use the free
and superior OGG format.

#### SMPEG

While SMPEG may be substituted for libmad, SMPEG has reported stability issues
and can be difficult to compile.

#### Adding Pre-Built Dependencies

If you are using a different platform, please consider getting in touch with
the development team so they can help you build the dependencies for your
platform and add them to the repository.

#### Installing Pre-Built Dependencies

Windows users can decompress the archives using [7-Zip](http://www.7-zip.org),
Linux users will need [XZ Utils](http://tukaani.org/xz), which can likely be
installed via package management. The dependencies should be placed in the
`eedeps` folder inside the main source distribution. For example, a MinGW user
who downloaded the source code to `C:\Code\eecs` would have the dependencies
installed at `C:\Code\eecs\eedeps\mingw`, and inside the `mingw` folder would be
`bin`, `include`, `info`, `lib`, `man`, `sbin`, and `share`.

### Building: Code::Blocks & Windows

The EECS Code::Blocks project file is located in the `codeblocks` folder. No
modifications should be necessary; open and build.

### Building: MSVC++ & Windows

The EECS MSVC++ project file is located in the `vc2008` folder. This build
platform is still in development, possible issues include problems with the
Solution/Project file (non-relative paths) and a lack of static linking (lots
of DLLs required by the main Eternity.exe executable). Please report problems
with the Solution/Project file; static linking will be added in the future.

### Building: Linux

The EECS Linux build system uses CMake. The steps are:

  * `mkdir build`
  * `cd build`
  * `cmake ../ -G"Unix Makefiles"`
  * `make`

This builds a binary `eternity.real` inside `build/source` (in our example).
Installation currently does not work; users who build from source are expected
to install eternity as they see fit.

