# Clear Input queue

```css
    op=6 or op=CLEARQUEUE
```  

Clear the input queue for this clients session. **Requires a valid session parameter**

**General format:**

```css
http://server:port/rest?
    vscpsession=session-key&
    format=plain|csv|xml|json|jsonp&
    op=6|clearqueue
```

**Arguments:**


*  **op** - Set to 6|clearqueue

*  **format** - can be 2|xml, 3|json or 4|jsonp (0|plain and 1|csv returns error).

*  **vscpsession** - A valid session key received from the open method.

## HTTP Request with GET

```css
http://demo.vscp.org:8884/vscp/rest?vscpsession=d1c13eb83f52f319f14d167962048521 &format=plain|csv|xml|json|jsonp&op=6|clearqueue    
```

to test this with **curl** use the following format

```bash
curl -X GET "http://host:port/vscp/rest? \
    vscpsession=d1c13eb83f52f319f14d167962048521 & \
    format=plain|csv|xml|json|jsonp& \
    op=6|clearqueue"
```


## Examples

##### example GET HTTP request

```css
    http://localhost:8884/vscp/rest?  
              vscpsession=d1c13eb83f52f319f14d167962048521&
              format=plain&
              op=6
```  


## HTTP Request with POST

```bash
curl -X POST "http://localhost:8884/vscp/rest" \
    -H "vscpsession: d1c13eb83f52f319f14d167962048521" \ 
    -d "op=clearqueue&format=plain"     
```

## Demo

There is a a [demo app.](https://github.com/grodansparadis/vscp-ux/tree/master/rest) in the source tree, that demonstrates this functionality using JavaScript.

### JavaScript Request with JSONP

```javascript
//////////////////////////////////////////////////////////////////
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
```

## Responses

### Plain

	
	1 1 Success 
	
	Everything is fine.


### CSV

	
	success-code,error-code,message,description
	1,1,Success,Success.


### XML

```xml
<vscp-rest success="true" code="1" message="Success" description="Success."/>
```

### JSON

```css
{"success":true,"code":1,"message":"success","description":"Success"}
```

### JSONP

```javascript
typeof handler === 'function' && handler({"success":true,"code":1,"message":"success","description":"Success"});
```

{% include "./bottom_copyright.md" %}
