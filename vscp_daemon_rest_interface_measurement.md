# Send a measurement

`<code=css>`
    op=10 or op=MEASUREMENT
`</code>`  
    
Sends a VSCP measurement event on a high level. **Requires a valid session parameter**

**General form:**

`<code=http>`
http://host:port/vscp/rest?
    vscpsession=d1c13eb83f52f319f14d167962048521&
    format=plain|csv|xml|json|jsonp&
    op=10|measurement&
    guid=00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:01
    type=valid VSCP measurement type
    eventformat=string|float&
    value=floating point value&
    [level=2]&
    [sensorindex]=0-7|255&
    [unit=(0-3)|255]&
    [zone=(0-255)]&
    [subzone=0-255]
`</code>`

**Arguments:**


*  **guid** is the GUID for the event. If not given it defaults to all zeros.

*  **type** is the [VSCP type value](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.measurement) specifying which type of measurement this is. Mandatory.

*  **eventformat** is optional and can be *string* or *float* to generate a string based or a float based event. If not give the default value, float, will be used.

*  **value** is a floating point value for the measurement.

*  **level** VSCP level (Level I or Level II) to send event as. Can be 1 or 2 and defaults to 2.

*  **sensorindex** is the index for the sensor for the unit. Can be in the range 0-7 for a Level I event and 0-255 for a Level II event. Defaults to zero.

*  **unit** is the measurement unit for this type of measurement. An be in the range 0-3 for a Level I event and 0-255 for a Level II event. Defaults to zero.

*  **zone** zone value for Level II events. Defaults to zero.

*  **subzone** zone value for Level II events. Defaults to zero.

## HTTP Request with GET

`<code=http>`
http://demo.vscp.org:8080/vscp/rest?vscpsession=d1c13eb83f52f319f14d167962048521&
    format=plain|csv|xml|json|jsonp&
    op=10|measurement&
    guid=00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:01
    type=6&
    value=floating point value&
    [level=2]&
    [sensorindex]=0-7|255&
    [unit=0-3|255]&
    [zone=0-255]&
    [subzone=0-255]&
`</code>`

to test this with **curl** use the following format

`<code=css>`
curl -X GET "http://host:port/vscp/rest? \
    vscpsession=d1c13eb83f52f319f14d167962048521 & \
    format=plain|csv|xml|json|jsonp& \
    op=10|measurement"
`</code>`

##### example GET HTTP request

`<code=css>`
    http://localhost:8080/vscp/rest?  
              vscpsession=d1c13eb83f52f319f14d167962048521&
              format=plain&
              op=10
`</code>`  

## HTTP Request with POST

`<code=css>`
curl -X POST "http://localhost:8080/vscp/rest" \
    -H "vscpsession: d1c13eb83f52f319f14d167962048521" \ 
    -d "op=measurement&format=plain"     
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
