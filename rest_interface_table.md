
:!:
The table functionality is broken in the head version. This is because it is being rewritten at the moment. 



# Read Table

Tables is a feature of the daemon that makes it easy to collect time + value data, typically measurements from a sensor. It is a feature of the decision matrix of the VSCP daemon and is described [here](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_decision_matrix#write_table). 

`<code=css>`
    op=11 or op=TABLE
`</code>`  
    
Read data from a server defined table. **Requires a valid session parameter**

**General Format**
`<code=css>`
http://host:port/vscp/rest?
    vscpsession=session-key&
    format=plain|csv|xml|json|jsonp&
    op=11|table&
    name=name-of-table&
    from=from-date-time&
    to=from-date-time  
`</code>`

**Arguments:**


*  **op** - Set to 11|gettable

*  **format** - can be 0|plain, 1|csv, 2|xml, 3|json or 4|jsonp.

*  **vscpsession** - A valid session key received from the open method.

*  **name** - Name of table to fetch data from.

*  **from** - Time on the form YY-MM-DD HH:MM:SS to start show values from.

*  **to** - Time on the form YY-MM-DD HH:MM:SS to show values to.

## HTTP Request with GET

`<code=css>`
http://host:port/vscp/rest?vscpsession=d1c13eb83f52f319f14d167962048521 &format=plain|csv|xml|json|jsonp&op=11|table    
`</code>`

to test this with **curl** use the following format

`<code=css>`
curl -X GET "http://host:port/vscp/rest? \
    vscpsession=d1c13eb83f52f319f14d167962048521 & \
    format=plain|csv|xml|json|jsonp& \
    op=11|table"
`</code>`

##### example GET HTTP request

`<code=css>`
    http://localhost:8080/vscp/rest?  
              vscpsession=d1c13eb83f52f319f14d167962048521&
              format=plain&
              op=11
`</code>`  

## HTTP Request with POST

`<code=css>`
curl -X POST "http://localhost:8080/vscp/rest" \
    -H "vscpsession: d1c13eb83f52f319f14d167962048521" \ 
    -d "op=table&format=plain"     
`</code>`

## Demo

There is a a [demo app](https///github.com/grodansparadis/vscp-ux/tree/master/rest) in the source tree, that demonstrates this functionality using JavaScript.

### Javascript Request with JSONP

## Responses

### Plain

	
	


### CSV

	
	


### XML

`<code=xml>`

`</code>`

### JSON

`<code=css>`

`</code>`

### JSONP

`<code=javascript>`

`</code>`



\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
