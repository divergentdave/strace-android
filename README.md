# strace-android

strace-android is a customized version of strace, modified by @adetaylor to read and interpret ioctl calls made on binder handles. Binder, formerly known as Open Binder, is a key interprocess communication API in Android systems. This repository has been slightly refreshed to work around some compile issues I ran into. There is a statically built ARM binary of strace on the "build" branch, for convenience.

## Building

I built strace-android in Ubuntu, though other Linux distributions should work just as well.

1. Install an ARM cross-compiler.
```sh
sudo apt-get install gcc-4.7-arm-linux-gnueabi
```
2. Set environment variables in the current sehll
```sh
export CC=/usr/bin/arm-linux-gnueabi-gcc-4.7
export STRIP=/usr/bin/arm-linux-gnueabi-strip
export CFLAGS="-O2 -static -DHAVE_LINUX_BINDER_H"
```
3. Set up and run automake. You may need to install the automake package if it isn't already installed.
```sh
automake --add-missing
autoreconf
```
4. Run configure.
```sh
./configure --host=arm-linux
```
5. Build.
```sh
make
```
6. Copy `strace` to a writable, executable partition on your phone and run it as root.
