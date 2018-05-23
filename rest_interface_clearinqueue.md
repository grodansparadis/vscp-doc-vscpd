# Clear Input queue

`<code=css>`
    op=6 or op=CLEARQUEUE
`</code>`  

Clear the input queue for this clients session. **Requires a valid session parameter**

**General format:**

`<code=css>`
http://server:port/rest?
    vscpsession=session-key&
    format=plain|csv|xml|json|jsonp&
    op=6|clearqueue
`</code>`

**Arguments:**


*  **op** - Set to 6|clearqueue

*  **format** - can be 2|xml, 3|json or 4|jsonp (0|plain and 1|csv returns error).

*  **vscpsession** - A valid session key received from the open method.

## HTTP Request with GET

`<code=css>`
http://demo.vscp.org:8080/vscp/rest?vscpsession=d1c13eb83f52f319f14d167962048521 &format=plain|csv|xml|json|jsonp&op=6|clearqueue    
`</code>`

to test this with **curl** use the following format

`<code=bash>`
curl -X GET "http://host:port/vscp/rest? \
    vscpsession=d1c13eb83f52f319f14d167962048521 & \
    format=plain|csv|xml|json|jsonp& \
    op=6|clearqueue"
`</code>`


## Examples

##### example GET HTTP request

`<code=css>`
    http://localhost:8080/vscp/rest?  
              vscpsession=d1c13eb83f52f319f14d167962048521&
              format=plain&
              op=6
`</code>`  


## HTTP Request with POST

`<code=bash>`
curl -X POST "http://localhost:8080/vscp/rest" \
    -H "vscpsession: d1c13eb83f52f319f14d167962048521" \ 
    -d "op=clearqueue&format=plain"     
`</code>`

## Demo

There is a a [demo app.](https///github.com/grodansparadis/vscp-ux/tree/master/rest) in the source tree, that demonstrates this functionality using JavaScript.

### JavaScript Request with JSONP

`<code=JavaScript>`
*/*//////////////////////////////////////////////////////////////////
// do_clrQueue
//
		
var do_clrQueue = function() {
			
    if ( VscpSessionKey.length > 0 ) {	
        $.ajax({
            url: VscpServer + '/vscp/rest?vscpsession=' + VscpSessionKey + 
                '&format=jsonp&op=clearqueue',
            type : "GET",
            jsonpCallback: 'handler',
            cache: true,
            dataType: 'jsonp',
            success: function(response) {
                // response will be a JavaScript
                // array of objects
                console.log("-----------------------------------------------------------");
                console.log("                         do_clrQueue");
                console.log("-----------------------------------------------------------");
                console.log("Success = " + response.success );
                console.log("Code = " + response.code );
                console.log("Message = " + response.message );
                console.log("Description = " + response.description );
                console.log("Info = " + response.info );
					
                if ( response.success ) {
                    $("#events").html( "Mask set" );
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
