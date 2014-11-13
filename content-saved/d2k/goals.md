+++
draft = false
title = "D2K Goals"
date = 2014-11-11T17:06:01Z
+++

## Goals

### Overview

Around 2012, I decided to leave the Doom community behind, but [I became
saddened by the prospect that (G)ZDoom and Zandronum are becoming the de facto
Doom experience](faq#zdoom) and instead of whining about it, decided to step up
and build a Doom source port I think is worthy of being the standard. What does
this mean?

### State Of The Art Netcode

The netcode model used by the major client/server ports (Odamex, Zandronum and
ZDaemon) is fundamentally flawed. D2K will implement netcode based on delta
compression, very similar to the system used by Quake 3.

In addition, D2K will also employ techniques to improve the experience for
players on lossy or lagged connections. This includes smoothing opponent
positions, adding backwards reconciliation (unlagged), and projectile lerping,
among other things.

### Faithful, Modern OpenGL Renderer

PrBoom+'s OpenGL renderer is outdated, using deprecated APIs and the
fixed-function pipeline. I will upgrade it to use the programmable pipeline,
and restore functionality lost to deprecation (paletted textures, for example).
I will also endeavour to ensure that anything possible with the original
software renderer will be possible with the new OpenGL renderer as well.

### Employ a Modern Scripting Language

Doom's extensive modifiability created an entire generation of game designers,
but it has failed to keep up. ACS, DECORATE, EDF and ExtraData all attempt to
improve Doom's extensibility, but all leave much to be desired. ACS is
particularly horrible.

D2K will employ [Lua](http://www.lua.org), a language [already widely used for
scripting](http://en.wikipedia.org/wiki/Category:Lua-scripted_video_games), for
its assets and behavior.

### Add Existing Features

Doom source ports have advanced tremendously over the years, but PrBoom+ has
remained relatively conservative. D2K will add many advanced features, from
those ports, including:

  * ACS scripting
  * DECORATE
  * EDF
  * ExtraData
  * MAPINFO
  * 3D floors
  * 3D MidTex
  * 3D physics
  * Portals
  * Slopes
  * Polyobjects
  * Ambient sounds
  * Support for other ID Tech 1 engines (Heretic, Hexen, etc.)
  * Cameras
  * UDMF
  * ZIP/PK3 resource files
  * Bots

...and much more. The goal, ultimately, is to be mod-compatible with even
highly advanced engines like the Eternity Engine and Zandronum.

### Maintain Compatibility

Doom has a rich demo history, and it is important to preserve it. D2K will
continue PrBoom+'s commitment to demo compatibility by following Odamex' lead
and building a demo testing framework.

### Internationalize

The days of ASCII dominance are over. D2K will use UTF-8 internally and support
environments using non-ASCII encodings.

### Use Modern Technology

D2K will use C99, and will be progressively reformatted to use C99 features.
Compilers and IDEs with inadequate C99 support (such as MSVC++) are
unsupported.

### Promote Openness

John Carmack released the Doom source code for Christmas in '97, and the Doom,
gaming, and developer communities owe him a huge debt of gratitude. None of
these modifications or advances would be possible without this initial gesture
of openness.

Unfortunately, it is much harder to work with PrBoom+'s source code than it is
to work with the original Doom source release. PrBoom+'s source is notoriously
impenetrable, full of hacks, and largely written in an unreadable style. This
has dramatically slowed the pace of contributions, and discourages would-be
developers from working on PrBoom+.

Other ports have ported their code to C++, and while some of these efforts are
examples of how C++ doesn't have to be disgusting and confusing, others prove
that it is far too easy to create impossibly complex code with the language.

Competitive Doom players are all too familiar with conservative developers
refusing to add features they or others personally disagree with. Such
recalcitrance has had a hugely negative impact on the entire Doom community.

D2K will continue the spirit of openness, not only through fulfilling its
obligations under the GPL, but by maintaining an accessible codebase. I will
diligently reformat code in a consistent, readable style, and I will attempt to
redesign hacked features in a more robust manner. Further, D2K will remain in C
to attempt to avoid C++'s complexity and lengthy compilation times. Finally,
D2K will always weigh new feature ideas on the merits, not on politics or
personal preference. A "vanilla" game will always be possible, and advanced
features will always be optional.

