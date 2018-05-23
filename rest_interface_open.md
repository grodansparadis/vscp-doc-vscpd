# Open

`<code=css>`
    op=1 or op=OPEN
`</code>`
    
This HTTP request open a new session with the server. This should be the first operation you do when you want to work with the VSCP REST interface. If all goes well you will be handed a session key and you should use this session key in further calls.

For GET requests you put the key in the request URL just as any other value 

    vscpsession=d1c13eb83f52f319f14d167962048521 

and for PUT HTTP requests you place the key in the header as

    vscpsession: d1c13eb83f52f319f14d167962048521 

If you do not use this session key within five minutes it will be invalid and you have to do a new open HTTP request.

**General format:**

`<code=css>`
http://host:port/vscp/rest?
    vscpuser=username&
    vscpsecret=password&
    format=plain|csv|xml|json|jsonp&
    op=1|open     
`</code>`

**Arguments:**


*  **op** - Set to 1|open

*  **format** - Can be 0|plain, 1|csv, 2|xml, 3|json or 4|jsonp.

*  **vscpuser** - A valid username.

*  **vscpuser** - A valid password.

:!:

**note** the __vscpsecret__ has been changed form a md5 password to a clear text password from version 1.12.14.12.

## HTTP Request with GET

`<code=css>`
http://host:port/vscp/rest?vscpuser=username&vscpsecret=password&format=plain|csv|xml|json|jsonp&op=1|open     
`</code>`
    
You can interact with the vscp demo server right now by plugging this into your browser.

`<code=css>`
http://demo.vscp.org:8080/vscp/rest?vscpuser=admin&vscpsecret=secret&format=plain&op=1
`</code>`

See "Read Event" section of REST Interface documentation for more details.  

##  CURL HTTP Request with GET

`<code=bash>`
    curl -X GET "http://localhost:8080/vscp/rest?vscpuser=admin&vscpsecret=secret&format=plain&op=open"
`</code>`

you should get a response with something like

	
	1 1 Success vscpsession=8fa1052598a988ad5166bc9c65f0a167 nEvents=0


where *8fa1052598a988ad5166bc9c65f0a167* is the session id to use for further calls.



##  CURL HTTP Request with POST

`<code=bash>`
curl -X POST "http://localhost:8080/vscp/rest" \
    -H "vscpuser: admin" \
    -H "vscpsecret: d50c3180375c27927c22e42a379c3f67" \ 
    -d "op=open&format=plain"     
`</code>`     

## Demo

There is a a [demo app.](https///github.com/grodansparadis/vscp-ux/tree/master/rest) in the source tree, that demonstrates this functionality using JavaScript.

### Bash sample

The following bash script fetches a session ID and automatically uses it to read VSCP events in plain format.

`<code=bash>`
#!/bin/bash

# Angus Galloway
# fetch a session ID from the daemon, it is valid for 5 minutes.

# option -s for silent
# option -X for specifying request cmd

curl -s -X GET "http://demo.vscp.org:8080/vscp/rest?vscpuser=admin&vscpsecret=secret&format=plain&op=1" > temp_file

awk '{ split($4,arr,"="); print "curl -X GET \"http://demo.vscp.org:8080/vscp/rest?session="arr[2]"&format=plain&op=4\""; }' temp_file

# execute result

awk '{ split($4,arr,"="); print "curl -X GET \"http://demo.vscp.org:8080/vscp/rest?session="arr[2]"&format=plain&op=4\"" | "bash"; }' temp_file
`</code>`

### JavaScript Request with JSONP

`<code=JavaScript>`
$.ajax({
    url: 'http://demo.vscp.org:8080/vscp/rest?vscpuser=admin&vscpsecret=secret&format=jsonp&op=1',
    type : "GET",
    jsonpCallback: 'handler',
    cache: true,
    dataType: 'jsonp',
    success: function(response) {
        // response will be a JavaScript
        // array of objects
        console.log("Success = " + response.success );
        console.log("Code = " + response.code );
        console.log("Message = " + response.message );
        console.log("Description = " + response.description );					
        console.log("Sessionkey = " + response.vscpsession );
        console.log("nEvents = " + response.nEvents );
					
        if (  response.success ) {
            console.log("Session key assigned to global object " + typeof( response.success) );
            gVscpSessionKey = response.vscpsession;
        }
    },
    error: function( xhr, status, error ) {
        console.log( error + " Status:" + status );
    }
});
`</code>`

Use the returned vscpsession key for all other calls.

## Responses

With the format parameter you set the format your want the response represented as. The following shows the positive outcome of the Open HTTP request for all formats available.

##### Response for format=plain

`<code=css>`
1 1 Success vscpsession=d1c13eb83f52f319f14d167962048521 nEvents=0
`</code>`

##### Response for format=csv

`<code=css>`
success_code,error-code,message,description,vscpsession,nEvents
1,1,Success,Success. 1,1,Success,Success,d1c13eb83f52f319f14d167962048521 
`</code>`

##### response for format=xml

`<code=xml>`
<vscp-rest success="true" 
       code="1" message="Success." 
       description="Success.">
       `<vscpsession>`d1c13eb83f52f319f14d167962048521 `</vscpsession>`
       `<nEvents>`0`</nEvents>`
`</vscp-rest>`
`</code>`

##### response for format=json

`<code=css>`
{"success":true,"code":1,"message":"success","description":"Success","vscpsession":"d1c13eb83f52f319f14d167962048521 ","nEvents":0}
`</code>`

##### response for format=jsonp

`<code=css>`
typeof handler === 'function' && handler({"success":true,"code":1,"message":"success","description":"Success","vscpsession":"d1c13eb83f52f319f14d167962048521 ","nEvents":0});
`</code>`



\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
