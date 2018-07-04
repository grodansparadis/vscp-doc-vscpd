# Multicast channels

Multicast channels is a way for level II nodes to set up a channel of interest among themselves which makes it possible to communicate with each other without the need for a central server. A multicast channel can be seen as a group of interest or as a subnet. A single node can be active on many multicast channels. 

## Configuration

The configuration of the multicast channel interface can be done in the VSCP server configuration file (/etc/vscp/vscpd.conf) or in the configuration database. The configuration is fully described [here](./configuring_the_vscp_daemon.md#multicast_channel_interface).


*  The first option is to decide if the multicast channel service should be enabled or not. This is set by setting enable equal to “true” or “false”.

If the service should be enabled you add one or more channels


*  Next you have to set **public** to a public ip-address of your machine. A 10... or 127.. address will not work here. 

*  Set **port** to the port your multicast channel group should use.

*  **Group** is set to the VSCP group. This should normally not be changed.

*  Set **ttl** to the value you want. See [spec](https://grodansparadis.gitbooks.io/the-vscp-specification/vscp_multicast.html) for a table of possible values.

*  With **guid** you set the GUID for the interface. If empty or all set to zeros the system will set a GUID for you.

*  By setting the **rxfilter/rxmask** you can filter out unwanted events. Both filter and mask is set as text strings on the form *"priority;class;type;guid"* This will filter which events that are received.

*  By setting the **txfilter/txmask** you can filter out events that you don't want to be sent on the channel. Both filter and mask is set as text strings on the form "priority;class;type;guid" 

*  Set **Encryption** to "none"/"AES128"/"AES192"/"AES256" to leave __sent__ frames unencrypted or to encrypt them. 

*  With **bSendAck** you can decide if the node sending an UDP frame should get an acknowledge event back. If set to *"true"* a  [CLASS1.ERROR, Type=0, Success](https://grodansparadis.gitbooks.io/the-vscp-specification/class1.error.html#type0) event will be replied on success and a [CLASS1.ERROR, Type=1, Error](https://grodansparadis.gitbooks.io/the-vscp-specification/class1.error.html#type1) is sent if something is wrong with the UDP frame. If set no *"false"* no acknowledgement frames will be sent.

*  The next thing is to decide if you should allow unencrypted frames. You do this by setting **bAllowUnsecure** to *"true"*. If set to *"false"* only encrypted frames will be received. 


## Sample code

You can find sample code (C/C++/Python) [here](https://github.com/grodansparadis/vscp/tree/master/tests/multicast) for both multicast announce and multicast channel interfacing. More will follow.


{% include "./bottom_copyright.md" %}
