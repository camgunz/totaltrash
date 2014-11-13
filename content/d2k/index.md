+++
date = "2014-11-11T23:03:45-05:00"
draft = true
title = "D2K"
type = "page"
+++
### Overview

D2K is an advanced Doom source port that aims to modernize the game while
remaining faithful to the original implementation. It is based on
[PrBoom+](http://prboom-plus.sourceforge.net).

### Getting Started

Download a D2K version for your platform, place an IWAD in the installation
folder, and then run `doom2k.exe -net <host>:<port>`.  Connection is currently
a manual process, but eventually D2K will include a server browser.

You can also start a server similarly, simply use all the command-line flags
you normally would, but add `-deltaserve` to the arguments.  If you need to
listen on a specific address, you can use
`doom2k.exe ... -deltaserve <host>:<port>`.

If you get into any trouble at all, please see the [FAQ](d2k/faq).  While
we're happy to help, you're likely to get a fix for your issue much more
quickly by using the information there than by waiting for us.

### Reporting Bugs

The issue tracker is where we keep track of problems in D2K, but it is also
useful for feature requests.  Reporting bugs is simple; there is a
[bug tracker](http://github.com/camgunz/d2k/issues), all you need to do is
create an account. Here are some guidelines for effective bug/feature posting:

  * Give as much information as you possibly can.
  * Use descriptive titles.
  * Be precise and specific.
  * Set label appropriately:
    * Bug: Incorrect behavior
    * Enhancement: New feature
  * Use an email address that you check.
  * If you can run a debugger, please post stack traces.

If more than a couple days goes by and no one's touched your bug or talked to
you about it, please contact us in [IRC](irc://chat.freenode.net/d2k).  The bug
tracker is not where bugs and ideas go to die, it's a list of things for the TT
team to fix so we don't forget them.

