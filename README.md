Droidian on Moto G Power (sofia)
========

Droidian is a GNU/Linux distribution based on top of Mobian, a Debian-based distribution for mobile devices. The goal of Droidian is to be able to run Mobian on Android phones.

## THE INSTRUCTIONS BELLOW WILL WIPE ALL THE DATA ON YOUR DEVICE

# Default password: 1234

## Prepare

 * You need unlocked bootloader and Android 10 on your phone with stock vendor partitions.
 * Go to Settings->About phone and tap the Build number 7 times
 * Got to Settings->System->Advanced->Developer options and activate USB debugging
 * Backup all your data, the installation steps will wipe everything in the userdata partition.
 * Using adb for example: `adb pull /dev/block/by-name/userdata`
 * Make sure you can boot both slots a & b

## Installation
 * Download the latest build here: https://github.com/arpio23/droidian-images/releases
 * Unpack the zip file
 * Boot to fastbootd:
   <pre><code>adb reboot fastboot</code></pre>
 * Using fastboot flash following partitions:
    <pre><code>fastboot flash boot data/boot.img
   fastboot flash userdata data/userdata.img</code></pre>
 * Reboot to system and "DO NOT PRESS THE POWER BUTTON WHEN SCREEN IS BLACK or BLANK, BE PATIENT"
 * If you have a Moto G Power (sofia) and the instructions did not work, create an issue: https://github.com/arpio23/droidian-images/issues
 * Find the solution here: https://t.me/DroidianLinux

## Mobile Data set up
 * You successfuly booted Droidian
 * Go to Setteings->Mobile Network and activate Mobile data
      Add the Acces Point for your provider
 * Using ssh or the terminal app on the phone:
      <pre><code>cd /usr/share/ofono/scripts
      ./deactivate-context 1
      ./set-context-property 0 AccessPointName YOUR_AP_NAME
      ./activate-context 1
      </code></pre>
* Reboot
* Go to Setteings->Mobile Network and toggle Mobile data

## Bugs and workarounds
* Camera not working, is a common issue on droidian. Some devices have camera working with waydroid. But does not work on sofia.
* Screen to dark: <br />
   I patched the gnome-settings-daemon https://github.com/arpio23/gnome-settings-daemon <br />
   It is preinstalled but not activated <br />
   Run this in terminal: <br />
<pre><code>gsettings set org.droidian.settings-daemon.power auto-brightness-linear true
</code></pre>
* Mobile data not working after calls or after dropping to 3g and back to 4g: <br />
   Toggle Mobile Data: Settings->Mobile Network
   
* Camera notch: <br />
   Patched phosh https://github.com/arpio23/phosh/tree/bookworm is preinstalled<br />
   <pre><code>gsettings set sm.puri.phosh top-panel-offset 64</code></pre>
   Reboot <br />
   Also need a custom gtk.css in your .config/gtk-3.0/<br />
   More to come ...
   
