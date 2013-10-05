# strace-android

strace-android is a customized version of strace, modified by @adetaylor (adetaylor/strace-android) to read and interpret ioctl() calls made on binder handles. Binder, formerly known as Open Binder, is an interprocess communication API used in Android systems. This repository includes some minor fixes to work around compile issues I ran into. There is a statically built ARM binary of strace on the "build" branch, for convenience.

## Downloading

Download the compiled ARM binary from [https://github.com/divergentdave/strace-android/raw/build/strace]() or scan this QR code.

![](http://chart.apis.google.com/chart?cht=qr&chs=350x350&chld=L&choe=UTF-8&chl=https%3A%2F%2Fgithub.com%2Fdivergentdave%2Fstrace-android%2Fraw%2Fbuild%2Fstrace)

## Building

I built strace-android in Ubuntu, though other Linux distributions should work just as well.

1. Install an ARM cross-compiler.

```
sudo apt-get install gcc-4.7-arm-linux-gnueabi
```

2. Set environment variables in the current shell. You may need to change the values of CC and STRIP if you install a different version of GCC or install it to a different path.

```
export CC=/usr/bin/arm-linux-gnueabi-gcc-4.7
export STRIP=/usr/bin/arm-linux-gnueabi-strip
export CFLAGS="-O2 -static -DHAVE_LINUX_BINDER_H"
```

3. Set up and run automake. You may need to install the automake package if it isn't already installed.

```
automake --add-missing
autoreconf
```

4. Run configure.

```
./configure --host=arm-linux
```

5. Build.

```
make
```

6. Copy `strace` to a writable, executable partition on your phone and run it as root.
