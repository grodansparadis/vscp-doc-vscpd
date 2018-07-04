# VSCP Daemon Websocket Protocol Description

The protocol is a text based protocol that is simple and effective. Only **AUTH** and **NOOP** commands are valid in a system where the client has not been authenticated. It is possible to configure the websocket interfaces  not to require this authentication with the [configuration setting](./configuring_the_vscp_daemon.md)

    `<websockets enable=“true” auth=“false” />` 

setting. This is recommended for testing situations only.

## Packet format

Message traffic on the socket is in text format as below

### commands

 | 'C' ; command ; optional data that may be separated by additional semicolons. | 
 | ----------------------------------------------------------------------------- | 

Positive reply 

 | '+' ; originator | 
 | ---------------- | 

Negative reply 

 | '-' ; originator ; Error code ; Error in real text | 
 | -------------------------------------------------- | 

**Example:**
 | -;E;Transmit buffer full | 
 | ------------------------ | 

###  events

Both sent and received events have the same format.

 | 'E' ; head , vscp_class , vscp_type ,obid, datetime, timestamp, GUID, data | 
 | -------------------------------------------------------------------------- | 
    

**Important note** datetime is introduced in version 1.12.20.0  
    
Positive reply 

 | '+' | 
 | --- | 

Negative reply 

 | '-' | 
 | --- | 

** Example:**

    E;0,30,5,0,2000-01-01T12:33:14,0,FF:FF:FF:FF:FF:FF:FF:FE:00:26:55:CA:00:06:00:00,0x01,0x01

 | Code | Description                                                                                            | 
 | :----: | -----------                                                                                            | 
 | C    | Command. Parameter is command and optional parameter(s).                                               | 
 | +    | Positive Reply. If send in response to a command the command is also  returned on the form '+;command' | 
 | -    | Negative reply. Payload is error code followed by error message in English. '-;2;Syntax Error'         | 
 | E    | Event. Payload is VSCP event.                                                                          | 

## Available commands

