# VSCP Tables

**Preliminary information that still may change**

VSCP tables is a built in feature of the VSCP daemon that let you collect data (measurements) from events in a SQL database over time automatically. The only thing you need to do is to add a VSCP decision matrix entry for the collection and a definition of your collection to the configuration.

You can build two types of tables


*  **Dynamic table** which works like any other database and save data in ever growing database.

*  **Static table** which is a table with a static number of record. A table of this type can for example collect temperatures from temperature sensor over the last 24 hours.

*  **Max table** which is a table that grows up to a specified **size** of elements and then clear all elements and start to fill the table again.

The collected data can be reached over


*  The tcp/ip interface.

*  The REST interface.

*  The websocket interface.

*  You can also read/write table data from Javascripts and LUA scripts.

Over the interfaces you can do statistical analysis of the data but the main use for the collected data is to display it in a user interface element such as a diagram or a table. The way VSCP handles measurements one display solution will work for all types of measurements. For a JavaScript application data over specific ranges or hole (static) tables can be fetched in an easy way over the REST or the websocket API's. Examples are provided. For higher level languages such as C/C++/C#/Java/Python etc the VSCP helper library is a great tool.

Tables are stored in


*  **/srv/vscp/tables** on Linux type systems.

*  **/programdata/vscp/tables** on Windows systems.

*  **In memory** on both Linux type and Windows systems.

The in memory type is very fast but is of course not persistent over time.

## Configure a tables

You can define and configure tables in the main configuration file vscpd.xml or in the configuration database. Definitions in the xml file override conflicting definitions in the database configuration file. 

Changes done in the VSCP administrative interface goes to the configuration database file.

The table definitions in [the configuration file is described here](http://www.vscp.org/docs/vscpd/doku.php?id=configuring_the_vscp_daemon#tables).

## Collect data

[described here](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_decision_matrix#write_table).

\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
