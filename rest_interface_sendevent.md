# Send Event

`<code=css>`
    op=3 or op=SENDEVENT
`</code>`  
    
Send a VSCP Event. The event should be given in string form "head,vscp-class,vscp-type,obid,datetime,timestamp,guid,data1,data2,data2..." **Requires a valid session parameter**

**Important note** datetime is introduced in version 1.12.20.0

**General format:**

`<code=css>`
http://server:port/rest?
    vscpsession=session-key&
    format=plain|csv|xml|json|jsonp&
    op=3|sendevent&
    vscpevent=event-in-string-form
`</code>`

Arguments:


*  **op** - Set to 3|sendevent

*  **format** - can be 0|plain, 1|csv, 2|xml, 3|json or 4|jsonp.

*  **vscpsession** - A valid session key received from the open method.

*  **vscpevent** - Event in string form. That is *head,class,type,obid,time-stamp,GUID,data1,data2,data3.... * for example *0,20,3,0,,0,0:1:2:3:4:5:6:7:8:9:10:11:12:13:14:15,0,1,35* to send [CLASS1.INFORMATION TYPE=3 ON event](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.information#type_3_0x03_on), for zone=1, sub-zone=35. Can also be sent as *0,20,3,0,0,-,0,1,35* which will use the GUID of the interface.

## HTTP Request with GET

`<code=css>`
http://demo.vscp.org:8080/vscp/rest?vscpsession=d1c13eb83f52f319f14d167962048521 &format=plain|csv|xml|json|jsonp&op=3|sendevent&vscpevent=0,10,6,0,,,-,138,0,255    
`</code>`

to test this with **curl** use the following format

`<code=css>`
curl -X GET "http://host:port/vscp/rest? \
    vscpsession=d1c13eb83f52f319f14d167962048521 & \
    format=plain|csv|xml|json|jsonp& \
    op=3|sendevent&vscpevent=0,10,6,0,,,-,138,0,255"
`</code>`


## Examples

##### example GET HTTP request

`<code=css>`
    http://localhost:8080/vscp/rest?  
              vscpsession=d1c13eb83f52f319f14d167962048521&
              format=plain&
              op=3&
              vscpevent=event-in-string-form
`</code>`  


##  HTTP Request with POST

`<code=css>`
curl -X POST "http://localhost:8080/vscp/rest" \
    -H "vscpsession: d1c13eb83f52f319f14d167962048521" \ 
    -d "op=sendevent&format=plain&vscpevent=0,10,6,0,,,-,138,0,255"     
`</code>`

## Demo

There is a a [demo app.](https///github.com/grodansparadis/vscp-ux/tree/master/rest) in the source tree, that demonstrates this functionality using JavaScript.

### JavaScript Request with JSONP

`<code=JavaScript>`
*/*//////////////////////////////////////////////////////////////////
// do_sendEvent
//
		
var do_sendEvent = function() {
			
    if ( VscpSessionKey.length > 0 ) {	
        $.ajax({
            url: VscpServer + '/vscp/rest?vscpsession=' + VscpSessionKey + '&format=jsonp&op=sendevent&vscpevent=' + txtSendEvent,
            type : "GET",
            jsonpCallback: 'handler',
            cache: true,
            dataType: 'jsonp',
            success: function(response) {
                // response will be a javascript
                // array of objects
                console.log("-----------------------------------------------------------");
                console.log("                         do_sendEvent");
                console.log("-----------------------------------------------------------");
                console.log("Success = " + response.success );
                console.log("Code = " + response.code );
                console.log("Message = " + response.message );
                console.log("Description = " + response.description);
                console.log("Info = " + response.info );
					
                if ( response.success ) {
                    $("#events").html( "event sent" );
                }					
					
            },
            error: function( xhr, status, error ) {
                console.log( "Close:" + error + " Status:" + status );
            }
        });
    }
    else {
        alert("Interface is not open!");
    }
};
`</code>`

## Responses

### Plain

	
	1 1 Success 
	
	Everything is fine.


### CSV

	
	success-code,error-code,message,description
	1,1,Success,Success.


### XML

`<code=xml>`
`<vscp-rest success="true" code="1" message="Success" description="Success."/>`
`</code>`

### JSON

`<code=css>`
{"success":true,"code":1,"message":"success","description":"Success"}
`</code>`

### JSONP

`<code=JavaScript>`
typeof handler === 'function' && handler({"success":true,"code":1,"message":"success","description":"Success"});
`</code>`



\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
