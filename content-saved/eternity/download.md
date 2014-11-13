## Downloads

### Windows

  * [Windows Installer](http://static.totaltrash.org/eternity/eternity-engine-3.40.22_windows-x86.exe)
  * [Windows ZIP Package](http://static.totaltrash.org/eternity/eternity.zip)

If you are installing for the first time, you need to download and run the
installer. Otherwise you can simply overwrite your old `eternity.exe` with the
executable.

### Linux

  * [Full Distribution](http://static.totaltrash.org/eternity/eternity-linux32.tar.xz)
  * [Executable Only](http://static.totaltrash.org/eternity/eternity.xz)

### Source

Users are encouraged to build their own binaries. The source can be checked out
using git and the following command:

    git clone https://github.com/camgunz/eternity

Client-server work is done on the `client-server` branch; to switch to this
branch, run:

    git checkout client-server

in the main `eternity` folder.

Linux users can follow the instructions in the `README-CMAKE.txt` file. Windows
users can follow the instructions in the `README-CODEBLOCKS.txt` file. Of
course these are not the only ways to build EECS, just the easiest.

### Dependencies

_(This section is for those compiling from source only)_

EECS has several dependencies, and rather than add them all to the codebase or
expect users to find/compile them on their own, we've pre-built them for
several platforms. These pre-built dependencies are located
[here](http://static.totaltrash.org/eternity/eedeps). If your platform is not
listed there, please consider downloading the source distribution, using the
`build_deps.py` script to build them, and sending them to me so I can update
the repository.