The following commands are currently available. **NOOP** is typically used to test if a connection is working. **OPEN**/**CLOSE** can be used to stop the stream from incoming events. Note that events still are collected at the server side and will be sent after a closed socket has been opened again. Use **CLRQUEUE** to clear the queue at the server before opening the stream if you don't want to receive collected events.

Variables on the server is a powerful tool. Variables are used by Level II drivers and the internal decision matrix of the daemon. This means that driver parameters can be changes and complex setups can be accomplished together with the decision matrix functionality. As an example you can set a variable to true and have an action executed by the daemon that does something useful. The possibilities are endless. Variables can be persistent meaning they will live over time so it can also be a method to save states.

### NOOP

No operation. Will always give a positive response.

### CHALLENGE

Send this command to initiate the authentication. This is process is normally started automatically on a connect.

###  AUTH

The AUTH process has changed 2017-10-04 (ux-framwork version 0.2, VSCP& Friends version 12.29.1.13). [Old description is here](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_websocket_protocol_description&rev=1507044582). 

This command is used for authentication. When connecting to a socket and the [auth configuration parameter](./configuring_the_vscp_daemon.md) is true (default) the server will send something like 
12.29.1.13

    "+;AUTH0:5a475c082c80dcdf7f2dfbd976253b24" 

as a security challenge to the client (Also sent after a **CHALLENGE** command has been sent to a host by a client.). The "5a475c082c80dcdf7f2dfbd976253b24" is a session id or sid that is different for every connection.

The client now should send an authentication message on the form

    "C;AUTH;sid;crypto"  

for example

    C;AUTH;5a475c082c80dcdf7f2dfbd976253b24;69b1180d2f4809d39be34e19c750107f

where the sid is used as a 16.byte random iv for AES-128 encryption over

    "username:password"

using the [vscpkey](./configuring_the_vscp_daemon.md#security) as a common secret key.  If the credentials are valid the server will respond with

    "+;AUTH1;userid;name;password;fullname;filtermask;rights;remotes;events;note"

and if invalid the server will respond with

    "-;8,Not authorized"

Note that in addition to the credentials the server IP address must also be valid as of the [configuration](./configuring_the_vscp_daemon.md) for this user.

**Note:** its is note allowed to have a username with a semicolon in the name.

The standard vscp password hash is calculated over "username:authdomain:password". 

*rights* a bit array presented as eight bytes separated with semicolon.
### OPEN

Start receiving events. Collected events in queue will be sent. Positive/negative response is returned.

**Example:** 

    “C;OPEN” 

response is 

    “+;OPEN”

###  CLOSE

Stop receiving events. Events are still collected in queue on server side. Positive/negative response is returned.

**Example:**

    “C;CLOSE” 
    
response is 

    “+;CLOSE”

###  CLRQ 

Clear events in input queue. Positive/negative response is returned.

"CLRQUEUE" also work.

**Example:**

    “C;CLRQE” 
    
response is 

    “+;CLRQ”

###  SF

Set filter/mask for incoming data. Positive/negative response is returned.

"SETFILTER" also work.

**Example:** 

    “C;SF;filter-priority, filter-class, 
       filter-type, filter-GUID;mask-priority, 
       mask-class, mask-type, mask-GUID” 
       
response is 

    “+;SF”

Note that there is a semicolon between filter and mask information and commas between parts of each filter and mask.

###  RVAR

Read a variable. 

"READVAR" also work.

**Format:** 

    "C;RVAR;variablename". 

Positive/negative response is returned.

**Example:** 

    “C;RVAR;name” 

response is 

    “+;RVAR;type;variable-value” 

where type is variable type and value is different depending on which type of variable it is ([format described here](http://www.vscp.org/docs/vscpd/doku.php?id=remote_variables#persistent_storage_format)). For a string the response is 

    “+;RVAR;1;hellow world” 

and for a boolean variable 

    “+;RVAR;2;true”

or

    “+;RVAR;2;false” 

etc. See [this page](./remote_variables.md#variable_types) for more information on variable types.

**Note:** its is note allowed to have a variable name with a semicolon in the name.

### WVAR

Set value for existing variable. The variable must exist.

"WRITEVAR" also works.

**Format:**

    "C;WVAR;variablename;value" 

The value is different depending on what variable type it is ([described here](./remote_variables.md#persistent_storage_format)). Positive/negative response is returned.

The response is
    
    “+;WVAR;variable-name”

or

    "-;WVAR;error-code;error-message"

**Note** that the response format has changed from version 1.12.14.7. Previously the variable value also was present in the reply.

**Example:** 

    “C;WVAR;test;false” 

which set the boolean value to false. The response is 

    “+;WVAR;name”
    
### CVAR

Add a new variable. A variable that already exists can be updated using this method. Stock variables (name starts with "vscp.") can not be created or updated.

"CREATEVAR" also works.

**Format:**

    “C;CVAR;name;type;accessrights;bPersistens;value;note” 

Only name is a required parameter. **type** default to *1/string*, **accessrights** to *744*, **bPersistens** to *0/false*, **value** and **note** to empty strings.

**Example:** 

    “C;CVAR;test;1;777;0;aGVsbG8gd29ybGQ=;VGhpcyBpcyBhIHRlc3Qgc3RyaW5n” 

which add the non persistent string value “hello world” and the note "This is a test string", both base64 encoded with all rights for all users

response is 

    “+;CVAR ”
    

**Note: its is note allowed to have a variable name with a semicolon in the name. Also the calling routine should have some handling so that semicolon in variable values are translated. ** 
    

    
###  DELVAR

Remove variable.

"REMOVEVAR" also works.

**Format:**

    “C;DELVAR;name” 

Positive response is returned on success.

**Example:** 

    “C;DELVAR;testvariable” 

response is 

    “+;DELVAR;”
    

**Note: its is note allowed to have a variable name with a semicolon in the name.**  
    
###  LSTVAR

List currently defined variables selectable by a regular expression. 

More info about regular expressions can be found [here](https://en.wikipedia.org/wiki/Regular_expression) and [ here](https://www.google.se/url?sa=t&rct=j&q=&esrc=s&source=web&cd=3&cad=rja&uact=8&ved=0ahUKEwjsj4izh5nPAhXrB5oKHV8sBJkQFggzMAI&url=https%3A%2F%2Fmsdn.microsoft.com%2Fen-us%2Flibrary%2Faz24scfc(v%3Dvs.110).aspx&usg=AFQjCNHGzAjfymZ56d-QY5maPEl67dKyxw&sig2=nNRdPVuu9routoaqIg1Yrw ).

If no regular expression is given all defined variables is returned.

"LISTVAR" also works.

**Format:**

    “C;LSTVAR[;optional-regular-expression]” 

Positive response is returned on success with the following format

    +;LSTVAR;ordinal;total:name;type;userid;accessrights;last_change;persistence

The *type* is always numeric. 
*ordinal* starts at zero and is increased by one for every variable record sent up to *total-1*. 
*total* is the total number of variables.
The optional regular expression can be used to list just matching variables.

**Example:** 

    “C;LSTVAR” 

response is 

    +;LSTVAR;0;4;test1;1;0;777;2016-09-12T14:20:00;true
    +;LSTVAR;1;4;variable2;1;0;777;2016-09-12T14:20:00;true
    +;LSTVAR;2;4;test13;1;3;777;2016-09-12T14:20:00;false
    +;LSTVAR;3;4;test;1;8;777;2016-09-12T14:20:00;true



### RSTVAR

Reset variable to its default value. Default values can be found [here](./remote_variables#variable_types).

"RESETVAR" also works.

**Format:**

    “C;RSTVAR;variablename” 

Positive response is returned on success

    "+;RSTVAR;variablename;type;value"

### LENVAR

Return the length for a string variable. Return zero for other types.

"LENGTHVAR" also works.

**Format:**

    “C;LENVAR;variablename” 

Positive response is returned on success

    "+;LENVAR;variablename;length
    

**Note:** its is note allowed to have a variable name with a semicolon in the name.
    
### LCVAR

Get the date and time for the last change of a variables value.

"LASTCHANGEVAR" also works.

**Format:**

    “C;LCVAR;variablename”

Positive response is returned on success

    "+;LCVAR;variablename;YY-MM-DD HH:MM:SS"
    

**Note:** its is note allowed to have a variable name with a semicolon in the name.

### GT

Get data from a table
 

**Format:**

    "C;GT;table-name;from;to"

Positive/negative response is returned plus table data.

If *from;to* is omitted the full table is returned. The range values should be on ISO form YY-MM-DD HH:MM:SS

**Example:** 

    “C;GT;from;to” 
    
response is 

    “+;GT;rows”
    
followed by none or several

    "+;TR;date time;value"  
    

**rows** is the number ow TR responses that will be received. Can be zero. 

### MEASUREMENT

**This command is a future command.**

Send a measurement. The measurement will be sent as either as a Level I event or a Level II event.
 

**Format:**

    "C;MEASUREMENT;type;unit;sensorindex;value;[guid];[level];[eventformat];[zone];[subzone]"

Positive/negative response is returned.

**Arguments:**


*  **type** is the [VSCP type value](https://grodansparadis.gitbooks.io/the-vscp-specification/class1.measurement.html) specifying which type of measurement this is. Mandatory.

*  **unit** is the measurement unit for this type of measurement. An be in the range 0-3 for a Level I event and 0-255 for a Level II event. Mandatory.

*  **sensorindex** is the index for the sensor for the unit. Can be in the range 0-7 for a Level I event and 0-255 for a Level II event. Mandatory.

*  **value** is a floating point value for the measurement.  Mandatory.

*  **guid** is the GUID for the event. If not given it defaults to all zeros meaning the interface GUID will be used. Optional.

*  **level** VSCP level (Level I or Level II) to send event as. Can be 1 or 2 and defaults to 2. Optional.

*  **eventformat** is optional and can be *string* or *float* to generate a string based or a float based event. If not give the default value, float, will be used. Optional.

*  **zone** zone value for Level II events. Defaults to zero. Optional.

**Response:**

    “+;MEASUREMENT”

for a positive reply or

    “-;MEASUREMENT”

*  **subzone** zone value for Level II events. Defaults to zero. Optional.

## Send events

The same format is used to send events as they are received. 

 | 'E';head,vscp_class,vscp_type,obid,datetime,timestamp,GUID,data | 
 | --------------------------------------------------------------- | 

and

 | +;EVENT | 
 | ------- | 

is received if it got sent and

 | -;EVENT;error-code;realtext-error | 
 | --------------------------------- | 

is returned if there was a problem sending the event.

**Important note** datetime is introduced in version 1.12.20.0

## Errors

This table list the errors that currently is defined

 | Error code | Error message                | 
 | :----------: | -------------                | 
 | 0          | No error                     | 
 | 1          | Syntax error.                | 
 | 2          | Unknown command.             | 
 | 3          | Transmit buffer full.        | 
 | 4          | Variable is already defined. | 
 | 5          | Unable to find variable.     | 
 | 6          | Authentication error         | 


{% include "./bottom_copyright.md" %}
