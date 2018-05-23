# VSCP Daemon Level I Drivers

This is just a .dll (Windows) or a .so (Linux) file with the CANAL interface exported. The interface is described [here](CANAL Interface Specification). Several Level I driver comes with the VSCP & Friends package.

The good thing with the Level I interface is that you can add the .dll or .so as a driver to VSCP daemon or use the dll/do directly from your own application such and in VSCP Works. 

The drivers are configured in the vscpd.conf file (format is [here](http://www.vscp.org/docs/vscpd/doku.php?id=configuring_the_vscp_daemon)). If you use more then one driver with different configuration it is very important that the prefix is set to different values for each of them. The prefix is prepended to a variable name before it is fetched from the daemon or set for that matter.

To make a Level I driver just create a dynamically linked library that export the CANAL interface. There are plenty of examples to use as a starting point for creating your own driver in the [source tree for the VSCP & Friends package at GitHub](https///github.com/grodansparadis/vscp_software). Look in  [src/vscp/drivers/level1](https///github.com/grodansparadis/vscp_software/tree/master/src/vscp/drivers/level1) folder.

For Python developers [python-can](http://python-can.readthedocs.io/en/latest/index.html) is a good tool. __Unfortunately__ the CANAL interface is names USB2CAN but it is there.


*  [8Devices USB2CAN Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_usb2can)

*  [Apox Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_apox)

*  [CAN4VSCP Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_can4vscp)

*  [CCS CAN Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_ccs)

*  [IXATT VCI Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_ixxat)

*  [Lawicel CAN232 Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_can232)

*  [Lawicel CANUSB Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_canusb)

*  [LIRC Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_lirc)

*  [Logger Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_logger)

*  [PEAK CAN Adapter Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_peak)

*  [Socketcan Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_socketcan)

*  [Tellstick Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_tellstick)

*  [Vector CAN Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_vector)

*  [Zanthic CAN Driver](http://www.vscp.org/docs/vscpd/doku.php?id=level1_driver_zanthic)
 
{% include "./bottom_copyright.md" %}
