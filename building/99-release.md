# VM Release Steps

This document covers the final steps for releasing a VM image.

These steps are completely irrelevant for setting up a live server, but they
contain useful tidbits of information, should you ever find yourself releasing
a Linux-based VM image.


## Disk Image Size Reduction

The steps in this section cut down the size of the VirtualBox disk image file
as much as possible.

1. Install `zerofree` and clean up the package manager's cache and old
   packages.

```bash
sudo apt-get update && sudo apt-get dist-upgrade
sudo apt-get install -y zerofree
sudo apt-get autoremove -y
sudo apt-get clean
```

1. Unmount and zero out the swap.

```bash
sudo swapoff -a
sudo dd if=/dev/zero of=/dev/sda5 bs=1024 count=524288
SUID=`cat /etc/fstab | grep UUID.*swap | awk -F'=| ' '{ print $2 }'`
echo $SUID
sudo mkswap --uuid $SUID /dev/sda5
```

1. Blow up the bash history.

```bash
rm ~/.bash_history
```

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

```bash
mount -n -o remount,rw /
rm -rf /tmp/*
rm -rf /var/log/*
mkdir /var/log/nginx
chown www-data:www-data /var/log/nginx
mount -n -o remount,ro /
zerofree /dev/sda1
halt
```

1. After `System halted` is printed, select `Machine` > `Close` from the
   VirtualBox menu, select the `Power off the machine` radio button and press
   the `OK` button.
1. Run the following command on the __host system__ (not in the VM).

```bash
VBoxManage modifyhd ~/VirtualBox\ VMs/MIT\ 6.470/mit6470.vdi --compact
```

### Commentary

It would make more sense to zero out the swap file after booting in single
mode. However, the required commands are long, and typing them is error-prone,
so it's preferable to have the commands issued in a SSH prompt, where they can
be copy-pasted from the documentation.

The bash history is cleaned up so that users wouldn't stumble upon the setup
commands (and possibly failed experiments) while doing their work. It's not
really a space-saving measure, but it is described here because it must be done
right before booting the VM in single mode.

`halt` is used because the VM doesn't seem to react to `Machine` >
`ACPI Shutdown` when booted in single mode.


## Packaging

Follow the steps below to produce the `mit6470-vm.7z` file.

1. In the VirtualBox main window, right-click on the `MIT 6.470` VM entry, and
select `Show in File Manager`.
1. Copy `MIT 6.470.vbox` into `mit6470.vbox`.
1. Compress `MIT 6.470.vbox` and `mit6470.vdi` into `mit6470-vm.7z`.

### Commentary

Using `.zip` instead of `.7z` would make the user setup a bit easier, because
all our target platforms have built-in Zip decompression. However, 7-Zip
produces significantly smaller files, which translate into less server badwidth
and better download times. On an early version of the VM, zip compression
yielded a 517MB file, while the 7-zip file was only 360MB.
