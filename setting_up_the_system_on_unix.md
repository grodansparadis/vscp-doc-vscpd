# Setting up the system on Unix

 
To install VSCP & Friends on Unix you need to build the system from source. The build process is simple and it usually don't give any problems. All packages are available for download at [Sourceforge](https///sourceforge.net/projects/m2m/files/VSCP%20Software/). Download the .zip or the .tgz archives of the package.

The build process is described in the file __BUILD_UNIX__ in the root of the source folder. You find the source in the same folder as the installation packages. The source for the system is also available on [GitHub](https///github.com/grodansparadis/vscp_software) if you want to use unstable code or just prefers GitHub for some other reason.

A sample configuration file for Unix is [here](https///github.com/grodansparadis/vscp_software/blob/master/config_examples/vscpd.conf_unix_distro).



## Getting VSCP & Friends working on a Debian system

Until we have a deb installation this is the steps to do to have vscp & friends working on a Debian system.

Your machine need to be connected to the Internet for this to work and you need to become root

    su -

or if you are on an Ubuntu system add 

    sudo

in front of the commands below or issue

    sudo -i  

to stay as the root user.

### Step 1

If you don't have a build environment on your system follow the steps on [this page](http://www.cyberciti.biz/faq/debian-linux-install-gnu-gcc-compiler/). Make (below) will complain if you don't. Or just issue

    apt-get update && apt-get upgrade
    apt-get install build-essential

If you are in a real hurry (or can't read) do

    apt-get install git build-essential libwxbase3.0-dev  libssl-dev libpcap0.8-dev libcurl4-openssl-dev libpcap-dev libcurl4-openssl-dev

and then

    git clone https://github.com/grodansparadis/vscp.git

and **go to step 10**

### Step 2

Install

    apt-get install libwxbase3.0-dev

or if you **want graphics support (VSCP Works builds)**

    apt-get install libwxgtk3.0-dev

Building GTK versions will build [VSCP Works](http://www.vscp.org/docs/vscpworks/doku.php) and other graphical components.

If you want wxWidgets 3.0 on Raspberry Pi read note [here](http://www.vscp.org/docs/vscpd/doku.php?id=setting_up_the_system_on_rasperry_pi).

###  Step 3

    apt-get install libssl-dev libpcap0.8-dev libcurl4-openssl-dev
    
###  Step 4

If you want to get the source from GitHub you may want to install Git.
    apt-get install git
    
###  Step 5 (optional)

If you want MQTT driver support (recommended). You need to install Mosquitto. Se [Installing mosquitto for use with VSCP](Installing moquitto for use with VSCP) for instructions.

The installation only affect the build of the MQTT driver so if you don't need that driver you can skip this step.
 

###  Step 6 (optional)

If you want rawethernet support (recommended).

    apt-get install libpcap-dev

The installation only affect the build of the raw ethernet driver so if you don't need that driver you can skip this step.

###  Step 7 (optional)

If you want LUA scripting support (recommended).

    apt-get install lua5.2 lua5.2-dev
    
    

###  Step 8 (optional)

If you want SQLite3 database support (recommended).

    apt-get install libsqlite3-0 libsqlite3-dev 

### Step 9

Normally you should consider working with one of the stable releases. All packages are available for download at [Sourceforge](https///sourceforge.net/projects/m2m/files/VSCP%20Software/). Download the .zip or the .tgz archives of the package.

You unpack the tgz with

    tar -zxvf vscp_src_0.4.0.11.tgz

You unzip the  with
    unzip -vscp_src_0.4.0.11.zip

As an alternative you can get the source from Github (need to gave Git installed as of above). If you get head software here you get the latest software but beware it can be unstable. If you clock **releases** you can fins stable software here as well.

    git clone https://github.com/grodansparadis/vscp_software.git

This takes time on slower machines (like Raspberry Pi). Especially "Compressing objects" and "Resolving deltas". Go for a long walk meanwhile. 

An other alternative way is to get the source is to download the zip file from

    https://github.com/grodansparadis/vscp_software and unpack it on your system.

Do this with 

    wget https://github.com/grodansparadis/vscp_software/archive/master.zip

Then unpack the archive with

    unzip master.zip  

There is a scripts that can be used to do these steps automagically for you    

    wget http://sourceforge.net/projects/m2m/files/VSCP%20Software/1.0.0%20Neon/fetch_master/download
    chmod a+x fetch_master
    sudo ./fetchmaster

will fetch the latest code, build it and install it for you. 

or add this to a a file

    #!/bin/sh
    sudo rm -rf vscp_software-master
    sudo wget https://github.com/grodansparadis/vscp_software/archive  /master.zip
    sudo unzip master.zip
    sudo rm -rf master.zip
    cd vscp_software-master
    sudo ./configure
    sudo make

make it executable with 

    chmod a+x 'filename'

and the run the file.  

###  Step 10

    cd vscp

### Step 11

    ./configure

If you get warnings about 

    ERR_remove_state(0);
    
being deprecated   

use 

    ./configure CFLAGS="-DOPENSSL_API_1_1"

to use openssl 1.1 instead of openssl 1.0

You can find out which version of openssl you have installed with

openssl version
    
    ls /usr/lib/i386-linux-gnu/libssl.so* (pc)
    ls /usr/lib/arm-linux-gnueabihf/libssl.so* (RPi)

{{after_configure.png?600}}   

#### Debugging

If you want a debug build use the flag

	
	--enable-debug


This flags used without a value is the same as

	
	--enable-debug="yes"


you can specify values as below

 | Value   | Description                                                                                | 
 | -----   | -----------                                                                                | 
 | yes     | Specifying 'yes' adds '-g -O0' to the compilation flags for all languages.                 | 
 | info    | Specifying 'info' adds '-g' to the compilation flags.                                      | 
 | profile | Specifying 'profile'adds '-g -pg' to the compilation flags and '-pg' to the linking flags. | 

### Step 12

    make

To make sure everything build OK you can issue make again and check the output for errors. You don't get bombarded with such masses of text on the second run. 

__If you did skip the MQTT installation you will get some complaints when the MQTT driver is compiled. This is nothing to worry about if you don't plan to use it. The same is true for other parts you skip as well__
    
It can be hard to see errors in all the text that is output by the build process. If you use

    make | grep error

it is much easier so see possible errors during the build process.  

    
###  Step 13

    make install

Instead of first doing *make* and then *make install* you can of course do *make install* directly.

    make install-conf

installs the default configuration files. Can always be used to restore them also.  

    make web-install

installs default web content.  

This is done with script 

 do_web_download

which downloads and installs the latest UX code in the default folder. This script is located in the project root folder and can be used without the makefile also.

###  Step 14

You can now remove the source packages if your want.
    
After doing this you can set up a working VSCP & Friends system.

###  Step 15

 
Now reboot and the daemon will run. or issue

    /init.d/vscpd start

to start the server.  
    
It is also possible to run the daemon as any other program with  

    /usr/local/bin/vscpd -s

this is probably the best test to do on a newly installed system to see that the daemon starts properly as error messages will be shown in the terminal windows in this mode.  Terminate the daemon with **ctrl+c**  
    
Default install directory is /usr/local/bin

###  Step 16

Not taking your newly installed system for a test ride \\  [ Take VSCP & Friends for a test ride](http://www.vscp.org/docs/vscpd/doku.php?id=new_system_install_test_ride )


----


### Extra

**Build wxWidgets 2.8.12**
    wget https://sourceforge.net/projects/wxwindows/files/2.8.12/wxGTK-2.8.12.tar.gz
./configure --disable-gui --enable-unicode

Disable GUI only for non GUI builds. Add --enable-debug for debug builds.

**Build wxWidgets 3.0.2**

    wget https://sourceforge.net/projects/wxwindows/files/3.0.2/wxWidgets-3.0.2.tar.bz2
    ./configure --disable-gui
    
Disable GUI only for non GUI builds.

    apt-get install libgtk2.0-dev

is needed for graphical builds.  

### Tips

If you want to know which version of wxWidgets you have installed

    wx-config --version
    
If you want to know which packages are installed  

    dpkg --get-selections
    
----  
 
Build statically 

    ./configure --enable-unicode --disable-shared --disable-gui
    
    
----

If your system does not have C++11 (Ubuntu Trusty) see this https://askubuntu.com/questions/428198/getting-installing-gcc-g-4-9-on-ubuntu  

\\ 
----
{{  ::copyright.png?400  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
