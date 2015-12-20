# Boost for Android
Boost for android is a set of tools to compile the main part of the [Boost C++ Libraries](http://www.boost.org/) for the Android platform.

Currently supported boost versions are 1.45.0, 1.48.0, 1.49.0 and 1.53.0. Boost 1.54.0 and 1.55.0 shall be considered experimental.

To compile Boost for Android you may use one of the following NDKs:

| NDK / boost | 1.45 | 1.48 | 1.49 | 1.53 |
| ----------- | ---- | ---- | ---- | ---- |
| r4 customized by [Dmitry Moskalchuk aka CrystaX](http://www.crystax.net/android/ndk.php). | x |   |   |   |
| r5 from the [official android repository](http://developer.android.com).                  | x |   |   |   |
| r5 customized by [CrystaX](http://www.crystax.net/android/ndk.php).                       | x |   |   |   |
| r7 customized by [CrystaX](http://www.crystax.net/android/ndk.php).                       | x | x | x |   |
| r8 from the [official android repository](http://developer.android.com).                  | x | x | x |   |
| r8b from the [official android repository](http://developer.android.com).                 |   | x | x |   |
| r8c from the [official android repository](http://developer.android.com).                 |   |   | x |   |
| r8d from the [official android repository](http://developer.android.com).                 |   |   | x | x |
| r8e from the [official android repository](http://developer.android.com).                 |   |   | x | x |
| r10 from the [official android repository](http://developer.android.com).                 |   |   | x | x |

# Quick Start

## Dependencies

 * NDK ([official](http://developer.android.com) or [customized by CrystaX](http://www.crystax.net/android/ndk.php))
 * GNU Make

## Usage

### Compiling

Linux.
```
./build-android.sh $(NDK_ROOT)
```
Windows:
```
build-android.bat $(NDK_ROOT)
```
NOTE: Do not forget to replace backslash with slashes in $(NDK_ROOT). For example set $(NDK_ROOT) to D:/android-ndk-r8e instead of D:\android-ndk-r8e
    
On windows you will need MSYS to be able to launch the corresponding bat files (http://www.mingw.org/wiki/MSYS).
    
This command will download and build boost against the NDK specified and output the final headers and libs in the `build` folder. Make sure to provide an absolute path the the NDK folder!

For more info about usage and available commands use `--help`.

### Including

Now that you got Boost compiled you must add it to your `Android.mk` file. Locate the `build` folder and copy the `include` and `lib` folders over to your project's `jni` folder. A recommended path inside your project is `/jni/boost/`.

Add the following to your `Android.mk` (note that here we're using Boost 1.48 and have assumed that Boost resides inside `/jni/boost`):

    LOCAL_CFLAGS += -I$(LOCAL_PATH)/boost/include/boost-1_48
    LOCAL_LDLIBS += -L$(LOCAL_PATH)/boost/lib/ -lboost_system -lboost_...

    LOCAL_CPPFLAGS += -fexceptions
    LOCAL_CPPFLAGS += -frtti

Now use `ndk-build` to build and have fun with it!

Note that you should build your project and Boost with the same version of NDK as the C++ STL inside NDK r4 and NDK r5 are not compatible in some subtle details.

## Contribute

The projects is split into two main branches, the master and devel. The master branch is where the current stable version lies and which should be used in most of the cases, the devel branch in turn is where development occurs. To contribute to the project make sure to use the devel branch which will make it easier to test changes and to merge incoming pull requests (PR).

## Troubleshooting

In case you encounter bunch of linker errors when building your app with boost, 
this might help:

### Building from a 64 bit machine (Linux)

Make sure you have installed the 32 bit libraries. Those are required to be able
to use the NDK.

To install them just use the following

    $ sudo apt-get install ia32-libs

### NDK 7 (CrystaX)

Add `-lgnustl_static` *AFTER* all boost libraries to the LOCAL_LDLIBS line in 
Android.mk. Example:

    LOCAL_LDLIBS += lboost_system-gcc-md lboost_thread-gcc-md -lgnustl_static

### NDK 8 (official)

Do everything that is in the NDK 7 Crystax section, but also
add full path to the gnustl_static library to the link paths. Example:

    LOCAL_LDLIBS += lboost_system-gcc-md lboost_thread-gcc-md \
                 -L$(NDK_ROOT)/sources/cxx-stl/gnu-libstdc++/libs/armeabi \
                 -lgnustl_static
=======
# OIS: Object oriented Input System

[![Software License](https://img.shields.io/badge/license-zlib%2Flibpng-green.svg)](LICENSE.md)

Cross Platform Object Oriented Input Lib System. Meant to be very robust and
compatiable with many systems and operating systems.

This is the official repository and is a continuation of the great work done by pjcast on the old sourceforge repo.

## Todo

- Merge pull requests/patches send in over time
- Cleanup and remove dead-code
- Start implementing support for new platforms and backends

### Linux

Dependencies: X11

To build and install:

    cmake -H. -B./build
    cd ./build
    make
    make install

### Windows

Dependencies: DirectInput 8

For Visual Studio:

    cmake -H. -B./build -G"Visual Studio 12 2013"

For CodeBlocks:

    cmake -H. -B./build -G"CodeBlocks"

### OSX

For XCode:

    cmake -H. -B./build -G"Xcode"

## License

The zlib/libpng License

Copyright (c) 2015 Andrew Fenn
Copyright (c) 2005-2010 Phillip Castaneda (pjcast -- www.wreckedgames.com)

This software is provided 'as-is', without any express or implied warranty. In no
event will the authors be held liable for any damages arising from the use of this
software.

Permission is granted to anyone to use this software for any purpose, including
commercial applications, and to alter it and redistribute it freely, subject to the
following restrictions:

    1. The origin of this software must not be misrepresented; you must not claim that
		you wrote the original software. If you use this software in a product,
		an acknowledgment in the product documentation would be appreciated
		but is not required.

    2. Altered source versions must be plainly marked as such, and must not be
		misrepresented as being the original software.

    3. This notice may not be removed or altered from any source distribution.


### License Explained
In case the license was not clear enough... Basically, you can link with this lib
which puts no restrictions on what you have to license your code as. You can modify
this lib, and not have release your changes. Though, as explained above,
**Altered source versions must be plainly marked as such, and must not be misrepresented
as being the original software.**

This is to allow users the greatest flexibility in what you can use this lib for.
