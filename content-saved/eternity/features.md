## Features

### Overview

The Eternity Engine has many often-overlooked features, this is just a short
list.

### Eternity Engine Features

 * Near-perfect Vanilla Doom compatibility and old-school gameplay.
 * Full Boom, MBF, and SMMU compatibility.
 * Removal of nearly all Vanilla Doom limits.
 * Translucency.
 * Multiple music formats, including (but not limited to) MOD, XM, MIDI, OGG/Vorbis, SPC, FLAC, MP3 and MUS.
 * 3D object clipping, so objects (like players and monsters) can exist and move above and below each other.
 * Cameras, for player-less viewpoints.
 * Chasecam (3rd-person viewpoint)
 * Spycam, allowing a player to see what other players are seeing.
 * ENDOOM and textmode startup support.
 * Cross-platform, supporting at least Windows, Linux and BSD.
 * Pre-beta BFG types.
 * Gamepad and joystick support.
 * EDF (Eternity Definition File) system allowing for extreme customization of game resources.
 * ExtraData data specification language replaces the original binary WAD format (this will be superceded by UDMF).
 * Quake-style console.
 * Legacy skin support.
 * Cardboard renderer, which is faster than and resolves fundamental problems with Doom's original renderer by using high-precision floating-point numbers instead of the original fixed-point. It also supports arbitrary, non-standard resolutions.
 * Highly advanced portal implementation, allowing for pseudo-3D or physically impossible architecture.
 * Portal overlays (translucent flats, etc.).
 * Support for the Doom Master Levels.
 * TerrainTypes, such as splashing water.
 * 3DMidTex, allowing for limited 3D architecture like bridges.
 * A full assortment of compatibility options.
 * 2-way wallrunning.
 * Crosshair.
 * Mouselook.
 * Jumping.
 * Advanced sound engine, supporting sector, polyobject, global, and pitched sounds as well as sound sequences.
 * Sound equalizer.
 * Burn damage (standing on torches or candles, for example).
 * Slopes (rendering only, clipping is not complete).
 * Particle effects.
 * BMP and PNG screenshots.
 * Flats and textures are interchangeable, meaning mappers can use flats on walls and textures on floors and ceilings.
 * Fullscreen graphical HUD translucency.
 * DECORATE state support (not full DECORATE support).
 * GFS (Game File Script) allows loading of multiple files using only one file - useful for drag and drop.
 * ACS (mostly complete).

### Eternity Engine - Client/Server Edition Features

 * Extremely smooth, high fidelity, configurable netcode. Players can make their own decisions about tradeoffs between accuracy, latency and smoothness.
 * Highly-accurate backwards reconciliation (unlagged) for hitscan weapons, autoaim, and BFG tracers:
 * Handles moving sectors.
 * Handles changing player states like invulnerability.
 * Master server with built-in web launcher (no separate launcher application is necessary).
 * On-the-fly WAD loading.
 * Automatic WAD downloading (uses HTTP, FTP, or other protocols for maximum speed and versatility).
 * Per-map WADs and configuration overrides.
 * Spectators.
 * Up to 32 players and 2 teams.
 * Player queue system.
 * Remote console (RCON).
 * Simple authorization system:
 * Four authorization levels, spectator, player, moderator, and administrator.
 * Clients save valid passwords and authenticate automatically whenever possible.
 * Bridge things (from ZDoom).
 * 3D radius attacks, used mainly for rocket jumping.
 * New multiplayer scoreboards.
 * Efficient handling of maps with large amounts of monsters; status and position are only broadcasted if they've changed.
 * TeamDM and CTF game modes (in addition to staples like Duel, Deathmatch, and Cooperative/Survival).
 * Advanced demos, split by map, and allowing speed up, slow down, pause, and checkpoints. Demos themselves are simple ZIP files that include JSON metadata, so no knowledge of the binary format is necessary to work with them.
 * Powerful keybinds:
 * Bind key down and key up events separately
 * Bind to only event activation or event deactivation
 * Bind a key to multiple events; useful for SR50 binds and more
 * No weapon switch on pickup.
 * Preferred weapon order (can also switch when picking up ammo for a preferred weapon).
 * Enable/Disable movebob.
 * Modifiable damage screen (red screen) intensity.
 * Highly customizable voting (commands, duration and pass threshold).
 * Quake &amp; Unreal Tournament style announcers.
 * Killing Sprees and Multi Kills
 * Fine-grained access controls, bans, temporary bans and whitelists.

