+++
draft = false
title = "Frequently Asked Questions"
date = 2014-11-11T17:06:01Z
type = "page"
+++

<a class="anchor" id="zdoom">
### What do you have against (G)ZDoom?
</a>

I became a competitive player on ZDaemon 1.08 (which was derived from ZDoom
1.23b33), and it is insanely fun to play; it might be the most fun I've ever
had playing a game. My argument against ZDoom and ZDoom-derived ports is not
that they aren't fun or that they're bad; I think they're tons of fun and
pretty amazing. I am dismayed that ZDoom and its derivatives are what people
think of as "Doom", when they are really entirely different engines that just
happen to load Doom resource files. What follows is heavy-handed, sharp
criticism of ZDoom, and while it may seem like I have a grudge against its
developers, in truth I respect and even like them. That said, here we go :) .

ZDoom is in no way compatible with Doom demos. It hasn't been for years.
Furthermore, ZDoom breaks compatibility with its own demos haphazardly. One of
Doom's strengths is its rich history, and ZDoom has no regard for preserving
it.

ZDoom's physics and renderer are also drastically different than Doom's, and it
isn't possible to configure them to revert to original settings, because
vanilla behavior is not a priority for ZDoom developers. Even the super-shotgun
spread was changed. Such changes have huge effects on competitive play, but
this is also not a priority for ZDoom developers.

ZDoom's licensing is restricted to non-commercial use only, which limits the
venues where Doom could expand. It also allows closing of the source code,
which has nearly destroyed the Doom community. There are several parts of the
codebase which, over the years, have illegaly incorporated code licensed under
incompatible licenses (Quake, for example). ZDoom's popularity is largely due
to these incorporations, either illegal or under restrictive licenses, and has
therefore come at the expense of the Doom community as a whole. Modders were
left with a choice between proprietary, restricted ZDoom or an open port with
fewer features, and as a result, the lion's share of Doom mods rely on
proprietary ZDoom features.

ZDoom continues to use features and code from non-free libraries and codebases,
most infamously FMOD and BUILD. However, to their credit, ZDoom developers
freely release their original code under the 2-clause BSD license, which, even
though it allows the source to be closed, at least offers other source port
developers the chance to incorporate those features in open ports.

ZDoom's scripting language, ACS, is a nightmare. It is a terrible, weak
scripting language requiring a custom VM. Instead of responsibly using a
proper, 3rd party scripting language, ZDoom chose to extend ACS (first included
by Hexen). Because of ZDoom's popularity, the de facto Doom scripting language
is ACS and the default level of ACS support is whatever ZDoom supports. Coupled
with the fact that until 2008, ACS could not be included in GPL source ports
due to its restrictive licensing, ZDoom essentially monopolized Doom scripting
with a proprietary, substandard language.

Finally, ZDoom's code style is inconsistent, at times unreadable, and often
downright dangerous.

### What do you have against C++?

C++'s templates and better type-safety are clear improvements over C. However,
C++ incorporates four major misfeatures that, even though they are technically
optional, you must interact with any 3rd party code. Altogether, these
misfeatures outweigh C++'s advantages over C.

#### Object-Oriented Programming

OOP is centered around three major ideas: polymorphism, encapsulation, and
inheritance. Polymorphism is just a different placement of the business logic
dispatch, encapsulation is just a different (worse) placement of the object
state, and inheritance is unnecessary and harmful. Even worse, OOP is slow.

Programmers often conflate powerful type systems with OOP, but there are type
systems even more powerful than that of C++ and Java in languages that do not
support OOP.

#### Exceptions

Exceptions disrupt the entire control flow of your program and are difficult to
reason about. This can be mitigated with checked exceptions, Java is an example
of this, but the try/catch syntax is burdensome, and developers consequently
let them become crashes rather than deal with them.

#### Operator Overloading

Operator overloading produces code that is impossible to understand, as one
cannot know what the code actually does. The only case for operator overloading
is implementing additional numeric types, and support for this should be added
at a lower level.

#### The Standard Template Library

While usually well-implemented and very useful, the STL is wildly over-verbose
and renders any application that uses it too complex to really use. In
fairness, this is because C++'s facilities for implementing generics are
over-verbose, but this is a criticism of C++, so the point is valid.

### What do you have against Microsoft Visual C++?

MSVC++'s support for C is substandard, and their response to this charge is
"use C++". That answer doesn't satisfy me, for the aforementioned reasons.

### Why did you fork PrBoom+? Don't you like Entryway?

I chose PrBoom+ for its OpenGL renderer, uncapped framerate, near-perfect
compatibility with several historical source ports, GPL license, and its C
codebase.

Entryway is obviously way smarter than me, which is why I chose to build upon
his work (not to mention the dozens of other contributors to PrBoom) work. It
would have taken me years to solve the problems he's solved, presuming I'm
even skilled enough to do so.  I don't mean this fork as an insult, I mean it
as a compliment :).

