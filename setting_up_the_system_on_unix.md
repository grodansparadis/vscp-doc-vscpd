# Setting up the system on Unix

To install VSCP & Friends on Unix you need to install the binary package or build the system from source. The build process is simple and it usually don't give any problems. You can find binary and source files [here](https://github.com/grodansparadis/vscp/releases)

## Installing from binary package

The binary package is supplied as a Debian package. 

### Debian package installation
This should work as an installation method on all distribution's that can handle Debian packages.


## Building from source

The build process is described in the file **BUILD_UNIX** in the root of the source folder. You find the source in the same folder as the installation packages. 

The source for the system is also available on [GitHub](https://github.com/grodansparadis/vscp) if you want to use unstable code or just prefers GitHub for some other reason.

### Step 1

Prepare the build environment with

```bash
sudo apt update
sudo apt install build-essential
sudo apt install git build-essential libopenssl-dev libexpat
```    
to install the build tools. 

### Step 2

Get the latest source release package from [https://github.com/grodansparadis/vscp/releases] and unpack it in the folder of your choice. 

You unpack the tgz with

```bash
tar -zxvf file.tgz
```
or

```
unzip file.zip
```

(use v)

As an alternative if you want bleeding edge software, go to a folder of your choice, and do

```bash
git clone https://github.com/grodansparadis/vscp.git
```    

For a production system choosing a release version is recommended.


###  Step 3

Enter the VSCP project folder and do

```bash
cd vscp
./configure
bash
```


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

### Step 4

```bash
make
```    

To make sure everything build OK you can issue make again and check the output for errors. You don't get bombarded with such masses of text on the second run. 

__You may get some complaints when the code is compiled. This is normally nothing to worry about and they are just warnings from subcomponents.__

Tip    
It can be hard to see errors in all the text that is output by the build process. If you use

```bash
make | grep error
```    

it is much easier so see possible errors during the build process.  

    
###  Step 5

Install the system with

```bash
make install
```

Instead of first doing *make* and then *make install* you can of course do *make install* directly.

```bash
make install-conf
```

installs the default configuration files. Can always be used to restore them also.  

```bash
sudo make install-systemd-script
```

installs systemd startup scripts.

Reboot or start service with

```
sudo systemcrl start vscpd
```

```bash
make web-install
```

installs default web content.  

This is done with script 

```bash
./do_web_download
```

which downloads and installs the latest UX code in the default folder. This script is located in the project root folder and can be used without the makefile also.

###  Step 6

You can now remove the source packages if your want.
    
After doing this you can set up a working VSCP & Friends system.

###  Step 7

 
Now reboot and the daemon will run. or issue

```bash
sudo systemctl enable vscpd
sudo systemctl start vscpd
```

to start the server.  
    
It is also possible to run the daemon as any other program with  

```bash
/usr/local/bin/vscpd -s
```

this is probably the best test to do on a newly installed system to see that the daemon starts properly as error messages will be shown in the terminal windows in this mode.  Terminate the daemon with **ctrl+c**  
    
Default install directory is */usr/local/sbin*

----

### Notes

If your system does not have C++11 (Ubuntu Trusty) see this https://askubuntu.com/questions/428198/getting-installing-gcc-g-4-9-on-ubuntu  

----

If you want to use SysVInit to SystemD instead of there is an init file in the service/sysvinit folder. Issue

```
make install_sysvinit
```

to install and then

```
sudo /etc/init.d/vscpd start to start
```

to start te service

----



[filename](./bottom_copyright.md ':include')
