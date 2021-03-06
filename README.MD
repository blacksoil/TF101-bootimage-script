# What is this?
Basically this is a tool to package zImage kernel file and a initramfs file into a valid TF101 boot.img
This was created to ease out TF101 kernel development while I'm playing around with postmarketos.
Postmarketos build system disallow kernel incremental build. So to work around it, I created this.
The idea is to build the kernel outside of postmarketos buildsystem (i.e. so we can do incremental build),
and then just flash it separately.

# Where can I find TF101 kernel?
There are lots of different kernel out there, but if you want to use mine, here it is:
```
https://github.com/blacksoil/TF101-GNU-kernel
```
It's being developed to work with postmarketos. See README inside for instruction to build.

# Any Caveat?
* Yes, kernel modules are built into initramfs, but since this script doesn't generate initramfs but
  is expecting one that's already generated, it means newly built kernel modules wouldn't get included!
  To work around it, just include the module as monolithic components, and when upstreaming to postmarket
  change it to module.

# How to use
* Modify ./build-github with the path to your zImage
* Copy and replace ./image/initramfs-asus-tf101 with your desired initramfs
* Pack zImage and initramfs to a boot.img by running ```./build-github ```
* Flash the boot.img to TF101

# How to get initramfs?
* One option is to use one that's generated by postmarketOS

# How to flash?
* Enter TWRP on your TF101
  * Restart
  * As soon as ASUS logo shows up, press volume down
  * A prompt to recovery would show up, press volume up
* Run ./flash
