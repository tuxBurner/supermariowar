# Super Mario War

## About

Super Mario War is a Super Mario multiplayer game.
The goal is to stomp as many other Marios as possible to win the game.
It's a tribute to Nintendo and the game Mario War by Samuele Poletto.

The game uses artwork and sounds from Nintendo games. We hope that this noncommercial fangame qualifies as fair use work. We just wanted to create this game to show how much we adore Nintendo's characters and games.

### Features

- Up to four players deathmatch fun
- a whole bunch of game modes (featuring GetTheChicken, Domination, CTF, ...)
- online and local multiplayer
- Comes with the leveleditor - you can create your own maps...
- ... and a lot of people did so. There are currently over 1000 maps
- More fun than poking a monkey with a stick
- The whole source code of the game is available, for free
- uses SDL and is fully portable to windows, linux, mac, ...
- CPU Players
- will make you happy and gives you a fuzzy feeling

### Supported platforms

- Linux
- Windows
- XBox (?)
- Mac OS X (?)
- asm.js



## Building instructions

### Requirements

- CMake
- SDL (1.2 or 2.0), with
    - SDL_image
    - SDL_mixer
- ENet (optional)

On Linux, this usually means the following packages: `cmake libsdl1.2-dev libsdl-image1.2-dev libsdl-mixer1.2-dev libenet-dev`.

For other systems, you can download the development files manually from:

- http://www.cmake.org/cmake/resources/software.html#latest
- http://www.libsdl.org/download-1.2.php
- http://www.libsdl.org/projects/SDL_image/release-1.2.html
- http://www.libsdl.org/projects/SDL_mixer/release-1.2.html
- http://enet.bespin.org/Downloads.html

### Linux

Create a build directory and run CMake there to configure the project. Then simply call `make` every time you want to build. The binaries will be generated in ./Build/Binaries/Release by default.

```sh
$ unzip data.zip
$ mkdir Build && cd Build && cmake ..
$ make -j4 # -jN = build on N threads
$ ./Binaries/Release/smw ../data
```

On raspberry-pi: http://72dpiarmy.supersanctuary.net/index.php?topic=11144.0

edit: *CMakeLists.txt* on line #98 comment out **add_definitions(-mfpu=neon -mfloat-abi=softfp)**

```sh
$ unzip data.zip
$ mkdir Build && cd Build
$ cmake .. -DNO_NETWORK=1
$ ./Binaries/Release/smw ../data
```

Currently, the following separate build targets are defined for `make`:

- smw
- smw-leveleditor
- smw-worldeditor
- smw-server

If you prefer to work within an IDE (CodeBlocks, Eclipse, ...), you can also generate project files using CMake. You can find more information in *Build configuration*.

To create installable packages, simply run `make packages`. This will create TGZ, DEB and RPM archives.

### Windows

On Windows, you can follow the Linux guide using environments like MinGW Shell/MSYS and Cygwin, or generate a project file with CMake for your IDE.

Visual Studio:

- make sure you have CMake in your PATH
- go to Build directory and issue `cmake ..`
- open the generated solution smw.sln, right-click on the smw project and go to Configuration Properties -> C/C++ - Command line and remove everything there
- on the same group, go to Linker and add your lib directory there
- change also system to WINDOWS (not console)
- now it will compile and smw.exe can be found in build\Binaries\Debug\smw.exe. make sure you copy the necessary SDL dlls along with smw.exe, otherwise it won't work

### ASM.JS

SMW can be build to run in your browser. For this, you need
Emscripten with the special LLVM backend, and Clang.
See [here](https://kripken.github.io/emscripten-site/docs/building_from_source/LLVM-Backend.html) for more information.

You can prepare a build directory with the following commands:

```sh
$ mkdir build-js && cd build-js
$ ln -s ../data data
$ emconfigure cmake .. -DUSE_EMSCRIPTEN=1 -DNO_NETWORK=1
```

Then build with:

```sh
$ emmake make
$ BUILDPARAMS="-O3 -v --preload-file data -s OUTLINING_LIMIT=60000 -s ALLOW_MEMORY_GROWTH=1 -s ASSERTIONS=1"
$ emcc Binaries/Release/smw.bc -o smw.html $BUILDPARAMS
$ emcc Binaries/Release/smw-leveledit.bc -o leveledit.html $BUILDPARAMS
$ emcc Binaries/Release/smw-worldedit.bc -o worldedit.html $BUILDPARAMS
```
### Build configuration

You can change the build configuration by setting various CMake flags. The simplest way to do this is by running `cmake-gui ..` from the Build directory. You can read a short description of an element by hovering the mouse on its name too.

Alternatively, you can pass these options directly to CMake as `-DFLAGNAME=VALUE` (eg. `cmake .. -DUSE_SDL2_LIBS=1`).



## How to play

Please see documentation in the docs/ directory.
