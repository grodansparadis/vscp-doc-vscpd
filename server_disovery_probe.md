# High end server/service probe

[CLASS1.PROTOCOL, Type=26, High end server/service probe](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.protocol#type_27_0x1b_high_end_server_service_probe) can be sent on a segment to discover available VSCP services on that segment. The response from a node that have a VSCP server/service is [CLASS1.PROTOCOL, Type=26, High end server/service response](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.protocol#type_28_0x1c_high_end_server_service_response) and for a Level II node [High end server/service capabilities](http://www.vscp.org/docs/vscpspec/doku.php?id=class2.protocol#type_20_0x14_high_end_server_service_capabilities). 

**Note** that a probe can result in none, one or many responses also from a single node on a segment.

A node that want to know what servers/services is available on a segment has two options. Either it listens on the [multicast announcement channel](http://www.vscp.org/docs/vscpd/doku.php?id=daemon_multicast_protocol_description_announce) for heartbeats and capabilities events over a minute or send a probe **CLASS1.PROTOCOL, Type=26**, High end server/service probe on the segment to immediately discover servers/services.

Note that [Who is there](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.protocol#type_31_0x1f_who_is_there) event have different response events for Level I and Level II nodes. A level I node respond with [CLASS1.PROTOCOL, Type=32, Who is there response](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.protocol#type_32_0x20_who_is_there_response). A level II node respond with [CLASS2.PROTOCOL, Type=32m Level II who is response](http://www.vscp.org/docs/vscpspec/doku.php?id=class2.protocol#type_32_0x20_level_ii_who_is_there_response) to this event.



----
\\ 
----
{{  ::copyright.png?600  |}}
