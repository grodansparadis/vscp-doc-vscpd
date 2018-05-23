# Set Filter

`<code=css>`
    op=5 or op=SETFILTER
`</code>`  
    
Set read filter. Requires a valid **session parameter** and **vscfilter** and **vscpmask** where 

**General format:**
`<code=css>`
http://server:port/rest?
    vscpsession=session-key&
    format=plain|csv|xml|json|jsonp&
    op=5|setfilter&
    vscpfilter=filter&
    vscpmask=mask
`</code>`

**Arguments:**


*  **op** - Set to 5|setfilter

*  **format** - can be 2|xml, 3|json or 4|jsonp (0|plain and 1|csv returns error).

*  **vscpsession** - A valid session key received from the open method.

*  **vscpfilter** - Filter as described above.

*  **vscpmask** - Mask as described above.

**vscpfilter** should be given as

    priority,class,type,GUID
    
and **vscpmask** as

    priority,class,type,GUID

It is possible to leave out parameters as long as they are left out at the end.

To rest the filter (let all events through) set booth stings to

    "0,0,0,00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00"

## HTTP Request with GET

`<code=url>`
http://host:port/vscp/rest?
    vscpsession=d1c13eb83f52f319f14d167962048521&
    format=plain|csv|xml|json|jsonp&
    op=5|setfilter&vscpfilter=filter&vscpmask=mask    
`</code>`

to test this with **curl** use the following format

`<code=css>`
curl -X GET "http://host:port/vscp/rest? \
    vscpsession=d1c13eb83f52f319f14d167962048521 & \
    format=plain|csv|xml|json|jsonp& \
    op=5|setfilter" & \
    vscpfilter=filter & \
    vscpmask=mask
`</code>`


## Examples

##### example GET HTTP request

`<code=css>`
    http://localhost:8080/vscp/rest?  
              vscpsession=d1c13eb83f52f319f14d167962048521&
              format=plain&
              op=5&
              vscpfilter=filter&
              vscpmask=mask
`</code>`  


## HTTP Request with POST

`<code=css>`
curl -X POST "http://localhost:8080/vscp/rest" \
    -H "vscpsession: d1c13eb83f52f319f14d167962048521" \ 
    -d "op=setfilter&format=plain&vscpfilter=filter&vscpmask=mask"     
`</code>`

## Demo

There is a a [demo app.](https///github.com/grodansparadis/vscp-ux/tree/master/rest) in the source tree, that demonstrates this functionality using JavaScript.

### JavaScript Request with JSONP

`<code=JavaScript>`
*/*//////////////////////////////////////////////////////////////////
// do_setFilter
//
		
var do_setFilter = function() {

    // Filter/Mask to filter just to receive heart beats CLASS1.INFORMATION, Type=9 Node heartbeat
    // both are "priority,class,type,guid"
    var txtVscpFilter = "0x0000,0x14,0x09,00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00";
    var txtVscpMask = "0x0000,0xffff,0xffff,00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00";
			
    if ( VscpSessionKey.length > 0 ) {	
        $.ajax({
             url: VscpServer + '/vscp/rest?vscpsession=' + VscpSessionKey + '&format=jsonp&op=setfilter&vscpfilter=' + txtVscpFilter + '&vscpmask=' + txtVscpMask,
             type : "GET",
             jsonpCallback: 'handler',
             cache: true,
             dataType: 'jsonp',
             success: function(response) {
                 // response will be a JavaScript
                 // array of objects
	         console.log("-----------------------------------------------------------");
                 console.log("                         do_setFilter");
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

or clearing the filter

`<code=JavaScript>`
*/*//////////////////////////////////////////////////////////////////
// do_clrFilter
//
		
var do_clrFilter = function() {
			
    if ( VscpSessionKey.length > 0 ) {	
        $.ajax({
            url: VscpServer + '/vscp/rest?vscpsession=' + VscpSessionKey + 
                '&format=jsonp&op=setfilter&vscpfilter=' + 
                "0,0,0,00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00" + 
                '&vscpmask=' + 
                "0,0,0,00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00",
           type : "GET",
           jsonpCallback: 'handler',
           cache: true,
           dataType: 'jsonp',
           success: function(response) {
               // response will be a JavaScript
               // array of objects
               console.log("-----------------------------------------------------------");
               console.log("                         do_clrFilter");
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

	
	
	##  Responses
	
	###  Plain
	`<code>`
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
