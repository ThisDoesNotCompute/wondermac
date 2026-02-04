With the Pi ready to go, next we'll set up Mini vMac. There are a number of classic Mac emulators out there, and while Mini vMac isn't perfect, it's lightweight and optimized for performance so it works well for this application.

1. Either download the desired minivmac Zip file from this repo, or compile it yourself (covered in another file). There are two options available for download here; one launches in windowed mode, while the other launches into fullscreen mode. They're identical in functionality otherwise, and are configured for 640x480 resolution. (If you want to customize this, you'll need to follow the guide to compile it on your own.)

2. Gather two more prerequisite files:
    * A Mac II ROM file. It needs to be for a Macintosh II specifically, not another model. I'm not hosting that here for (hopefully) obvious reasons, but oh hey this link is interesting http://hampa.ch/pub/software/ROM/Macintosh%2068K
    * A disk image to boot from. If you have experience with Mac emulation you know what this is about; if you don't, this URL has a number to choose from, I'd recommend this one to start: https://mega.nz/folder/8hA3AQCJ#pWUq92L70yDXlogy9lk5Dg/file/N5YxFQzS

3. Use an FTP client to connect to the Pi. On macOS I like Cyberduck; on Windows there's WinSCP; and on Linux you should already know because you use Linux.
    * Create a new directory on the Pi called minivmac. Putting this on the Desktop is convenient, but it doesn't really matter
    * Copy the above 3 files to this directory

4. Through VNC or attached keyboard/mouse, navigate to that folder on the Pi and launch minivmac. Click Execute when prompted. The emulated Mac should boot straight away.

5. Some basic Mini vMac controls:
    * Ctrl-F toggles fullscreen
    * Ctrl-Q quits the app, or you can do Special --> Shut Down in Mac OS
    * Ctrl-H toggles the menu; note that you need to continue to hold down Ctrl to keep it visible

6. Let's set up Mini vMac to launch automatically when the Pi boots. We're going to use SSH for this because it's easy and if you don't know much about the command line, this is a good opportunity to learn. macOS, Windows and Linux all have this built into their respective command prompts (yes, even Windows!)
    * ssh username@hostname.local (where username and hostname are the ones you set when you imaged the SD card)
    * mkdir -p ~/.config/autostart
    * nano ~/.config/autostart/minivmac.desktop
    * Paste this into the file (again, changing the path where you saved the minivmac folder):
   ````
    [Desktop Entry]
    Name=minivmac
    Type=Application
    Exec=sh -c "sleep 10;/home/username/Desktop/minivmac/minivmac"
    Path=/home/pi/Desktop/minivmac
    Terminal=false
   ````
    * Press Ctrl-X to exit nano, then press Y to save
    * sudo reboot to reboot the Pi. If Mini vMac doesn't launch automatically within 10 seconds of reaching the desktop, something's wrong.
