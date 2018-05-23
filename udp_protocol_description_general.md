# UDP - General description

## General

UDP communication is simple and easy to set up but also unsecure in the way that you do not know if a datagram is received or not. This is normally not a problem for VSCP as there is almost always a way to determine that an event has been received. A typical example is a lamp that should be turned on. The controller typically send

[CLASS1.CONTROL, Type=5 ,TurnOn](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.control#type_5_0x05_turnon)

we then expect the receiving node to reply with 

[CLASS1.INFORMATION, Type=3, On](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.information#type_3_0x03_on)

to verify that the lamp was turned on. It is therefore easy to make sure a command has been received by a remote node and has been carried out and if not resend.

The VSCP server can be setup to receive UDP datagrams on a specific port and it can be setup to send VSCP events to a specified number of nodes. Filters can be used to limit sent and received events. It is possible to get an automatic acknowledgement event when a VSCP UDP event is received by the VSCP server. Encryption is available in the form of AES128/AES192/AES256 or unencrypted frames. 

## Security

One can send unencrypted frames to the VSCP server. This means that anyone can send a VSCP event to a central VSCP server/system. This will of course be very dangerous on most systems. You can specify a user that the UDP sub system will be acting as and this gives some possibilities to limit the what can be sent and be received. Best is to use encrypted frames. Here the remote node and the server share a secret key and therefore they can trust each other using state of the art encryption. This also makes it impossible for someone that is not authorized to see what is sent on the wire or over the air.

## Configuration

The full configuration is described [here](http://www.vscp.org/docs/vscpd/doku.php?id=configuring_the_vscp_daemon#udp_interface).

The configuration consist of two parts. 

 1.  The receiving UDP port and the functionality for it. 
 2.  Configuration for receiving UDP nodes.

### Configuring the receiving UDP port


*  Enable enables the UDP interface if set to **//"true"//**. This applies for receiving nodes also. Set to **//"false"//** to disable VSCP UDP functionality.

*  The second thing to configure is the **interface** to use. This is typically **//"`<nowiki>`udp://44444`</nowiki>`"//** which says "listen on all interfaces and use port 44444 (default)". One can use an IP address like **//"`<nowiki>`udp//:192.168.1.45:44444`</nowiki>`"//** to listen only at a specific interface.

*  Next you should consider using a user account that UDP connections use. You do this by setting the username in **user** and the password in **password**. Password should be set as salt;password in the standard way. By doing this you can specify which events that can be received and from which IP addresses. Leave both user and password bland to not connect to a user account.

*  The next thing is to decide if you should allow unencrypted frames. You do this by setting **bAllowUnsecure** to **//"true"//**. If set to **//"false"//** only encrypted frames will be received.

*  With **bSendAck** you can decide if the node sending an UDP frame should get an acknowledge event back. If set to **//"true"//** a  [CLASS1.ERROR, Type=0, Success](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.error#type_0_0x00_success) event will be replied on success and a [CLASS1.ERROR, Type=1, Error](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.error#type_1_0x01_error) is sent if something is wrong with the UDP frame. If set no **//"false"//** no acknowledgement frames will be sent.

*  By setting the **filter/mask** you can filter out unwanted events. Both filter and mask is set as text strings on the form "priority;class;type;guid"

*  With **guid** you set the GUID for the interface. If empty or all set to zeros the system will set a GUID for you.

### Configuring receiving UDP nodes

Receiving UDP nodes are nodes that will get events from the VSCP server. You can specify as many nodes as you need.


*  **Enable** enables the UDP receiving node if set to **//"true"//**. Set to **//"false"//** to disable VSCP UDP functionality.

*  **interface** is the address and port of the receiving node. It should be entered on the form **//"`<nowiki>`udp//:192.168.1.45:29001`</nowiki>`"//** 

*  By setting the **filter/mask** you can filter out events that should not be sent to this node. Both filter and mask is set as text strings on the form "priority;class;type;guid"

*  **Encryption** tells how the sent UDP frames should be encrypted. Valid values are **"none"/"aes128"/"aes192"/"aes256"** and empty

## Samples

You can find some sample/test code [here](https///github.com/grodansparadis/vscp/tree/master/tests/udp).


\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
