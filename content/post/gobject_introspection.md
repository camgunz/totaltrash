+++
Categories = []
Description = ""
Tags = []
author = "Ladna"
date = "2014-12-08T20:46:22Z"
menu = "news"
title = "gobject_introspection"

+++

I had originally planned to use [Lua](http://www.lua.org) to re-implement D2K's
console, but using [GObject
Introspection](http://wiki.gnome.org/GObjectIntrospection) via [Lua GObject
Introspection](http://github.com/pavouk/lgi) was just too hard, because GObject
Introspection depends on Python, which requires dozens of patches to
cross-compile using MinGW-w64.  You can find these patches scattered
everywhere, from random GitHub or Bitbucket accounts to the MinGW-Builds
tarballs, and what's clear from the number of patches is that none of it is
guaranteed to work at all, let alone work correctly.

So now my plan is to essentially build my own bindings.  I can only imagine
what's really involved with this, so it may be that I abandon this as well.

Designing as I write this, I envision something like:

    =======================================================================
    |                                                                     |
    |                       xf.Console (in Lua)                           |
    |                           ||                                        |
    |                           \/                                        |
    |                     Widget Library (in Lua)                         |
    |                           ||                                        |
    |                           \/                                        |
    |                       PangoCairo                                    |
    |                         /    \                                      |
    |                     Pango    Cairo                                  |
    |                                                                     |
    =======================================================================

This is, unfortunately, lots of work.  I'm currently planning on not providing
full bindings to Pango, Cairo or PangoCairo, although I don't know how hard it
would be to do so.  If it ends up that it's as simple as generating (or
C-N-P'ing) the rest of the code, then I'll go the whole way.  I certainly won't
hold up D2K development for 100% coverage here.

I would feel remiss if I left this post without noting my dismay at Python's
lack of MinGW support, which is starting to snowball into a general dislike of
Python.  Its abject slowness, inability to use more than 1 CPU core, wild
memory consumption, total mishandling of Unicode, lack of support for MinGW,
and insane Python3 redesign (for essentially no good reason, because the
Unicode redesign is broken) rule it out for almost anything I will ever do.
I'd rather build a GUI in C++ with wxWidgets or QT, or C and GTK than I would
with Python and respective bindings.  I'd sooner build a website in Go or Java
than I would with Python and its frameworks.  Its CPU and RAM usage rule it out
for systems programming, where C/C++/Go/Java shine.

These days, all I use Python for are when I need better scripting than what
Bash will provide, and to be honest, I'm thinking about improving my Bash
knowledge so I won't have to do that either.  It's crazy because I have a lot
of deep Python knowledge, but it's just not useful anymore.

Anyway, I think this delays scripting and the console for a while.  I was
hoping for a quick translation between the existing C code and the (to be
rewritten more performantly) new Lua implementation, but it looks like there's
some plumbing I have to add first.  That's a shame because I was excited about
this, but now it just looks like 90% grunt work.

