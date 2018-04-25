# tagtraum FFmpeg package

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.tagtraum/ffmpeg-package/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.tagtraum/ffmpeg-package)

The *tagtraum FFmpeg package* is a binary release of some of the libraries released by
the [FFmpeg](http://www.ffmpeg.org) project. Its purpose is to provide easy access
to Windows and OS X binaries and sources for decoding audio via a
[Maven](http://maven.apache.org/) repository.

Thus it serves as an upstream project for [Java JNI projects wishing to interface
with the native libraries](http://www.tagtraum.com/ffsampledsp/).
Codecs with known patent problems are disabled (but can be enabled, see below).
However, this obviously is no guarantee.

Also, as the focus lies on decoding audio, most encoders are disabled.

This distribution comes with absolutely no support, warranty etc. you name it.

*tagtraum FFmpeg package's* online home is at http://www.tagtraum.com/ffmpeg/


## Build

Currently you can only build this library on OS X.

To do so, you also need:

- Maven 3.0.5, http://maven.apache.org/
- a MinGW-w64 crosscompiler, http://mingw-w64.sourceforge.net/, e.g. via [MacPorts](http://mingw-w64.org/doku.php/download/macports)
- Apple Command Line Tools, available via https://developer.apple.com/, or XCode, https://developer.apple.com/xcode/
- a JDK (to run Maven)

Once you have all this, you need to adjust some properties in the parent `pom.xml`.
Or.. simply override them using `-Dname=value` notation. E.g. to build with
another version of zlib, add

    -Dzlib.version=1.2.7

to your `mvn` call. If you didn't add the `bin` folder of your crosscompiler to the
`PATH`, you might also want to set `-Dmingw.i386.path=...` and `-Dmingw.x86_64.path=...`

If you would like to change the FFmpeg configuration, add

    "-Dffmpeg.configure=--enable-static --disable-programs ... "

Note that you need to add quotes around the entire `-D` parameter to allow for spaces
in the value part.


Enjoy,

-hendrik
