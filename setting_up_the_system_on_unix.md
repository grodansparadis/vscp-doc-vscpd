# Setting up the system on Unix

To install VSCP & Friends on Unix you need to install the binary package or build the system from source. The build process is simple and it usually don't give any problems. You can find binary and source files [here](https://github.com/grodansparadis/vscp/releases)

## Installing from binary package

The binary package is supplied as a Debian package and as a snap image. Select one of them.

### Debian package installation
This should work as an installation method on all distribution's that can handle Debian packages.

### Snap istallation
This should work on all distributions that support the snap packages.

## Building from source

The build process is described in the file **BUILD_UNIX** in the root of the source folder. You find the source in the same folder as the installation packages. 

The source for the system is also available on [GitHub](https://github.com/grodansparadis/vscp_software) if you want to use unstable code or just prefers GitHub for some other reason.

### Step 1

If you don't have a build environment on your system follow the steps on [this page](https://www.cyberciti.biz/faq/debian-linux-install-gnu-gcc-compiler/). 

### Step 2

```bash
apt-get install git build-essential libopenssl-dev 
```    

and then

```bash
git clone https://github.com/grodansparadis/vscp.git
```    

and **go to step 10**



Install

```bash
apt-get install libwxbase3.0-dev
```

or if you **want graphics support (VSCP Works builds)**

```bash
apt-get install libwxgtk3.0-dev
```

Building GTK versions will build [VSCP Works](https://www.vscp.org/docs/vscpworks/doku.php) and other graphical components.

If you want wxWidgets 3.0 on Raspberry Pi read note [here](./setting_up_the_system_on_rasperry_pi.md).

###  Step 3

```bash
apt-get install libssl-dev libpcap0.8-dev libcurl4-openssl-dev
```
    
###  Step 4

If you want to get the source from GitHub you may want to install Git.

```bash
apt-get install git
```
    
###  Step 5 (optional)

If you want MQTT driver support (recommended). You need to install Mosquitto. Se [Installing mosquitto for use with VSCP](installing_moquitto_for_use_with_vscp.md) for instructions.

The installation only affect the build of the MQTT driver so if you don't need that driver you can skip this step.
 

###  Step 6 (optional)

If you want rawethernet support (recommended).

```bash
apt-get install libpcap-dev
```

The installation only affect the build of the raw ethernet driver so if you don't need that driver you can skip this step.

###  Step 7 (optional)

If you want LUA scripting support (recommended).

```bash
apt-get install lua5.2 lua5.2-dev
```
    
    

###  Step 8 (optional)

If you want SQLite3 database support (recommended).

```bash
apt-get install libsqlite3-0 libsqlite3-dev 
```

### Step 9

Normally you should consider working with one of the stable releases. All packages are available for download at [Sourceforge](https://sourceforge.net/projects/m2m/files/VSCP%20Software/). Download the .zip or the .tgz archives of the package.

You unpack the tgz with

```bash
tar -zxvf vscp_src_0.4.0.11.tgz
```

You unzip the  with

```bash
unzip -vscp_src_0.4.0.11.zip
```

As an alternative you can get the source from Github (need to gave Git installed as of above). If you get head software here you get the latest software but beware it can be unstable. If you clock **releases** you can fins stable software here as well.

```bash
git clone https://github.com/grodansparadis/vscp_software.git
```

This takes time on slower machines (like Raspberry Pi). Especially "Compressing objects" and "Resolving deltas". Go for a long walk meanwhile. 

An other alternative way is to get the source is to download the zip file from

```bash
https://github.com/grodansparadis/vscp_software and unpack it on your system.
```

Do this with 

```bash
wget https://github.com/grodansparadis/vscp_software/archive/master.zip
```

Then unpack the archive with

```bash
unzip master.zip  
```

There is a scripts that can be used to do these steps automagically for you    

```bash
wget https://sourceforge.net/projects/m2m/files/VSCP%20Software/1.0.0%20Neon/fetch_master/download
chmod a+x fetch_master
sudo ./fetchmaster
```    

will fetch the latest code, build it and install it for you. 

or add this to a a file

```bash
#!/bin/sh
sudo rm -rf vscp_software-master
sudo wget https://github.com/grodansparadis/vscp_software/archive  /master.zip
sudo unzip master.zip
sudo rm -rf master.zip
cd vscp_software-master
sudo ./configure
sudo make
```    

make it executable with 

```bash
chmod a+x 'filename'
```    

and the run the file.  

###  Step 10

```bash
cd vscp
bash

### Step 11

```bash
./configure
bash

If you get warnings about 

    ERR_remove_state(0);
    
being deprecated   

use 

```bash
./configure CFLAGS="-DOPENSSL_API_1_1"
```

to use openssl 1.1 instead of openssl 1.0

You can find out which version of openssl you have installed with

```bash
openssl version
```

```bash    
ls /usr/lib/i386-linux-gnu/libssl.so* (pc)
ls /usr/lib/arm-linux-gnueabihf/libssl.so* (RPi)
```    

{{after_configure.png?600}}   

#### Debugging

If you want a debug build use the flag

```bash	
--enable-debug
```

This flags used without a value is the same as

	
	--enable-debug="yes"


you can specify values as below

 | Value   | Description | 
 | -----   | ----------- | 
 | yes     | Specifying 'yes' adds '-g -O0' to the compilation flags for all languages. | 
 | info    | Specifying 'info' adds '-g' to the compilation flags. | 
 | profile | Specifying 'profile'adds '-g -pg' to the compilation flags and '-pg' to the linking flags. | 

### Step 12

```bash
make
```    

To make sure everything build OK you can issue make again and check the output for errors. You don't get bombarded with such masses of text on the second run. 

__If you did skip the MQTT installation you will get some complaints when the MQTT driver is compiled. This is nothing to worry about if you don't plan to use it. The same is true for other parts you skip as well__
    
It can be hard to see errors in all the text that is output by the build process. If you use

```bash
make | grep error
```    

it is much easier so see possible errors during the build process.  

    
###  Step 13

```bash
make install
```

Instead of first doing *make* and then *make install* you can of course do *make install* directly.

```bash
make install-conf
```

installs the default configuration files. Can always be used to restore them also.  

```bash
make web-install
```

installs default web content.  

This is done with script 

```bash
./do_web_download
```

which downloads and installs the latest UX code in the default folder. This script is located in the project root folder and can be used without the makefile also.

###  Step 14

You can now remove the source packages if your want.
    
After doing this you can set up a working VSCP & Friends system.

###  Step 15

 
Now reboot and the daemon will run. or issue

```bash
/init.d/vscpd start
```

to start the server.  
    
It is also possible to run the daemon as any other program with  

```bash
/usr/local/bin/vscpd -s
```

this is probably the best test to do on a newly installed system to see that the daemon starts properly as error messages will be shown in the terminal windows in this mode.  Terminate the daemon with **ctrl+c**  
    
Default install directory is */usr/local/bin*

###  Step 16

Not taking your newly installed system for a test ride \\  [ Take VSCP & Friends for a test ride](new_system_install_test_ride.md)


----


### Extra

**Build wxWidgets 2.8.12**
```bash
wget https://sourceforge.net/projects/wxwindows/files/2.8.12/wxGTK-2.8.12.tar.gz
./configure --disable-gui --enable-unicode
```

Disable GUI only for non GUI builds. Add --enable-debug for debug builds.

**Build wxWidgets 3.0.2**

```bash
wget https://sourceforge.net/projects/wxwindows/files/3.0.2/wxWidgets-3.0.2.tar.bz2
./configure --disable-gui
```    
    
Disable GUI only for non GUI builds.

    apt-get install libgtk2.0-dev

is needed for graphical builds.  

### Tips

If you want to know which version of wxWidgets you have installed

```bash
wx-config --version
```
    
If you want to know which packages are installed  

```bash
dpkg --get-selections
```
    
----  
 
Build statically 

```bash
./configure --enable-unicode --disable-shared --disable-gui
```
    
    
----

If your system does not have C++11 (Ubuntu Trusty) see this https://askubuntu.com/questions/428198/getting-installing-gcc-g-4-9-on-ubuntu  

[filename](./bottom_copyright.md ':include')
