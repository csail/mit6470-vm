# VM Release Steps

This document covers the final steps for releasing a VM image.

These steps are completely irrelevant for setting up a live server, but they
contain useful tidbits of information, should you ever find yourself releasing
a Linux-based VM image.


## Disk Image Size Reduction

The steps in this section cut down the size of the VirtualBox disk image file
as much as possible.

1. Run the following commands in the VM to install `zerofree` and clean up the
   package manager's cache and old packages.

        sudo apt-get install -y zerofree
        sudo apt-get autoremove -y
        sudo apt-get clean

1. Select the VirtualBox window for the VM. The following steps cannot be done
   from an SSH client.
1. From the Window menu, select `Machine` > `Insert Ctrl+Alt+Del` to reboot the
   VM.
1. When the VM reboots, and the GRUB menu shows up, press the down arrow
   quickly to prevent the default selection.
1. Press _Enter_ to select the `Advanced options for Ubuntu` menu entry.
1. Press the down arrow and _Enter_ to select the most recent menu entry that
   ends in `(recovery mode)`.
1. Press the down arrow a few times to select
   `root - Drop to root shell prompt` in the Recovery Menu.
1. Run the following commands in the console.

        mount -n -o remount,rw /
        rm -rf /tmp/*
        rm -rf /var/log/*
        mount -n -o remount,ro /
        zerofree /dev/sda1
        dd if=/dev/zero of=/dev/sda5 bs=1024 count=524288
        SUID=`cat /etc/fstab | grep UUID.*swap | awk -F'=| ' '{ print $2 }'`
        echo $SUID
        mkswap --uuid $SUID /dev/sda5
        halt

1. After `System halted` is printed, select `Machine` > `Close` from the
   VirtualBox menu, select the `Power off the machine` radio button and press
   the `OK` button.
1. Run the following command on the __host system__ (not in the VM).

        VBoxManage modifyhd ~/VirtualBox\ VMs/MIT\ 6.470/mit6470.vdi --compact


## Packaging

Go into the `VirtualBox VMs` folder in your home directory and follow the steps
below to produce the .zip file.

1.

