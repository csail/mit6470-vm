# Using the MIT 6.470 development VM on Windows

This document contains step-by-step instructions for using the MIT 6.470
development VM on a computer with Windows XP or better.


## One-Time Setup

Follow the steps below exactly once, to get everything set up.

Set up stable and development versions of Firefox and Google Chrome.

1. Go to the [Firefox Channels page](http://www.mozilla.org/firefox/channel/).
1. Download and install the `Firefox` channel build.
1. Download and install the `Aurora` channel build.
1. Go to the
   [Chrome Release Channels page](http://www.chromium.org/getting-involved/dev-channel/).
1. Download and install the `Stable channel for Mac` build.
1. Download and install the `Canary build for Mac`.

Get the development VM image.

1. Go to the [7-Zip download page](http://7-zip.org/download.html).
1. Download and open the `.msi` version of 7-Zip for your version of Windows.
   In the installation wizard, click the `Next` button until 7-Zip is
   installed.
   If you're not sure whether you have 32-bit or 64-bit Windows, try both
   `.msi` files. Only one will install without errors.
1. Download the development VM `mit640-vm.7z` file from the
   [MIT 6.470 downloads section](http://6.470.scripts.mit.edu/TBD).
1. Right-click the `mit6470-vm.7z` file that you have just downloaded.
1. Check the `Select a program form a list of installed programs` radio button
   in the dialog box that pops up, then press the `OK` button.
1. Click the `Browse...` button in the `Open with` dialog box.
1. In the `Open with...` dialog box, double-click the `7-Zip` folder, and then
   double-click the `7zFM` file.
1. Press the `OK` button in the `Open with` dialog box. This will close the
   dialog box and open the `.7z` archive in 7-Zip.
1. Press the `Extract` button in the toolbar.
1. Press the `...` button next to the text field in the `Copy` dialog box.
1. Select `My Documents`.
1. Press the `Make New Folder` button.
1. Type `mit-6470` and press the `OK` button in the dialog box.
1. Press the `OK` button in the `Copy` dialog box.

Set up VirtualBox, so you can run the development VM.

1. Download VirtualBox for OSX hosts from the
   [VirtualBox download page](https://www.virtualbox.org/wiki/Downloads)
1. Open the downloaded `.dmg` file and double-click on the package icon to
   install VirtualBox.
1. Open the Start menu, select `All Programs` > `VirtualBox` > `VirtualBox`.
1. From the VirtualBox menu, select `File` > `Preferences...`.
1. Select the `Network` tab.
1. Click the button with a green plus sign on the right side of the window.
   (tooltip: `Add host-only network`)
1. Click the screwdriver button. (tooltip: `Edit host-only network`)
1. Select the `DHCP server` tab.
1. Check the `Enable Server` checkbox.
1. Enter `192.168.56.2` in the `Server Address` field.
1. Enter `255.255.255.0` in the `Server Mask` field.
1. Enter `192.168.56.100` in the `Lower Address Bound` field.
1. Enter `192.168.56.128` in the `Upper Address Bound` field.
1. Click the `OK` buttons to dismiss the dialog boxes.
1. From the VirtualBox menu, select `Machine` > `Add...`.
1. Go to the `mit6470-vm` folder in the `Documents` folder, and select the
   `mit6470.vbox` file.
1. Right-click on the `MIT 6.470` entry that just showed up and select
   `Create Shortcut on Desktop`

Set up PuTTY, so you can connect to the development VM's console.

1. Go to the
   [PuTTY download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).
1. Download the `Installer`, under `Binaries` >
   `A Windows installer for everything except PuTTYtel`.
1. Run the installer `.exe` to set up PuTTY.

## Run Stuff

Follow these steps every time you restart your computer.

1. Double-click the `MIT 6.470` desktop shortcut to launch the VM.

Connect to the VM's file share, so you can use the VM's files from Windows.

1. TBD

## Troubleshooting

This section contains common issues that students have ran into while setting
up the 6.470 development VM on Windows.


