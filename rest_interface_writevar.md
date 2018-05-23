# Write variable

`<code=css>`
    op=8 or op=WRITEVAR
`</code>`  
    
Write/change a remote variable value. If you want to change other parameters then the valiue of a variable use [create Variable](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_rest_interface_creatvar).

**Requires a valid session parameter**

**General form:**
http://host:port/vscp/rest?
    vscpsession=session-key&
    format=plain|csv|xml|json|jsonp&
    op=8|writevar&
    variable=name&
    value=value

**Arguments:**


*  **op** - Set to 8|writevar

*  **format** - can be 2|xml, 3|json or 4|jsonp (0|plain and 1|csv returns error).

*  **vscpsession** - A valid session key received from the open method.

*  **variable** - Name of variable.

*  **value** - Value for variable.

## HTTP Request with GET

`<code=css>`
http://demo.vscp.org:8080/vscp/rest?vscpsession=d1c13eb83f52f319f14d167962048521 &format=plain|csv|xml|json|jsonp&op=8|writevar&variable=name&value=value    
`</code>`

to test this with **curl** use the following format

`<code=css>`
curl -X GET "http://host:port/vscp/rest? \
    vscpsession=d1c13eb83f52f319f14d167962048521 & \
    format=plain|csv|xml|json|jsonp& \
    op=8|writevar"
`</code>`


## Examples

##### example GET HTTP request

`<code=css>`
    http://localhost:8080/vscp/rest?  
              vscpsession=d1c13eb83f52f319f14d167962048521&
              format=plain&
              op=8
`</code>`  

## Curl example HTTP Request with POST

`<code=css>`
curl -X POST "http://localhost:8080/vscp/rest" \
    -H "vscpsession: d1c13eb83f52f319f14d167962048521" \ 
    -d "op=writevar&format=plain"     
`</code>`

## Demo

There is a a [demo app.](https///github.com/grodansparadis/vscp-ux/tree/master/rest) in the source tree, that demonstrates this functionality using JavaScript.

### JavaScript Request with JSONP

`<code=JavaScript>`
*/*//////////////////////////////////////////////////////////////////
// do_writeVariable
//
		
var do_writeVariable = function() {
			
    if ( VscpSessionKey.length > 0 ) {

        var txtVariableName = window.prompt("Name of variable to write:","test");
        var txtVariableValue = window.prompt("New value (BASE64 encoded for string types):","");
				
        $.ajax({
            url: VscpServer + '/vscp/rest?vscpsession=' + VscpSessionKey + 
                    '&format=jsonp&op=writevar&variable=' + txtVariableName +
                    '&value=' + encodeURIComponent( txtVariableValue ),
                    type : "GET",
            jsonpCallback: 'handler',
            cache: true,
            dataType: 'jsonp',
            success: function(response) {
                // response will be a javascript
                // array of objects
                console.log("-----------------------------------------------------------");
                console.log("                   do_writeVariable");
                console.log("-----------------------------------------------------------");
                console.log("Success = " + response.success );
                console.log("Code = " + response.code );
                console.log("Message = " + response.message );
                console.log("Description = " + response.description );
                console.log("Info = " + response.info );
                if ( response.success ) {
                    $("#events").html( "OK Variable written" );
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
