# Core VM Setup

This document covers setting up the VM image, installing the operating system,
and getting it to the point where one can SSH into it.


## Install Image

Download the
[Ubuntu 12.10 32-bit server image](http://releases.ubuntu.com/quantal/ubuntu-12.10-server-i386.iso).

### Commentary

32-bit environments use up less RAM, and RAM is the critical resource in a VM
environment. If you're setting up a real server, download a 64-bit server image
from the [advanced download page](http://releases.ubuntu.com/quantal/).


## VirtualBox Setup

You need [VirtualBox](https://www.virtualbox.org/) and clients for SSH and mDNS
to set up the VM. Follow the instructions in `using/` to get this software.

Once you have VirtualBox, start it and create a new VM image with the following
properties.

1. Name: `MIT 6.470`
1. Type: `Linux`
1. Version: `Ubuntu` (default)
1. Memory: `512` MB (default)
1. Create a virtual hard drive
1. Hard disk file type: `VDI` (default)
1. Storage on physical hard drive: `dynamically allocated` (default)
1. Hard drive file name: `mit6470`
1. Hard drive size: `10.00` GB

Before starting the VM, go to `Settings` and do the following customizations.

1. In `System` > `Motherboard`
    1. In `Boot Order`, uncheck `Floppy`
    1. In `Extended Features`, uncheck `Enable absolute pointing device`
1. In `Storage`
    1. Select the `Empty` slot under `Controller: IDE`
    1. Under `Attributes` > `CD / DVD Drive`, click the CD icon
       (tooltip: `Set up the virtual CD/DVD drive`)
    1. In the drop-down, click `Choose a virtual CD/DVD disk file`
    1. Navigate to the `.iso` image that you downloaded earlier
1. In `Audio`, uncheck `Enable Audio`
1. In `Network` > `Adapter 1` > `Advanced`, change `Adapter Type` to
   `Paravirtualized Network (virtio-net)`
1. In `Network` > `Adapter 2`
    1. Check `Enable Network Adapter`
    1. Change `Attached to` to `Host-only Adapter`
    1. In `Advanced`, change `Adapter Type` to
       `Paravirtualized Network (virtio-net)`
1. In `USB`, uncheck `Enable USB Controller`

### Commentary

[MIT SIPB's VM free service](https://xvm.mit.edu) has a 512 MB RAM limit. We
also use that limit to make sure our setup can be used with this service. This
limit is not very important, it can be changed with a VM restart.

The 10GB disk limit is important, because it is hard to change, and setting it
is a trade-off between the following considerations. If students have large
data sets, they will run out of disk space, and will have to diagnose the
problem and then resize the disk. If students fill up their VM disk by mistake,
and it is too big, it might fill up their real disk, which would render their
real OS unusable, and might cause them to lose everything.

Most customizations squeeze more efficiency out of the VM setup, by disabling
unused hardware. We set up a second network card so students can connect to any
service they install on the VM without exposing the service to the outside
world.


## Operating System Setup

Start the VM and click the  follow the steps below to go through the installation wizard.

1. Press _Enter_ to choose `English` as the boot prompt language.
1. Choose `Check disk for defects`
1. When the test completes, press _Enter_ to choose `Continue`
1. Press _Enter_ to choose `English` as the boot prompt language.
1. Choose `Install Ubuntu Server`
1. Press _Enter_ to choose `English` as the installation language.
1. Press _Enter_ to choose `United States` as the country.
1. Press _Enter_ to choose `No` in the `Configure the keyboard` dialog.
1. Press _Enter_ to choose `English (US)` as the keyboard type. This is largely
   irrelevant, because SSH will be used to access the server.
1. Press _Enter_ to choose `English (US)` as the keyboard layout.
1. Press _Enter_ to choose `eth0: Ethernet` as the primary network interface.
1. Type `webdev` as the hostname and press _Tab_, and then _Enter_ to continue.
1. Type `six470` as the admin user name and press _Tab_, and then _Enter_ to
   continue.
1. Type `webdev` as the admin password and press _Enter_ to continue.
1. Re-type `webdev` to confirm the admin password and press _Enter_ to
   continue.
1. Press the left arrow, and then _Enter_ to acknowledge the weakness of the
   password.
1. Press _Enter_ to decline having the admin's home directory encrypted.
1. Press _Enter_ to accept the default time zone.
1. Press the up arrow to select `Guided - use entire disk` as the partitioning
   method.
1. Press _Enter_ to select the only available hard disk.
1. Press _Enter_ to accept the default partitioning scheme.
1. Press _Enter_ to skip setting up an HTTP proxy.
1. Press _Enter_ to select `No automatic updates`.
1. Press the space bar to select the `OpenSSH server` then press _Tab_ and
   _Enter_ to continue.
1. Press _Enter_ to accept installing GRUB to the MBR.
1. Press _Enter_ to reboot.

After the VM reboots, go to `Devices` in the VirtualBox menu for the VM window,
and click `CD / DVD devices` > `Remove disk from virtual drive`. If the menu
item is grayed out, the installer ejected the virtual CD on its own. You may
now discard the `.iso` image that you downloaded.

Follow the steps below to set up mDNS so you can SSH into your machine.

1. Log into the VM as `six470` with password `webdev`.
1. Run the command `sudo apt-get update && sudo apt-get dist-upgrade -y`
1. Re-type the password `webdev` to appease _sudo_.
1. Run the command `sudo apt-get install -y avahi-daemon`
1. Run the command `sudo vim /etc/network/interfaces` (if you don't use vim,
   replace `vim` with `nano`)
1. Add the following lines at the end of the file and save it.

        # The host-only network interface
        auto eth1
        iface eth1 inet dhcp

1. Run the command `sudo reboot`

If everything went well, you will never have to log into the VM console again.
