+++
Categories = []
Description = ""
Tags = []
author = "Ladna"
date = "2015-02-07T00:25:14Z"
menu = "news"
title = "d2k_scripting"

+++

Scripting in D2K has come a long way.  The interface is coming along nicely,
largely because Lua makes it so easy to write bindings.  For example, this is
the function used to match key events to key presses:

    static int XI_InputEventIsKeyPress(lua_State *L) {
      event_t *ev = (event_t *)luaL_checkudata(L, 1, "InputEvent");
      int key = luaL_checkint(L, 2);

      if (ev->type == ev_key && ev->pressed && ev->key == key)
        lua_pushboolean(L, true);
      else
        lua_pushboolean(L, false);

      return 1;
    }

`XI_InputEventIsKeyPress` is a method inside the InputEvent class, which is
registered like this:

    X_RegisterType("InputEvent", 21, 
      "new",                  XI_InputEventNew,
      "reset",                XI_InputEventReset,
      "__tostring",           XI_InputEventToString,
      "is_key",               XI_InputEventIsKey,
      "is_mouse",             XI_InputEventIsMouse,
      "is_joystick",          XI_InputEventIsJoystick,
      "is_mouse_movement",    XI_InputEventIsMouseMovement,
      "is_joystick_movement", XI_InputEventIsJoystickMovement,
      "is_joystick_axis",     XI_InputEventIsJoystickAxis,
      "is_joystick_ball",     XI_InputEventIsJoystickBall,
      "is_joystick_hat",      XI_InputEventIsJoystickHat,
      "is_movement",          XI_InputEventIsMovement,
      "is_press",             XI_InputEventIsPress,
      "is_release",           XI_InputEventIsRelease,
      "get_key",              XI_InputEventGetKey,
      "get_key_name",         XI_InputEventGetKeyName,
      "get_value",            XI_InputEventGetValue,
      "get_xmove",            XI_InputEventGetXMove,
      "get_ymove",            XI_InputEventGetYMove,
      "get_char",             XI_InputEventGetChar,
      "is_key_press",         XI_InputEventIsKeyPress
    );


The implementation of `X_RegisterObjects` is a little long, but it's not
terribly complex.

All this scaffolding enables a simple, but powerful scripting interface.  For
example, here's the console's event handler:

    function Console:handle_event(event)
      if event:is_key_press(d2k.Key.BACKQUOTE) then
        self:toggle_scroll()
      end

      if self.scroll_rate < 0 or self.height == 0 then
        return
      end

      if d2k.KeyStates.shift_is_down() then
        if event:is_key_press(d2k.Key.UP) then
          self.output:scroll_up(Console.HORIZONTAL_SCROLL_AMOUNT)
          return true
        elseif event:is_key_press(d2k.Key.PAGE_UP) then
          self.output:scroll_up(Console.HORIZONTAL_SCROLL_AMOUNT * 10)
          return true
        elseif event:is_key_press(d2k.Key.DOWN) then
          self.output:scroll_down(Console.HORIZONTAL_SCROLL_AMOUNT)
          return true
        elseif event:is_key_press(d2k.Key.PAGE_DOWN) then
          self.output:scroll_down(Console.HORIZONTAL_SCROLL_AMOUNT * 10)
          return true
        end
      elseif event:is_key_press(d2k.Key.UP) then
        self.input:show_previous_command()
      elseif event:is_key_press(d2k.Key.DOWN) then
        self.input:show_next_command()
      elseif event:is_key_press(d2k.Key.LEFT) then
        self.input:move_cursor_left()
      elseif event:is_key_press(d2k.Key.RIGHT) then
        self.input:move_cursor_right()
      elseif event:is_key() and event:is_press() then
        self.input:insert_text(event:get_char())
      end

      return false
    end

Never mind the temporary placeholder constants
(`Console.HORIZONTAL_SCROLL_AMOUNT`, etc.) ;).  The point is that it was very
easy to build an entirely new object-oriented event handling interface.

I **did** have to refactor nearly all the SDL event stuff in C, but it was in
need anyway.  As a result, after events are pulled from SDL in C, event
dispatch and handling happens in Lua now.  This means I can slowly start to
move things like the menu and screen drawing (**NOT** the renderer) into Lua,
and delete reams of junk code in the process (man, I dream of the day the C
menu code dies).

Now that event handling happens in Lua, interfaces can be implemented using
only scripting.  The console is my test case; as I develop it, I'm learning to
use Lua GObject Introspection and fixing the scripting interface I've built so
far.  It's not a perfect test (there's not a **ton** of interaction with
D2K-proper), but it's pretty good for a first test.

