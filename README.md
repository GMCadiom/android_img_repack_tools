android_img_repack_tools
====================

android_img_repack_tools is a kit utilites for unpack/repack android ext4 and boot images

for download choose any brunch

## Converting sparse flashing system.img from flashing android sparse img to ext4 img

$ simg2img system.img system.raw.img
## or all parts of sparse img
$ simg2img system.img* system.raw.img

## Mounting ext4 img for edit

$ mkdir system_mnt
$ mount -t ext4 -o loop system.raw.img system_mnt

## Creating new android sparse img for flashing (android 2.3.6-4.2)

$ mkuserimg.sh -s system_mnt system_new.img ext4 ./system [size partition MB for example 1024M]
## or
$ make_ext4fs -s -l 1024M system_new.img system_mnt

more

$ mkuserimg.sh -s system system.img ext4 /system [size partition MB for example 1024M] file_contexts

## Converting ext4 img to sparse img for flashing (android 4.3-etc)

$ ext2simg -v system.raw.img system_new.img

## Changing sparse img header size from 28bit to 32bit (for Samsung Exynos Octa)

$ sgs4ext4fs --bloat system_new.img system_32bit.img

## Remove Moto extra header... (for Motorola G-series, making after unsparse img)

$ mv system.raw.img system.moto.img
$ dd if=system.moto.img of=system.raw.img ibs=131072 skip=1
