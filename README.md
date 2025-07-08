Android 12
==========

Pre-requisites
--------------

- At least 200 GB of storage

The following packages might require building:

```
sudo apt-get update -y

sudo apt install -y asciidoc autotools-dev bash bc binutils bison \
build-essential bzip2 chrpath cpio curl cvs dblatex default-jre \
device-tree-compiler diffstat expect-dev fakeroot file flex g++ gawk gcc \
gcc-aarch64-linux-gnu gcc-arm-linux-gnueabihf g+conf genext2fs git git-core \
git-gui gitk graphviz gzip intltool lib32stdc++6 libdrm-dev libglade2-dev \
libglib2.0-dev libgtk2.0-dev liblz4-tool libncurses5 libparse-yapp-perl \
libsigsegv2 libssl-dev libudev-dev libusb-1.0-0-dev m4 make mercurial mtools \
openssh-client parted patch patchutils perl python3 python-is-python3 \
qemu-user-static rsync sed subversion swig tar texinfo u-boot-tools unzip w3m \
wget
```

Cloning the source
-------------------

```
repo init --no-tags --no-clone-bundle -u https://github.com/vicharak-in/rockchip-android-manifest -b master -m rockchip-s-vicharak.xml
```

Syncing the source
-------------------

After the configuration is complete, you can start compiling the firmware.

To download the code sources from the repositories to your local machine, use the following command.

```
repo sync -j$(nproc)
```

Source the Android 12 environment setup
------------------------------------------

```
source build/envsetup.sh
```

Copy Android Specific configs into Kernel Repository
------------------------------------------------------

```
cp -vr mkcombinedroot/configs/android-1* kernel-5.10/arch/arm64/configs
```

The device-specific configuration file for Android 12.1 is located at :
- `device/rockchip/rk3399` for **Vaaman** device 
- `device/rockchip/rk3588` for **Axon** device.

Lunch the device configuration
-------------------------------

```
lunch <device>-userdebug
```

Building the Android 12 firmware
-----------------------------------

After the configuration is complete, you can start compiling the firmware.

```
./build.sh -UACKup
```

Note
-----

build.sh is the firmware build script that can be used to interactively build the firmware. It can accept command line arguments to customize the build process.

-U -> Build U-Boot

-A -> Build Android

-C -> Build kernel using clang compiler

-K -> Build kernel

-u -> Build rockchip update image

-p -> Pack the firmware

