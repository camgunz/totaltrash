+++
draft = false
title = "Building D2K"
date = 2014-11-11T17:06:01Z
+++

## Building

### Source Code

D2K's source code is located [here](https://github.com/camgunz/d2k); you can
clone it with Git like so:

    git clone https://github.com/camgunz/d2k

Afterwards, there is a `build.sh` script which will build D2K; the resulting
executable is built in the `cbuild` folder.

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
  * Lua
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

### Cross-Compiling

[mingw64-builds](https://github.com/camgunz/mingw64-builds) is a project that
cross-compiles dozens of popular libraries using the Mingw-w64 cross-compiler.
You can clone it with Git like so:

    git clone https://github.com/camgunz/mingw64-builds

By default, mingw64-builds builds all the libraries in the `build` subfolder.
When cross-compiling D2K, D2K expects the dependencies to be in its `crossdeps`
folder. You can change both of these options if you need to. D2K contains a
`crossbuild.sh` script which will cross-compile it for Windows. The resulting
executable is built in the `crossbuild` folder.

### Building on Windows

There is currently no support for building on Windows.  I'll accept patches for
IDEs or compilers that support C99, but I will not accept patches that modify
the code in order for it to work with a non-compliant system (MSVC++, for
example).

Support for IDEs like Code::Blocks or CDT is planned, but not currently a
priority.

### MP3

MP3 support is on sketchy legal ground due to patents covering MP3 technology.
Use at your own risk. We strongly encourage mappers and modders to use the free
and superior OGG format.

