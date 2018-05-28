# Installing moquitto for use with VSCP

[The VSCP Level II MQTT Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level2_driver_mqtt) can not, as most other packages, work with the old mosquitto library that you can find on most Debian systems including Raspberry Pi. 



**Currently the simplest step is to compile the package yourself so skip to that step. Otherwise follow the steps below.**
## Step 1

To find out if you have the latest Mosquitto library installed issue

    ls -la /usr/lib libmosquitto*

If you have nothing here go to step 2. If you you get  

    lrwxrwxrwx 1 root root    19 May 14 17:03 /usr/lib/libmosquittopp.so -> libmosquittopp.so.1
 1. rw-r--r-- 1 root root  8576 Jan  9  2013 /usr/lib/libmosquittopp.so.0
 2. rw-r--r-- 1 root root 20972 Jan  9  2013 /usr/lib/libmosquitto.so.0
 3. rw-r--r-- 1 root root 47008 May  7 23:50 /usr/lib/libmosquitto.so.1

you are alright and everything is OK. No need to continue here.

If you see

    libmosquitto.so.1

but not

    /usr/lib/libmosquittopp.so -> libmosquittopp.so.1
    
do

    cd /usr/lib
    ln -s libmosquittopp.so.1 libmosquittopp.so  

and you are ready to continue.

If you see 

    lrwxrwxrwx 1 root root    19 Dec 29  2012 libmosquittopp.so -> libmosquittopp.so.0
 1. rw-r--r-- 1 root root 10620 Dec 29  2012 libmosquittopp.so.0
 2. rw-r--r-- 1 root root 18016 May  7 16:46 libmosquittopp.so.1
 3. rw-r--r-- 1 root root 28656 Dec 29  2012 libmosquitto.so.0

or nothing continue with next step.

## Step 2

First follow the instructions [here](http://mosquitto.org/2013/01/mosquitto-debian-repository/). Works for Raspoberry Pi to (wheezy). A short list follow here form the link which can be outdated so **follow the link**

    wget http://repo.mosquitto.org/debian/mosquitto-repo.gpg.key
    sudo apt-key add mosquitto-repo.gpg.key
    cd /etc/apt/sources.list.d/

    sudo wget http://repo.mosquitto.org/debian/mosquitto-wheezy.list

or

    sudo wget http://repo.mosquitto.org/debian/mosquitto-jessie.list

    apt-get update

## Step 3

The logical step now would be to install the 

    libmosquitto1 - MQTT version 3.1 client library

you can get a list of Mosquitto packages with

    apt-cache search libmosquitto

but it will conflict with the old lib. 

The good thing is that the mosquitto programs themself use the new lib so if you issue

    apt-get install mosquitto mosquitto-clients

you will also get the lib. So after this install you will find the correct version of  the lib (libmosquittopp.so.1) in /usr/lib and you only need to fix the symlink with

    cd /usr/lib
    rm libmosquittopp.so
    ln -s libmosquittopp.so.1 libmosquittopp.so

## Compile the library yourself

You can compile the library yourself to always have the latest version. When this is written 1.4 is the latest but check your self [here](http://mosquitto.org/files/source).

First install some required libraries

    apt-get install uuid-dev
    apt-get install apt-get install libc-ares-dev

Then fetch the source

    wget http://mosquitto.org/files/source/mosquitto-1.4.tar.gz
    tar -zxvf mosquitto-1.4.tar.gz
    cd mosquitto-1.4
    make
    make install

Default install location is  /usr/local/lib

The installation only affect the build of the MQTT driver so if you don't need that driver you can skip this step. 




\\ 
----
Copyright (c) 2000-2015 [Åke Hedman](mailto/akhe@grodansparadis.com), [Paradise of the Frog / Grodans Paradis AB](http://www.grodansparadis.com)


