# Hearbeats and announcements

A level I node sends [CLASS1.INFORMATION, Type=9, node heartbeats](https://grodansparadis.gitbooks.io/the-vscp-specification/content/class1.information.html#type--9-0x09-node-heartbeat) on the segment it is connected to. muticast announce channel.  

A level II node sends [CLASS2.INFORMATION, Type=2, Level II Node Heartbeat](https://grodansparadis.gitbooks.io/the-vscp-specification/content/class2.information.html#type2-0x0002-level-ii-node-heartbeat)

A level II node in addition sends [CLASS2.PROTOCOL, Type=20, High end server/service capabilities](https://grodansparadis.gitbooks.io/the-vscp-specification/content/class2.protocol.html#type20-0x14-high-end-serverservice-capabilities) on the multicast announce channel.

A level II node, like the VSCP server, that act as a gateway for other nodes send [CLASS2.Information, Type=3, Level II Proxy Node Heartbeat](https://grodansparadis.gitbooks.io/the-vscp-specification/content/class2.information.html#type3-0x0003-level-ii-proxy-node-heartbeat).

{% include "./bottom_copyright.md" %}
