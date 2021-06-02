# Test 1

This test is intended to understand the rawdraw library on C.

## Platform statuses

 * Windows, 100% Support for CNFGOGL and/or CNFGRASTERIZER, Native (GDI32) does not support alpha-blitting, or variable line width.
 * Linux, 100% Support for CNFGOGL and/or CNFGRASTERIZER, Native (X11) doe not support alpha-blitting, or variable line thickness
.
 * Android, 100% Support for CNFGOGL (It is forced on) CNFGRASTERIZER not allowed.
 * WASM, 100% Support for CNFGOGL
 * Other EGL (Like Raspberry Pi Raw Metal) Platforms, same as Android, but fixed window size.
 * EGL, CNFGOGL represent OpenGL or OpenGL ES depending on platform support.
 * Vulkan support in progress.
 * CNFG3D Support has been ported with fixed-precision numericals to ESP8266.
 * Mac/OSX Support currently unknown.  Legacy files moved here: https://github.com/cntools/rawdrawtools/tree/main/attic

 

## Prerequisites and some instructions for running on linux

firstly, make sure you have the following libraries installed:
```
xorg-dev
libx-dev
libxinerama-dev libxext-dev
mesa-common-dev libglu1-mesa-dev
```
to do so and also to install them incase they are not already, run the following commands:
```
sudo apt-get update
sudo apt-get install xorg-dev libx11-dev libxinerama-dev libxext-dev mesa-common-dev libglu1-mesa-dev
```
then to run the sample program in rawdraw, go to the clone of the repository on your system, open a terminal window there, and run the command `make`. this will create an executable file called "simple" from the c file called "simple.c". You should be able to run the executable "simple" with the command `./simple`


## Building

Windows compile:
```
C:\tcc\tcc simple.c -Irawdraw -lopengl32 -lgdi32 -luser32 C:\windows\system32\msvcrt.dll
```

Linux compile:
```
gcc -o simple simple.c -lm -lX11
```

Note, with the STB-style header, you don't need to
`#define CNFG_IMPLEMENTATION` anywhere in your code, and instead can also
compile in `cnfg.c`

## Configurations
Rawdraw is a very disjoint set of configurations

CNFG Configuration options include:
* `CNFG_IMPLEMENTATION` = Include code for implementation.
* `__android__` = build Android port
* `WINDOWS`, `WIN32`, `WIN64` = Windows build
* `CNFGOGL` = Make underlying functions use OpenGL if possible.
* `CNFGRASTERIZER` = Make the underlying graphics engine rasterized functions (software rendering)
* `CNFG3D` = Include CNFG3D with this rawdraw build.  This provides *rasterized* graphics functions.  Only use this option with the rasterizer.

Platform-Specific
* `HAS_XSHAPE` = Include extra functions for handling on-screen display functionality in X11.
* `HAS_XINERAMA` = Use X11's Xinerama to handle full-screen more cleanly.

Flags you will probably never want to use:
* `EGL_LEAN_AND_MEAN` = Bare bones EGL Driver


## Extra goodies

### chew.h

You can copy-and-paste `chew.c` and `chew.h` into your program for a single-file compile-only
version of GLEW.  This is WAY BETTER than having to deal with the complicated system they have
set up, but it doesn't include all the functions.  You can easily add OpenGL functions to it.

It provides a very easy-to-use interface for OpenGL Extensions.

### os_generic.h

os_generic is a platform independent way of creating threads, managing TLS, mutices, 
semaphores as well as getting the current time.  It has the following configuration options:

`OSG_NO_IMPLEMENTATION` - Do not include implementation as static functions.
`OSG_PREFIX` - Override function prefix
`OSG_NOSTATIC` - Do not declare the functions as static.

### TextTool/Text.c etc...

There is a sister repository, https://github.com/cntools/rawdrawtools which houses a text tool.

## Warnings

OSX Support has been moved to attic.