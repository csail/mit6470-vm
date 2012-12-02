# Using the MIT 6.470 development VM on Mac OS X

This document contains step-by-step instructions for using the MIT 6.470
development VM on a computer with Mac OS X 10.6 or better.


## One-Time Setup

Follow the steps below exactly once, to get everything set up.

Set up stable and development versions of Firefox and Google Chrome.

1. Go to the [Firefox Channels page](http://www.mozilla.org/firefox/channel/).
1. Download and install the `Firefox` channel build.
1. Download and install the `Aurora` channel build.
1. Go to the [Chrome Release Channels page](http://www.chromium.org/getting-involved/dev-channel/).
1. Download and install the `Stable channel for Mac` build.
1. Download and install the `Canary build for Mac`.

Download the development VM image.

1. Open Finder and go to the `Documents` folder from the left sidebar.
1. Create a folder named `mit6470-vm`.
1. Download the development VM .zip file from the
[MIT 6.470 downloads section](http://6.470.scripts.mit.edu/TBD).
1. Unpack the .zip file in the `mit6470-vm` folder that you have just created.

Set up VirtualBox, so you can run the development VM.

1. Download VirtualBox for OSX hosts from the
   [VirtualBox download page](https://www.virtualbox.org/wiki/Downloads)
1. Open the downloaded `.dmg` file and double-click on the package icon to
   install VirtualBox.
1. Run VirtualBox from the `/Applications` directory.
1. From the VirtualBox menu, select `Machine` > `Add...`.
1. Go to the `mit6470-vm` folder in the `Documents` folder, and select the
   `mit6470.vbox` file.
1. Right-click on the `MIT 6.470` entry that just showed up and select
   `Create Shortcut on Desktop`

Set up SSHFS, so you can use the VM's files from OSX.

1. Go to to the [Fuse for OS X download page](http://osxfuse.github.com/).
1. Download and install the `OSXFUSE` package listed under `Stable Releases`.
1. Download and install the `SSHFS` package listed under `Stable Releases`.
1. Open Finder, go to the `Applications` folder and double-click `Terminal`.
1. Right-click on the `Terminal` application  icon in the dock, and select
   'Options' > 'Keep in Dock' from the pop-up menu.
1. Run the following command in `Terminal` to make a folder for the VM's files.

    mkdir ~/Documents/mit6470-vm/files

1. Run the following command in `Terminal` to check that SSHFS works.

    sshfs --version

1. Verify that the output is similar to the following. The numbers can be
   different. Make sure the word `error` does not show up.

        SSHFS version 2.4
        FUSE library version: 2.9.2
        fusermount version: 2.9.2
        using FUSE kernel interface version 7.19

1.  Press `Command`+`W` to close the Terminal window.


## Run Stuff

Follow these steps every time you restart your computer.

1. Double-click the `MIT 6.470` desktop shortcut to launch the VM.
1. Click the `Terminal` icon in the dock.
1. Run the following command in `Terminal` to access the VM's files.

        sshfs webdev.local:/ ~/Documents/mit6470-vm/files

1. Run the following command in `Terminal` to connect to the server.

        ssh six470@webdev.local

1. You can find the server files in the `files` folder inside the `mit6470-vm`
   folder that you created when you set up the VM.


## Troubleshooting

This section contains common issues that students have ran into while setting
up the 6.470 development VM on Mac OS X.


