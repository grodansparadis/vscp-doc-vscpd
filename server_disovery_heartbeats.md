# Hearbeats and announcements

A level I node sends [CLASS1.INFORMATION, Type=9, node heartbeats](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.information#type_9_0x09_node_heartbeat) on the segment it is connected to. muticast announce channel.  

A level II node sends [CLASS2.INFORMATION, Type=2, Level II Node Heartbeat](http://www.vscp.org/docs/vscpspec/doku.php?id=class2.information#type_2_0x0002_level_ii_node_heartbeat)

A level II node in addition sends [CLASS2.PROTOCOL, Type=20, High end server/service capabilities](http://www.vscp.org/docs/vscpspec/doku.php?id=class2.protocol#type_20_0x14_high_end_server_service_capabilities) on the multicast announce channel.

A level II node, like the VSCP server, that act as a gateway for other nodes send [CLASS2.InformationL, Type=3, Level II Proxy Node Heartbeat](http://www.vscp.org/docs/vscpspec/doku.php?id=class2.information#type_3_0x0003_level_ii_proxy_node_heartbeat).

----
\\ 
----
{{  ::copyright.png?600  |}}
