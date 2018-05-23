# VSCP Daemon REST interface security 

The REST interface is protected by a user/password pair. The username is sent a digest over the net but the password is a hash over "username:authdomain|raltext-password".((authdomain is described here http://www.vscp.org/docs/vscpd/doku.php?id=configuring_the_vscp_daemon#configuration))

I addition to the username/password which also groups users in security levels it is possible to have table where the hosts allowed to connect to the system is stored.

In addition to this SSL can be enabled on the interface.

Also a privilege based system is used to protect critical functionality. A user need a specific privilege to send an event for example and can be set up to be allowed just to send a limited set of events. Also a filter on incoming events is possible to set up to limit what a user can receive.

Remote user settings are configured [here](http://www.vscp.org/docs/vscpd/doku.php?id=configuring_the_vscp_daemon&#remote_user_settings).

Put together this makes the VSCP Daemon one of the safest systems to use for remote maintenance of IoT/m2m systems.

\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
