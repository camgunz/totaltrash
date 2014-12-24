+++
Categories = []
Description = ""
Tags = []
author = "Ladna"
date = "2014-11-13T15:06:50Z"
menu = "news"
title = "D2K Client Sync"

+++

[Rev. c6a8550](https://github.com/camgunz/d2k/commit/c6a8550d0f161c970efaca4bc705abe3914c07ae)
is my latest attempt at solidifying clientside sync (along with a couple of
preceding commits).  After trying dozens of different schemes, I finally
discovered one that works nearly perfectly.

First of all, clients need to know what commands a server ran between the
delta's start state and end state.  This isn't so important for consoleplayer's
position, but it important in order to get accurate sounds from the other
players.  The client runs commands from other players (non-consoleplayer
commands, or "NCP" commands), during this phase, called "synchronization", and
that's where the it will start sounds such as rockets/plasma firing, lifts
starting, etc.  It's possible for consoleplayer's commands to affect NCPs'
positions, so they need to run in tandem.  Currently they are run all at once;
it would be better to have a way to run them the way the server did, or at
least stretch them out as much as possible.

Once this is finished, the client loads the new, latest state received from the
server.  Re-running the commands the server ran between the delta's start &amp;
end state is an imperfect process, so it can't be relied on to perfectly create
the state.  After this step, synchronization is complete, and re-prediction
commences.

The server won't always run consoleplayer's commands in lock-step.  The client
may send commands 100/80, 101/81, and 102/82 (TIC/Index), but the server may
run them all on TIC 101.  Let's stipulate that command 81 triggered a lift at
TIC 101.

The client will then (possibly, but let's say it does for the sake of our
example) receive a delta "server received commands <= 82 at TIC 101".  So it
synchronizes all commands <= 82, and spawns the lift at 101.

When the client first ran command 82, the lift had already been activated, so
this TIC (102) would be the 2nd time the lift had been moved.  However, after
synchronization, the TICs will still align, but the commands won't.  Let's say
that the client has 3 commands left (103/83, 104/84, 105/85) that the server
has yet to acknowledge receipt of.  It will now run each of these commands
separately, and move the lift 3 more times.  However, initially, by the
time the client ran command 85, the lift had already been moved 5 times.  So
when the client initially predicted the world out to 105/85, the lift had moved
5 times, but now after re-prediction, the lift has only moved 4 times.  This
will cause the lift to snap back 1 TIC's worth of movement.

You'll also notice that the client is about to run TIC 102, but will then run
command 103/83.  This disparity allows the client to know that it's fallen
behind.  When the client notices this, it runs an extra TIC, without a command.
This runs the world simulation, but doesn't move consoleplayer.

