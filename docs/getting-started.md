# Getting Started

## Finish WROLPi Installation

To finish your WROLPi installation follow these steps:

1. Modify fstab to mount your external drive. In the example below, `/dev/sda1` will be mounted to `/media/wrolpi`
    1. `echo '/dev/sda1 /media/wrolpi auto defaults,nofail 0 0' | sudo tee -a /etc/fstab`
2. Finish the installation with the repair script: `sudo bash /opt/wrolpi/repair.sh`
3. Reboot: `sudo reboot`
4. After reboot, browse to `http://wrolpi.local` or `http://127.0.0.1` on the WROLPi itself.
5. [Refresh your files](modules/files/index.md#refreshing)

# Creating a new WROLPi

## Raspberry Pi

The following instructions are the steps necessary to create a new WROLPi, either as a backup, or to restore your WROLPi
on a new Raspberry Pi.

### Image an SD Card on Linux

1. Plug in your SD card, find its device path with: `sudo blkid`
2. Extract and copy the WROLPi image to your drive (/dev/sdb in this example):
    * `xzcat WROLPi-v0.10-aarch64-desktop.img.xz | sudo dd of=/dev/sdb status=progress`

### Image an SD Card on Windows

1. Copy the WROLPi image to your micro SD card using [Balena Etcher](https://www.balena.io/etcher)

### First Boot

1. Unplug your Raspberry Pi
2. Insert the micro SD card from step 2 into your Raspberry Pi
3. Connect any peripherals to your Raspberry Pi, then turn it on.
4. Login as the **pi** user with the password **wrolpi**
5. Launch the Terminal application
    1. Change your password with: `passwd`
    2. Modify fstab to mount your external drive to **/media/wrolpi**
        * `echo '/dev/sda1 /media/wrolpi auto defaults,nofail 0 0' | sudo tee -a /etc/fstab`
    3. Finish the installation with the repair script:
        * `sudo bash /opt/wrolpi/repair.sh`
    4. Reboot: `sudo reboot`

## Debian

The following instructions are the steps necessary to create a new WROLPi, either as a backup, or to restore your WROLPi
on a new Debian computer.

1. Copy the Debian WROLPi ISO to a thumb-drive.
2. Insert the thumb-drive into the laptop, boot to the thumb-drive.
    1. Select **Start Installer**
    2. Install Debian 12.
3. Unplug the thumb-drive after the installation has completed
4. Login as the user you created during installation.
5. Switch to the root user: `su -`
6. Finish the installation with the repair script: `sudo bash /opt/wrolpi/repair.sh`
7. Reboot: `sudo reboot`
8. Join the Hotspot or browse to `http://wrolpi.local` or the IP address of your WROLPi!
9. [Refresh your files](modules/files/index.md#refreshing)
