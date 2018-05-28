# TCP/IP Link interface protocol description

## Port

Default Port for the tcp/ip interface is 9598 but the interface can be available on several port and several interfaces on a specific hardware.

## Command and response format

The VSCP TCP protocol is very much like the POP3 protocol.

*  A command is sent (ending with CRLF)

*  A response line is received starting with either ”**+OK**” for success or ”**-OK**” for failure. The initial “token” is followed by some descriptive text that is separated from the initial token with “ - “ (a dash with a space on it's both sides).

For some commands there can be data in between the two lines. For instance the “**VERS**” command looks like this

    send: 'VERS<CR><LF> 
    received line 1: '1,0,0<CR><LF> 
    received line 2: '+OK - <CR><LF>

## VSCP Link Interfaces (VSCP-LI)

The daemon interface can be visible also on lower end (typically TC/IP) nodes. A subset of the commands are required to be available on such a node. Commands marked with yes in the link column below are the ones that a link node must have. All others are not mandatory on this type of nodes. 

## List of available commands

 | Command  | Privilege | Link | From version | Description  | 
 | -------  | :---------: | :----: | :------------: | -----------  | 
 | +        | 0         | yes  | 0.0.2        | Repeat the last command  | 
 | [NOOP](./tcp_ip_protocol_description.md#noop_-_no_operation)                                                                                                  | 0         | yes  | 0.0.1        | No operation.                                                                                      | 
 | [HELP](./tcp_ip_protocol_description.md#help_-_give_help)                                                                                                     | 0         | no   | 0.0.2        | Give command help.                                                                                 | 
 | [QUIT](./tcp_ip_protocol_description.md#quit_-_close_the_connection)                                                                                          | 0         | yes  | 0.0.1        | Close the connection.                                                                              | 
 | [USER](./tcp_ip_protocol_description.md#user_-_username_for_login)                                                                                            | 0         | yes  | 0.0.1        | Username for login.                                                                                | 
 | [PASS](./tcp_ip_protocol_description.md#pass_-_password_for_login)                                                                                            | 0         | yes  | 0.0.1        | Password for login.                                                                                | 
 | [CHALLENGE](./tcp_ip_protocol_description.md#challenge_-_get_challenge_session_id)                                                                            | 0         | yes  | 1.12.14.4    | Get session id.                                                                                    | 
 | [SEND](./tcp_ip_protocol_description.md#send_-_send_an_event)                                                                                                 | 4         | yes  | 0.0.1        | Send an event.                                                                                     | 
 | [RETR](./tcp_ip_protocol_description.md#retr_-_retrieve_one_or_several_event_s)                                                                               | 2         | yes  | 0.0.1        | Retrieve one or several event(s).                                                                  | 
 | [RCVLOOP](./tcp_ip_protocol_description.md#rcvloop_-_send_events_to_client_as_soon_as_they_arrive) | 2         | yes  | 0.0.2        | Will retrieve events in an endless loop until the connection is closed by the client.  | 
 | [QUITLOOP](./tcp_ip_protocol_description.md#quitloop_-_quit_receiving_loop)                                                                                   | 2         | yes  | 0.4.29       | Terminate RCVLOOP                                                                                  | 
 | [CDTA/CHKDATA](./tcp_ip_protocol_description.md#cdta_chkdata_-_check_if_there_are_events_to_retrieve) ((Both versions of the command should be supported))    | 1         | yes  | 0.0.1        | Check if there are events to retrieve.                                                             | 
 | [CLRA/CLRALL](./tcp_ip_protocol_description.md#clra_clrall_-_clear_all_events_in_in-queue) ((Both versions of the command should be supported))               | 1         | yes  | 0.0.1        | Clear all events in in-queue.                                                                      | 
 | [STAT](./tcp_ip_protocol_description.md#stat_-_get_statistics_information)                                                                                    | 1         | yes  | 0.0.1        | Get statistics information.                                                                        | 
 | [INFO](./tcp_ip_protocol_description.md#info_-_get_status_information)                                                                                        | 1         | yes  | 0.0.1        | Get status information.                                                                            | 
 | [CHID/GETCHID](./tcp_ip_protocol_description.md#chid_-_get_channel_id) ((Both versions of the command should be supported))                                   | 1         | yes  | 0.0.1        | Get channel ID.                                                                                    | 
 | [SGID/SETGUID](./tcp_ip_protocol_description.md#sgid_setguid_-_set_guid_for_channel) ((Both versions of the command should be supported))                     | 6         | yes  | 0.0.1        | Set GUID for channel.                                                                              | 
 | [GGID/GETGUID](./tcp_ip_protocol_description.md#ggid_getguid_-_get_guid_for_channel) ((Both versions of the command should be supported))                     | 1         | yes  | 0.0.1        | Get GUID for channel.                                                                              | 
 | [VERS/VERSION](./tcp_ip_protocol_description.md#vers_version_-_get_vscp_daemon_version) ((Both versions of the command should be supported))                  | 0         | yes  | 0.0.1        | Get CANAL/VSCP daemon version.                                                                     | 
 | [SFLT/SETFILTER](./tcp_ip_protocol_description.md#sflt_setfilter_-_set_incoming_event_filter) ((Both versions of the command should be supported))            | 6         | yes  | 0.0.1        | Set incoming event filter.                                                                         | 
 | [SMSK/SETMASK](./tcp_ip_protocol_description.md#smsk_setmask_-_set_incoming_event_mask)                                                                       | 6         | yes  | 0.0.1        | Set incoming event mask.  | 
 | TEST | 15        | no   | 0.0.2        | Do test sequence. Only used for debugging.                                                         | 
 | [SHUTDOWN](./tcp_ip_protocol_description.md#shutdown)                                                                                                         | 15        | no   | 0.0.2        | Shutdown the daemon.                                                                               | 
 | [RESTART](./tcp_ip_protocol_description.md#restart)                                                                                                           | 15        | no   | 0.0.2        | Restart the daemon.                                                                                | 
 | [DRIVER](./tcp_ip_protocol_description.md#driver)                                                                                                             | 15        | no   | 0.0.2        | Driver manipulation.  Have secondary commands.                                                     | 
 | [FILE](./tcp_ip_protocol_description.md#file)                                                                                                                 | 15        | no   | 0.0.2        | File handling. Have secondary commands.                                                            | 
 | [UDP](./tcp_ip_protocol_description.md#udp)                                                                                                                   | 15        | no   | 0.0.2        | UDP handling.                                                                                      | 
 | [REMOTE](./tcp_ip_protocol_description.md#remote)                                                                                                             | 15        | no   | 0.0.2        | User manipulation.                                                                                 | 
 | [INTERFACE](./tcp_ip_protocol_description.md#interface)                                                                                                       | 15        | no   | 0.0.2        | Interface manipulation. Have secondary commands.                                                   | 
 | [DM](./tcp_ip_protocol_description.md#dm)                                                                                                                     | 15        | yes  | 0.0.2        | Decision Matrix manipulation. Have secondary commands.                                             | 
 | [VAR](./tcp_ip_protocol_description.md#var)                                                                                                                   | 4         | yes  | 0.2.9        | Variable handling.(Changed from "VARIABLE" to "VAR" in version 1.12.14.6) Have secondary commands. | 
 | [TABLE](./tcp_ip_protocol_description.md#table)                                                                                                               | 4         | no   | 0.4.29       | Table handling.  Have secondary commands.                                                          | 
 | [WCYD/WHATCANYOUDO](./tcp_ip_protocol_description.md#whatcanyoudo_-_ask_the_capabilities_of_this_server) ((Both versions of the command should be supported)) | 0         | yes  | 0.4.29       | Request what this sever can do                                                                     | 

## NOOP - No operation

 This operation does nothing. It just replies with ”**+OK**”.

##  QUIT - Close the connection

Close the connection to the host. 


##  HELP - Give help

'HELP' alone givs help about all commands. 'HELP command" gives command specific help.

## USER - Username for login.

Used to enter username for a password protected server.

Used on the following form:

    USER username<CR><LF>

## PASS - Password for login

Used to enter username for a password protected server.

Used on the following form:

    PASS password<CR><LF>

## CHALLENGE - Get challenge session id

Used to get a session unique id

Used on the following form:

    CHALLENGE password<CR><LF>

and give a response such as

    +OK - e14712fa9d6a62ff388a701848e24a32

where "e14712fa9d6a62ff388a701848e24a32" is the 32 byte sid.

## RESTART

Restart the daemon. Must have highest privilege to be able to do this. 

##  SHUTDOWN

shutdown the daemon. Must have highest privilege to be able to do this. 

## SEND - Send an event.

Used on the following form:

    send head,class,type,obid,datetime,timestamp,GUID,data1,data2,data3....
or
    send $variablename  
    

**Important note** datetime is introduced in version *1.12.20.0*

The GUID is given on the form MSB-byte:MSB-byte-1:MSB-byte-2……. The GUID can also be given as ”-” in which case the GUID of the interface is used for the event. This GUID is constructed from the Ethernet MAC address and some other parameters to be globally unique.

**datetime** is UTC date time (Coordinated Universal Time) on ISO format 
    YYYY-MM-DDTHH:MM:DD
Can be empty left empty and in that case the current UTC date/time is set by the system.

If timestamp is a relative time in microseconds. It can be empty in which case a timestamp will be set by the system. Before version *1.12.20.0* a timestamp of zero would be replaced by a system set timestamp this is not the case anymore. 

Note: obid is just a place holder here to have a similar line as the receive command and is used internally by the daemon as an interface index. The value you use will always be overwritten by the daemon. head is currently not used.

CLASS=512 - CLASS=1023 is treated in a special way by the daemon. If you use the interface GUID as the first sixteen data bytes the event will only be set through that interface. This is the correct way to send a Level I event through the daemon. You can send Level I events without the GUID also but in that case the event will be sent out on all interfaces and as each interface can have nodes with this nickname all will be affected.

The variable send form makes it possible to send the content in a variable that is of type event. In this case give the name of the variable as argument preceded with a dollar ('$') sign.

**head** is defined as 
    bit 7,6,5 priority => Priority 0-7 where 0 is highest.
    bit 4 = hard coded, true for a hard coded device.
    bit 3 = Don't calculate CRC, Set to zero to use CRC.
    bit 2 = Undefined.
    bit 1 = Undefined.
    bit 0 = Undefined.

**Example:**
Send a full GUID event

    send 0,20,3,,,,0:1:2:3:4:5:6:7:8:9:10:11:12:13:14:15,0,1,35<CR><LF>

Send Event. The example is the same as above but the GUID of the interface will be used.

    send 0,20,3,,,,-,0,1,35<CR><LF> 
    
Send event with UTC time set

    send 0,20,3,,2001-11-02T18:00:01,,-,0,1,35<CR><LF>  

Both send the [CLASS1.INFORMATION TYPE=3 ON event](https://grodansparadis.gitbooks.io/the-vscp-specification/content/class1.information.html), for zone=1, sub-zone=35

**Send event to specific interface**
It is possible to send Level I events to a specific interface. To do this use the Level II mirror Level I events ( Class=512-1023 VSCP Level II Level I events - CLASS2.LEVELI). This is events with class equal to 512 - 1023 which mirrors the Level I events but have the destination GUID in data bytes 0-15. Thees data-bytes is set to the interface (14 upper bits) and the node-ID for the node one wants to communicate with is in GUID[0]. This event will be sent to the correct interface.

So the above example would be

    send 0,20,3,,,0,-,15,14,13,12,11,10,9,8,7,6,5,4,3,2,0,0,1,35<CR><LF>

where class becomes *532* (512 + 20) and where *15,14,13,12,11,10,9,8,7,6,5,4,3,2,0,0* is the interface the events should be routed to. Note the two zeros at the two least significant bytes which is always zero for an interface and is used for node id's.


**Send content of variable**

    send $tempevent1
 
In this example the content of the variable tempevent1 is sent. The variable is of type event.  

## RETR - Retrieve one or several event(s).

This command can be used to retrieve one or several events from the input queue. Events are returned as

    head,class,type,obid,datetime,timestamp,GUID,data0,data1,data2,...........

**Important note** datetime was added in version *1.12.20.0*

GUID with MSB first.

Used on the following form:

    RETR 2<CR><LF>

which gives

    0,20,3,0,2001-11-02T17:43:15,0,FF:FF:FF:FF:FF:FF:FF:FE:0:5:93:140:2:32:0:1 
    0,20,4,0,2001-11-02T17:43:15,0,FF:FF:FF:FF:FF:FF:FF:FE:0:5:93:140:2:32:0:1 
    +OK - Success 

If no events is available in the queue

	
	-OK - No event(s) available


is received by the client.

If you try to fetch more events then there are in the queue you will get

    retr 100
    0,1,1,4,2001-11-02T17:43:15,0,FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:F5:00:04:00:00
    0,1,1,4,2001-11-02T17:43:15,0,FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:F5:00:04:00:00
    0,1,1,4,2001-11-02T17:43:15,0,FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:F5:00:04:00:00
    0,1,1,4,2001-11-02T17:43:15,0,FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:F5:00:04:00:00
    0,1,1,4,2001-11-02T17:43:15,0,FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:F5:00:04:00:00
    0,1,1,4,2001-11-02T17:43:15,0,FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:F5:00:04:00:00
 1. OK - No event(s) available

You request 100 events but there is only 6 available so you get a negative reply.

VSCP Event originating from a CANAL driver have the nickname of the node in the LSB of the GUID ( GUID[15] ). The rest of the GUID is the GUID for the interface.

If no argument is given one event is fetched even if there are more in the queue. 

If you try to receive more events then there is events in the buffer -OK will be returned after the available number of events have been retrieved and been listed.

## RCVLOOP - Send events to client as soon as they arrive.

This command set the channel in a closed loop that only can be interrupted by a client closing the connection or by sending the CLOSELOOP command. The server will now send out an event as soon as it is reserved. This is done in a very effective way with high throughput. This means the client does not have to poll for new events. It just open one channel where it sends events and do control tasks and one channel where it receive evens.

To help in determining that the line is alive

    +OK

is sent with a two second interval. The format for the event data is the same as for RETR command.

Some applications may not implement this feature and should output

    -OK - Command not implemented<CR><LF>

to indicate this. 

## QUITLOOP - quit receiving loop

Quit a receive loop started by the RCVLOOP command.

## CDTA/CHKDATA - Check if there are events to retrieve.

This command are used to check how many events are in the input queue waiting for retrieval.

Used on the following form:

    CDTA<CR><LF> 

and reply is

    8 <CR><LF>
    +OK<CR><LF>

## CLRA/CLRALL - Clear all events in in-queue.

This command are used to clear all events in the input queue.

Used on the following form:

   CLRA<CR><LF> 

and reply is

    +OK - All events cleared.<CR><LF>

## STAT - Get statistics information.

Get interface statistics information. The returned format is

    x,y,z,cntReceiveData,cntReceiveFrames,cntTransmitData,cntTransmitFrames

Where x,y,z currently is undefined values.

**Example:**

    STAT<CR><LF> 

reply is 
    0,0,0,12356,56,9182,20<CR><LF> 
    +OK - <CR><LF>

## INFO - Get status information.

This command fetch the status information for the interface. Returned format is

    channel_status,lasterrorcode,lasterrorsubcode,lasterrorstr

**Example:**

    INFO<CR><LF> 

and the reply is  
    
    7812,12,0,"Overrun"<CR><LF> 
    +OK - <CR><LF>

## CHID - Get channel ID.

Get the channel ID for the communication channel. This is the same parameter as the obid which is present in events.

**Example:**

    CHID<CR><LF> 

and the reply is
    
    1234<CR><LF> 
    +OK<CR><LF>

## SGID/SETGUID - Set GUID for channel.

Set the GUID for this channel. The GUID is given on the form

The format is:

    SETGUID 0:1:2:3:4:5:6:7:8:9:10:11:12:13:14:15<CR><LF> 

or
    SGID 0:1:2:3:4:5:6:7:8:9:10:11:12:13:14:15<CR><LF>

and reply is 

    +OK<CR><LF>

## GGID/GETGUID - Get GUID for channel.

Get the GUID for this channel. The GUID is received on the form

    0:1:2:3:4:5:6:7:8:9:10:11:12:13:14:15<CR><LF>
    +OK<CR><LF>

## VERS/VERSION - Get VSCP daemon version.

Get the current version for the daemon. The returned format is

    major-version,minor-version,sub-minor-version,build-version

**Note:** *build-version* added in version 13.0.0.14

## SFLT/SETFILTER - Set incoming event filter.

Set the incoming filter. The format is

    filter-priority, filter-class, filter-type, filter-GUID

**Example:**

    1,0x0000,0x0006,ff:ff:ff:ff:ff:ff:ff:01:00:00:00:00:00:00:00:00

Note: The GUID values always is given as hexadecimal values without a preceding “0x”.
Note: If you want to filter on nickname-ID you should filter on GUID LSB byte. 

## SMSK/SETMASK - Set incoming event mask.

Set the incoming mask. The format is

    mask-priority, mask-class, mask-type, mask-GUID

**Example:**

    1,0x0000,0x0006,ff:ff:ff:ff:ff:ff:ff:01:00:00:00:00:00:00:00:00

Note: that the GUID values always is given as hexadecimal values without a preceding “0x”.
Note: If you want to mask on nickname-ID you should mask on GUID LSB byte.


## WCYD / WHATCANYOUDO - Ask the capabilities of this server.

This command reports server capabilities of this server. 

The capabilities are described in a 64-bit array (8 bytes). The capabilities is reported on the form

    +OK - 00-00-00-00-00-00-00-00

where each pair of hex digits is a byte in the 64-bit capabilities structure. MSB is the first byte.

The VSCP server 16-bit capability code is described in the specification document for [CLASS2.PROTOCOL, Type=28, High end server capabilities](). It gives information about the capabilities of a VSCP server.

## MEASUREMENT - Send a measurement.

Send a measurement. The measurement will be sent as either as a Level I event or a Level II event.
 

**Format:**

    measurement type,unit,sensorindex,value,[guid],[level],[eventformat],[zone],[subzone]

Positive/negative response is returned.

**Arguments:**


*  **type** is the [VSCP type value](https://grodansparadis.gitbooks.io/the-vscp-specification/content/class1.measurement.html) specifying which type of measurement this is. Mandatory.

*  **unit** is the measurement unit for this type of measurement. An be in the range 0-3 for a Level I event and 0-255 for a Level II event. Mandatory.

*  **sensorindex** is the index for the sensor for the unit. Can be in the range 0-7 for a Level I event and 0-255 for a Level II event. Mandatory.

*  **value** is a floating point value for the measurement.  Mandatory.

*  **guid** is the GUID for the event. If not given it defaults to all zeros meaning the interface GUID will be used. Optional.

*  **level** VSCP level (Level I or Level II) to send event as. Can be 1 or 2 and defaults to 2. Optional.

*  **eventformat** is optional and can be *string* or *float* to generate a string based or a float based event. If not give the default value, float, will be used. Optional.

*  **zone** zone value for Level II events. Defaults to zero. Optional.

*  **subzone** zone value for Level II events. Defaults to zero. Optional.

## DRIVER

** The commands described here has not been activated yet due to security issues **

With this command drivers can be handled. The argument defines which operation is performed. 

### driver install

Install a new driver. Full format is DRIVER install “path to driver package”. It's possible to just install a driver temporarily or make it persistent to the system so it is loaded when the daemon starts. The driver package is a zip'ed file with a manifest file in XML format that tells where different components should go. 

### driver uninstall

Uninstall a driver that is currently installed. 

Full format is 

    DRIVER uninstall “drivername”/id. 

### driver upgrade

Upgrade a driver that is currently installed. 

Full format is 

    DRIVER upgrade “drivername”/id.

### driver start

Start an installed driver. 

Full format is 

    DRIVER start “drivername”/id. 

### driver stop

Stop an installed driver. 

Full format is 

    DRIVER stop “drivername”/id. 

### driver reload

Reload an installed driver. 

Full format is 

   DRIVER reload “drivername”/id. 

## FILE

** Not active at the moment **

With this command files can be handled. It is implemented to enable an administrator to handle driver and configuration files from a remote location and for client applications so they can dump collected data. Only files relative to the configured root folder (in and under) can be handled. 

### dir 

Show a directory listing for a folder given by the argument. 

### copy

Copy a file from one location to another. 

### move

Move a file from one location to another. 

### delete

Delete a file. 

### list

List content of file. 

## UDP

### enable

Enable the UDP interface. 

Full format is 

    UDP enable 

### disable

Disable the UDP interface. 

Full format is 

    UDP disable

## REMOTE

** The commands described here has not been activated yet due to security issues **

Remote user manipulation. 

### list

List user(s). Full format is 

    REMOTE list wild-card 

The list user command has the following format

    'count' rows<CR><LF>
    user1<CR><LF> 
    user2<CR><LF>
    ... 
    usern<CR><LF> 
    +OK<CR><LF>

### add

Add a user. Full format is 

    REMOTE add “username”,”MD5 password”,”from-host(s)”,”access-right-list”,”event-list”,”filter”,”mask” 

The add user parts of the arguments can be left out after password. All arguments below the one that is left out must be present. No argument in the middle can be taken away.

### remove

Remove a user. Full format is 

    REMOTE remove “username” 

### privilege

Set new privilege for a user. Full format is 

    REMOTE privilege “username”,”access-right-list” 

### password

Set new privilege for a user. Full format is 

    REMOTE password “username”,”MD5 for password” 

### host-list

Set locations user can connect from. Full format is 

    REMOTE password “username”,”host-list” 

### event-list

Set list of events user can send. Full format is

    REMOTE password “username”,”event-list” 

### filter

Set user filter. Full format is 

    REMOTE password “username”,”filter” 

### mask

Set user mask. Full format is 

    REMOTE password “username”,”mask”

## INTERFACE

Handle the interfaces on the VSCP daemon.

### list

List interfaces. 

For the list interfaces command the daemon respond with

    'count' rows<CR><LF>
    interface_id1, type, interface_GUID1, interface_realname1<CR><LF> 
    interface_id2, type, interface_GUID2, interface_realname2<CR><LF> 
    ... 
    interface_idn, type, interface_GUIDn, interface_realnamen<CR><LF> 
    +OK - Success.<CR><LF>

type is 

 | Type | Description                    | 
 | :----: | -----------                    | 
 | 0    | Unknown (should not see this). | 
 | 1    | Internal daemon client         | 
 | 2    | Level I driver                 | 
 | 3    | Level II driver                | 
 | 4    | TCP/IP interface client        | 
 | 5    | UDP interface client           | 
 | 5    | Webserver interface client     | 
 | 6    | Websocket interface client     | 
 | 7    | REST interface client          | 

###  close

Close interfaces. 

Full format is 

    interface close interface_GUID

Unique access to an interface can only be queried once for one interface. So two unique operations after each other deselects the first chosen interface before acquire the second. 

## DM

### enable

Enable a decision matrix row. Argument is a comma separated list with DM row number(s) or “ALL” for all rows. 

### disable

Disable a decision matrix row. Argument is a comma separated list with DM row number(s) or “ALL” for all rows. 

### list

Show a decision matrix row number. Argument is DM row number(s) or “ALL” for all rows. 

The list command gives a list of the following format

     enabled,groupid,from,to,weekday,time,mask,filter,index,zone,sub-zone,control-code,action-code,action-param,comment,trig-counter,error-counter<CR><LF> 
     .... 
     +OK<CR><LF>


*  Enabled: First parameter is enabled if the row is active else disabled (“enabled”/”true”/1 or “disabled”/”false”/0). 

* From: Allowed date plus time from which the action can be triggered. Form is YYYY-MM-DD HH:MM:SS.

*  To: Allowed date plus time up to which the action can be triggered. Form is YYYY-MM-DD HH:MM:SS.

*  Weekdays: Allowed weekdays for the action to be triggered. 

*  Time: The time(s) when the action should be triggered. This is a string on the form YYYY-MM-DD HH:MM:SS. where both parts can be replaced with a '*' to indicate that it is a no care. This means that * * is for all dates and all time while * HH:MM:SS is for all dates but a specific times. Further, all elements such as YYYY, MM, DD, HH, MM, SS can be replaced with a * to represent a no care for each place where it is present. Each can also be given as a list separated with '/' characters to indicate several choices. So YYYY-MM-DD HH:0/5/10;SS means the action should be performed on a specific date and hour on every full hour (0), five minutes past (5) and ten minutes past (10).

*  **Mask**: A standard VSCP mask on the form Priority;Class;Type;GUID where all describe the masks part. 

*  **Filter**: A standard VSCP filter on the form Priority;Class;Type;GUID where all describe the filter part. 

*  **Index**: Is also part of the filter but is an absolute value from data-byte 0. 

*  **Zone**: Is also part of the filter but is an absolute value from data-byte 1. 

*  **Sub-zone**: Is also part of the filter but is an absolute value from data-byte 2. 

*  **Control-code**: The 32-bit control code. Note that enable/disable is part of this code. 

*  **Action-code**: The action code follows next. 

*  **Action-param**: A string consisting of action parameters. 

*  **Comment**: A comment for the row.

*  **Trig-counter**: This is a counter for how many time the action for the row has been executed. 

*  **Error-counter**: This is a counter for action execution errors for the row.

See the DM description in the VSCP specification for information about the content of the control code etc. 

### add

Add a decision matrix row. The add-command needs a parameter of the following format

    enabled,from,to,weekday,time,mask,filter,index,zone,sub-zone,control-code,action-code,action-param,comment

See the list command [des:decision matrix list command] for a detailed description of the items.

###  delete

Delete a decision matrix row. 

Argument is a comma separated list with DM row number(s). 

### reset

Resets all variables and read in persistent values. 

### clrtrig

Clear trig counter for a decision matrix row.

Argument is a comma separated list with DM row number(s) or “ALL” for all rows. 

### clrerr

Clear error counter for a decision matrix row. 

Argument is a comma separated list with DM row number(s) or “ALL” for all rows. 

### save

Save current decision matrix to a file. If no filename is given dm.xml is used with the path set to the configuration folder. Se [sub:The-decision-matrix-file-format] for decision matrix file format.

### load

Load decision matrix from a file. If no filename is given dm.xml is used with the path set to the configuration folder. A path + filename can be used and this file will be used instead. The last argument is replace or add (default). replace - replaces the old decision matrix content with the new and the option add adds the decision matrix from the file at the end of the current decision matrix. Se [sub:The-decision-matrix-file-format] for decision matrix file format.

## VAR / VARIABLE

Note: Changed to "VAR" from "VARIABLE" in version 1.12.15 but both works.


### list

List all defined variables selected by an optional [regular expression](https://www.cheatography.com/davechild/cheat-sheets/regular-expressions/). Default is that all variables is listed (no argument). 

Use for example

    variable list vscp.
    
to list all stock variables or

    variable list vscp.dm.

to list all stock variables related to the decision matrix.

Output for the command is

a first row with 

    n rows.`<CR>`LF>
    
where "n" is the number of rows that follow (# variables)

and then followed by zero or more

    ordinal;variablename;numeric-variabletype;userid;access-rights;last-change;persistance<CR><LF>

where ordinal goes from zero and upwards and then a

    +OK<CR><LF>

at the end as a positive response.

If there is no variables that meet the regular expression

    0 rows.<CR><LF>
    +OK<CR><LF>
    
is returned.      

### write

Write a variable. If the variable is not already defined it is created.  Argument is 

    "variable name";"type";"persistence";"owner";"rights";"value";"note"


*  **name** is the name of the variable.

*  **variable-type** is the variable type in numerical or string form (default is string).  

*  **persistence** can be “true” or “false” (default is "false"). If set to true a persistent variable is created.

*  **owner** is the owner of the variable. Can be given on numerical (userid) or in text form. If not given the current user is used.

*  **access-rights** is the numerical access rights (default is 0x744).

*  **value** is the value for the variable. Note that certain forms of variables always expect the value to be coded in BASE64, for example the string type expects this. [See table](./remote_variables.md#variable_types) for info about which variables expect BASE64 encoded value input.

*  **note** is a note for the variable. Always coded in BASE64.

You can have empty items like

    “name of variable”;;;;”value” 

which get default values set for the missing parts. Not entering fields like the field "note" above give the same effect. So to write a variable with all default values one can write

 "name of variable"

this will be a non-persistent string owned by the current user and with permission 744.

Also note that if a variable already exist, access-rights, persistence, value and note will have there values changed for the existing variable. The type of a variable can never be changed if it already exists. In this case remove it first.

Response for a successful write is

	
	  +OK - Success.


else error

	
	  -OK - 'some message describing error'.

### read

Read a variable. Argument is “name of variable”.

The response (if the variable exist) is

	
	  name;type;user;access-rights;persistence;last-change;value;note
	  +OK - Success.


where type and user always is numeric. 

If an error occurs

	
	  -OK - Variable does not exists.


if the variable is non existent.


**Note:** Prior to build 13.0.1 the variable info string was perpended with "+OK - ". This has been removed for consistency with other parts of the link interface.


### readvalue

Read a variables value. The value is BASE64 encoded if internally stored as such (type=string etc). Arguments is “name of variable” The response is

	
	  value<CR><LF>
	  +OK - Success.  


or if the variable is not defined

	
	  -OK - Variable is not defined.<CR><LF>

 

### writevalue

Write a variables value. Arguments is “name of variable” and "value". The response is

	
	  +OK - Success.


or if the variable is not defined

	
	  -OK - Variable is not defined.<CR><LF>


The format for different variable types is [here](./remote_variables.md#variable_types). 

### readnote

Read a variables note. The note is always returned BASE64 encoded. Arguments is “name of variable” The response is

	
	  note<CR><LF>
	  +OK - Success. 


or if the variable is not defined

	
	  -OK - Variable is not defined.<CR><LF>

 

### writenote

Write a variables note. Arguments is “name of variable” and "note". The response is

	
	  +OK - Success.


or if the variable is not defined

	
	  -OK - Variable is not defined.<CR><LF>


### reset

Variable  value is set to its default value. The default values for different variables types can be found [here](./remote_variables.md#reset_variable_values). Command does not work with stock variables ad they can not be reseted.

Response for a successful reset of a variable is

	
	  +OK - Success.


else error

	
	  -OK - 'some message describing error'.

### readreset

This is a combination of **read** + **reset** doing them together in an atomic way. Command does not work with stock variables ad they can not be reseted.

Response for a successful read/reset of a variable is

	
	  +OK - Success.


else error

	
	  -OK - 'some message describing error'.


### remove

Removes a variable. Argument is name of the variable. Command does not work with stock variables ad they can not be removed.

Response for a successful removal of a variable is

	
	  +OK - Success.


else error

	
	  -OK - 'some message describing error'.

### readremove

This is a combination of **read** + **remove** doing them together in an atomic way. Command does not work with stock variables ad they can not be removed.

Response for a successful read/remove of a variable is
	
	  +OK - Success.

else error
	
	  -OK - 'some message describing error'.

### length

Get the length for a string variable. No effect for other variable types (returns 0 ). 


Response for a successful length request is

	
	  length<CR><LF>
	  +OK - Success.


else error

	
	  -OK - 'some message describing error'.

### save

Save persistent, non-persistent or both variable types to an external XML file. 

Argument is 

   * **path** to where the XML file should be written.
   * **select** Which is "1" for only writing persistent variables, "2" only write non-persistent variables and "3" or "0" for writing both types. Defaults to "0".
   * **regex** Optional regular expression that selects which variables to write. Default is all.

Output format from daemon for variable list/read commands is

[Here is an example](./remote_variables#persistent_storage_format.md) of how variables are stored on disk.

Response for a successful save is

	
	  +OK - Success.


else error

	
	  -OK - 'some message describing error'.

### load

Load variables from XML file on disk.

   * **path** to where the XML file to be loaded is located.

This is how the variables look like using the variable list all command in the TCP/IP interface.

![](./images/variables_in_tcpip_interface.png)

Response for a successful load is

	
	  +OK - Success.


else error

	
	  -OK - 'some message describing error'.

## TABLE

The VSCP daemon can handle [three types of tables](./vscp-tables.md). 


*  Dynamic tables which is ever growing tables that will grow until all disk space is used or deleted or cleared by a users. Just as any database.

*  Static tables which consist of a limited set of data which is filled in up to a specified size and when that size is reached the number of items in the table will be kept at this level by removing the oldest records.

*  Max tables which is tables that just like static tables have a set size but which collect data up to the set size and then delete all content and start to collect data again.

Both are intended as a way for time stamp ,measurement pairs to be logged in an easy way and then being displayed in diagram form in a user UI. The most convenient way to handle this information from a web base application is through the [REST api](./rest_interface.md) or the [websocket interface](./websocket_interface) but sometime the tcp/ip interface is more convenient to use and it is thus possible to get table data also here.

### create 'table-name' 'create-parameters...'

Create a new table with name 'table-name' using the supplied parameters described below.

The parameters is given as a comma separated list. Some parameters which could have comma or other *invalid characters* in them can be encoded in BASE64 and if so should be preceded with "BASE64:".

 | Parameter   | Description  | 
 | ---------   | -----------  | 
 | tblname     | Name to be used for the table. Must not already be used for a table.                                                            | 
 | bEnable     | "true" or "false" to enable or disable the loading of the table.                                                                | 
 | bInMemory   | "true" or "false" to create the table in memory or on disk.                                                                     | 
 | type        | "dynamic", "static" or "max" for the type of table to construct,                                                                | 
 | size        | Size for the table when it is of type "static" or "max". Ignored for other types.                                               | 
 | owner       | The user that should own the table. The user should exist.                                                                      | 
 | rights      | Rights for usage of the table.                                                                                                  | 
 | title       | Title of the table. If "BASE64:" is preceding this value it is decoded from base64 before use.                                  | 
 | xname       | X axis label. If "BASE64:" is preceding this value it is decoded from base64 before use.                                        | 
 | yname       | y axis label. If "BASE64:" is preceding this value it is decoded from base64 before use.                                        | 
 | note        | Note used for table diagram. If "BASE64:" is preceding this value it is decoded from base64 before use.                         | 
 | sqlcreate   | SQL statement to create table. If "BASE64:" is preceding this value it is decoded from base64 before use.                       | 
 | sqlinsert   | SQL statement used to insert a value into the table. If "BASE64:" is preceding this value it is decoded from base64 before use. | 
 | sqldelete   | SQL statement used to delete values from table. If "BASE64:" is preceding this value it is decoded from base64 before use.      | 
 | description | Description of tables use. If "BASE64:" is preceding this value it is decoded from base64 before use.                           | 
 | vscpclass   | VSCP class for data in table.                                                                                                   | 
 | vscptype    | VSCP type for data in the table.                                                                                                | 
 | sensorindex | Sensor index for data in the table (optional).                                                                                  | 
 | unit        | Unit used for data in the table (optional).                                                                                     | 
 | zone        | Zone use for data in the table (optional).                                                                                      | 
 | subzone     | Subzone used for data in the table (optional).                                                                                  | 

### delete 'table-name' [true]

Delete an existing table and optional remove it's associating database file if the last argument is 'true'. Default is to leave the database file. If this is done and a new table with the same name later is created this file will be reused. This can cause troubles if the two tables have different columns defined.

**'del'** can be used instead of **'delete'**

### list

List all available tables.

    'count' rows<CR><LF>
    table-name1;type;description<CR><LF>
    table-name2;type;description<CR><LF>
    ...
    table-namen;type;description<CR><LF>
    +OK - Success.<CR><LF>

Where type is either 'dynamic', 'static' or "max".

Description will be BASE64 encoded.

### list 'table-name' [xml]

List full information for a specific table with name 'table-name'. The standard output is

```json
    name=table-name<CR><LF>
    enable=true|false<CR><LF>
    type="dynamic"|"static"|"max"//<CR><LF>
    bmemory=true|false<CR><LF>
    size=Size of table or zero<CR><LF>
    owner=name of owner<CR><LF>
    permission=user permissions<CR><LF>
    description=Free text description of the table<CR><LF>
    xname=diagram x-axis text<CR><LF>
    yname=diagram y-axis text<CR><LF>
    title=diagram title<CR><LF>
    note=diagram note<CR><LF>
    vscp-class=n<CR><LF>
    vscp-type=n<CR><LF>
    vscp-sensor-index=n<CR><LF>
    vscp-unit=n<CR><LF>
    vscp-zone=n<CR><LF>
    vscp-subzone=n<CR><LF>
    sql-create=Table create SQL expression<CR><LF>
    sql-insert="Table insert SQL expression<CR><LF>
    sql-delete="Table delete SQL expression<CR><LF>
    +OK - Success.<CR><LF>
```  
    
If the optional argument **'xml'** is given the output will be a BASE64 encoded XML content with the following format

```xml
<table 
    name = "test_table1"
    benable = "true"
    binmemory = "false"
    type = "dynamic"
    size = "0"
    owner = "admin"
    rights = "0x777"
    title = "This is a title"
    xname = "This the x-lable"
    yname = "This is the y-label"
    note = "This is a note"
    sqlcreate = "CREATE TABLE 'vscptable' ( `idx` INTEGER NOT NULL PRIMARY KEY UNIQUE, `datetime` TEXT, `value` REAL DEFAULT 0 );"
    sqlinsert = "INSERT INTO 'vscptable' (datetime,value) VALUES ('%%s','%%f');"
    sqldelete = ""
    description = "This is the description"
    vscpclass = "10"
    vscptype = "6"
    sensorindex = "0"
    unit = "1"
    zone = "0"
    subzone = "0"
/>
```

which will be outputed as 

	
	  PHRhYmxlcz4gICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIA0KPHRhYmxlIA0KICAgIG5hbWUgPSAidGVzdF90YWJsZTEiDQogICAgYmVuYWJsZSA9ICJ0cnVlIg0KICAgIGJpbm1lbW9yeSA9ICJmYWxzZSINCiAgICB0eXBlID0gImR5bmFtaWMiDQogICAgc2l6ZSA9ICIwIg0KICAgIG93bmVyID0gImFkbWluIg0KICAgIHJpZ2h0cyA9ICIweDc3NyINCiAgICB0aXRsZSA9ICJUaGlzIGlzIGEgdGl0bGUiDQogICAgeG5hbWUgPSAiVGhpcyB0aGUgeC1sYWJsZSINCiAgICB5bmFtZSA9ICJUaGlzIGlzIHRoZSB5LWxhYmVsIg0KICAgIG5vdGUgPSAiVGhpcyBpcyBhIG5vdGUiDQogICAgc3FsY3JlYXRlID0gIkNSRUFURSBUQUJMRSAndnNjcHRhYmxlJyAoIGBpZHhgIElOVEVHRVIgTk9UIE5VTEwgUFJJTUFSWSBLRVkgVU5JUVVFLCBgZGF0ZXRpbWVgIFRFWFQsIGB2YWx1ZWAgUkVBTCBERUZBVUxUIDAgKTsiDQogICAgc3FsaW5zZXJ0ID0gIklOU0VSVCBJTlRPICd2c2NwdGFibGUnIChkYXRldGltZSx2YWx1ZSkgVkFMVUVTICgnJSVzJywnJSVmJyk7Ig0KICAgIHNxbGRlbGV0ZSA9ICIiDQogICAgZGVzY3JpcHRpb24gPSAiVGhpcyBpcyB0aGUgZGVzY3JpcHRpb24iDQogICAgdnNjcGNsYXNzID0gIjEwIg0KICAgIHZzY3B0eXBlID0gIjYiDQogICAgc2Vuc29yaW5kZXggPSAiMCINCiAgICB1bml0ID0gIjEiDQogICAgem9uZSA9ICIwIg0KICAgIHN1YnpvbmUgPSAiMCINCi8+CQ0KPC90YWJsZXM+DQo=<CR><LF>
	  +OK - Success.<CR><LF>

    
### get 'table-name' 'from' 'to' ["full"]

Get table data from a named table over an optional interval **to - from** which each should be on the form (ISO 8601) YY-MM-DDTHH:MM:SS.

If "full" is specified all fields of the table is listed. **datetime** is always listed first followed by **value** and after that the rest of the fields are listed.

The output will look like this

    'count' rows<CR><LF>
    YY-MM-DDTHH:MM:SSsss, value1[,other fields]<CR><LF>
    YY-MM-DDTHH:MM:SSsss, value2[,other fields]<CR><LF>
    YY-MM-DDTHH:MM:SSsss, value3[,other fields]<CR><LF>
    ...
    YY-MM-DDTHH:MM:SS, valuen[,other fields]<CR><LF>
    +OK - Success.<CR><LF>


### getraw 'table-name' 'from' 'to' 

Get table data from a named table over an optional interval **to - from** which each should be on the form (ISO 8601) YY-MM-DDTHH:MM:SS. 

The difference between get and getraw is that getraw always outputs all fields of a table as a comma separated list while get treat datetime and value as special values and put them before all other values.
### log 'table-name' value [datetime]

log data to a named table.

Table-name and value must be given. Table-name must be a valid and existing table. The value should be a floating point value. A period ('.') is always used as a decimal separator regardless of language settings. The datettime value is on standard ISO date/time format (YYYY-MM-DDTHH:MM:SS.sssZ) and should always be given as UTC time. The "sss" is millisecond part. 

If datetime is not given the current UTC time will be used. 
### logsql 'table-name' 'sql'

Log data to a named table using custom SQL expression. 

Regardless to say this is a **very dangerous** command and you need the highest privileges to use it as a user which normally means admin privileges.

### records 'table-name' [from to]

Statistical function that return the number of records in the database over a date range *from to* or over the full table if no range is given. The date time ranges should be given in ISO format YYYYMMDDTHH:MM:SS as usual.

### firstdate 'table-name' [from to]

Statistical function that return the first date in a date range *from to* or over the full table if no range is given. The date time ranges should be given in ISO format YYYYMMDDTHH:MM:SS as usual.

### lastdate 'table-name' [from to]

Statistical function that return the last date in a date range *from to* or over the full table if no range is given. The date time ranges should be given in ISO format YYYYMMDDTHH:MM:SS as usual.

### sum 'table-name' [from to]

Statistical function that return the sum of all values over a date range *from to* or over the full table if no range is given. The date time ranges should be given in ISO format YYYYMMDDTHH:MM:SS as usual.

### min 'table-name' [from to]

Statistical function that return the minimum value of all values over a date range *from to* or over the full table if no range is given. The date time ranges should be given in ISO format YYYYMMDDTHH:MM:SS as usual.

### max 'table-name' [from to]

Statistical function that return the max of all values over a date range *from to* or over the full table if no range is given. The date time ranges should be given in ISO format YYYYMMDDTHH:MM:SS as usual.

### average 'table-name' [from to]

Statistical function that return the average of all values over a date range *from to* or over the full table if no range is given. The date time ranges should be given in ISO format YYYYMMDDTHH:MM:SS as usual.

### median 'table-name' [from to]

Statistical function that return the median / third quartile of all values over a date range *from to* or over the full table if no range is given. The date time ranges should be given in ISO format YYYYMMDDTHH:MM:SS as usual.


### stddev 'table-name' [from to]

Statistical function that return the standard deviation of all values over a date range *from to* or over the full table if no range is given. The date time ranges should be given in ISO format YYYYMMDDTHH:MM:SS as usual.

### variance 'table-name' [from to]

Statistical function that return the variance of all values over a date range *from to* or over the full table if no range is given. The date time ranges should be given in ISO format YYYYMMDDTHH:MM:SS as usual.

### mode 'table-name' [from to]

Statistical function that return the mode of all values over a date range *from to* or over the full table if no range is given. The date time ranges should be given in ISO format YYYYMMDDTHH:MM:SS as usual.

### lowerq 'table-name' [from to]

Statistical function that return the first quartile / lower quartile of all values over a date range *from to* or over the full table if no range is given. The date time ranges should be given in ISO format YYYYMMDDTHH:MM:SS as usual.

### upperq 'table-name' [from to]

Statistical function that return the third quartile / upper quartile of all values over a date range *from to* or over the full table if no range is given. The date time ranges should be given in ISO format YYYYMMDDTHH:MM:SS as usual.

### clear 'table-name' [to from]

Clear records in table, possibly to-from a date time range.




{% include "./bottom_copyright.md" %}
