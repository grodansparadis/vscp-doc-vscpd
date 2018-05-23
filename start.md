![Very Simple Control Protocol](./images/logo_100.png "Very Simple Control Protocol") 

# the VSCP Server

**Reversion**: 13.0 [history](history)

Copyright © 2000-2018 Åke Hedman, [Paradise of the Frog AB](https://www.grodansparadis.com), `<[akhe@paradiseofthefrog.com](akhe@paradiseofthefrog.com)>`  


# Abstract

The VSCP daemon is an open source server program that is part of [VSCP & Friends](https://www.vscp.org) and is built and maintained by [Grodans Paradis AB](https://www.grodansparadis.com). The server act as a hub and collects information from different sources and let clients collect this information over a TCP/IP, websocket, REST interface etc and makes it easy to present or work on this date in real time. The daemon also has an internal scheduler that makes it possible to control different scenarios such as simple tasks like to automatically turn on a group of lamps at a specific time of the day or do complex industrial control tasks.

On Unix systems the daemon is a standard server application that is started in the background. It is possible also to compile it to start as a standard application if that way of running it is preferred.

On Windows the daemon is available as a standard Windows service and as a standard application. Normally the standard application is not used, but for debugging and testing the application can be useful.

The daemon uses simple to construct, yet very capable, drivers to talk to the real world. This means that a driver abstract real world things to look to the system as any other VSCP enabled device even if it itself has no knowledge what so ever about VSCP




{% include "./bottom_copyright.md" %}


