+++
Categories = ["development"]
Description = ""
Tags = ["d2k"]
author = "Ladna"
date = "2014-03-02T21:09:13-05:00"
menu = "news"
title = "D2K"

+++

I've decided to start working on a new source port called [Doom2K](/d2k) or
"D2K" for short.  My goal is to build a state-of-the-art multiplayer source
port capable of being the standard-bearer for multiplayer Doom.  This, in my
mind, means a couple of things.

<!--more-->

### Message-Based Netcode Is Broken

ZDaemon, Zandronum, and Odamex all use message-based netcode.  For example,
there is (historically) a function called `P_SpawnMobj` which spawns a new
actor into the game.  Serverside, inside of `P_SpawnMobj` is a call to a
function that broadcasts a "mobj spawned" message; let's call it
`SV_BroadcastMobjSpawned`.  For illustration's sake, it generally looks
something like this:

    ---------
    | ID    |
    ---------
    | X     |
    ---------
    | Y     |
    ---------
    | Z     |
    ---------
    | Angle |
    ---------
    | Type  |
    ---------

This model "works" for any number of game events.  EECS, for example, has 44
messages.  Odamex has 112.  The way message-based netcode "scales up" is
message proliferation, and there are a number of downsides to this.

#### You have to litter your code with network messages

Ugly, error-prone, and overly complicates extending the engine (scripting).

#### You have to exempt huge swaths of code from running clientside

Same as above.

#### Consistency is complicated

Unless you package up all your message into a single packet (assuming it will
all fit), consistency requires sequencing and a "tic ended" message.

### Doom Scripting Is Busted

Probably the best scripting out there is Doomsday.  Otherwise, you can use
EDGE/3DGE and COAL, or you can use ZDoom and ACS.  I think you can use
FraggleScript in Legacy.

The situation isn't great though.

With a powerful scripting language, it would be possible to implement new game
modes (like CTF), convert most of Doom's physics and original game play, and
represent assets and configuration in scripting also.  PWO, for example, could
simply be a user-provided function in a config.

### ASCII Is Out, Unicode Is In

Unless Doomsday uses UTF-8, I'm unaware of any source ports that are
Unicode-aware.  This has serious implications for Doom's popularity outside of
English-speaking countries.

### Software Rendering Is Limited And Slow

Software rendering is much slower than hardware-accelerated OpenGL rendering.
In general, people who prefer software rendering do so because it's more
faithful to Doom's original renderer (which almost no port uses anymore, due to
its bugs and limitations).  However, with display pixel count rising, software
rendering is becoming less and less feasible.

Software renderers also have various limitations: lack of support for portals,
3D architecture (slopes, room-over-room, etc.), bad math (wobbling flats,
problems with long walls, inaccurate flat rendering, etc.), and so on.

### Goals

[My major goals are to fix all of this](/d2k/goals).

Instead of network messages, D2K will use delta-compressed game states, which
avoids all of the problems with message-based netcode (at the expense of
increased CPU usage and RAM consumption).

D2K will use Lua for scripting.  Current plans include:

  - Implement console in scripting
  - Implement new game modes in scripting
  - Move Doom physics, game play, and assets to scripting

D2K will use UTF-8 instead of ASCII.

Regarding the renderer, I haven't entirely decided to remove the software
renderer.  My main focus will be on the OpenGL renderer, however, because it's
easier to add advanced renderer features to it.  Further, I will work on
implementing a shader for the OpenGL renderer that accurately emulates Doom's
lighting.

