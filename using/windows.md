# Using the MIT 6.470 development VM on Windows

This document contains step-by-step instructions for using the MIT 6.470
development VM on a computer with Windows XP or better.


## One-Time Setup

Follow the steps below exactly once, to get everything set up.

Set up stable and development versions of Firefox and Google Chrome. You do not
need them to use the development VM, but having multiple browsers helps
tracking down problems in your Web application.

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
   If you're not sure whether you have 32-bit or 64-bit Windows, try the 64-bit
   `.msi` first. It will not install on a 32-bit system.
1. Download the development VM `mit640-vm.7z` file from the
   [MIT 6.470 downloads section](http://6.470.scripts.mit.edu/TBD).
1. Double-click the `mit6470-vm.7z` file that you have just downloaded.
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
1. Close the 7-Zip window after the exctracting operation completes.

Set up VirtualBox, so you can run the development VM.

1. Go to the
   [VirtualBox download page](https://www.virtualbox.org/wiki/Downloads)
1. Download `VirtualBox for Windows hosts`.
1. Open the downloaded `.exe` file to install VirtualBox.
1. Click the `Next` / `Yes` / `Install` / `Finish` buttons to accept the
   default settings throughout the installation process.
1. If VirtualBox does not start up after the installation completes, open the
   Start menu and select `All Programs` > `Oracle VM VirtualBox` >
   `Oracle VM VirtualBox`.
1. From the VirtualBox menu, select `File` > `Preferences...`.
1. Select the `Network` tab.
1. If you see a `VirtualBox Host-Only Ethernet Adapter` under the
   `Host-only Networks` list, skip the following 10 steps.
   (up to and including "Click the `OK` buttons to dismiss the dialog boxes.")
1. Click the button with a green plus sign on the right side of the window.
   (tooltip: `Add host-only network`)
1. Click the screwdriver button. (tooltip: `Edit host-only network`)
1. Find the shield in the task bar, click it, and click the `Yes` button in the
   `User Account Control` dialog box.
1. Select the `DHCP server` tab.
1. Check the `Enable Server` checkbox.
1. Enter `192.168.56.100` in the `Server Address` field.
1. Enter `255.255.255.0` in the `Server Mask` field.
1. Enter `192.168.56.101` in the `Lower Address Bound` field.
1. Enter `192.168.56.254` in the `Upper Address Bound` field.
1. Click the `OK` buttons to dismiss the dialog boxes.
1. From the VirtualBox menu, select `Machine` > `Add...`.
1. Go to the `mit6470-vm` folder in the `My Documents` folder, and double-click
   the `mit6470` file. (if your Windows Explorer shows file extensions, the
   file name will be `mit6470.vbox`)
1. Right-click on the `MIT 6.470` entry that just showed up and select
   `Create Shortcut on Desktop`
1. Double-click the desktop shortcut to start the VM.

Set up [Apple Bonjour](http://www.apple.com/support/bonjour/) so you can
use the `webdev.local` name to connect to your VM, instead of having to
remember the `192.168.56.101` IP address.

1. Go to the
   [Bojour Print Services for Windows download page](http://support.apple.com/kb/DL999).
1. Click the `Download` button and open the downloaded `.exe` file.
1. Click the `Next` buttons to accept the default settings throughout the
   installation process.
1. Open the Start menu and select `All Programs` > `Apple Software Update`.
1. If the `Install` button is not grayed out, click it to update Bonjour.

Set up PuTTY, so you can connect to the development VM's terminal.

1. Go to the
   [PuTTY download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).
1. Download the `Installer`, under `Binaries` >
   `A Windows installer for everything except PuTTYtel`.
1. Run the installer `.exe` to set up PuTTY.
1. Click the `Next` buttons to accept the default settings throughout the
   installation process.
1. Open the Start menu and select `All Programs` > PuTTY` > `PuTTY`.
1. Type `webdev.local` in the `Host Name (or IP address)` field in the
   `Putty Configurtation` dialog.
1. Type `MIT 6.470` in the text field under the `Saved Sessions` label.
1. Click the `Save` button.
1. Click the `Open` button.
1. Click `Yes` in the `PuTTY Security Alert` warning dialog box.
1. Type `six470` at the `login as:` prompt, and then press _Enter_.
1. Type `webdev` at the password prompty, and then press _Enter_.
1. If everything worked, you should see a bunch of text ending with a prompt
   that resembles the following.

```
six470@webdev:~$
```

1. Type `exit` and pres _Enter_. The terminal window should close.

Shut down your development VM.

1. Go to your VM's VirtualBox window.
1. Press the `X` button at the top-right of the window to close it.
1. Check the `Send the shutdown signal` radio button.
1. Press `OK`.

## Run Stuff

Follow these steps every time you restart your computer.

1. Double-click the `MIT 6.470` desktop shortcut to launch the VM.
1. Verify that you can open [http://webdev.local](http://webdev.local) in a Web
   browser.

Connect to the VM's file share, so you can use the VM's files from Windows.

1. Open `Windows explorer`.
1. Open the Start menu and select `Computer`.
1. Click the `Map network drive` button in the toolbar.
1. Type `\\webdev\files` in the `Folder:` textbox.
1. Uncheck the `Reconnect at logon` checkbox.
1. Check the `Connect using different credentials` checkbox.
1. Press the `Finish` button.
1. Enter `six470` in the `User name` field in the `Enter Network Password`
   dialog box.
1. Enter `webdev` in the `Password` field.
1. Check the `Remember my credentials` checkbox.
1. Press the `OK` button.

Connect to the VM's terminal.

1. Open the Start menu and select `All Programs` > PuTTY` > `PuTTY`.
1. Click `MIT 6.470` in the `Saved Sessions` list.
1. Press the `Open` button.
1. Type `six470` at the `login as:` prompt, and then press _Enter_.
1. Type `webdev` at the password prompty, and then press _Enter_.


## Troubleshooting

This section contains common issues that students have ran into while setting
up the 6.470 development VM on Windows.


