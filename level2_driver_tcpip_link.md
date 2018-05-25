# TCP/IP link level II driver

**Available for**: Linux, Windows

The tcp driver can be used to connect to other daemons or connect to limited TCP/IP devices that export a subset of the commands available in the VSCP daemons. A required subset must be available described here [sub:Link-Commands] and here [sub:Available-tcpip-commands].

The driver will try to hold a connection open even if the remote node disconnects. This makes it possible to replace a node or take it down for maintenance and still have the link online again as soon as the node is powered up. 

**Driver Linux**: vscpl2_tcpdrv.so\\ 
**Driver Windows**: vscpl2_tcpdrv.dll

The configuration string have the following format

    host;port;user;password;filter;mask

*Host* and *port* tells the address to the remote server. *User* and *password* is the credentials to log in to the remote machine. Filter and mask can be used to filter incoming traffic from the remote host. All of the parameters in the configuration string can also be set with variables.
The configuration string have the following format

 | Variable name    | Type    | Description                                                                                                                                                                                                                                     | 
 | -------------    | ----    | -----------                                                                                                                                                                                                                                     | 
 | _host_remote     | string  | IP address or a DNS resolvable address to the remote host. Mandatory and must be declared either in the configuration string or in this variable.                                                                                               | 
 | _port_remote     | integer | The port to use on the remote host. Default is 9598.                                                                                                                                                                                            | 
 | _user_remote     | string  | Username used to log in on the remote sever.                                                                                                                                                                                                    | 
 | _password_remote | string  | Password used to login on the remote server.                                                                                                                                                                                                    | 
 | _filter          | string  | Standard VSCP filter in string form. 1,0x0000,0x0006,ff:ff:ff:ff:ff:ff:ff:01:00:00:00:00:00:00:00:00 as priority,class,type,GUID Used to filter what events that is received from the socketcan interface. If not give all events are received. | 
 | _mask            | string  | Standard VSCP mask in string form. 1,0x0000,0x0006,ff:ff:ff:ff:ff:ff:ff:01:00:00:00:00:00:00:00:00 as priority,class,type,GUID Used to filter what events that is received from the socketcan interface. If not give all events are received.   | 

The full variable name is built from the name you give the driver (prefix before _variablename) in vscpd.conf. So in the examples below the driver have the name **tcpiplink1** and the full variable name for the **_host_remote** will thus be

    tcpiplink1_host_remote

If you have another diver and name it  **tcpiplink2** it will therefore instead request variable **tcpiplink2_host_remote**

If your driver name contains spaces, for example “name of driver” it will get a prefix that is “name_of_driver”. Leading and trailing spaces will be removed. 

##### vscpd.conf example

`<code="xml">`                
`<driver enable="true" >`                 
    `<name>`tcpiplink1`</name>`
    `<path>`/usr/local/lib/vscp2drv_tcpiplink.so`</path>`
    `<config>`192.168.1.20;9598;admin;secret`</config>`                 
    `<guid>`00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00`</guid>`             
`</driver>`
```


\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
