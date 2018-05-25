# CANAL Interface Specification (Level I driver)

{{vscp_logo.jpg?150}} \\ 

The CAN Abstraction Layer\\ 
Version 1.14 (2008-10-28)\\ 
[akhe@grodansparadis.com](mailto/akhe@grodansparadis.com) \\ 
[http://www.vscp.org](http://www.vscp.org) 

\\ \\ \\ \\ 






# What is CANAL

CANAL (CAN Abstraction Layer) is a very simple approach to interfacing a CAN card or some other CAN hardware. It consists mostly of open, close, read, write and filter/mask handling. If you need to do more this is not the model for you and we recommend **CanPie** 

http://sourceforge.net/projects/canpie 

or **VCA** (Virtual CAN API) used in the OCERA project above 

http://www.ocera.org/download/components/WP7/canvca-0.01.html 

which are much more advanced, and capable implementations.

CANAL has been constructed from a need to use CAN in the form of control networks in the SOHO (Small Office/Home) environment. This kind of environment is totally different to the very tough automotive or industry control world where Canal probably would not be the best solution. The goal has not been to construct something that will take over the world just something that does solve a problem at hand. 

For CANAL there is some code available. First of all some drivers and also a daemon/service (VSCP Daemon) that can be used to simulate CAN networks on a PC, over Ethernet/TCP/IP etc. The daemon is available for both Windows and Linux and can be found at http://can.sourceforge.net.

CANAL is tightly coupled with the Very Simple Control Protocol, VSCP and the VSCP daemon. This is a protocol constructed for SOHO control situations. The model has been constructed as a two-layer model so that the VSCP Daemon can also be useful for people that are just  interested in CAN and not in VSCP. You can find more information about vscp at http://www.vscp.org.

CANAL is open and free to use with no restrictions, as is the above software, which is released under GPL/LGPL.

Current information about CANAL, the VSCP Daemon and VSCP (Very Simple Control Protocol) can be found at http://www.vscp.org and http://can.sourceforge.net. There are two mailinglists available on Sourceforge 

https://sourceforge.net/mail/?group_id=53560 

that are about CANAL (can_canal) and VSCP (can_vscp) topics.


*  To subscribe to the canal list go to [http://lists.sourceforge.net/lists/listinfo/can-canal](http://lists.sourceforge.net/lists/listinfo/can-canal)

*  To subscribe to the VSCP list go to [http://lists.sourceforge.net/lists/listinfo/m2m-development](http://lists.sourceforge.net/lists/listinfo/m2m-development)


# CANAL-API Specification





## long CanalOpen( const char *pConfigStr, unsigned long flags )

Opens a CAN channel.

### Params

####  pDevice
Physical device to connect to. This is the place to add device specific parameters and filters/masks. This is a text string. It can be a name, some parameters or whatever the interface creator chooses.
#### flags

Device specific flags with a meaning defined by the interface creator.



### Returns

Handle for open physical interface or < = 0 on error. 
For an interface where there is only one channel the handle has no special meaning and can only be looked upon as a status return parameter.




## int CanalClose( long handle  )

Close the channel and free all allocated resources associated with the channel.

### Params

handle – Handle for open physical interface.

### Returns

TRUE on success or FALSE if failure.





## unsigned long CanalGetLevel( long handle  )

### Params

handle – Handle for open physical interface.


### Returns

Returns the canal level this interface can handle.  An error is indicated by a zero return value. At the moment the following levels are defined

 | CANAL_LEVEL_STANDARD   | A starndard CANAL driver as of this specification.                                                                                                                                                                                                                                                                                                                                                                                          | 
 | --------------------   | --------------------------------------------------                                                                                                                                                                                                                                                                                                                                                                                          | 
 | CANAL_LEVEL_USES_TCPIP | This driver does not respond to any of the methods, even if they must be implemented. The driver will instead use the TCP/IP interface of the VSCP daemon for its data transfer. This driver type is called a VSCP Level II driver because it is constructed to work just with VSCP Level II events which does not fit in standard CAN frames. This type of driver does not need any buffers as no data is exchanged through the interface. | 






## int CanalSend( long handle, const PCANALMSG pCanMsg  )



### Params

*  handle – Handle for open physical interface.

*  pCanMsg – Message to send.

### Returns

CANAL_ERROR_SUCCESS on success or an error code on failure.







## int CanalBlockingSend( long handle, const PCANALMSG pCanMsg, unsigned long timeout  )


### Params

*  handle – Handle for open physical interface.

*  pCanMsg – Message to send.

*  timeout - Timeout in milliseconds. 0 to wait forever.


### Returns

CANAL_ERROR_SUCCESS, CANAL_ERROR_TIMEOUT on timeout on success or an error code on failure.





## int CanalReceive( long handle,  PCANALMSG pCanMsg  )


### Params

*  handle – Handle for open physical interface.

*  pCanMsg – Received message.
### Returns

CANAL_ERROR_SUCCESS on success or an error code on failure.

:!: Note that if bit 2 in flags of the CANAL message is set and error status message is returned from the adapter. 



## int CanalBlockingReceive( long handle,  PCANALMSG pCanMsg, unsigned long timeout  )


### Params

*  handle – Handle for open physical interface.

*  pCanMsg – Received message.

*  timout - Timeout in milliseconds. 0 to wait forever.


### Returns

CANAL_ERROR_SUCCESS on success, CANAL_ERROR_TIMEOUT on timeout or an error code on failure.

:!: Note that if bit 2 in flags of the CANAL message is set and error status message is returned from the adapter. 





## int CanalDataAvailable( long handle  )

Check if there is data available in the input queue for this channel that can be fetched with CanalReceive.

### Params

handle – Handle for open physical interface.

### Returns

Number of frames available to read.





## int CanalGetStatus( long handle,  PCANALSTATUS pCanStatus  )

Returns a structure that gives some information about the state of the channel.  How the information is interpreted is up to the interface designer. Typical use is for extended error information.


### Params

*  handle – Handle for open physical interface.

*  pCanStatus – Status.

### Returns

CANAL_ERROR_SUCCESS on success or an error code on failure.




## int CanalGetStatistics ( long handle,  PCANALSTATISTICS pCanalStatistics  )

Return some statistics about the interface. If not implemented for an interface FALSE should always be returned.


### Params

*  handle – Handle for open physical interface.

*  pCanalStatistics – Statistics for the interface.

### Returns

CANAL_ERROR_SUCCESS on success or an error code on failure.




## int CanalSetFilter ( long handle, unsigned long filter  )

Set the filter for a channel. There is only one filter available. The CanalOpen call can be used to set multiple filters.  If not implemented FALSE should always be returned.

Enable filter settings in the open call if possible. If available in the open method this method can be left unimplemented returning false.

### Params

handle – Handle for open physical interface.
filter – filter for the interface.

### Returns

CANAL_ERROR_SUCCESS on success or an error code on failure.




## int CanalSetMask ( long handle, unsigned long mask  )

Set the mask for a channel. There is only one mask available for a channel. The CanalOpen call can be used to set multiple masks.  If not implemented FALSE should always be returned.

Enable mask settings in the open call if possible. If available in the open method this method can be left unimplemented returning false.

### Params

handle – Handle for open physical interface.
mask – filter for the interface.

### Returns

CANAL_ERROR_SUCCESS on success or an error code on failure.




## int CanalSetBaudrate ( long handle, unsigned long baudrate  )

Set the bus speed for a channel. The CanalOpen call may be a better place to do this.  If not implemented FALSE should always be returned.

Enable baudrate settings in the open call if possible. If available in the open method this method can be left unimplemented returning false.

### Params

handle – Handle for open physical interface.
baudrate – The bus speed for the interface.

### Returns

CANAL_ERROR_SUCCESS on success or an error code on failure.




## unsigned long CanalGetVersion ( void  )

Get the Canal version. This is the version derived from the document that has been used to implement the interface.  Version is located on the front page of the document.

### Returns

Canal version expressed as an unsigned long.

## unsigned long CanalGetDllVersion ( void  )

Get the version of the interface implementation. This is the version of the code designed to implement Canal for some specific hardware.

### Returns

Canal dll version expressed as an unsigned long.





## const char * CanalGetVendorString ( void  )

Get a pointer to a null terminated vendor string for the maker of the interface implementation. This is a string that identifies the constructor of the interface implementation and can hold copyright and other valid information.

### Returns

Pointer to a vendor string.








## const char *  CanalGetDriverInfo( void )

This call returns a documentation object in XML form of the configuration string for the driver. This string and the flags setting and  can be used to help users to enter the configuration data in an application which allows for this.

The configuration string locks like

    pos0;pos1;pos2;pos3;pos4;....

that is items separated with semicolons. The **pos** attribute for the `<item>` tag is the ordinal for these. Always starting with base zero.

All items are sub strings when they are part of the configuration string but can be typed withing the `<item>` tag with the **type** attribute. Valid types are

 | Type        | Description                                                                              | 
 | ----        | -----------                                                                              | 
 | **string**  | The should be interpreted as a sting                                                     | 
 | **boolean** | The item should be interpreted as a boolean. Valid values are TRUE, FALSE, 0, 1          | 
 | **int32**   | A signed integer. The attributes **max** and **min** can be used to specify limits       | 
 | **uint32**  | An unsigned integer. The attributes **max** and **min** can be used to specify limits    | 
 | **float**   | A floating point value. The attributes **max** and **min** can be used to specify limits | 
 | **choice**  | Specify a list with choices that can be set                                              | 

The **optional** attribute tells if an item is optional. If set on a pos all items on positions after it must also be optional.

The `<flags>` tag describe the bits in the flags value. It should have a `<bit>` tag for each bit in the flags that have a meaning. The **width** attribute can be used to tell the width for a configurable item and in that case the bits affected are the bits from the value in **pos** to **pos+width**. Width defaults to one as expected.

	:::xml
	`<?xml version = "1.0" encoding = "UTF-8" ?>`
	 
	`<!-- Version 2.0   2015-10-13   -->`
	
	`<!-- Configuration strings are given as a semicolon separated list          -->`
	`<!-- This list is described with and item tag for each configuration option -->`
	`<!-- Items can be of different types, string, number                        -->`
	`<config>`
	   `<description format="text|html">`Description of the driver`<description>`
	   `<level>`1|2`</level>` `<!-- Is 1 for a level I driver and 2 for a level II driver -->`
	   `<blocking>`yes|no`</blocking>`
	   `<infourl>`path to url with info about this item`</infourl>`
	   <!-- pos is the position on the configuration line i.e.
	             item0;item1;item2;item3;item4.....
	   --> 
	   `<items>`
	       `<item pos="nn"  optional="true|false" type="string" description="Description about this item" infourl=path to url with info about this item"/>`
	       `<item pos="nn"  optional="true|false" type="number" min="min-value" max="max-value" infourl=path to url with info about this item" />`
	       `<item pos="nn"  optional="true|false" type="choice" infourl=path to url with info about this item" >`
	           `<choice value="0" description = "First choice" />`
	           `<choice value="0" description = "Second choice" />`
	           `<choice value="0" description = ".............." />`
	           `<choice value="0" description = "Last choice" />`
	       `</item>`
	   `</items>`
	  
	   `<flags>`
	       `<bit pos="0" width="2" type="choice" description="" infourl="" >`
	           `<choice value="0" description="First choice." />`
	           `<choice value="1" description="Second choice." />`
	           `<choice value="2" description="Third choice." />`
	           `<choice value="3" description="Fourth choice." />`
	       `<bit>`
	       `<bit pos="2" width="1" type="bool" description="" infourl="" >`
	       `<bit pos="3" width="3" type="number" description="" infourl="" >`
	    `</flags>`
	   
	`</config>`
	


A real world example (the [can4vscp driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_can4vscp) looks like this.

```xml
`<?xml version = "1.0" encoding = "UTF-8" ?>`
`<config>`
    `<description>`CAN4VSCP standard serial driver`</description>`
    `<level>`1`</level>`
    `<blocking>`yes`</blocking>`
    `<infourl>`http://www.grodansparadis.com/frankfurt/rs232/manual/doku.php?id=the_can4vscp_mode`</infourl>`
    `<items>`
        <item pos="0" 
                type="string" 
                description="Serial port (COM1, COM2...)"
                infourl="http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_can4vscp#parameter_string" />
        <item pos="1" 
                type="choice" 
                optional="true" 
                description="Baudrate to use for communication with the adapter.Default is 115200 baud. " 
                infourl="http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_can4vscp#parameter_string" >
            `<choice value="0" description = "115200 baud" />`
            `<choice value="1" description = "128000 baud" />`
            `<choice value="3" description = "230400 baud" />`
            `<choice value="4" description = "256000 baud" />`
            `<choice value="5" description = "460800 baud" />`
            `<choice value="6" description = "500000 baud" />`
            `<choice value="7" description = "625000 baud" />`
            `<choice value="8" description = "921600 baud" />`
            `<choice value="9" description = "1000000 baud" />`
            `<choice value="0" description = "9600 baud" />`
            `<choice value="10" description = "19200 baud" />`
            `<choice value="11" description = "38400 baud" />`
            `<choice value="12" description = "57600 baud" />`
        `</item>`
    `</items>`    
	
    `<flags>`
        `<bit pos="0" width="2" type="choice" description="Select the mode the device should be opened in. The normal mode opens the interface for receive and transmit. The listen mode only listen on traffic on the bus. Loopback just connect the receive and transmit lines without sending anything on the bus. The manual describes the modes in detail." infourl="http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_can4vscp#flags" >`
            `<choice value="0" description="Open CAN4VSCP interface in normal mode." />`
            `<choice value="1" description="Open CAN4VSCP interface in listen mode." />`
            `<choice value="2" description="Open CAN4VSCP interface in loopback mode." />`
        `</bit>`
        `<bit pos="2" width="1" type="bool" description="If this flag is set the driver will not switch to VSCP mode. This means it already must be in VSCP mode. The advantage is that the open operation will be faster." infourl="http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_can4vscp#flags" />`
        `<bit pos="3" width="1" type="bool" description="If this flag is set the driver will wait for an ACK from the physical device for every sent frame. This will slow down sending but make transmission very secure." infourl="http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_can4vscp#flags" />`
        `<bit pos="4" width="1" type="bool" description="If this flag is set it enable timestamps in hardware meaning the timestamp will be written by the hardware instead of by the driver. The disadvantage is that it consumes bandwidth." infourl="http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_can4vscp#flags" />`
        `<bit pos="5" width="1" type="bool" description="If this flag is set enable hardware handshake. Recommended for lower baudrates to prevent buffer overflows." infourl="http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_can4vscp#flags" />`
    `</flags>`
`</config>`
```
### Returns

Pointer to a configuration string or NULL if no configuration string is available.


### Params

*  handle – Handle for open physical interface.

*  pDriverInfo – Pointer to unsigned long that holds driver information after call. \\ **Bit 31** - Driver support blocking calls. \\ all other bits undefined at the moment.


### Returns

CANAL_ERROR_SUCCESS on success or an error code on failure.


# CANAL - Data Structures


## CANMSG

This is the general message structure



### unsigned long flags

Flags for the package.


*  Bit 0 – if set indicates that an extended identifier (29-bit id) else standard identifier (11-bit) is used.

*  Bit 1 – If set indicates a RTR (Remote Transfer) frame.

*  Bit 2 – If set indicates that this is an error package. The data byts holds the error information. id is set to zero. For format see CANAL_IDFLAG_STATUS below. 

*  Bit 3 – Bit 30 Reserved.

*  Bit 31 – This bit can be used as a direction indicator for application software. 0 is receive and 1 is transmit.
 

### unsigned long obid

Used by the driver or higher layer protocols.

### unsigned long id

The 11-bit or 29 bit message id.

### unsigned char data[8]

Eight bytes of data.

### unsigned char count

Number of data bytes 0-8

### unsigned long timestamp

A time stamp on the message from the driver or the interface expressed in microseconds. Can be used for relative time measurements.

## CANALSTATUS




### unsigned long channel_status

Current state for CAN channel

    CANAL_STATUS_NONE                 0x00000000
    CANAL_STATUS_BUS_OFF              0x80000000
    CANAL_STATUS_BUS_WARN             0x40000000
    CANAL_STATUS_PASSIVE              0x20000000
    CANAL_STATUS_ACTIVE               0x10000000
    CANAL_STATUS_PHY_FAULT            0x08000000
    CANAL_STATUS_PHY_H                0x04000000
    CANAL_STATUS_PHY_L                0x02000000
    CANAL_STATUS_SLEEPING             0x01000000
    CANAL_STATUS_STOPPED              0x00800000
    CANAL_STATUS_RECEIVE_FIFO_FULL    0x00400000
    CANAL_STATUS_TRANSMIT_FIFO_FULL   0x00200000
    
    

Bits from 16-31 are reserved, bits from 0-15 are user defined and can be defined by the driver maker.

## PCANALSTATISTICS 

This is the general statistics structure

### unsigned long cntReceiveFrames

Number of received frames since the channel was opened.

### unsigned long cntTransmittFrames

Number of frames transmitted since the channel was opened.

### unsigned long cntReceiveData

Number of bytes received since the channel was opened.

### unsigned long cntTransmittData

Number of bytes transmitted since the channel was opened.

### unsigned long cntOverruns

Number of overruns since the channel was opened.

### unsigned long cntBusWarnings

Number of bus warnings since the channel was opened.

### unsigned long cntBusOff

Number of bus off’s since the channel was opened.








#  Error codes

 | Error                         | Error code | Description                             | 
 | -----                         | ---------- | -----------                             | 
 | CANAL_ERROR_SUCCESS           | 0          | All is OK.                              | 
 | CANAL_ERROR_BAUDRATE          | 1          | Baudrate error.                         | 
 | CANAL_ERROR_BUS_OFF           | 2          | Bus off error                           | 
 | CANAL_ERROR_BUS_PASSIVE       | 3          | Bus Passive error                       | 
 | CANAL_ERROR_BUS_WARNING       | 4          | Bus warning error                       | 
 | CANAL_ERROR_CAN_ID            | 5          | Invalid CAN ID                          | 
 | CANAL_ERROR_CAN_MESSAGE       | 6          | Invalid CAN message                     | 
 | CANAL_ERROR_CHANNEL           | 7          | Invalid channel                         | 
 | CANAL_ERROR_FIFO_EMPTY        | 8          | Noting available to read. FIFO is empty | 
 | CANAL_ERROR_FIFO_FULL         | 9          | FIFO is full                            | 
 | CANAL_ERROR_FIFO_SIZE         | 10         | FIFO size error                         | 
 | CANAL_ERROR_FIFO_WAIT         | 11         |                                         | 
 | CANAL_ERROR_GENERIC           | 12         | Generic error                           | 
 | CANAL_ERROR_HARDWARE          | 13         | A hardware related fault.               | 
 | CANAL_ERROR_INIT_FAIL         | 14         | Initialization failed.                  | 
 | CANAL_ERROR_INIT_MISSING      | 15         |                                         | 
 | CANAL_ERROR_INIT_READY        | 16         |                                         | 
 | CANAL_ERROR_NOT_SUPPORTED     | 17         | Not supported.                          | 
 | CANAL_ERROR_OVERRUN           | 18         | Overrun.                                | 
 | CANAL_ERROR_RCV_EMPTY         | 19         | Receive buffer empty                    | 
 | CANAL_ERROR_REGISTER          | 20         | Register value error                    | 
 | CANAL_ERROR_TRM_FULL          | 21         |                                         | 
 | CANAL_ERROR_ERRFRM_STUFF      | 22         | Errorframe: stuff error detected        | 
 | CANAL_ERROR_ERRFRM_FORM       | 23         | Errorframe: form error detected         | 
 | CANAL_ERROR_ERRFRM_ACK        | 24         | Errorframe: acknowledge error           | 
 | CANAL_ERROR_ERRFRM_BIT1       | 25         | Errorframe: bit 1 error                 | 
 | CANAL_ERROR_ERRFRM_BIT0       | 26         | Errorframe: bit 0 error                 | 
 | CANAL_ERROR_ERRFRM_CRC        | 27         | Errorframe: CRC error                   | 
 | CANAL_ERROR_LIBRARY           | 28         | Unable to load library                  | 
 | CANAL_ERROR_PROCADDRESS       | 29         | Unable get library proc address         | 
 | CANAL_ERROR_ONLY_ONE_INSTANCE | 30         | Only one instance allowed               | 
 | CANAL_ERROR_SUB_DRIVER        | 31         | Problem with sub driver call            | 
 | CANAL_ERROR_TIMEOUT           | 32         | Blocking call timeout                   | 
 | CANAL_ERROR_NOT_OPEN          | 33         | The device is not open.                 | 
 | CANAL_ERROR_PARAMETER         | 34         | A parameter is invalid.                 | 
 | CANAL_ERROR_MEMORY            | 35         | Memory exhausted.                       | 
 | CANAL_ERROR_INTERNAL          | 36         | Some kind of internal program error     | 
 | CANAL_ERROR_COMMUNICATION     | 37         | Some kind of communication error        | 

Codes up to  0xffff are reserved, codes from 0x10000  and up are user defined.



# Message ID Flags

Each message has some flags set to give information about the events. The flags are defined as follow

 | Flag                  | Value      | Description                                                       | 
 | ----                  | -----      | -----------                                                       | 
 | CANAL_IDFLAG_STANDARD | 0x00000000 | Standard message id (11-bit)                                      | 
 | CANAL_IDFLAG_EXTENDED | 0x00000001 | Extended message id (29-bit)                                      | 
 | CANAL_IDFLAG_RTR      | 0x00000002 | RTR-Frame                                                         | 
 | CANAL_IDFLAG_STATUS   | 0x00000004 | This package is an error indication (data holds error code,id=0). | 
 | CANAL_IDFLAG_SEND     | 0x80000000 | Reserved for use by application software to indicate send.        | 

**CANAL_IDFLAG_SEND** may seam strange but can be very useful for software to use as a way to distinguish between sent and received frames.

CANAL_IDFLAG_STATUS can be used by CAN controllers to report status data back to a host or an application. At the moment  the following error codes are defined. All status events consist of four data bytes where the first byte tell the status code, the second is the receive error counter, the third the transmit error counter and the fourth byte is reserved and should be set to zero. 

 | Flag                     | Value | Description                                                                         | 
 | ----                     | ----- | -----------                                                                         | 
 | CANAL_STATUSMSG_OK       | 0x00  | Normal condition.                                                                   | 
 | CANAL_STATUSMSG_OVERRUN  | 0x01  | Overrun occured when sending data to CAN bus.                                       | 
 | CANAL_STATUSMSG_BUSLIGHT | 0x02  | Error counter has reached 96.                                                       | 
 | CANAL_STATUSMSG_BUSHEAVY | 0x03  | Error counter has reached 128.                                                      | 
 | CANAL_STATUSMSG_BUSOFF   | 0x04  | Device is in BUSOFF. CANAL_STATUSMSG_OK is sent when returning to operational mode. | 
 | CANAL_STATUSMSG_STUFF    | 0x20  | Stuff Error.                                                                        | 
 | CANAL_STATUSMSG_FORM     | 0x21  | Form Error.                                                                         | 
 | CANAL_STATUSMSG_ACK      | 0x23  | Ack Error.                                                                          | 
 | CANAL_STATUSMSG_BIT0     | 0x24  | Bit1 Error.                                                                         | 
 | CANAL_STATUSMSG_BIT1     | 0x25  | Bit0 Error.                                                                         | 
 | CANAL_STATUSMSG_CRC      | 0x26  | CRC Error.                                                                          | 

# History

*  2015-10-19 - Added some more info to CanalGetDriverInfo 

*  2008-10-28 - Fixed error in status flags. Clarified error status return. 

*  2008-04-15 - Added Message ID flags description. CANAL_IDFLAG_ERROR changed to CANAL_IDFLAG_STATUS

*  2008-04-04 - Driver description format final.

*  2007-12-08 - CanalGetDriverInfo does not need a handle.

*  2007-11-22 - CANAL_ERROR_INTERNAL and CANAL_ERROR_COMMUNICATION added.

*  2007-11-13 - getDriverConfigInfo added.

*  2007-11-12 - added const in front of send messages.

*  2007-11-01 - CANAL_LEVEL_USES_TCPIP CANAL driver Level introduced for use with the VSCP Daemon.

*  2007-10-30 - CanalGetDriverInfo call added.

*  2007-05-13 - CanalOpen device set to const char * instead of incorrect char *

*  2007-03-06 - CANALSTATUS table was wrong. Corrected.

*  2007-01-14 - Handle changed from int to long.

*  2005-07-26 - CanalBlockingOpen call removed. CanalBlockingSend and CanalBlockingReceive added. Fixed returned values that where wrong.

*  2005-03-17 - CanalBlockingOpen call added.

*  2004-07-08 – Bit 31 of the canmsg flag defined as direction bit for application software use.

*  2004-07-01 – Added some clarifications on the CanalSetMask, CanalSetFilter and 	CanalSetBaudrate methods

*  2004-06-07 – CANALASTATUS had a typo and was called CANALSTATE. Fixed. 

*  2004-06-07 – Recovery from version lost in hard disk crash and realest as version 1.00

*  2003-02-18 – Initial version. 

\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
