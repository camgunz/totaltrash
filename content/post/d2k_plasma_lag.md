+++
Categories = []
Description = ""
Tags = []
author = "Ladna"
date = "2014-11-13T15:54:38Z"
menu = "news"
title = "D2K Plasma/Bullet Lag"

+++

[Rev. 42f4ae5](https://github.com/camgunz/d2k/commit/42f4ae5f65a630844284c049393db58233225c0a)
lessens the amount of data sent for certain types of actors (plasma, spider
demon plasma, bullet puffs and blood spots) when they spawn.  This was
necessary because these actors tend to spawn very rapidly, causing lots of new
information to be sent over the wire (delta compression doesn't help here
because the actors are new), which would lag (throttle) clients on bad
connections.  A little more could be done here, and in fact, the solution could
be seen as a hack.  I think Valve, for example, has fine-tuned controls about
what entity fields are synchronized between client and server, which can be
helpful for mods.  In D2K, if you add more rapidly-spawning actors, there's not
a great way to tell the engine to only send certain data about them, let alone
specify what that data should be, and how to fill in the blanks clientside.

D2K struggled with this more than other C/S ports because of its "send
everything" philosophy.  Delta compression works because the world usually
changes very little, but an actor is 312 bytes, and delta compression can't
leave any of that data out when an actor first spawns.  2-3 new actors over a
couple of TICs isn't a big deal, but the SSG spawns something like 20 bullet
puffs; that's over 6K!

To fix this, we pull the size down from 312 to 48 bytes (44 for puffs &amp;
blood).  This is still a lot of data for 1 SSG shot (~900 bytes), and we can
probably pull it down even more if we get smarter (puffs don't need angle,
pitch or flags, can save 16 bytes, or 320 per SSG shot, there).

