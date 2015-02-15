+++
draft = false
title = "Building D2K"
date = 2014-11-11T17:06:01Z
type = "page"
+++

### Source Code

D2K's source code is located [on GitHub](https://github.com/camgunz/d2k) and
can be cloned (downloaded) with Git like so:

    git clone https://github.com/camgunz/d2k

### Dependencies

D2K has quite a few dependencies.

  * GLib
    * libffi
    * pcre
      * bzip2
      * zlib
    * libiconv (part of glibc)
    * libxslt
      * libxml2
        * xz
        * zlib
    * gettext
  * cairo
    * GLib
    * libpng
    * Pixman
    * gtk-doc
      * libxslt
  * Pango
    * GLib
    * cairo
    * HarfBuzz
    * Fontconfig
      * Expat
      * FreeType2
  * GObject Introspection
    * GLib
    * cairo
  * pcre
  * Lua
  * Lua GObject Introspection
    * libffi
  * OpenGL
  * libXDiff
  * ENet
  * SDL
  * SDL\_image
    * libpng\*
    * libjpeg\*
    * libtiff\*
    * WebP\*
  * SDL\_mixer
    * MikMod\*
    * libmad\*
    * libogg\*
    * libvorbis\*
    * libFLAC\*
  * PortMidi\*
  * FluidSynth\*
  * gperf\*

_* = optional_

We plan to add more, at least json-c, libcurl, and PolarSSL.

On Arch Linux, the only dependency not bundled is libXDiff, which can be found
in the AUR. I'm afraid I can't help with other distributions.

### Building on Linux

Dependencies should be installed according to your distribution
(Debian/Ubuntu/Mint will use `apt-get`, RedHat/Fedora will use `yum`, Arch
Linux will use `pacman`, etc.).  Afterwards, `build.sh` will build `doom2k` in
the `cbuild` subfolder.

### Building on Mac OS X

Dependencies may be installed using the [Homebrew](http://brew.sh) project and
the `install_macosx_packages.sh` script found in the D2K source repository.
Afterwards, `build-mac.sh` will build the `doom2k` in the `cbuild`
subfolder.

### Building on Windows

D2K can be built on Windows using
[Code::Blocks](http://www.codeblocks.org/downloads/26#windows).  Building using
MSVC++ is not supported due to a lack of support for C99.  Assuming you cloned
D2K to `C:\d2k`, the Code::Blocks project file expects dependencies at
`C:\d2k\deps`, so that `flac.exe` resides at `C:\d2k\deps\bin\flac.exe`.

Because satisfying D2K's dependencies on Windows is difficult, I have either
located or built them and put them
[here](http://static.totaltrash.org/mingw64-builds.tar.xz).  You will need
[7-Zip](http://www.7-zip.org) (or something that handles `.tar.xz` files) to
decompress the archive.

The dependencies are built using the MinGW-w64 compiler toolchain on Linux.
Should you wish to build them yourself, I recommend looking at [the
Arch Linux AUR](http://aur.archlinux.org) (search for
"mingw-w64-&lt;package\_name&gt;") and the
[MinGW64-Builds](https://github.com/camgunz/mingw64-builds) project.  

#### Cross-Compiling

D2K can be cross-compiled on Linux for Windows; in fact, this is how Windows
binaries are built.  To do so:

  - Clone D2K
    - Assuming install folder of `~/d2k`
  - Unpack
    [the dependencies](http://static.totaltrash.org/mingw64-builds.tar.xz) to
    `~/d2k/crossdeps`, so that `flac.exe` is at `~/d2k/crossdeps/bin/flac.exe`
  - Run `crossbuild.sh`
  - Executable will be `~/d2k/crossbuild/doom2k.exe`

### MP3

MP3 support is on tenuous legal ground due to patents covering MP3 technology.
Use at your own risk. We strongly encourage mappers and modders to use the
superior and free OGG format.

