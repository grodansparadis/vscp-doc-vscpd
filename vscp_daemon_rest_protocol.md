# VSCP REST Protocol Description

This page describes the protocol and HTTP requests available for the VSCP REST protocol.

The format here uses some special characters that may need some extra explanation.


*  **\** is a sign that indicates that the current line continues on the next line.

*  **|** is **or**. It is often written on the form *type=option|option2|optionm3|option4* and means you can select one of the options.
## HTTP Request Parameters

 | Parameter       | Example                                      | description                                                                                                                                                                                                                                      |    
 | ---------       | -------                                      | -----------                                                                                                                                                                                                                                      |    
 | **vscpuser**    | vscpuser=admin                               | Sets the username                                                                                                                                                                                                                                |    
 |                 |                                              |                                                                                                                                                                                                                                                  |    
 | **vscpsecret**  | vscpsecret=d50c3180375c27927c22e42a379c3f67  | Set password. The password is made up of the md5 hash of *username:auth-domain:realtextpassword*. The **mkpasswd** tool that comes with VSCP & Friends can be used to generate the hash or one can use any of the on-line resources available. |    
 |                 |                                              |                                                                                                                                                                                                                                                  |    
 | **vscpsession** | vscpsession=d1c13eb83f52f319f14d167962048521 | This is a key that is received from the server after the **open** command. It is used as a parameter for all other parameters to identify the client session and reuse it                                                                        |    
 |                 |                                              |                                                                                                                                                                                                                                                  |    
 | **format**      | `<nowiki>`format=plain                         | csv                                                                                                                                                                                                                                              | xml | json | jsonp`</nowiki>` | Sets the format responses should be delivered on. See format table below for possible values. | 
 |                 |                                              |                                                                                                                                                                                                                                                  |    
 | **op**          | op=open                                      | Operation to perform. op can have a token or a numerical value.                                                                                                                                                                                  |    

## Supported output formats 

The currently available formats are

 | Format    | Description                                    | 
 | ------    | -----------                                    | 
 | **plain** | Plain text format                              | 
 | **csv**   | Comma Separated Values                         | 
 | **xml**   | XML format                                     | 
 | **json**  | JSON format popular in Javascript              | 
 | **jsonp** | JSONP format popular in Javascript crossdomain | 


## Operations

The available operations currently are

 | operation token                                                                                  | Code | Description                        | 
 | ---------------                                                                                  | ---- | -----------                        | 
 | [STATUS](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_status)           | 0    | Gives status for session           | 
 | [OPEN](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_open)               | 1    | Open a new session session         | 
 | [CLOSE](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_close)             | 2    | Close a session                    | 
 | [SENDEVENT](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_sendevent)     | 3    | Send VSCP Event                    | 
 | [READEVENT](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_readevent)     | 4    | Read VSCP Event                    | 
 | [SETFILTER](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_setfilter)     | 5    | Set filter for this session        | 
 | [CLEARQUEUE](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_clearinqueue) | 6    | Clear input queue for this session | 
 | [LISTVAR](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_listvar)         | 12   | List variables variable            | 
 | [READVAR](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_readvar)         | 7    | Read the value of a variable       | 
 | [WRITEVAR](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_writevar)       | 8    | Write the value of a variable      | 
 | [CREATEVAR](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_creatvar)      | 9    | Create a variable                  | 
 | [MEASUREMENT](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_measurement) | 10   | Send a measurement                 | 
 | [TABLE](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_table)             | 11   | Read a table                       | 

## Errors

### General - Error = -1

This error is received as a general error message.

### Invalid session - Error = -2

The login session is invalid or have timeout because of inactivity. An Open call is needed before most commands can be used.

##### Error code format=plain

`<code=css>`
0 -2 Invalid session 

The session must be opened with 'open' before a session command can be used. It may also be possible that the session has timed out.
`</code>`

##### Error code format=csv

`<code=css>`
success-code,error-code,message,description\r\n0,-2,Invalid session,The session must be opened with 'open' before a session command can be used. It may also be possible that the session has timed out.
`</code>`


##### Error code format=xml

`<code=xml>`
<vscp-rest success="false" 
    code="-2" 
    message="Invalid session" 
    description="The session must be opened with 'open' before a session command can be used. It may also be possible that the session has timed out."/>
`</code>`

##### Error code format=json

`<code=js>`
{\"success\":false,\"code\":-2,\"message\":\"Invalid session\",\"description\":\"The session must be opened with 'open' before a session command can be used. It may also be possible that the session has timed out.\"}
`</code>`

##### Error code format=jsonp

`<code=js>`
typeof handler === 'function' && handler(("{\"success\":false,\"code\":-2,\"message\":\"Invalid session\",\"description\":\"The session must be opened with 'open' before a session command can be used. It may also be possible that the session has timed out.\"});
`</code>`

### Unsupported format - Error = -3

This error is received because the format of the call is not valid.

### Unable to create session - Error = -4

The system was unable to create the session.

### Missing data/parameter - Error = -5

Needed data or a parameter to a call is missing. 

### Input queue empty - Error = -6

There is no events to read from the input queue.

### Variable not found - Error = -7

A requested variable can't be found and is probably undefined.

### Variable could not be created - Error = -8

A variable could not be created. This can be a memory or a naming problem.

\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
