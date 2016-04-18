# Introduction #

Here are some simple instructions to install the toolchain to the iPhone.  The guide assumes that BSD subsystem is installed.  There is a bit of command-line work, so either SSH package or Terminal + iphuc must be installed.  These packages were built and tested on firmware 1.1.4, but they may work on older firmwares, too (YMMV).

# Details #

All the packages from this project will go in /usr/local on the iPhone, so make sure you have plenty of space.  I chose to put my /usr/local on the Media partition.  Here are the steps:
```
$ cd Media
$ mkdir local
$ login -pf root
Password:
# ln -s /var/mobile/Media/local /usr/local
# exit
```

Copy [gcc-4.0.1-iphone-1.tgz](http://iphone-gcc.googlecode.com/files/gcc-4.0.1-iphone-1.tgz) to the iPhone to /var/mobile/Media/gcc-4.0.1-iphone-1.tgz and unpack it:
```
$ cd /
$ tar -xzf /var/mobile/Media/gcc-4.0.1-iphone-1.tgz
$ rm /var/mobile/Media/gcc-4.0.1-iphone-1.tgz
```

Copy [odcctools-9.2-ld-iphone-1.tgz](http://iphone-gcc.googlecode.com/files/odcctools-9.2-ld-iphone-1.tgz) to the iPhone to /var/mobile/Media/odcctools-9.2-ld-iphone-1.tgz and unpack it:
```
$ cd /
$ tar -xzf /var/mobile/Media/odcctools-9.2-ld-iphone-1.tgz
$ rm /var/mobile/Media/odcctools-9.2-ld-iphone-1.tgz
```

Copy [make-3.81-iphone-1.tgz](http://iphone-gcc.googlecode.com/files/make-3.81-iphone-1.tgz) to the iPhone to /var/mobile/Media/make-3.81-iphone-1.tgz and unpack it:
```
$ cd /
$ tar -xzf /var/mobile/Media/make-3.81-iphone-1.tgz
$ rm /var/mobile/Media/make-3.81-iphone-1.tgz
```

Copy headers-4.0.0-iphone-1.tgz to the iPhone to /var/mobile/Media/headers-4.0.0-iphone-1.tgz and unpack it:
```
$ cd /
$ tar -xzf /var/mobile/Media/headers-4.0.0-iphone-1.tgz
$ rm /var/mobile/Media/headers-4.0.0-iphone-1.tgz
```

Okay, so you don't have headers-4.0.0-iphone-1.tgz; you have to build this package yourself.  The following steps must be done on your MAC OS X computer if you arent on OSX see the next step below to obtain headers:
```
$ svn co http://iphone-dev.googlecode.com/svn/branches/include-1.2-sdk
$ wget http://iphone-gcc.googlecode.com/files/headers.patch.gz
$ THISPATH=`pwd`
$ INSTPATH=$THISPATH/usr/local
$ MACOSXDK=/Developer/SDKs/MacOSX10.4u.sdk
$ pushd include-1.2-sdk
$ ./configure --with-macosx-sdk=$MACOSXDK --prefix=$INSTPATH
$ bash install-headers.sh
$ cd $INSTPATH/include && zcat $THISPATH/headers.patch.gz | patch -p1
$ cd $INSTPATH/include/c++ && ln -s 4.0.0 4.0.1
$ popd
$ tar -czf headers-4.0.0-iphone-1.tgz usr
```

If you aren't on Mac OS X, replace the /Developer/SDKs/MacOSX10.4u.sdk path with the full path to the unpacked Mac OS X 10.4 Universal SDK.  If you don't have a copy of this, download the Xcode 3.0 DMG from Apple's Developer Tools download page.  It is free, but you will need to register with them.
Extract the Packages/MacOSX10.4.Universal.pkg directory from the Xcode DMG (use PowerISO, TransMac or plain old mount if on Linux).  You'll also need [xar](http://xar.googlecode.com):
```
$ xar -xf MacOSX10.4.Universal.pkg
$ gzip -dc Payload | cpio -i
```

The last missing bit is headers.patch.gz, which will be available shortly.