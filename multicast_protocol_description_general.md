# Multicast - General description

Multicast is described [here in the VSCP specification](https://grodansparadis.gitbooks.io/the-vscp-specification/vscp_multicast.html).

The multicast interface of the VSCP server uses the VSCP assigned multicast group and consist of two parts. **Multicast announce** and **multicast channels**.

**Multicast announce** is a way for a level II node to announce that it is available and tell what it can do to other nodes in a a system. If a level II node can implement this interface it should implement it. A node that listen for at least one minute in the multicast announce channel will after that know the existence of all VSCP nodes on that system that want to be known.

**Multicast channels** is a way for level II nodes to set up a channel of interest among themselves which makes it possible to communicate with each other without the need for a central server. A multicast channel can be seen as a group of interest or as a subnet. A single node can be active on many multicast channels.

There is no quarantined delivery of a VSCP event when using multicast functionality. This however, most of the time, does not impose a problem as the VSCP protocol functionality often rely on responses back when sending events and therefore have a way to detect am event that gone lost. This must however be kept in mind when designing systems around this functionality.


Multicast frames can be encrypted using AES128, AES192, AES256 for state of art security.

{% include "./bottom_copyright.md" %}
