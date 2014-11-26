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

D2K has quite a few dependencies:

  * libiconv (part of glibc)
  * zlib
  * libpng
  * libffi
  * gettext
  * pcre
  * GLib
  * Fontconfig
  * FreeType
  * HarfBuzz
  * Expat
  * Pixman
  * Cairo
  * Pango
  * libXDiff
  * ENet
  * SDL
  * SDL\_mixer
  * OpenGL
  * LZMA\*
  * libjpeg\*
  * libtiff\*
  * WebP\*
  * SDL\_image\*
  * DUMB\*
  * PortMidi\*
  * FluidSynth\*
  * MikMod\*
  * libmad\*
  * libvorbis\*
  * libogg\*
  * libFLAC\*
  * gperf\*

_* = optional_

We plan to add more, at least Jansson, libcurl, and PolarSSL.

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

Dependencies may be installed using the
[MinGW64-Builds](https://github.com/camgunz/mingw64-builds) project.  Pre-built
binaries are located
[here](http://static.totaltrash.org/mingw64-builds.tar.xz), and you will need
[7-Zip](http://www.7-zip.org) (or something that handles `.tar.xz` files) to
decompress the archive.

D2K can be built on Windows using
[Code::Blocks](http://www.codeblocks.org/downloads/26#windows).  Building using
MSVC++ is not supported due to a lack of support for C99.  Assuming you cloned
D2K to `C:\d2k`, the Code::Blocks project file expects dependencies at
`C:\d2k\deps`, so that `curl.exe` resides at `C:\d2k\deps\bin\curl.exe`.

#### Dependencies

Running an executable built this way on your local machine will work, because
the required DLL files are in your path.  However, distributing the executable
will require dozens of DLL files:

  - libcairo-2.dll
  - libexpat-1.dll
  - libffi-6.dll
  - libFLAC-8.dll
  - libfluidsynth.dll
  - libfontconfig-1.dll
  - libfreetype-6.dll
  - libgcc\_s\_sjlj-1.dll
  - libgio-2.0-0.dll
  - libglib-2.0-0.dll
  - libgmodule-2.0-0.dll
  - libgthread-2.0-0.dll
  - libharfbuzz-0.dll
  - libiconv-2.dll
  - libintl-8.dll
  - libjpeg-9.dll
  - liblzma-5.dll
  - libmikmod-3.dll
  - libogg-0.dll
  - libpango-1.0-0.dll
  - libpangocairo-1.0-0.dll
  - libpangoft2-1.0-0.dll
  - libpangowin32-1.0-0.dll
  - libpcre-1.dll
  - libpcreposix-0.dll
  - libpixman-1-0.dll
  - libpng15-15.dll
  - libportmidi.dll
  - libssp-0.dll
  - libtiff-5.dll
  - libvorbis-0.dll
  - libvorbisfile-3.dll
  - libwebp-5.dll
  - libwinpthread-1.dll
  - SDL.dll
  - SDL\_image.dll
  - SDL\_mixer.dll
  - zlib1.dll

We recommend using the [official Windows D2K
distribution](http://static.totaltrash.org/d2k.zip) and simply replacing the
executable.  Otherwise you will need to provide these yourself, as well as the
`doom2k.wad` resource WAD and the fonts.  Should you decide against this, DLL
files may be found in the `deps` folder, `doom2k.wad` can be built using
[deutex](https://github.com/chungy/deutex), and the fonts can be found on the
web.

### Cross-Compiling

D2K can be cross-compiled on Linux for Windows; in fact, this is how Windows
binaries are built.

#### Instructions

  - Clone D2K
    - Assuming install folder of `~/d2k`
  - Clone and build MinGW64-Builds
    - Assuming install folder of `~/mingw64-builds`
    - Assuming build folder of `~/mingw64-builds/build`
  - Copy `~/mingw64-builds/build` to `~/d2k/crossdeps` so that `curl.exe` is
    at `~/d2k/crossdeps/bin/curl.exe`
  - Run `crossbuild.sh`
  - Executable will be `~/d2k/crossbuild/doom2k.exe`

### MP3

MP3 support is on tenuous legal ground due to patents covering MP3 technology.
Use at your own risk. We strongly encourage mappers and modders to use the
superior and free OGG format.