Speaking of Lua GObject Introspection, I'm making progress building D2K's
dependencies on Windows.  Mingw-builds provides a native, MinGW-w64-built
Python which can be used for GObject Introspection, so I've been going through
the process of writing a bunch of scripts to automatically build everything D2K
needs on Windows.  This has been a huge roadblock.  My secret dream is that
peopel can use my work as a kind of cross-platform shim for C/C++ projects, but
given the relative unpopularity of similar projects (win-builds, MSYS2, MXE),
I'm not optimistic, haha.

Having developed a fair amount of code in Lua, I feel qualified -- nay,
compelled -- to give an opinion!

Lua as an API is fantastic.  I wish the documentation were slightly better, but
honestly it's pretty good.  The Lua site itself is hideous; I remember better
pages from 1998.  It sounds like I'm kidding, but I am not.  I wish there were
better errors in Lua; while they technically make sense, you only realize
**why** they make sense once you guess correctly as to what the problem is.
Lua the language is overall a fairly positive experience.  The "different just
to be different" stuff like `~=` meaning 'not equal to', `elseif` instead of
literally anything else (`else if`, `elif`), and arrays starting at 1 are all
extremely bothersome.  Especially the array index thing, my God what an
abomination.  For loop syntax is a little free-form to me; I really don't
understand why

    for i=0,10,2 do
      print(string.format('i is %d', i))
    end

is better than:

    for (int i = 0; i <= 10, i += 2) {
      printf("i is %d\n", i);
    }

I **do** understand why it's worse though: it's less explicit.

`local` is a big mistake too.  Lua argues that "Local by default is wrong.
Maybe global by default is also wrong, [but] the solution is not local by
default", but come on:

  * I am typing `local` everywhere
  * In Python, I type `global` only when I have to, and it serves as
    documentation
  * If you forget to type `local`, you can destroy your program in a very
    hard-to-discover way
  * If you forget to type `global`, the damage is limited to that function and
    whatever depends on it.  Which, admittedly, is still pretty bad, but what
    is better, more damage that's hard to reason about, or less damage that's
    easier to reason about?
  * If you meant "declarations should look like declarations", `var` would have
    sufficed, and wouldn't get conflated with the scoping issue.
  * If you meant "scope should be explicit", how much more explicit than "I
    defined this variable in this scope, therefore that's where it lives" can
    you get?  Do you want to define variables for other scopes?  **MADNESS**

The other annoying thing in Lua is that while syntactic sugar abounds for
things that really aren't that big a deal (using `:` instead of `.` to pass the
implicit `self` to object method calls, omitting parentheses when only passing
a single string/table argument, etc.), there is no syntactic sugar for
implementing a class or building a module.  You have to wade into this morass
of metatables and the implicit workings of `require` in order to access basic
functionality.  You can't argue that Lua isn't object-oriented because it has
`:` and has a whole section on "Object-Oriented Programming" in the book
(complete with helpful APIs for defining userdata types).  By the way,
"userdata" is really poorly named.  Regular userdata is a blob managed by Lua,
light userdata is a blob -- tracked by a pointer -- managed in native code.
Boom, that's it.  Anyway, there ought to be an easier way to define classes and
modules without understanding the deep workings of `require` and Lua's method
dispatch.

Lua is also a little too flexible.  Leaving off parentheses is just a huge
problem for readability, and in a language that makes you type so much
("function", "then", "end", "do", "repeat", "until") it doesn't make a lot of
sense.  I guess maybe they were worried about weird symbols confusing users,
but how much does dropping the parentheses really buy you when 99% of the time
what follows is a "{" ?  Plus, while I pretty much chose Lua over Python
because it isn't whitespace-sensitive, there are times I really wish it were.
If I read another piece of code with all the if blocks on the same line, I'm
gonna burn Github to the ground.  Whew!

In fact, those three annoyances pretty much sum up the Lua experience on the
script side.  Lua is everything you want in a scripting language: fast, simple,
flexible and powerful.  But then you find a bunch of code written in a totally
unreadable style and you get pissed, or you find yourself mucking about with
Lua's internals because there's no syntactic sugar for this very simple thing
you want to do, or your code doesn't work because Lua does something different
for absolutely no reason.

All that said, if you can live with 1-based indexing, Lua is an excellent
language.  None of the other annoyances are problematic enough to justify not
choosing it.

