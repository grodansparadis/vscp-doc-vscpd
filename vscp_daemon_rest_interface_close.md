# Close

`<code=css>`
    op=2 or op=CLOSE
`</code>`

Close a session with the server. **Requires a valid session parameter**

**General format:**
`<code=css>`
http://host:port/vscp/rest?
    vscpsession=session-key&
    format=plain|csv|xml|json|jsonp&
    op=2|close    
`</code>`

**Arguments:**


*  **op** - Set to 2|close

*  **format** - can be 0|plain, 1|csv, 2|xml, 3|json or 4|jsonp.

*  **vscpsession** - A valid session key received from the open method.

## HTTP Request with GET

`<code=css>`
http://demo.vscp.org:8080/vscp/rest?vscpsession=d1c13eb83f52f319f14d167962048521 &format=plain|csv|xml|json|jsonp&op=2|close    
`</code>`

To test this with **curl** use the following format

`<code=css>`
curl -X GET "http://demo.vscp.org:8080/vscp/rest? \
    vscpsession=d1c13eb83f52f319f14d167962048521 & \
    format=plain|csv|xml|json|jsonp& \
    op=2|close"
`</code>`

## Examples

##### example GET HTTP request

`<code=css>`
    http://localhost:8080/vscp/rest?  
              vscpsession=d1c13eb83f52f319f14d167962048521&
              format=plain&
              op=2
`</code>`  

##  HTTP Request with POST

`<code=css>`
curl -X POST "http://localhost:8080/vscp/rest" \
    -H "vscpsession: d1c13eb83f52f319f14d167962048521" \ 
    -d "op=close&format=plain"     
`</code>`

## Demo

There is a a [demo app](https///github.com/grodansparadis/vscp-ux/tree/master/rest) in the source tree, that demonstrates this functionality using JavaScript.

### JavaScript Request with JSONP

`<code=JavaScript>`
*/*//////////////////////////////////////////////////////////////////
// do_close
//
		
var do_close = function() {
			
    if ( VscpSessionKey.length > 0 ) {	
        $.ajax({
            url: VscpServer + '/vscp/rest?vscpsession=' + VscpSessionKey + '&format=jsonp&op=2',
            type : "GET",
            jsonpCallback: 'handler',
            cache: true,
            dataType: 'jsonp',
            success: function(response) {
                // response will be a JavaScript
		// array of objects
		console.log("-----------------------------------------------------------");
		console.log("                         do_close");
		console.log("-----------------------------------------------------------");
		console.log("Success = " + response.success );
		console.log("Code = " + response.code );
		console.log("Message = " + response.message );
		console.log("Description = " + response.description );
		
	        if (  response.success ) {
                    console.log("Sessionkey cleared"  );
                    VscpSessionKey = "";
                    $("#sessionkey").html("`<b>`Sessionkey`</b>`: " );
                    $("#nevents").html(" " );
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

`<code=javascript>`
typeof handler === 'function' && handler({"success":true,"code":1,"message":"success","description":"Success"});
`</code>`

\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
