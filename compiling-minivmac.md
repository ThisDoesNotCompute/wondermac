## The problem

Put simply, the Mini vMac project hasn't gotten much attention and the Linux-ARM binaries available for download don't work on newer versions of Raspberry Pi OS. This isn't a knock on anyone, life gets in the way sometimes. Thankfully, the source code is available and even more thankfully, the version 37.03 beta happens to work on RPi OS Trixie if you compile it yourself. This may not be the case with later RPi OS releases; for a truly future-proof solution another emulator should be considered. But for now, Mini vMac works well, so let's make hay while the sun shines.

## Why you may want/need to compile it yourself

There's 3 main reasons:
1. A new version of Mini vMac is released
2. A new version of RPi OS is released, and my binaries here don't work on it
3. You want to change the default config to something custom

## About Mini vMac configuration

Mini vMac has a *lot* of config options, many of which aren't exposed through its menu system. Instead, they need to be added as arguments when compiling the app. The binaries I have available in this repo assume the following:
1. You're running them on a Linux system with an ARM CPU
2. You want to emulate a Mac II
3. The display should be in color
4. The display resolution should be 640x480
5. The -fs version launches into fullscreen mode right away

If you want something different than these, you're gonna need to compile Mini vMac yourself.

## This isn't that scary, really

Two pieces of good news:
1. This process is blessedly quick and reasonably painless
2. You can do it on the Raspberry Pi itself

As lightweight as Mini vMac is when running, it's also pretty lightweight to compile, and the source code includes the necessary tools/scripts to do so.

## Let's go!

1. SSH into your Raspberry Pi.
2. Let's install some dependencies:

     sudo apt update && sudo apt install build-essential libx11-dev wget -y
4. Download the Mini vMac source file. The command below references 37.03 beta; browse to https://www.gryphel.com/c/minivmac/beta.html to find the latest beta release.

     wget https://www.gryphel.com/d/minivmac/minivmac-37.03/minivmac-37.03.src.tgz
6. Extract the file.
   
     tar -zxvf minivmac-37.03.src.tgz
8. Switch to the minivmac directory.
   
     cd minivmac
10. Compiling the minivmac executable involves the use of a tool provided with the source code. We need to set that tool up first:
    
     gcc setup/tool.c -o setup_t
12. The tool is set up by a shell script, which we need to build with the options we want. The complete list of options is at https://www.gryphel.com/c/minivmac/options.html. This command is what I used to build the binaries offered in this repo, modify it as appropriate:
    
     ./setup_t -t larm -m II -hres 640 -vres 480 -depth 3 -fullscreen 1 > setup.sh
14. We need to make the script executable, then run it:
    
     chmod +x setup.sh
    
     ./setup.sh
16. Finally, one simple command to actually build the binary:
    
     make

You should end up with a minivmac binary in the working directory. Drop a ROM file and disk image into that same folder and it should, hopefully, work as intended. If it doesn't and you need to try building it again, delete the setup.sh file (rm setup.sh) and try again from step 12 onwards.
