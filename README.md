[![LGPL 2.1](https://img.shields.io/badge/License-LGPL_2.1-blue.svg)](https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.tagtraum/ffmpeg-package/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.tagtraum/ffmpeg-package)
[![Build and Test](https://github.com/hendriks73/tagtraum-FFmpeg-package/workflows/Build%20and%20Test/badge.svg)](https://github.com/hendriks73/tagtraum-FFmpeg-package/actions)

# tagtraum FFmpeg package

The *tagtraum FFmpeg package* is a binary release of some of the libraries released by
the [FFmpeg](https://www.ffmpeg.org) project. Its purpose is to provide easy access
to Windows, macOS, and Linux (currently Ubuntu) binaries and sources for decoding audio
via a [Maven](https://maven.apache.org/) repository.

Thus it serves as an upstream project for [Java JNI projects wishing to interface
with the native libraries](https://www.tagtraum.com/ffsampledsp/).
Codecs with known patent problems are disabled (but can be enabled, see below).
However, this obviously is no guarantee.

Also, as the focus lies on decoding audio, most encoders are disabled.

This distribution comes with absolutely no support, warranty etc. you name it.

*tagtraum FFmpeg package's* online home is at https://www.tagtraum.com/ffmpeg/

## Usage

To use this package, simply introduce a Maven dependency like this:

```xml
<dependency>
    <groupId>com.tagtraum</groupId>
    <artifactId>ffmpeg-x86_64-macos</artifactId>
    <!-- <artifactId>ffmpeg-aarch64-macos</artifactId> -->
    <!-- <artifactId>ffmpeg-x86_64-win</artifactId> -->
    <!-- <artifactId>ffmpeg-i386-win</artifactId> -->
    <!-- <artifactId>ffmpeg-x86_64-linux</artifactId> -->
    <!-- <artifactId>ffmpeg-aarch64-linux</artifactId> -->
</dependency>
```

The dependency is a `.jar` file containing static libraries. To compile
against them, you will need to first `unpack` the jar, for example using the
[dependency:unpack](https://maven.apache.org/plugins/maven-dependency-plugin/usage.html#dependency:unpack).
goal.

Should you need sources to compile your native code against, use
a dependency like this:

```xml
<dependency>
    <groupId>com.tagtraum</groupId>
    <artifactId>ffmpeg-x86_64-macos</artifactId>
    <type>tar.bz2</type>
    <classifier>ffmpeg-sources</classifier>
    <scope>provided</scope>
</dependency>
```

Again, you will need to `unpack` this to use it.

## Build

Currently, this library is built automatically via [GitHub Actions](https://github.com/features/actions). 

If you want to build it yourself, you'll need:

- [Maven](https://maven.apache.org/)
- [Apple Command Line Tools](https://developer.apple.com/) or [Xcode](https://developer.apple.com/xcode/) for macOS
- MSYS2 for Windows with a GCC toolchain (`mingw-w64-i686-toolchain` / `mingw-w64-x86_64-toolchain`)
- [YASM](https://yasm.tortall.net/releases/Release1.3.0.html), available via `brew install yasm` (macOS), `pacman -S mingw-w64-x86_64-yasm` (msys2 for 64bit Windows), `pacman -S mingw-w64-i686-yasm` (msys2 for 64bit Windows, crosscompile for 32bit Windows) or whatever your Linux distro makes you do 
- a JDK (to run Maven)

Once all pre-requisites are in place, you must invoke the *right* profile.
Automatic activation is *off* by default.

To build the package for macOS (x86_64), run

```shell
$ mvn --activate-profiles compile,ffmpeg-x86_64-macos install
```

The profile `compile` ensures that FFmpeg and other sources are downloaded and built.
`ffmpeg-x86_64-macos` packages the resulting static library files `*.a` into a jar
with the artifact name `ffmpeg-x86_64-macos` and group id `com.tagtraum`.

If you would like to change the FFmpeg configuration, add

    "-Dffmpeg.configure=--enable-static --disable-programs ... "

Note that you need to add quotes around the entire `-D` parameter to allow for spaces
in the value part.


## Release Notes

Please see [here](NOTES.md).


Enjoy.
