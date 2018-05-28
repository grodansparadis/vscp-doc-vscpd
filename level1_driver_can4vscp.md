# CAN4VSCP Level I Driver

**Available for:** Windows, Linux

**Driver for Windows** vscpl1_can4vscpdrv.dll (install-dir/drivers) 

**Driver for Linux** vscpl1_can4vscpdrv.so (*/usr/local/lib/vscpl1_can4vscpdrv.so*) When using the drive on Linux remember to set rw permissions for the user that the VSCP daemon and VSCP works run under (*chmod a+rw /dev/ttyUSB0* for example).

This is a driver for the low cost **Frankfurt RS-232 module** that us the [VSCP serial protocol](https://grodansparadis.gitbooks.io/the-vscp-specification/content/vscp_over_a_serial_channel_rs-232.html). The Frankfurt RS-232 module is described [here](https://www.grodansparadis.com/can4vscp_rs232/can4vscp_rs232.html) where there also is a description of how to use it with VSCP Works and the VSCP daemon.  

As the VSCP serial protocol is very generic this may also be the driver to use for your own hardware that have a serial port available.

## Parameter String

### Windows

    port[;nBaud]

##### port

The first parameter is the serial port to use (COM1, COM2 and so on). 



### Linux

    device[;nBaud]

##### device

The first parameter is the device to use (// /dev/ttyS0, /dev/ttyS1 or /dev/ttyUSB0, /dev/ttyUSB1 etc // ) etc. 

##### nBaud

This is an optional baudrate code. If not given the dafault 115200 will be used. The following settings are available

 | Baudrate | Code | Error  | Windows | Linux | 
 | :--------: | :----: | :-----:  | :-------: | :-----: | 
 | 115200   | 0    | -1.36% | yes     | yes   | 
 | 128000   | 1    | -2.34% | yes     | no    | 
 | 230400   | 2    | -1.36% | no      | yes   | 
 | 256000   | 3    | -2.34% | yes     | no    | 
 | 460800   | 4    | 8.51%  | no      | no    | 
 | 500000   | 5    | 0%     | yes     | yes   | 
 | 625000   | 6    | 0%     | bad     | no    | 
 | 921600   | 7    | -9.58% | no      | bad   | 
 | 1000000  | 8    | 16.67% | no      | bad   | 
 | 9600     | 9    | 0.16%  | yes     | yes   | 
 | 19200    | 10   | 0,16%  | yes     | yes   | 
 | 38400    | 11   | 0,16%  | yes     | yes   | 
 | 57600    | 12   | 0.94%  | yes     | yes   | 

Tests on Windows and Linux has been done on a Windows 10 machine and on a Ubuntu machine with the USB serial adapter that ship with [Frankfurt RS-232](http://www.grodansparadis.com/frankfurt/rs232/frankfurt-rs232.html).

Typical settings for VSCP daemon config

```xml
    <driver enable="true" >
        <name>can4vscp</name>
        <config>/dev/ttyUSB0</config>
        <path>/usr/local/lib/vscpl1_can4vscpdrv.so</path>
        <flags>0</flags>
        <guid>00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00</guid>
    </driver>
```


## Flags

 | Bits | Usage | 
 | ----  | ----- | 
 | Bit 0,1  | **Open Mode** <br> **0** - normal <br> **1** - Listen mode <br> **2** - Loopback mode <br> **3** - Reserved | 
 | Bit 2    | If set the driver will not switch to VSCP mode. That is it must be in VSCP mode. Open will be faster. | 
 | Bit 3    | If set the driver will wait for an ACK from the physical device for every sent frame. This will slow down sending but make transmission it very secure. | 
 | Bit 4    | Enable timestamp. The timestamp will be written by the hardware instead of the driver. | 
 | Bit 5    | Enable hardware handshake.  | 
 | Bit 6-31 | Reserved.  | 

## Status return

The CanalGetStatus call returns the status structure with the channel_status member having the following meaning:

 | Bit      | Description                      | 
 | ---      | -----------                      | 
 | Bit 0-7  | TX Error Counter.                | 
 | Bit 8-15 | RX Error Counter.                | 
 | Bit 16   | Overflow. Cleard by status read. | 
 | Bit 17   | RX Warning.                      | 
 | Bit 18   | TX Warning.                      | 
 | Bit 19   | TX bus passive.                  | 
 | Bit 20   | RX bus passive.                  | 
 | Bit 21   | Reserved.                        | 
 | Bit 22   | Reserved.                        | 
 | Bit 23   | Reserved.                        | 
 | Bit 24   | Reserved.                        | 
 | Bit 25   | Reserved.                        | 
 | Bit 26   | Reserved.                        | 
 | Bit 27   | Reserved.                        | 
 | Bit 28   | Reserved.                        | 
 | Bit 29   | Bus Passive.                     | 
 | Bit 30   | Bus Warning status.              | 
 | Bit 31   | Bus off status.                  | 

## Serial Protocol

You can find the description of the VSCP serial protocol in the [VSCP specification](http://www.vscp.org/docs/vscpspec/doku.php?id=physical_level_lower_level_protocols#vscp_over_a_serial_channel_rs-232).

{% include "./bottom_copyright.md" %}
