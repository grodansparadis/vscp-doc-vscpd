# Get Status

`<code=css>`
    op=0 or op=STATUS
`</code>`  

Check status. Can be used to hold the session active but also to check how many event are waiting in the input queue. **Requires a valid session parameter**

**General format:**

`<code=css>`
http://server:port/rest?
    vscpsession=key&
    format='plain|csv|xml|json|jsonp'&
    op='0|status'
`</code>`

**Arguments:**


*  **op** - Set to 0|status

*  **format** - can be 0|plain, 1|csv, 2|xml, 3|json or 4|jsonp.

*  **vscpsession** - A valid session key received from the open method.

## HTTP Request with GET

`<code=css>`
http://demo.vscp.org:8080/vscp/rest?vscpsession=d1c13eb83f52f319f14d167962048521 &format=plain|csv|xml|json|jsonp&op=0|status    
`</code>`

to test this with **curl** use the following format

`<code=css>`
curl -X GET "http://host:port/vscp/rest? \
    vscpsession=d1c13eb83f52f319f14d167962048521 & \
    format=plain|csv|xml|json|jsonp& \
    op=0|status"
`</code>`

## Examples

##### example GET HTTP request

`<code=css>`
    http://localhost:8080/vscp/rest?  
              vscpsession=d1c13eb83f52f319f14d167962048521&
              format=plain&
              op=0
`</code>`  


##  HTTP Request with POST

`<code=css>`
curl -X POST "http://localhost:8080/vscp/rest" \
    -H "vscpsession: d1c13eb83f52f319f14d167962048521" \ 
    -d "op=status&format=plain"     
`</code>`

## Demo

There is a a [demo app.](https///github.com/grodansparadis/vscp-ux/tree/master/rest) in the source tree, that demonstrates this functionality using JavaScript.

### JavaScript Request with JSONP

`<code=JavaScript>`
*/*//////////////////////////////////////////////////////////////////
// do_status
//
		
var do_status = function() {
			
if ( VscpSessionKey.length > 0 ) {	
   $.ajax({
       url: VscpServer + '/vscp/rest?vscpsession=' + VscpSessionKey + '&format=jsonp&op=status',
       type : "GET",
       jsonpCallback: 'handler',
       cache: true,
       dataType: 'jsonp',
       success: function(response) {
           // response will be a JavaScript
           // array of objects
           console.log("-----------------------------------------------------------");
           console.log("                         do_status");
           console.log("-----------------------------------------------------------");
           console.log("Success = " + response.success );
           console.log("Code = " + response.code );
           console.log("Message = " + response.message );
           console.log("Description = " + response.description );
           console.log("Number of events = " + response.nEvents );   
           		
           if (  response.success ) {
               VscpEventCount = response.nEvents;
               $("#nevents").html("`<b>`Number of events in queue`</b>`: " + response.nEvents );
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
	vscpsession=b3c85bb85aa38ecaf25b15a5865178f2 nEvents=14


### CSV

	
	success-code,error-code,message,description,vscpsession,nEvents
	1,1,Success,Success. 1,1,Success,Sucess,b3c85bb85aa38ecaf25b15a5865178f2,84


### XML

`<code=xml>`
`<vscp-rest success="true" code="1" message="Success." description="Success.">`
`<vscpsession>`b3c85bb85aa38ecaf25b15a5865178f2`</vscpsession>`
`<nEvents>`46`</nEvents>`
`</vscp-rest>`
`</code>`

### JSON

`<code=css>`
{"success":true,"code":1,"message":"success","description":"Success","vscpsession":"b3c85bb85aa38ecaf25b15a5865178f2","nEvents":59}
`</code>`

### JSONP

`<code=JavaScript>`
typeof handler === 'function' && handler({"success":true,"code":1,"message":"success","description":"Success","vscpsession":"b3c85bb85aa38ecaf25b15a5865178f2","nEvents":69});
`</code>`


\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
