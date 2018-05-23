# Remote Variables 

Remote variables is a very powerful feature of the VSCP Daemon. At first they are often neglected as something exotic but if looking at them a bit closer one soon find that they are actually a very useful tool. Variables is just persistent typed objects that can be reached and/or read/updated from remote interfaces or updated when things happen in the system. A typical variable can be the state of a physical thing out in the world. The “thing” updates it's status from time to time and then also updates the variable. One can therefore just read the variable to know the last state of the "thing". Valuable when a software start from being down so it can get an initial state or for keeping track of the state of "things" that is not always connected.

A variable may also for example hold the energy consumption over a month of a year. When energy consumption events comes in to the system they are just added to this variable. In short variables can be viewed as a sort of database but with discrete values.

In the decision matrix you can


*  Store a value to a variable
*  Add a value to a variable
*  Subtract a value from a variable
*  Multiply a value to a variable.
*  Divide a value with a variable.
*  Make decisions based on variable values.
*  Read/Write variables in LUA scripts.

The first time variable is used it is constructed. So if you for example add a value to a variable that does not exist it will first be created. For add/subtract/multiply/divide variables that does not exist will be created as a floating point value. The store variable on the other hand let you select the type.


Note that there is possible to create dynamically created variables by using the [available escapes](decision_matrix_variables.md#variable_substitution_for_parameters). As an example a variable **energy_usage_%monthtxtfull_%year** can be created that will have names like "//energy_usage_october_2014//", *energy_usage_november_2014*". So if you create a decision matrix entry that trigger on the **CLASS1.MEASUREMENT, Type=13, Energy** and where the action adds the measurement to the variable  **energy_usage_%monthtxtfull_%year** you will get the energy usage for each month of a year in it's own clearly named variable. Variables that can be fetched and presented to a user in a diagram for example.

## Variable types

Action that store variables and variables that are written in the the [TCP/IP interface](https://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_tcp_ip_protocol_description#variable) and in the [websocket interface](https://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_websocket_protocol_description) have a string format. This format is described in the table below

**Note** Types with **base64**=//yes// will be read (and should be set) as base64 encoded values.

The second boolean parameter of the string form is persistent (true) or non persistent (false). A persistent variable is saved on disk, a non persistent variable is only kept in memory and will be lost on a restart of the software. 

 | Variable Type           | Numerical code | Base64 | Type token               | String Format                                                                                                        |                          
 | -------------           | -------------- | ------ | ----------               | -------------                                                                                                        |                          
 | **string**              | 1              | Yes    | STRING                   | STRING`<nowiki>`                                                                                                       | `</nowiki>`1;true`<nowiki>`   | `</nowiki>`false;0;0x777;"some kind of BASE64 encoded string"                         |               
 | **bool**                | 2              | No     | BOOL                     | BOOL`<nowiki>`                                                                                                         | `</nowiki>`2;true`<nowiki>`   | `</nowiki>`false;0;0x777;true`<nowiki>`                                                 | `</nowiki>`false | 
 | **integer**             | 3              | No     | INT/INTEGER              | INT`<nowiki>`                                                                                                          | `</nowiki>`2;true`<nowiki>`   | `</nowiki>`false;0;0x777;integer-number                                               |               
 | **long**                | 4              | No     | LONG                     | LONG`<nowiki>`                                                                                                         | `</nowiki>`4;true`<nowiki>`   | `</nowiki>`false;0;0x777;long-integer-number                                          |               
 | **float**               | 5              | No     | FLOAT/DOUBLE             | DOUBLE`<nowiki>`                                                                                                       | `</nowiki>`5;true`<nowiki>`   | `</nowiki>`false;0;0x777;decimal-number                                               |               
 | **measurement**         | 6              | No     | MEASUREMENT              | MEASUREMENT`<nowiki>`                                                                                                  | `</nowiki>`6;true`<nowiki>`   | `</nowiki>`false;0;0x777;value,unit,sensor-index,zone,subzone                         |               
 | **event**               | 7              | No     | EVENT                    | EVENT`<nowiki>`                                                                                                        | `</nowiki>`7;true`<nowiki>`   | `</nowiki>`false;0;0x777;head,class;type,obid,datetime,timestamp,GUID,data1,data2,... |               
 | **VSCP GUID**           | 8              | No     | GUID/EVENTGUID           | GUID`<nowiki>`                                                                                                         | `</nowiki>`8;true`<nowiki>`   | `</nowiki>`false;0;0x777;00:00:EA:B8:76:77:30:37:81:00:7C:C7:87:02:B0:17              |               
 | **VSCP Data**           | 9              | No     | DATA/EVENTDATA           | DATA`<nowiki>`                                                                                                         | `</nowiki>`9;true`<nowiki>`   | `</nowiki>`false;0;0x777;data1,data2,data3,...                                        |               
 | **VSCP Class**          | 10             | No     | VSCPCLASS/EVENTCLASS     | VSCPCLASS`<nowiki>`                                                                                                    | `</nowiki>`10;true`<nowiki>`  | `</nowiki>`false;0;0x777;integer-number                                               |               
 | **VSCP Type**           | 11             | No     | VSCPTYPE/EVENTTYPE       | VSCPTYPE`<nowiki>`                                                                                                     | `</nowiki>`11;true`<nowiki>`  | `</nowiki>`false;0;0x777;integer-number                                               |               
 | **VSCP timestamp**      | 12             | No     | TIMESTAMP/EVENTTIMESTAMP | TIMESTAMP`<nowiki>`                                                                                                    | `</nowiki>`12;true`<nowiki>`  | `</nowiki>`false;0;0x777;integer-number                                               |               
 | **Date and time**       | 13             | No     | DATETIME                 | DATETIME`<nowiki>`                                                                                                     | `</nowiki>`13;true`<nowiki>`  | `</nowiki>`false;;0;0x7772014-09-26T13:05:01                                          |               
 | **Date**                | 14             | No     | DATE                     | DATE`<nowiki>`                                                                                                         | `</nowiki>`15;true`<nowiki>`  | `</nowiki>`false;0;0x777;2014-09-26                                                   |               
 | **Time**                | 15             | No     | TIME                     | TIME`<nowiki>`                                                                                                         | `</nowiki>`16;true`<nowiki>`  | `</nowiki>`false;0;0x777;13:05:01                                                     |               
 | **Base64 encoded blob** | 16             | Yes    | BLOB                     | BASE64`<nowiki>`                                                                                                       | `</nowiki>`13;true`<nowiki>`  | `</nowiki>`false;0;0x777;Base64 data                                                  |               
 | **MIME encoded**        | 100            | Yes    | MIME                     | MIME`<nowiki>`                                                                                                         | `</nowiki>`100;true`<nowiki>` | `</nowiki>`false;0;0x777;mime-identifier;base64 encoded content                       |               
 | **HTML encoded**        | 101            | Yes    | HTML                     | HTML`<nowiki>`                                                                                                         | `</nowiki>`101;true`<nowiki>` | `</nowiki>`false;0;0x777;true if escaped;base64 encoded content                       |               
 | **Javascript encoded**  | 102            | Yes    | JAVASCRIPT               | JAVASCRIPT`<nowiki>`                                                                                                   | `</nowiki>`101;true`<nowiki>` | `</nowiki>`false;0;0x777;true if escaped;base64 encoded content                       |               
 | **LUA script**          | 200            | Yes    | LUA                      | LUA`<nowiki>`                                                                                                          | `</nowiki>`200;true`<nowiki>` | `</nowiki>`false;0;0x777;true if escaped;script-content                               |               
 | **LUA script result**   | 201            | Yes    | LUARES                   | LUARES`<nowiki>`                                                                                                       | `</nowiki>`200;true`<nowiki>` | `</nowiki>`false;0;0x777;true if escaped;script-content                               |               
 | **UX type 1**           | 300            | Yes    | UXTYPE1                  | UXTYPE1`<nowiki>`                                                                                                      | `</nowiki>`300;true`<nowiki>` | `</nowiki>`false;0;0x777;UX-description base 64 encoded                               |               
 | **DM row**              | 500            | Yes    | DMROW                    | ;0;0x777;enabled,from,to,weekday,time,mask,filter,index,zone,sub-zone,control-code,action-code,action-param,comment. |                          
 | **Driver**              | 501            | Yes    | DRIVER                   | ;0;0x777;A comma separated driver row.                                                                               |                          
 | **User**                | 502            | Yes    | USER                     | ;0;0x777;name;password;fullname;filter-mask;rights;remotes;events;note                                               |                          
 | **Filter**              | 503            | Yes    | FILTER                   | ;0;0x777;'filter-priority, filter-class, filter-type, filter-GUID'.                                                  |                          

The *0;0x777* above is user=0 and user rights = 0x777 = all read/write/delete.


You can use either the numerical type (**"1"** for the string type for example) or the type token (**"STRING"** for the string type for example). So a string can be defined either as 
    STRING;true;0;0x777;c29tZSBraW5kIG9mIHN0cmluZw==
or as 
    1;true;0;0x777;c29tZSBraW5kIG9mIHN0cmluZw==
where 
    c29tZSBraW5kIG9mIHN0cmluZw==
is the string content
    “some kind of string”
    

**Notes**

*  GUID is always on the form "FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF:FF" or "-" where the dash means "use the interface GUID".

*  Data of an event will always be a comma separated list of data with variable length where the length depends on how many data bytes the event actually have.

*  Complete list of MIME codes is [here](http://www.sitepoint.com/web-foundations/mime-types-complete-list/).

## Reset variable values

To reset a variable may seem a strange thing to do. But it is just setting it's value to a known default value. The reset variable command available in the [TCP/IP interface]() and the [websocket interface](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_vscp_websocket_interface) set variables to the following values. 

 | Variable            | type | Reset value                                                           | 
 | --------            | ---- | -----------                                                           | 
 | string              | 1    | Empty string                                                          | 
 | bool                | 2    | "false"                                                               | 
 | int                 | 3    | zero                                                                  | 
 | long                | 4    | zero                                                                  | 
 | float               | 5    | zero                                                                  | 
 | measurement         | 6    | value=0, unit=0,sensorindex=0, zone=0, subzone=0                      | 
 | event               | 7    | all values set to zero                                                | 
 | VSCP GUID           | 8    | set to zero                                                           | 
 | VSCP Data           | 9    | Set to zero                                                           | 
 | VSCP Class          | 10   | Set to zero                                                           | 
 | VSCP Type           | 11   | Set to zero                                                           | 
 | VSCP timestamp      | 12   | Set to zero                                                           | 
 | Date and time       | 13   | Set to current date + time in ISO format. **YYYY-MM-DDTHH:MM:SS.sss** | 
 | Date                | 14   | Set to current date in ISO format. **YYYY-MM-DD**                     | 
 | Time                | 15   | Set to current time in ISO format. **HH:MM:SS.sss**                   | 
 | Base64 encoded blob | 16   | Empty                                                                 | 
 | MIME encoded        | 100  | Empty                                                                 | 
 | HTML encoded        | 101  | Empty                                                                 | 
 | Javascript encoded  | 102  | Empty                                                                 | 
 | LUA script          | 200  | Empty                                                                 | 
 | UX Type1            | 300  | Empty                                                                 | 
 | DM row              | 500  | Empty                                                                 | 
 | Driver              | 501  | Empty                                                                 | 
 | User                | 502  | Empty                                                                 | 
 | Filter              | 503  | Empty                                                                 | 
## XML storage format

The main storage for persistent variables from version 1.12.10 is in a database. But variables can still be loaded/save from/to XML files. One typical use can be to load initialised non-persistent variables into memory on start up. Loaded persistent variables will be written to persistent storage and if already available in the database there value will be updated with the XML version. 

`<code=xml>`
`<?xml version="1.0" encoding="utf-8"?>`

`<variables>` `<!-- <persistent>` is an older form --> 

    `<!-- Modern format -->`
    <variable name="variable name"
              type="numerical type|textual type" 
              persistent="true|false"  
              user="user who owns the variable" 
              access-rights="accessrights for variable" 
              value="variable value, some value types should be base64 encoded."
              note="note about variable"  
              note-base64="base64 encoded note (saved in this form)" >
    `</variable>`

    `<!-- Legacy format  -->` 
    `<variable type="string" user="12" access-rights="777" >`                  
        `<name>`testvariable_string`</name>`         
        `<value>`String value`</value>`
        `<note>`note about variable`</note>`    
    `</variable>`

`</variables>`
`</code>` 

## Non-persistent variables

Non persistent variables is stored in RAM and will disappear when the VSCP daemon is restarted. They are therefore mostly used for session data and similar things.

## Persistent variables

Persistent variables is stored in a persistent way. They will survive VSCP Daemon restarts.

## Read only variables

Read only variables can only be read not changed. The typical use is for most stock variables generated by the daemon itself. 

## Access rights for variables

Access rights are given in the Unix format uuugggooo, where uuu is owner rights, gggg is group rights (currently no use) and ooo rights for other. Each part then is rwx for read, write and execute. So 7 is the same as all rights allowed and 0 none. Or 777 to allow everyone to do anything. A zero makes it possible only for the admin user to do things with the variable. Execute have meaning for LUA and Javascript execution.

## Stock variables

Stock variables is variables that are generated dynamically by the VSCP daemon. They are therefore always non-persistent in there nature but is always available if the feature they belong to is enabled. 

In the stock variables you can get information about most configuration variables of the VSCP daemon and also about dynamic things that happen inside the system such as when the last heartbeat event was sent.

Here is a list of defined stock variables.

### Version and copyright information

 | Variable                           | Type    | Description                                                                        | 
 | --------                           | ----    | -----------                                                                        | 
 | **vscp.version.major**             | Integer | Major version for the VSCP & Friends system.                                       | 
 | **vscp.version.minor**             | Integer | Minor version for the VSCP & Friends system.                                       | 
 | **vscp.version.release**           | Integer | Release version for the VSCP & Friends system.                                     | 
 | **vscp.version.build**             | Integer | Build version for the VSCP & Friends system.                                       | 
 | **vscp.version.str**               | String  | Version for the VSCP & Friends system in string form.                              | 
 | **vscp.copyright**                 | String  | Copyright for the VSCP & Friends system.                                           | 
 | **vscp.wxwidgets.version.major**   | Integer | Major version for the wxWidgets library.                                           | 
 | **vscp.wxwidgets.version.minor**   | Integer | Minor version for the wxWidgets library.                                           | 
 | **vscp.wxwidgets.version.release** | Integer | Release version for the wxWidgets library.                                         | 
 | **vscp.wxwidgets.version.sub**     | Integer | Sub version for the wxWidgets library.                                             | 
 | **vscp.wxwidgets.version.str**     | String  | Version for the wxWidgets library in string form.                                  | 
 | **vscp.wxwidgets.copyright**       | String  | Copyright for the wxWidgets library.                                               | 
 | **vscp.lua.version.major**         | Integer | Major version for the LUA library. **Only available if LUA support is enabled**.   | 
 | **vscp.lua.version.minor**         | Integer | Minor version for the LUA library. **Only available if LUA support is enabled**.   | 
 | **vscp.lua.version.release**       | Integer | Release version for the LUA library. **Only available if LUA support is enabled**. | 
 | **vscp.lua.version.str**           | String  | Version for the LUA library. **Only available if LUA support is enabled**.         | 
 | **vscp.lua.copyright**             | String  | Copyright for the LUA library. **Only available if LUA support is enabled**.       | 
 | **vscp.mongoose.version.str**      | String  | Version for the Mongoose library in string form.                                   | 
 | **vscp.mongoose.copyright**        | String  | Copyright for the Mongoose library.                                                | 
 | **vscp.duktape.version.major**     | Integer | Major version for the Duktape library.                                             | 
 | **vscp.duktape.version.minor**     | Integer | Minor version for the Duktape library.                                             | 
 | **vscp.duktape.version.release**   | Integer | Release version for the Duktape library.                                           | 
 | **vscp.duktape.version.str**       | String  | Version for the Duktape library.                                                   | 
 | **vscp.duktape.copyright**         | String  | Copyright for the Duktape library.                                                 | 
 | **vscp.sqlite.version.major**      | Integer | Major version for the SQLite library.                                              | 
 | **vscp.sqlite.version.minor**      | Integer | Minor version for the SQLite library.                                              | 
 | **vscp.sqlite.version.release**    | Integer | Release version for the SQLite library.                                            | 
 | **vscp.sqlite.version.build**      | Integer | Build version for the SQLite library.                                              | 
 | **vscp.sqlite.version.str**        | String  | Version for the SQLite library.                                                    | 
 | **vscp.sqlite.copyright**          | String  | Copyright for the SQLite library.                                                  | 
 | **vscp.openssl.version.str**       | String  | Version for Openssl library.                                                       | 
 | **vscp.openssl.copyright**         | String  | Copyright for Openssl library.                                                     | 
 | **vscp.civitweb.copyright**        | String  | Copyright for Civitweb library (forked from ver. 1.10).                            | 







### System information

 | Variable                            | Type    | Description                                                                                                                                    | 
 | --------                            | ----    | -----------                                                                                                                                    | 
 | **vscp.version.os**                 | String  | Operation system version string.                                                                                                               | 
 | **vscp.os.width**                   | Integer | **32** or **64**.                                                                                                                              | 
 | **vscp.os.width.is32bit**           | Boolean | True if system is a 32-bit system.                                                                                                             | 
 | **vscp.os.width.is64bit**           | Boolean | True if system is a 64-bit system.                                                                                                             | 
 | **vscp.os.width.str**               | String  | **"32-bit"** or **"64-bit"**.                                                                                                                  | 
 | **vscp.os.endiness.str**            | String  | **"Little endian"** or **"Big endian"**.                                                                                                       | 
 | **vscp.os.endiness.isLittleEndian** | Boolean | True if system is little endian.                                                                                                               | 
 | **vscp.host.name**                  | String  | Full system name.                                                                                                                              | 
 | **vscp.host.ip**                    | String  | IP-address for system ("a.b.c.d").                                                                                                             | 
 | **vscp.host.mac**                   | String  | MAC address for network card on standard form "AA:BB:CC:DD:EE:FF". May not be available and in that case it is reported as "00:00:00:00:00:00" | 
 | **vscp.host.userid**                | String  | The user the VSCP daemon is running as.                                                                                                        | 
 | **vscp.host.username**              | String  | Full name of user.                                                                                                                             | 
 | **vscp.host.guid**                  | GUID    | GUID for VSCP daemon on the standard form AA:BB:CC:DD:EE:....                                                                                  | 
 | **vscp.loglevel**                   | Integer | [Log level](http://www.vscp.org/docs/vscpd/doku.php?id=configuring_the_vscp_daemon#loglevel) for VSCP daemon.                                  | 
 | **vscp.loglevel.str**               | String  | [Log level](http://www.vscp.org/docs/vscpd/doku.php?id=configuring_the_vscp_daemon#loglevel) in string form.                                   | 
 | **vscp.client.receivequeue.max**    | Integer | Max allowed events in receive queue.                                                                                                           | 
 | **vscp.host.root.path**             | String  | VSCP daemon working folder                                                                                                                     | 

### TCP/IP

 | Variable              | Type   | Description                   | 
 | --------              | ----   | -----------                   | 
 | **vscp.tcpip.addess** | String | Address for TCP/IP interface. | 

### Multicast

 | Variable                  | Type   | Description                      | 
 | --------                  | ----   | -----------                      | 
 | **vscp.multicast.addess** | String | Address for multicast interface. | 
 | **vscp.multicast.ttl**    | String | Multicast time to live.          | 

### UDP

 | Variable            | Type    | Description                       | 
 | --------            | ----    | -----------                       | 
 | **vscp.udp.enable** | Boolean | True if UDP interface is enabled. | 
 | **vscp.udp.addess** | String  | Address for UDP interface.        | 





### Discovery

 | Variable                  | Type    | Description                             | 
 | --------                  | ----    | -----------                             | 
 | **vscp.discovery.enable** | Boolean | True if discovery mechanism is enabled. | 

### Automation

*Only available if automation subsystem is enabled.*

 | Variable                                           | Type     | Description                                                                                         | 
 | --------                                           | ----     | -----------                                                                                         | 
 | **vscp.automation.calc.last**                      | DateTime | Date time for last calculation                                                                      | 
 | **vscp.automation.longitude**                      | Double   | Set longitude for automation system.                                                                | 
 | **vscp.automation.latitude**                       | Double   | Set latitude for automation system.                                                                 | 
 | **vscp.automation.heartbeat.enable**               | Boolean  | Heartbeats are enabled.                                                                             | 
 | **vscp.automation.heartbeat.period**               | Long     | Period in seconds for heartbeats.                                                                   | 
 | **vscp.automation.heartbeat.last**                 | DateTime | Date and time when last heartbeat was sent by the system.                                           | 
 | **vscp.automation.segctrl.heartbeat.enable**       | Boolean  | Segment controller heartbeats are enabled.                                                          | 
 | **vscp.automation.segctrl.heartbeat.period**       | Long     | Period in seconds for segment controller heartbeats.                                                | 
 | **vscp.automation.segctrl.heartbeat.last**         | DateTime | Date and time when last segment controller heartbeat was sent by the system.                        | 
 | **vscp.automation.daylength**                      | String   | Holds calculated length of day as "hours:minutes".                                                  | 
 | **vscp.automation.declination**                    | Double   | Holds calculated [declination](https///en.wikipedia.org/wiki/Declination) in floating point format. | 
 | **vscp.automation.sun.max.altitude**               | Double   | Holds max altitude for the sun this day in floating point format.                                   | 
 | **vscp.automation.twilightsunrise.event.enable **  | Boolean  | True if twilight unrise event is enabled.                                                           | 
 | **vscp.automation.twilightsunrise**                | Time     | Time for twilight sunrise in ISO time format.                                                       | 
 | **vscp.automation.twilightsunrise.event.sent**     | DateTime | Date and time when last twilight sunrise event was sent.                                            | 
 | **vscp.automation.sunrise.event.enable **          | Boolean  | True if sunrise event is enabled.                                                                   | 
 | **vscp.automation.sunrise**                        | Time     | Time for sunrise in ISO time format.                                                                | 
 | **vscp.automation.sunrise.event.sent**             | DateTime | Date and time when last sunrise event was sent.                                                     | 
 | **vscp.automation.sunset.event.enable **           | Boolean  | True if sunset event is enabled.                                                                    | 
 | **vscp.automation.sunset**                         | Time     | Time for sunset in ISO time format.                                                                 | 
 | **vscp.automation.sunset.event.sent**              | DateTime | Date and time when last sunset event was sent.                                                      | 
 | **vscp.automation.twilightsunset.event.enable **   | Boolean  | True if twilight sunset event is enabled.                                                           | 
 | **vscp.automation.twilightsunset**                 | Time     | Time for twilight sunset in ISO time format.                                                        | 
 | **vscp.automation.twilight.event.sent**            | DateTime | Date and time when last twilight sunset event was sent.                                             | 
 | **vscp.automation.calculatednoon.event.enable**    | Boolean  | Enable send of calculated noon even.                                                                | 
 | **vscp.automation.calculatednoonevent.event.last** | DateTime | Date and time when last calculated noon event was sent.                                             | 
### Web server

 | Variable                                 | Type    | Description                             | 
 | --------                                 | ----    | -----------                             | 
 | **vscp.websrv.address**                  | String  | Web server address.                     | 
 | **vscp.websrv.authenticationOn**         | Boolean | True if authentication is enabled.      | 
 | **vscp.websrv.root.path**                | String  | Rootfolder for web server.              | 
 | **vscp.websrv.cert.path**                | String  | Path to certificates.                   | 
 | **vscp.websrv.extramimetypes**           | String  | Extra mime types.                       | 
 | **vscp.websrv.ssipatterns**              | String  | SSI patterns.                           | 
 | **vscp.websrv.ipacl**                    | String  | ACL on ip.                              | 
 | **vscp.websrv.cgi.interpreter.path**     | String  | Path CGI interpreter.                   | 
 | **vscp.websrv.cgi.pattern**              | String  | CGI pattern.                            | 
 | **vscp.websrv.directorylistings.enable** | Boolean | True if directory listings are enabled. | 
 | **vscp.websrv.hidefile.pattern**         | String  | Patterns for files to hide.             | 
 | **vscp.websrv.indexfiles**               | String  | List of index files.                    | 
 | **vscp.websrv.urlrewrites**              | String  | URL rewrites.                           | 
 | **vscp.websrv.auth.file.directory**      | String  | Directory authentication file.          | 
 | **vscp.websrv.auth.file.global**         | String  | Global authentication file.             | 


### MQTT server

 | Variable                     | Type    | Description                                          | 
 | --------                     | ----    | -----------                                          | 
 | **vscp.mqtt.server.enable**  | Boolean | Enable internal MQTT server (broker) functionality). | 
 | **vscp.mqtt.server.address** | String  | Address for internal MQTT server (broker).           | 

### CoAP server

 | Variable                     | Type    | Description                                 | 
 | --------                     | ----    | -----------                                 | 
 | **vscp.coap.server.enable**  | Boolean | Enable internal CoAP server functionality). | 
 | **vscp.coap.server.address** | String  | Address for internal CoAP server .          | 
 
### Websockets

 | Variable                       | Type    | Description                                                    | 
 | --------                       | ----    | -----------                                                    | 
 | **vscp.websocket.auth.enable** | Boolean | True if authentication for the websocket subsystem is enabled. | 




### Decision matrix

 | Variable                                         | Type     | Description                                                                                                                                                                                                         | 
 | --------                                         | ----     | -----------                                                                                                                                                                                                         | 
 | **vscp.dm.db.path**                              | String   | Path to DM database.                                                                                                                                                                                                | 
 | **vscp.dm.xml.path**                             | String   | Path to static XML variable file which is optionally read at startup.                                                                                                                                               | 
 | **vscp.dm.allow.xml.save**                       | Boolean  | Allow DM XML file save after edit/delete if true.                                                                                                                                                                   | 
 | **vscp.dm.count**                                | Integer  | Number of elements in decision matrix. Can only be read.                                                                                                                                                            | 
 | **vscp.dm.count.active**                         | Integer  | Number of elements in decision matrix that is currently enabled. Can only be read.                                                                                                                                  | 
 | **vscp.dm.**//n//[.field]                        | String   | Decision matrix field. n represent the record. A field name can optionally be given which selects that field. Without the optional field a comma separated list with all values (see after table) is used as value. | 
 | **vscp.dm.**//n//**.id**                         | String   | Database record id for the DM row. *n* is record number.                                                                                                                                                          | 
 | **vscp.dm.**//n//**.bEnable**                    | Boolean  | Enable (true) for the DM row. *n* is record number.                                                                                                                                                               | 
 | **vscp.dm.**//n//**.groupid**                    | String   | Group-id for the DM row. *n* is record number.                                                                                                                                                                    | 
 | **vscp.dm.**//n//**.mask.priority**              | Integer  | Mask for priority for the DM row. *n* is record number.                                                                                                                                                           | 
 | **vscp.dm.**//n//**.mask.class**                 | Long     | Mask for class for the DM row. *n* is record number.                                                                                                                                                              | 
 | **vscp.dm.**//n//**.mask.type**                  | Long     | Mask for type for the DM row. *n* is record number.                                                                                                                                                               | 
 | **vscp.dm.**//n//**.mask.guid**                  | GUID     | Mask for GUID for the DM row. *n* is record number.                                                                                                                                                               | 
 | **vscp.dm.**//n//**.filter.priority**            | Integer  | Filter for priority for the DM row. *n* is record number.                                                                                                                                                         | 
 | **vscp.dm.**//n//**.filter.class**               | Long     | Filter for class for the DM row. *n* is record number.                                                                                                                                                            | 
 | **vscp.dm.**//n//**.filter.type**                | Long     | Filter for type for the DM row. *n* is record number.                                                                                                                                                             | 
 | **vscp.dm.**//n//**.filter.guid**                | GUID     | Filter for GUID for the DM row. *n* is record number.                                                                                                                                                             | 
 | **vscp.dm.**//n//**.allowed.start**              | DateTime | Startdate for the DM row. *n* is record number.                                                                                                                                                                   | 
 | **vscp.dm.**//n//**.allowed.end**                | DateTime | Enddate for the DM row. *n* is record number.                                                                                                                                                                     | 
 | **vscp.dm.**//n//**.allowed.monday**             | Boolean  | True if action can happen on Mondays for the DM row. *n* is record number.                                                                                                                                        | 
 | **vscp.dm.**//n//**.allowed.tuesday**            | Boolean  | True if action can happen on Tuesday for the DM row. *n* is record number.                                                                                                                                        | 
 | **vscp.dm.**//n//**.allowed.wednesday**          | Boolean  | True if action can happen on Wednesday for the DM row. *n* is record number.                                                                                                                                      | 
 | **vscp.dm.**//n//**.allowed.thursday**           | Boolean  | True if action can happen on Thursday for the DM row. *n* is record number.                                                                                                                                       | 
 | **vscp.dm.**//n//**.allowed.friday**             | Boolean  | True if action can happen on Friday for the DM row. *n* is record number.                                                                                                                                         | 
 | **vscp.dm.**//n//**.allowed.saturday**           | Boolean  | True if action can happen on Saturday for the DM row. *n* is record number.                                                                                                                                       | 
 | **vscp.dm.**//n//**.allowed.sunday**             | Boolean  | True if action can happen on Sunday for the DM row. *n* is record number.                                                                                                                                         | 
 | **vscp.dm.**//n//**.allowed.time**               | String   | Allowed time for the DM row. *n* is record number.                                                                                                                                                                | 
 | **vscp.dm.**//n//**.bCheckIndex**                | Boolean  | Flag for index check for the DM row. *n* is record number.                                                                                                                                                        | 
 | **vscp.dm.**//n//**.index**                      | Integer  | Index for the DM row. *n* is record number.                                                                                                                                                                       | 
 | **vscp.dm.**//n//**.bCheckZone**                 | Boolean  | Flag for zone check for the DM row. *n* is record number.                                                                                                                                                         | 
 | **vscp.dm.**//n//**.zone**                       | Integer  | Zone for the DM row. *n* is record number.                                                                                                                                                                        | 
 | **vscp.dm.**//n//**.bCheckSubZone**              | Boolean  | Flag for sub zone check for the DM row. *n* is record number.                                                                                                                                                     | 
 | **vscp.dm.**//n//**.subzone**                    | Integer  | Subzone for the DM row. *n* is record number.                                                                                                                                                                     | 
 | **vscp.dm.**//n//**.measurement.value**          | Double   | Measurement value for the DM row. *n* is record number.                                                                                                                                                           | 
 | **vscp.dm.**//n//**.measurement.unit**           | Integer  | Measurement unit code for the DM row. *n* is record number.                                                                                                                                                       | 
 | **vscp.dm.**//n//**.measurement.compare**        | Integer  | Measurement compare code for the DM row. *n* is record number.                                                                                                                                                    | 
 | **vscp.dm.**//n//**.measurement.compare.string** | Integer  | Measurement compare in string form for the DM row. *n* is record number.                                                                                                                                          | 
 | **vscp.dm.**//n//**.measurement.comment**        | String   | Comment for the DM row. *n* is record number.                                                                                                                                                                     | 
 | **vscp.dm.**//n//**.count.trigger**              | Long     | Number of times this rows action has been performed. *n* is record number.                                                                                                                                        | 
 | **vscp.dm.**//n//**.count.error**                | Long     | Number of times this rows action has resulted in an error. *n* is record number.                                                                                                                                  | 
 | **vscp.dm.**//n//**.error**[.string]             | String   | Last error string. *n* is record number.                                                                                                                                                                          | 

Requesting the variable **vscp.dm.**//n// will give the following list. The same list format is used for writing a value to this variable.

	
	  id;bEnable;groupid;mask-priority;mask-class;mask-type;mask-guid;filter-priority;filter-class;filter-type;filter-guid;
	  allowed-start;allowed-end;allowed-monday;allowed-tuesday;allowed-wednesday;allowed-thursday;allowed-friday;
	  allowed-saturday;allowed-sunday;allowedtime;bCheckIndex;index;bCheckZone;zone;bCheckSubZone;subzone;
	  bCheckMeasurementIndex;measurement-index;actioncode;actionparameter;measurement_value;measurement_unit;
	  measurement_compare;comment

### Variables

 | Variable                   | Type   | Description                        | 
 | --------                   | ----   | -----------                        | 
 | **vscp.variable.xml.path** | String | Path to XML variable read in file. | 
 | **vscp.variable.db.path**  | String | Path to variable database.         | 
### Logging

 | Variable                     | Type   | Description                                                              | 
 | --------                     | ----   | -----------                                                              | 
 | **vscp.log.syslog.enable**   | Bool   | Enable syslog.                                                           | 
 | **vscp.log.database.enable** | Bool   | Enable to send log data to a database instead of to separate text files. | 
 | **vscp.log.database.count**  | Long   | Number of elements in database log. Can only be read.                    | 
 | **vscp.log.database.path**   | String | Path to logging database.                                                | 

### Database

 | Variable                           | Type   | Description                                                | 
 | --------                           | ----   | -----------                                                | 
 | **vscp.database.vscpdata.path**    | String | Path to VSCP data database containing class/type info etc. | 
 | **vscp.database.vscpdconfig.path** | String | Path to VSCP daemon database containing settings etc.      | 




### Drivers

Must be administrator or part of the administrator group to access.

 | Variable                     | Type    | Access             | Description                                                                                                                                                                                                      | 
 | --------                     | ----    | ------             | -----------                                                                                                                                                                                                      | 
 | **vscp.driver**              | String  | Read Only          | Simple driver info.                                                                                                                                                                                              | 
 | **vscp.driver.add**          | String  | Read/Write (admin) | Add a driver. Read as empty string. Only the admin user can add a driver.                                                                                                                                        | 
 | **vscp.driver.delete**       | String  | Read/Write (admin) | Delete a driver. Read as empty string. Only the admin user can delete a driver.                                                                                                                                  | 
 | **vscp.driver.start**        | Boolean | Read/Write (admin) | Start a driver. Read as empty string. Only the admin user can start a driver.                                                                                                                                    | 
 | **vscp.driver.pause**        | Boolean | Read/Write (admin) | Pause a driver. Read as empty string. Only the admin user can pause a driver.                                                                                                                                    | 
 | **vscp.driver.stop**         | Boolean | Read/Write (admin) | Stop a driver. Read as empty string. Only the admin user can stop a driver.                                                                                                                                      | 
 | **vscp.driver.count**        | Integer | Read Only          | Number of drivers (Level I + Level II ).                                                                                                                                                                         | 
 | **vscp.driver.level1.count** | Integer | Read Only          | Number of level I drivers.                                                                                                                                                                                       | 
 | **vscp.driver.level2.count** | Integer | Read Only          | Number of level II drivers.                                                                                                                                                                                      | 
 | **vscp.driver.**n[.field]    | String  | Read Only          | Driver field. n represent the record. \\ A field name can optionally be given which selects that field. \\ Without the optional field a comma separated list with all values (see after table) is used as value. | 

### Interfaces

 | Variable                                 | Type    | Description                                                                                                                                                                                                        | 
 | --------                                 | ----    | -----------                                                                                                                                                                                                        | 
 | **vscp.interface.count**                 | Integer | Number of interfaces. Can only be read.                                                                                                                                                                            | 
 | **vscp.interface.**//n//[.field]         | String  | Interface field. n represent the record. A field name can optionally be given which selects that field. Without the optional field a comma separated list with all values (see after table) is used as value.      | 
 | **vscp.interface.**//n//**.id**          | Integer | Id for interface. *n* is record number.                                                                                                                                                                          | 
 | **vscp.interface.**//n//**.type**        | Integer | Type for interface. *n* is record number.                                                                                                                                                                        | 
 | **vscp.interface.**//n//**.type.string** | String  | Type for interface in string form. *n* is record number.                                                                                                                                                         | 
 | **vscp.interface.**//n//**.name**        | String  | Name for interface. *n* is record number.                                                                                                                                                                        | 
 | **vscp.interface.**//n//**.guid**        | String  | GUID for interface. *n* is record number.                                                                                                                                                                        | 
 | **vscp.interface.**//n//**.start**       | Date    | Date/time when interface was started. *n* is record number.                                                                                                                                                      | 
 | **vscp.interface.type.count**            | Integer | Number of interface types. Can only be read.                                                                                                                                                                       | 
 | **vscp.interface.type.**//n//[.field]    | String  | Interface type field. n represent the record. A field name can optionally be given which selects that field. Without the optional field a comma separated list with all values (see after table) is used as value. | 
 | **vscp.interface.type.**//n//**.name**   | String  | Name for interface type. *n* is record number.                                                                                                                                                                   | 
### Discovery

 | Variable                                        | Type      | Description                                                                                                                                                                                                        | 
 | --------                                        | ----      | -----------                                                                                                                                                                                                        | 
 | **vscp.discovery.count**                        | Integer   | Number of elements in discovery database. Can only be read.                                                                                                                                                        | 
 | **vscp.discovery.**n[.field]                    | String    | Discovery field. n represent the record.\\ A field name can optionally be given which selects that field.\\  Without the optional field a comma separated list with all values (see after table) is used as value. | 
 | **vscp.discovery.**n**.type**                   | Integer   | Type for discovered item.                                                                                                                                                                                          | 
 | **vscp.discovery.**n**.name**                   | String    | Name for discovered item.                                                                                                                                                                                          | 
 | **vscp.discovery.**n**.guid**                   | VSCP GUID | GUID for discovered item.                                                                                                                                                                                          | 
 | **vscp.discovery.**n**.date**                   | Date      | Date discovered for discovered item.                                                                                                                                                                               | 
 | **vscp.discovery.**n**.address**                | String    | Address for discovered item.                                                                                                                                                                                       | 
 | **vscp.discovery.**n**.capabilities**           | String    | Capabilities for discovered item.                                                                                                                                                                                  | 
 | **vscp.discovery.**n**.capabilities.tcp**       | Boolean   | TCP capability for discovered item.                                                                                                                                                                                | 
 | **vscp.discovery.**n**.capabilities.udp**       | Boolean   | UDP capability for discovered item.                                                                                                                                                                                | 
 | **vscp.discovery.**n**.capabilities.multicast** | Boolean   | Multicast capability for discovered item.                                                                                                                                                                          | 
 | **vscp.discovery.**n**.capabilities.raweth**    | Boolean   | Raw Ethernet capability for discovered item.                                                                                                                                                                       | 
 | **vscp.discovery.**n**.capabilities.web**       | Boolean   | Web capability for discovered item.                                                                                                                                                                                | 
 | **vscp.discovery.**n**.capabilities.websocket** | Boolean   | Websocket capability for discovered item.                                                                                                                                                                          | 
 | **vscp.discovery.**n**.capabilities.rest**      | Boolean   | REST capability for discovered item.                                                                                                                                                                               | 
 | **vscp.discovery.**n**.capabilities.mqtt**      | Boolean   | MQTT capability for discovered item.                                                                                                                                                                               | 
 | **vscp.discovery.**n**.capabilities.coap**      | Boolean   | CoAP capability for discovered item.                                                                                                                                                                               | 
 | **vscp.discovery.**n**.capabilities.ssl**       | Boolean   | SSL capability for discovered item.                                                                                                                                                                                | 
 | **vscp.discovery.**n**.capabilities.ipv4**      | Boolean   | IPv4 capability for discovered item.                                                                                                                                                                               | 
 | **vscp.discovery.**n**.capabilities.ipv6**      | Boolean   | IPv6 capability for discovered item.                                                                                                                                                                               | 
 | **vscp.discovery.**n**.capabilities.accept2**   | Boolean   | Acccept >2 connections capability for discovered item.                                                                                                                                                             | 
 | **vscp.discovery.**n**.nonstandard**            | String    | Nonstandard data for discovered item.                                                                                                                                                                              | 
 | **vscp.discovery.**n**.description**            | String    | Description for discovered item.                                                                                                                                                                                   | 


### Users

Only admin user can write data. 

 | Variable                            | Type    | Access     | Description                                                                                                                                                                                                                                                                                                                                                                  | 
 | --------                            | ----    | ------     | -----------                                                                                                                                                                                                                                                                                                                                                                  | 
 | **vscp.user.count**                 | Integer | Read       | Number of defined users. Can only be read.                                                                                                                                                                                                                                                                                                                                   | 
 | **vscp.user.**n[.field]             | String  | Read/Write | User field. n represent the record.\\ A field name can optionally be given which selects that field.\\  Without the optional field a comma separated list with all records (see after table) is used as value.                                                                                                                                                               | 
 | **vscp.user.names**                 | String  | Read       | All usernames in a comma separated list.                                                                                                                                                                                                                                                                                                                                     | 
 | **vscp.user.**n.**userid**          | Long    | Read       | id for this user record.                                                                                                                                                                                                                                                                                                                                                     | 
 | **vscp.user.**n.**name**            | String  | Read/Write | Username for record n.                                                                                                                                                                                                                                                                                                                                                       | 
 | **vscp.user.**n.**password**        | String  | Read/Write | Password for record n.                                                                                                                                                                                                                                                                                                                                                       | 
 | **vscp.user.**n.**fullname**        | String  | Read/Write | Full name for record n.                                                                                                                                                                                                                                                                                                                                                      | 
 | **vscp.user.**n.**filter**          | Filter  | Read/Write | Receive filter for record n.                                                                                                                                                                                                                                                                                                                                                 | 
 | **vscp.user.**n.**rights**          | String  | Read/Write | Rights, comma separated list for record n.                                                                                                                                                                                                                                                                                                                                   | 
 | **vscp.user.**n.**rights**.m        | Integer | Read/Write | Rights byte, m=0,1,2,3,4,5,6,7 for record n. If m is not given all right bytes is returned as a slash "/" separated list.                                                                                                                                                                                                                                                    | 
 | **vscp.user.**n.**allowed.remotes** | String  | Read/Write | Allowed remote host this user can connect from.                                                                                                                                                                                                                                                                                                                              | 
 | **vscp.user.**n.**allowed.events**  | String  | Read/Write | Allowed events this user can send.                                                                                                                                                                                                                                                                                                                                           | 
 | **vscp.user.**n.**note**            | String  | Read/Write | Note for this user record n.                                                                                                                                                                                                                                                                                                                                                 | 
 | **vscp.user.**n.**write**           | String  | Write      | This is the same as *vscp.user.n* This variable can only be written and is used to update data for a user. Argument is a comma separated list with format *name;password;fullname;filtermask;rights;remotes;events;note* where note is BASE64 encoded. An empty field (two commas after each other) will not be updated. The admin users data can't be updated remotely. | 
 | **vscp.user.add**                   | String  | Write      | This variable can only be written to and is used to add a user. Argument is a comma separated list with format *name;password;fullname;filtermask;rights;remotes;events;note* where note is BASE64 encoded.                                                                                                                                                                | 
 | **vscp.user.delete**                | String  | Write      | This variable can only be written to and is used to delete a user. Write the userid for the user to this variable to delete the users record. Only the admin user is allowed to do this. Internal variables (admin, driver etc) can not be deleted.                                                                                                                          | 

A user record have the following format.

	
	  userid;name;password;fullname;filter;mask;rights;remotes;events;note


**userid** This is the database id for a user. The user id for the admin user is zero. Local users (not stored in the database) have id's that start at 0x10000. For the **vscp.user.add** userid is not given. 

**password** will be reported with "*" for all characters in the password.

**filtermask** is *filter-priority, filter-class, filter-type, filter-GUID, mask-priority, mask-class, mask-type, mask-GUID*

**rights** is a slash "/" separated list with the eight rights bytes starting with the MSB. 

**remotes** is a slash "/" separated list with ipv4 or ipv6 addresses with wildcards ('*').

**events** is a slash "/" separated list with class:type pairs where both can be wildcards ('*').

**note** is BASE64 encoded.
   
### Tables

 | Variable                                        | Type          | Description                                                                                                                                                                 | 
 | --------                                        | ----          | -----------                                                                                                                                                                 | 
 | **vscp.table.count**                            | Integer       | Number of defined tables. __Can only be read.__                                                                                                                             | 
 | **vscp.table**                                  | String        | Return a comma separated list of defined table names. Can only be read.                                                                                                     | 
 | **vscp.table.from**                             | Date and time | A date time on the form **"YYYY-MM-DDTHH:MM:SS.sss,value"**. Set before reading a table range variable.                                                                     | 
 | **vscp.table.to**                               | Date and time | A date time on the form **"YYYY-MM-DDTHH:MM:SS.sss,value"**. Set before reading a table range variable.                                                                     | 
 |                                                 |               |                                                                                                                                                                             | 
 | **vscp.table.**//name//**.count**               | Integer       | Number of records for a named table. Can only be read.                                                                                                                      | 
 | **vscp.table.**//name//**.range.count**         | Integer       | Number of records for a named table and a datetime range. Can only be read.                                                                                                 | 
 | **vscp.table.**//name//**.fields**              | String        | A list with all fields in the vscptable  of table 'name'. Can only be read.                                                                                                 | 
 | **vscp.table.**//name//                         | String        | All records of table 'name'. Can only be read.                                                                                                                              | 
 | **vscp.table.**//name//**.range**               | String        | All records of table 'name' and a datetime range. Can only be read.                                                                                                         | 
 | **vscp.table.**//name.n[.field]//               | String        | Record n of table 'name'. If given only named 'field' of record. Can only be read.                                                                                          | 
 | **vscp.table.**//name//**.range**//.n[.field]// | String        | Record n of table 'name' and a datetime range. If given only named 'field' of record. Can only be read.                                                                     | 
 | **vscp.table.**//name//**.range.average**       | Double        | [Average](https///en.wikipedia.org/wiki/Average) for values over a period. Can only be read.                                                                                | 
 | **vscp.table.**//name//**.range.median**        | Double        | [Median](https///en.wikipedia.org/wiki/Median) ([second quartile](https///en.wikipedia.org/wiki/Quartile)) for values over a period. Can only be read.                      | 
 | **vscp.table.**//name//**.range.stdev**         | Double        | [Standard deviation](https///en.wikipedia.org/wiki/Standard_deviation) for values over a period. Can only be read.                                                          | 
 | **vscp.table.**//name//**.range.variance**      | Double        | [Variance](http://www.financereference.com/learn/variance) ([wikipedia](https///en.wikipedia.org/wiki/Variance)) for values over a period. Can only be read.                | 
 | **vscp.table.**//name//**.range.mode**          | Double        | [Statistical mode](https///en.wikipedia.org/wiki/Mode_%28statistics%29) for values over a period. Can only be read.                                                         | 
 | **vscp.table.**//name//**.range.lowerquartile** | Double        | [Lower quartile](https///en.wikipedia.org/wiki/Quartile) for values over a period. Can only be read.                                                                        | 
 | **vscp.table.**//name//**.range.upperquartile** | Double        | [Upper quartile](https///en.wikipedia.org/wiki/Quartile) for values over a period. Can only be read.                                                                        | 
 | **vscp.table.**//name//**.range.min**           | Double        | Minimum for values over a period. Can only be read.                                                                                                                         | 
 | **vscp.table.**//name//**.range.max**           | Double        | Maximum for values over a period. Can only be read.                                                                                                                         | 
 | **vscp.table.**//name//**.range.sum**           | Double        | Sum for values over a period. Can only be read.                                                                                                                             | 
 | **vscp.table.**//name//**.add.value**           | String        | Add a value to a table. Format is **"YYYY-MM-DDTHH:MM:SS.sss,value"** where value is a floating point value. Several values can be seperated with ":". Can only be written. | 
 | **vscp.table.**//name//**.add.sql**             | String        | Execute sql expression on a table. Can only be written.                                                                                                                     | 
 | **vscp.table.**//name//**.add.table**           | String        | Add a new table.                                                                                                                                                            | 
 | **vscp.table.**//name//**.delete**              | String        | Delete a table. Only owner can do this.                                                                                                                                     | 
 | **vscp.table.**//name//**.clear**               | String        | Clear content of a table.                                                                                                                                                   | 
 | **vscp.table.range.clear**                      | String        | Clear content of a table over a period.                                                                                                                                     | 


For all table variables that work __over a period__ the **vscp.table.from** and **vscp.table.to** should be filled in before a read or write.


## Other way to interact with variables

You are not limited to handle variables in the [decision matrix](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_decision_matrix).  You can write/read/create variables in the [tcp/ip interface](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_tcp_ip_control_interface). As the [VSCP helper library](http://www.vscp.org/docs/vscphelper/doku.php?id=non_graphic_lib_api#variable_handling) includes functionality to write/read/create variables you can actually handle them from any program language available. But variables can also written/read/created in the [webserver](http://www.vscp.org/docs/vscpd/doku.php) admin interface, in the [websocket interface](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_vscp_websocket_interface) and in the [REST interface](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_vscp_daemon_rest_interface).

Variables is a powerful tool that makes your work easier.


{% include "./bottom_copyright.md" %}