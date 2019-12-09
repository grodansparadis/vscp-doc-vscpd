# Setting up the system on 8Devices Carambola




## Setup your system on OpenWrt

General information is [here](./setting_up_the_system_on_openwrt.md)

## VSCP & Friends on OpenWrt/Carambola

From version 0.4.0.11 VSCP & Friends compiles and installs on the Carambola board available from [8Devices](https://8devices.com/) with web/libwebsocket and all drivers and also other OpenWrt platforms.  

The files needed to install is available in the 

## Install binaries

From version 0.4.0.11 I will try to maintain a binary distribution for OpenWrt. You can find these files at [Sourceforge](https://sourceforge.net/projects/m2m/files/VSCP%20binaries/openwrt/). The binary package builds all drivers so it use a lot of flash but you can remove the drivers you don't need after everything is installed to save space.

The first thing you have to do before installing VSCP itself is to install the libraries it depends on. For your convenience they are added to the binary distribution.

Connect to the board with ssh which must be Internet connected and install as of below

#####  Step 1

```bash
    wget http://sourceforge.net/projects/m2m/files/VSCP%20binaries/openwrt/openwrt_0.4.0.11/terminfo_5.7-5_ramips.ipk/download
    opkg install terminfo_5.7-5_ramips.ipk
    rm terminfo_5.7-5_ramips.ipk
```    
    
#####  Step 2

```bash
    wget http://sourceforge.net/projects/m2m/files/VSCP%20binaries/openwrt/openwrt_0.4.0.11/libncurses_5.7-5_ramips.ipk/download
    opkg install libncurses_5.7-5_ramips.ipk
    rm libncurses_5.7-5_ramips.ipk
```
    
##### Step 3

 ```bash   
    wget http://sourceforge.net/projects/m2m/files/VSCP%20binaries/openwrt/openwrt_0.4.0.11/uclibcxx_0.2.4-1_ramips.ipk/download
    opkg install uclibcxx_0.2.4-1_ramips.ipk
    rm uclibcxx_0.2.4-1_ramips.ipk
```    

##### Step 4

```bash
    wget http://sourceforge.net/projects/m2m/files/VSCP%20binaries/openwrt/openwrt_0.4.0.11/libstdcpp_4.7-linaro-1_ramips.ipk/download  
    opkg install libstdcpp_4.7-linaro-1_ramips.ipk
    rm libstdcpp_4.7-linaro-1_ramips.ipk
```
    
#####  Step 5

```bash    
    wget http://sourceforge.net/projects/m2m/files/VSCP%20binaries/openwrt/openwrt_0.4.0.11/zlib_1.2.7-1_ramips.ipk/download
    opkg install zlib_1.2.7-1_ramips.ipk
    rm zlib_1.2.7-1_ramips.ipk
```    

##### Step 6

```bash
    wget http://sourceforge.net/projects/m2m/files/VSCP%20binaries/openwrt/openwrt_0.4.0.11/libopenssl_1.0.1c-1_ramips.ipk/download
    opkg install libopenssl_1.0.1c-1_ramips.ipk
    rm libopenssl_1.0.1c-1_ramips.ipk
```    

##### Step 7

```bash
    wget http://sourceforge.net/projects/m2m/files/VSCP%20binaries/openwrt/openwrt_0.4.0.11/libexpat_2.0.1-1_ramips.ipk/download
    opkg install libexpat_2.0.1-1_ramips.ipk
    rm libexpat_2.0.1-1_ramips.ipk
```    

##### Step 8

```bash
    wget http://sourceforge.net/projects/m2m/files/VSCP%20binaries/openwrt/openwrt_0.4.0.11/libwxbase_2.8.10-1_ramips.ipk/download
    opkg install libwxbase_2.8.10-1_ramips.ipk
    rm libwxbase_2.8.10-1_ramips.ipk
```

##### Step 9

```bash
    wget http://sourceforge.net/projects/m2m/files/VSCP%20binaries/openwrt/openwrt_0.4.0.11/libmosquitto-nossl_1.0.3-1_ramips.ipk/download
    opkg install libmosquitto-nossl_1.0.3-1_ramips.ipk
    rm libmosquitto-nossl_1.0.3-1_ramips.ipk
```

#####  Step 10

    
This one is actually not needed if you will not develop with mosquitto

```bash
    wget http://sourceforge.net/projects/m2m/files/VSCP%20binaries/openwrt/openwrt_0.4.0.11/libmosquitto_1.0.3-1_ramips.ipk/download
    opkg install libmosquitto_1.0.3-1_ramips.ipk
    rm libmosquitto_1.0.3-1_ramips.ipk
```

##### Step 11

```bash
    wget http://sourceforge.net/projects/m2m/files/VSCP%20binaries/openwrt/openwrt_0.4.0.11/libmicrohttpd_0.9.19-1_ramips.ipk/download
    opkg install libmicrohttpd_0.9.19-1_ramips.ipk
    rm libmicrohttpd_0.9.19-1_ramips.ipk
```

##### Step 12

```bash
    wget http://sourceforge.net/projects/m2m/files/VSCP%20binaries/openwrt/openwrt_0.4.0.11/vscp_0.4.0.11-Fluorine_ramips.ipk/download
    opkg install vscp_0.4.0.11-Fluorine_ramips.ipk
    rm vscp_0.4.0.11-Fluorine_ramips.ipk
```

##### Step 13

After this is done the VSCP daemon should run on your board. If you point your browser to 

    http://your-ip/vscp

you should see the internal web pages. Now you can follow the second part of the instructions at [Setup your system on Linux](howto/setup_linux) to understand your system and maybe install the websocket lib and test pages [Websockets guide](howto/howto_start_websockets).
    
    
## Building from source

    src/vscp/daemon/linux/openwrt folder

You need to install some other packages before you install VSCP & Friends. 

##### Step 1

Install the OpenWrt SDK as explained on the [8Devices site](http://8devices.com/wiki_carambola/doku.php/carambola_where_to_start).

For carambola 2 clone 

    https://github.com/8devices/carambola2 
    
instead.  

##### Step 2

```bash
    scripts/feeds install uclibcxx
    scripts/feeds install libwxbase
    scripts/feeds install libgnutls-openssl 
    scripts/feeds install libpcap
    scripts/feeds install libmosquitto
```    

Then issue

    make menuconfig
    
and select the packages.
    
   
#####  Step 2

When this is written the mosquitto makefile have a bug that does not copy the libraries to the stagedir and make the necessary symlinks so replace the one installed by the one in 

    src/vscp/daemon/linux/carambola folder
    
called **Makefile.mosquitto**  

Copy it to

    package/feeds/packages/mosquitto/Makefile
      
#####  Step 3

The Makefile for VSCP & Friends is available in the 

    src/vscp/daemon/linux/carambola
    
folder. Make a folder in package with

    mkdir package/vscp
    
and copy the makefile

    Makefile.vscp 
    
to this folder and change it's name to just **Makefile**  After that issue

    make menuconfig
    
and select vscp in the **utilities** section.


#####  Step 4

Now issue

    make
    
and your system would build with VSCP support.

    
## Related Links

*  Home for the thingi - [https://www.8devices.com](https://www.8devices.com)
*  Using sysupgrade to upgrade firmware - https://8devices.com/wiki_carambola/doku.php/firmware_upgrade:sysupgrade
*  http://lnxpps.de/can2udpe/smallest-rocrail-server-ever/
*  http://lnxpps.de/can2udpe/openwrt/
*  Old VSCP daemon precompiled - http://geomi.org/vscp/carambola/



[filename](./bottom_copyright.md ':include')
