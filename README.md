# uuu (Universal Update Utility), mfgtools 3.0

[![Build status](https://ci.appveyor.com/api/projects/status/github/NXPmicro/mfgtools?svg=true)](https://ci.appveyor.com/project/nxpfrankli/mfgtools-kvqcg)
[![Build Status](https://travis-ci.com/NXPmicro/mfgtools.svg?branch=master)](https://travis-ci.com/NXPmicro/mfgtools)

![GitHub](https://img.shields.io/github/license/NXPmicro/mfgtools.svg)

Freescale/NXP I.MX Chip image deploy tools.
**original linux version uses "linux" branch, windows version uses "windows" branch**

    uuu (universal update utility) for nxp imx chips -- libuuu-1.0.1-gffd9837

    Succeded:0       Failed:3               Wait for Known USB Devices to Appear...

    1:11     5/5 [                                        ] SDP: jump -f u-boot-dtb.imx -ivtinitramf....
    2:1      1/5 [===>                                    ] SDP: boot -f u-boot-imx7dsabresd_sd.imx ....

# Key features
 - The real cross platform. Linux, Windows, MacOS(not test yet)
 - Multi devices program support
 - Daemon mode support
 - Few depedencies (only libusb, zlibc, libbz2)
 - Firmware (uboot/kernel) uses WCID to auto load the winusb driver on the Windows side. Windows7 users need to install the winusb driver from https://zadig.akeo.ie/  Windows10 will install the driver automatically.

# Examples:
```
  uuu u-boot.imx            Download u-boot.imx via HID device

  uuu list.uu               Run all the commands in list.uu

  uuu -s                    Enter shell mode. Input command.

  uuu -v u-boot.imx         verbose mode

  uuu -d u-boot.imx         Once it detects the attachement of a known device, download boot.imx.

                            u-boot.imx can be replaced, new file will be download once board reset.

                            Do not unplug the SD card, write to the SD card, nor plug in a SD card when debugging uboot.

  uuu -b emmc u-boot.imx    write u-boot.imx to emmc boot partition. u-boot.imx need enable fastboot

  uuu -b emmc_all u-boot.imx sdcard.bz2\*
                            decompress sdcard.bz2 file and download the whole image into emmc
```

# Prebuilt Image and pdf document

The prebuilt image and document are here:
  - https://github.com/NXPmicro/mfgtools/releases
  - UUU.pdf is snapshot of [wiki](https://github.com/NXPmicro/mfgtools/wiki)

# How to Build:

## Windows
- `git clone https://github.com/NXPmicro/mfgtools.git`
- `cd mfgtools`
- `git submodule init`
- `git submodule update`
- `open msvs/uuu.sln with Visual Studio 2017`

Visual Studio

Note that, since uuu is an OSI compliant Open Source project, you are entitled to download and use the freely available Visual Studio Community Edition to build, run or develop for uuu. As per the Visual Studio Community Edition license this applies regardless of whether you are an individual or a corporate user.

## Linux
- `git clone https://github.com/NXPmicro/mfgtools.git`
- `cd mfgtools`
- `sudo apt-get install libusb-1.0-0-dev libzip-dev libbz2-dev pkg-config cmake libssl-dev g++`
- `cmake . && make`

## macOS
- `git clone https://github.com/NXPmicro/mfgtools.git`
- `cd mfgtools`
- `brew install cmake libusb libzip openssl pkg-config`
- `cmake -DOPENSSL_ROOT_DIR=$(brew --prefix)/opt/openssl . && make`

Note that we assume [brew](https://brew.sh) is installed and can be used to resolve dependencies as shown above. The remaining dependency `libbz2` can be resolved via the XCode supplied libraries.

# Run environment
 - Windows 10 64 bit
 - Linux (Ubuntu) 64 bit
 - macOS (Catalina)
 - 32 bit systems will have problems with big files.

# License
uuu is licensed under the BSD license. See LICENSE.
The BSD licensed prebuilt Windows binary version of uuu is statically linked with the LGPL libusb library, which remains LGPL.

 - bzip2 (BSD license) is from https://sourceware.org/git/bzip2.git
 - zlib  (zlib license) is from https://github.com/madler/zlib.git
 - libusb (LGPL-2.1) is from  https://github.com/libusb/libusb.git



# TechNexion Addendum

*****************************************************************************************
Release date: 2021-02-04
# update uuu of windows and linux platform binary version to V1.4.77
# add multiboard support burning emmc simultaneously

*****************************************************************************************
Release date: 2020-03-23
# update uuu of windows and linux platform binary version to V1.3.154
# add multiboard support burning emmc simultaneously

*****************************************************************************************
Release date: 2020-02-12
# update uuu of windows and linux platform binary
# added imx6ul and imx6ull flash emmc command parameter

*****************************************************************************************
Release date: 2020-02-04
# support PICO-iMX6UL and PICO-iMX6ULL

*****************************************************************************************
Release date: 2019-12-26
# support PICO-iMX6DL and PICO-iMX6Q
# support PICO-iMX7D

*****************************************************************************************
normal usage:
$ uuu -b cmd_type parameter1 parameter2 parameter3

cmd_type:
- emmc_imx6_img : Avaible CPU TYPE => iMX6Q and iMX6DL
- emmc_imx7_img : Avaible CPU TYPE => iMX7D
- emmc_imx6ul_img : Avaible CPU TYPE => iMX6UL and iMX6ULL

parameter1 : secondary program loader (SPL)
parameter2 : universal boot loader (u-boot.img)
parameter3 : system image without compressing which generated by Yocto

imx6 example:
$ suod PATH_TO/uuu -b emmc_imx6_img imx6-SPL imx6-u-boot.img fsl-image-qt5-validation-imx-pico-imx6-xxxxxx.rootfs.sdcard
or
$ sudo PATH_TO/uuu -b emmc_imx6_img imx6-SPL imx6-u-boot.img fsl-image-qt5-validation-imx-pico-imx6-xxxxxx.rootfs.sdcard.bz2/*

imx7 example:
$ sudo PATH_TO/uuu -b emmc_imx7_img imx7-SPL imx7-u-boot.img fsl-image-qt5-validation-imx-pico-imx7-xxxxxx.rootfs.sdcard
or
$ sudo PATH_TO/uuu -b emmc_imx7_img imx7-SPL imx7-u-boot.img fsl-image-qt5-validation-imx-pico-imx7-xxxxxx.rootfs.sdcard.bz2/*

imx6ul example:
$ sudo PATH_TO/uuu -b emmc_imx6ul_img imx6ul-SPL imx6ul-u-boot.img fsl-image-qt5-validation-imx-pico-imx6ul-xxxxxx.rootfs.sdcard
or
$ sudo PATH_TO/uuu -b emmc_imx6ul_img imx6ul-SPL imx6ul-u-boot.img fsl-image-qt5-validation-imx-pico-imx6ul-xxxxxx.rootfs.sdcard.bz2/*

*****************************************************************************************
multiboard usage:
1. copy all of binaries you need include xxx-SPL, xxx-u-boot.img, fsl-image-xxx.rootfs.sdcard into multiboard folder
2. change file name to specific name for script recognize.
for iMX6 iMX7 iMX6UL iMX6ULL
   xxx-SPL => _SPL
   xxx-u-boot.img => _UBOOT
   fsl-image-xxx.rootfs.sdcard => _rootfs.sdcard
for iMX8MQ iMX8M-mini
   xxx-imx8mx-xxx.bin => _flash.bin
   fsl-image-xxx.rootfs.sdcard => _rootfs.sdcard

3. change directory to multiboard
$ ../uuu/linux64/uuu -d xxxx.auto

imx6 multiboard example
$ cp imx6/imx6-SPL multiboard/_SPL; cp imx6/imx6-u-boot.img multiboard/_UBOOT; cp path_to/fsl-image-xxx.rootfs.sdcard /multiboard/_rootfs.sdcard
$ cd multiboard
$ sudo ../uuu/linux64/uuu -d emmc_imx6_img.auto

imx8mm multiboard example
$ cp imx8mm/pico-imx8mm-flash.bin multiboard/_flash.bin; cp path_to/fsl-image-xxx.rootfs.sdcard /multiboard/_rootfs.sdcard
$ cd multiboard
$ sudo ../uuu/linux64/uuu -d emmc_img.auto

*****************************************************************************************
For more details information and iMX8 series please refer to the following website
https://github.com/TechNexion/u-boot-tn-imx/wiki/Use-mfgtool-%22uuu%22-to-flash-eMMC

