Computer vision with iOS: Building an OpenCV framework
------------------------------------------------------

This is the source code that accompanies our [article][1] on how to build an OpenCV framework for iOS devices. The framework can be added to your projects by dragging and dropping and supports video capture using the OpenCV highgui module. 

[1]: http://aptogo.co.uk/2011/09/opencv-framework-for-ios/The autocrop repository, when built inside dirveaxle-android,
requires this repository's OpenCV.framework to be present.

Eleos Build
===========

This fork of OpenCVForiPhone includes patches to support both armv6/armv7 and armv7/armv7s builds, depending on the devices you plan to target.

This repository is primarily just CMake build scripts that make OpenCV build for iPhone. You need to supply this repository with a copy of the OpenCV source tree before attempting the build.

Check this repository out, including OpenCV's repository as a submodule:

    git clone --recursive git@github.com:eleostech/OpenCVForiPhone.git

Patch opencv to build for armv6 or armv7s, whichever you like:

    patch -p0 < ../opencv-armv6.patch
    # or
    patch -p0 < ../opencv-armv7s.patch

Then build:

    cd ..
    ./opencvbuild.sh opencv .

You can verify that everything worked with the following command:

    otool -f ~/OpenCVForiPhone/OpenCV.framework/OpenCV

You should have these results:

    Fat headers
    fat_magic 0xcafebabe
    nfat_arch 3
    architecture 0
        cputype 12
        cpusubtype 6
        capabilities 0x0
        offset 68
        size 22255632
        align 2^2 (4)
    architecture 1
        cputype 12
        cpusubtype 9
        capabilities 0x0
        offset 22255700
        size 21009016
        align 2^2 (4)
    architecture 2
        cputype 7
        cpusubtype 3
        capabilities 0x0
        offset 43264716
        size 27063960
        align 2^2 (4)
    Archive : /Users/eleos/OpenCVForiPhone/OpenCV.framework/OpenCV (architecture armv6)
    Archive : /Users/eleos/OpenCVForiPhone/OpenCV.framework/OpenCV (architecture armv7)
    Archive : /Users/eleos/OpenCVForiPhone/OpenCV.framework/OpenCV (architecture i386)

Or you may see an "unknown architecture" if you've built for armv7s.

You can now use the built OpenCV.framework to link for the Simulator or devices.
