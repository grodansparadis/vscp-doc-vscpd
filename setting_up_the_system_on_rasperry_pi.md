![](./images/pi1l.jpg)

# Setting up the system on Rasperry Pi

The [Raspberry Pi](https://www.raspberrypi.org/) is a very nice single board computer and a perfect match for VSCP & Friends. __The VSCP daemon should work on all Raspberry Pi's except the RPi1 with 256 MB memory where the SSL lib fails probably due to out of memory.__ 

If the startup script does not work or if you experience other startup problems you may need to update the firmware of your Raspberry Pi with **rpi-update**

VSCP & Friends has been tested and works very well on Raspberry Pi. 

The setup is the same as on other Unix systems so the instructions to [setup VSCP & Friends on a Unix system](./setting_up_the_system_on_unix.md) can be used. 

As an alternative David Steeman have written easy to follow step by step instruction [here](http://www.steeman.be/posts/Installing%20VSCP%20on%20a%20Raspberry%20Pi). 

**IMPORTANT**
If you plan to use a Raspberry Pi in a control situation you will probably want to make the root file system read only. This is described [here](https://wiki.debian.org/ReadonlyRoot) and [here](https://learn.adafruit.com/read-only-raspberry-pi/).  If you don't do this you most certainly will find your board not starting after a power loss. Well you may be lucky for some time but eventually it will happen. So make the root partition read only!

Expect the build of VSCP to take half an hour on a Pi version 2 and an hour and a half on Pi version 1.

##  Compile wxWidgets 3.0 on Raspberry Pi

**wxWidgets 3.0 is now available as a package also in Raspian.**

Instead of 2.8.12 you may want the latest version (3.0.2 as of this writing) instead. If so follow these steps
    
    sudo apt-get install build-essential  
    
Install gtk library

    sudo apt-get install libgtk2.0-dev
    
Compile wxWidgets

```bash    
    cd /path/to/wxWidgets-3.0.x
    mkdir gtk-build
    gtk-build
    ../configure
    make
    make install
```
    
## Read only SD on Raspberry Pi

For the full story read [this](https://wiki.debian.org/ReadonlyRoot)

Short instructions form [here](https://www.raspberrypi.org/forums/viewtopic.php?p=213440). There is an alternative solution [here](https://www.raspberrypi.org/forums/viewtopic.php?f=29&t=23154)

When working with this and you need to add a driver or something you can always mount the filesystem rw again with

    mount -o remount,rw /

### Step 1

mount /var/log and /tmp in ram (here 30MB per each) by adding 

    # Tempfiles in RAM
    RAMTMP=yes

to 

   /etc/default/rcS 

### Step 2

Change 

    /etc/fstab 
    
to

     tmpfs           /tmp            tmpfs   nodev,nosuid,size=30M,mode=1777          0    0
     tmpfs           /var/log        tmpfs   nodev,nosuid,size=30M,mode=1777          0    0
     #/dev/mmcblk0p1 /boot           vfat    defaults                                 0    2
     /dev/mmcblk0p2  /               ext2    defaults,ro,noatime,errors=remount-ro    0    1
     #/dev/mmcblk0p3 /home           ext4    defaults,noatime                         0    1
     # a swapfile is not a swap partition, so no using swapon|off from here on, use  dphys-swapfile swap[on|off]  for that

It is good to have a rw home partition, or desktop session will fail to start. With this configuration you won't be able to upgrade packages, as apt and dpkg need */var/lib* and */var/cache* writable. Consider using a rw /var or per-subdirectory configuration.

### Step 3

edit

    /etc/init.d/hwclock.sh


in line 60 (the first of start case) change "-f" to "-L"

### Step 4

edit 

    /etc/environment 
    
and add

    BLKID_FILE="/var/local/blkid.tab"

### Step 5

Fix mtab

    sudo rm /etc/mtab
    sudo ln -s /proc/self/mounts /etc/mtab
    
###  Step 6

*  Make sure VSCP log files go to /var/log or that they are turned off.
*  Remember that any logger driver has to log to a r/w location.



{% include "./bottom_copyright.md" %}
 
