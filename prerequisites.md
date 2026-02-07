## What you'll need

This guide is based around the following:
* a Maclock (affiliate link): https://amzn.to/4qqzL5c or from AliExpress, etc.
* Raspberry Pi Zero W or Zero 2 W (I like this kit, affiliate link): https://amzn.to/4tozTVi
* Waveshare 2.8" LCD (affiliate link): https://amzn.to/4qoIWTx or https://www.waveshare.com/2.8inch-dpi-lcd.htm

## Raspberry Pi OS and the Waveshare screen

The easiest way to get Raspberry Pi OS on your SD card is using the Raspberry Pi Imager tool (https://www.raspberrypi.com/software).

1. Launch the app and...
    * Choose your Pi hardware (Zero or Zero 2)
    * Choose Raspberry Pi OS (32-bit), which should be the Trixie release
    * Select your SD card from the list
    * Supply a hostname, like "wondermac" or whatever
    * Choose the appropriate options for localization
    * Supply a username and password
    * Supply your WiFi connection details
    * Enable SSH, and most people will want to choose password authentication
    * Raspberry Pi Connect is optional; use it if you know what it is and leave it off if you don't
    * Click Write and confirm the prompts
    * When writing to the card is done, on most/all platforms it'll automatically be ejected; reinsert it into your computer as we're not done with it yet

Next, we need to set up the software for the Waveshare screen. The Wiki page for the 2.8" WaveShare screen is here:
https://www.waveshare.com/wiki/2.8inch_DPI_LCD

Follow the instructions for the Bullseye/Bookworm RPi OS branch, they work on Trixie as well. Briefly:

2. Copy these lines to the end of the config.txt file on the SD card:
```
dtoverlay=vc4-kms-v3d
dtoverlay=waveshare-28dpi-3b-4b   
dtoverlay=waveshare-28dpi-3b
dtoverlay=waveshare-28dpi-4b
dtoverlay=waveshare-touch-28dpi
dtoverlay=vc4-kms-dpi-2inch8
```
3. Extract the contents of the DBTO file you downloaded from the Wiki to /overlays on the SD card.

## Initial OS setup

After powering the Pi on for the first time, there's a couple of changes you'll want to make.

1. Enable VNC for easier remote control (do this now if you don't want to connect a USB keyboard/mouse to the Pi):
    * SSH to the Pi using the hostname/IP and credentials you supplied in the RPi OS imaging tool.
    * Run the command sudo raspi-config
    * Choose option 3 ("Interface Options")
    * Choose VNC, then select Yes
    * When it takes you back to the main config menu, hit Tab to switch to the buttons on the bottom, then arrow right to select Finish.
    * You can then exit the SSH session

3. Rotate the display image:
    * You can do this either through VNC or with an attached USB keyboard/mouse
    * Go to the Pi menu --> Preferences --> Control Centre, then scroll down to find the Screen Configuration section
    * Click the Screens menu, then choose DPI-1 --> Orientation and select Right
    * Drag the Preferences window to the left so you can click the Apply button
    * As soon as you click Apply, the display will rotate and you'll need to confirm the change within a few seconds. If you're doing this over VNC, the screen/mouse alignment gets messed up so you won't be able to click OK to confirm. Instead, quickly press Tab until the OK button is highlighted, then press Enter/Return to confirm. (If you have a USB keyboard/mouse, just click the OK button like normal.)

4. Turn off the onscreen keyboard, which gets annoying fast:
    * While still in the Preferences window, scroll up to the Display section
    * Set On-Screen Keyboard to Disabled
    * If you didn't enable VNC using SSH in step 1, now's the time to do that -- Click the Interfaces section and toggle VNC on
    * Let the Pi reboot if prompted

That's it for basic setup of the Pi!
