# Some App Installation and Hard Drive Mounting Basics

## Installing Snap

Think it's just `sudo apt install snapd`

## Generic upgrade line

`sudo apt-get update && sudo apt-get dist-upgrade` is a good way to upgrade everything.

## How to install from an AppImage if it's not going easily

[This tutorial](https://itsfoss.com/use-appimage-linux/) instructs to right-click the download appimage file, go to "Properties" > "Permissions" and then check "Allow executing file as program". Alternatively `chmod u+x <AppImage File>` to make it executable.

## How to mount an external hard drive that's formatted as exFAT

Simply install these programs by running this line: `sudo apt-get install exfat-fuse exfat-utils` ([via](https://www.reddit.com/r/Ubuntu/comments/6r954q/mount_exfat_drive_in_ubuntu_1704/)). 
