## Frequently Asked Questions

### Troubleshooting

#### EECS doesn't find the IWAD.
Put the IWAD (for example, `doom2.wad`) in the ` user/wads` folder.  By default
this will be ` C:\Program Files\Eternity Engine\user\wads`.

#### Client hangs in the full-screen console before connecting.
You might need to enter a password.  Be sure to read the text
in the console to make sure it's not asking you to input a
password.

#### A weird box pops up in the browser when clicking on server links.

It's asking you if you want to launch Eternity, which you do.

#### Clicking on server links doesn't work on Vista.

  * Uninstall Eternity using the uninstaller
  * Reinstall Eternity to `C:\Eternity`

Whatever you do, do not ask mikehail about this.  Not even once.

#### Clicking on server links doesn't work on Linux.

The server links use the `eternity://` protocol, and there's no 100% sure way
to set protocol handlers in Linux.  If you're using Firefox or you have Gnome
libs installed, you can try the instructions
[here](http://kb.mozillazine.org/Register_protocol#Linux").

Personally, I launch EECS from the command-line like:
`eternity -csjoin eternity://master.totaltrash.org/servers/totaltrash/ctf`.
We plan to fix this as well.

#### Blood spawned from shots doesn't seem to match up with damage.

EECS has a `predict_shots` option that predicts shot collision and spawns
bullet puffs or blood instantly instead of waiting for the server.  While this
feels more "crisp", it can be inaccurate, possibly resulting in the feeling
that too much blood gushes out of your opponent when you shoot them.  You can
set `predict_shots` to `no` to disable this, but while shot results will be
accurate, they will be lagged.

#### After alt-tabbing to a different application, part of the EE screen is frozen.

This is likely an SDL bug, and it only shows up in Windows Vista and Windows 7
with Desktop Video Acceleration disabled.  To work around it, use EE's GL-in-2D
mode (in `system.cfg`):

  * set `i_videodriverid` to 1 (SDL GL2D)
  * set `d_fastrefresh` to 1

#### Mouse lag

Using VSYNC on some video drivers will cause mouse input to be lagged.  To
avoid this, disable VSYNC in your video driver's configuration.

#### Mouse gets slightly "stuck"

The mouse may be sampled unevenly due to Doom's 35Hz framerate cap, and this
may result in the mouse feeling like it's "stuck" turning or moving.  To avoid
this, enable `d_fastrefresh`.

#### Adding fonts

EE supports TTF fonts, and adding them is as simple as copying the font file
(i.e. `arial.ttf`) to the `user/fonts` folder.

### Netcode

EECS has both clientside and serverside buffers designed to improve smoothness,
however, the tradeoff is increased latency.

#### Clientside packet buffer

The client has an optional packet buffer that buffers messages received from
the server.  Players can enable the packet buffer using `packet_buffer`, and
they can set the size using `packet_buffer_size`  A size of `0` causes the
buffer to adapt to your latency and packet loss.  Other sizes specify how many
TICs of messages to buffer.  Again, be aware that the larger the buffer, the
more latency is artifically added to your connection.

#### Serverside command buffer

The server has an optional command buffer that buffers commands received from
every client.  This is enabled/disabled using the `buffer_client_commands`
option in the server configuration file.  The buffer is adaptive; size cannot
be set manually.

#### Using Netstats

The `show_netstats` command can help players get an idea of their connection
quality.  To enable them, type `show_netstats yes` into the console.

The 1st number is the number of TICs it takes for a message to arrive from the
server to the client.

The 2nd number is the current number of TICs that are buffered in the
clientside packet buffer.

The 3rd number is the number of your commands the server has buffered in the
serverside command buffer.

The 4th number is the percentage of packets that successfully arrive at the
server the first time they're sent.  If this number is less than 100%, it
doesn't mean information is being lost; packets that are lost are always
resent.  However, resending adds to your latency.

### Bandwidth

One of our design assumptions was "bandwidth is cheap".  If you are using a
modem or your internet download bandwidth is less than 256kbps (that's 256
kilobits per second, or 32kB/s is the max you see while - for example -
downloading in your browser) you will almost certainly have serious problems
playing EECS.

To be specific, a player's minimum position requires at least 32 bytes.  We
have to add 16 bytes to that for sequencing and identification (position for
**which** player at **which** TIC), for a grand total of 48 bytes.
Assuming a 16 player server, you are receiving 15 positions every TIC, so 525
positions per TIC.  48 * 525 is 25.2kB/s, or 201.6kbps.

This is a best-case scenario, because we're assuming there are only 15 other
actors (players, monsters, plasma balls, etc.).  Cooperative games will
requires more bandwidth, especially WADs with a huge amount of monsters.
Additionally we are only calculating bandwidth used by position messages.
While they are certainly the lion's share of messages, there are over 30
messages overall; in particular moving platforms will send a large amount of
(small) messages.

We plan to be more flexible in this area in the future.  Other ports (Odamex
and ZDaemon that we're aware of) allow you to specify your update rate so you
have the option of reducing your incoming bandwidth 50%-67%, but you pay a high
price in accuracy.  Because of our focus on competition, we always err on the
side of accuracy, however we recognize that not all players are competitive and
may not mind or even notice the difference.  On the other hand, we also plan to
optionally use more bandwidth to alleviate some of the negative effects of
packet loss.

