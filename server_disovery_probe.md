# High end server/service probe

[CLASS1.PROTOCOL, Type=27, High end server/service probe](https://grodansparadis.gitbooks.io/the-vscp-specification/class1.protocol.html#type27) can be sent on a segment to discover available VSCP services on that segment. The response from a node that have a VSCP server/service is [CLASS1.PROTOCOL, Type=28, High end server/service response](https://grodansparadis.gitbooks.io/the-vscp-specification/class1.protocol.html#type28) and for a Level II node [High end server/service capabilities](https://grodansparadis.gitbooks.io/the-vscp-specification/class2.protocol.html#type20). 

**Note** that a probe can result in none, one or many responses also from a single node on a segment.

A node that want to know what servers/services is available on a segment has two options. Either it listens on the [multicast announcement channel](./multicast_protocol_description_announce.md) for heartbeats and capabilities events over a minute or send a probe **CLASS1.PROTOCOL, Type=26**, High end server/service probe on the segment to immediately discover servers/services.

Note that [Who is there](https://grodansparadis.gitbooks.io/the-vscp-specification/class1.protocol.html#type31) event have different response events for Level I and Level II nodes. A level I node respond with [CLASS1.PROTOCOL, Type=32, Who is there response](https://grodansparadis.gitbooks.io/the-vscp-specification/class1.protocol.html#type32). A level II node respond with [CLASS2.PROTOCOL, Type=32 Level II who is response](https://grodansparadis.gitbooks.io/the-vscp-specification/class2.protocol.html#type32) to this event.



{% include "./bottom_copyright.md" %}
