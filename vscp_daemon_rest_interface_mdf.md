# Get MDF

`<code=css>`
    op=11 or op=mdf
`</code>`  
    
Get and display MDF for a device. **Requires a valid session parameter**

Intended for devices that can't download the MDF by themselves. Building a web-app. around this functionality is usually a bad idea. It is much better to use the functionality in the [HTML5 & JavaScript library](http://www.vscp.org/docs/html5/doku.php). This is because the VSCP daemon can not always be expected to be available in every setup (typically wireless and Ethernet setups). If that is the case for you (it is available all the time) use this functionality by all means.

**General Format:**

`<code=http>`
http://host:port/vscp/rest?vscpsession=session-key&
    format=xml|json|jsonp&
    op=11|mdf&
    url=http://www.eurosource.se/beijing_2.xml
`</code>`

**Arguments:**


*  **op** - Can be 11|mdf

*  **format** - can be 2|xml, 3|json or 4|jsonp (0|plain and 1|csv returns error).

*  **vscpsession** - A valid session key received from the open method.

*  **url** - the url to the MDF file. 

## HTTP Request with GET

`<code=http>`
http://demo.vscp.org:8080/vscp/rest?vscpsession=d1c13eb83f52f319f14d167962048521&
    format=xml|json|jsonp&
    op=11|mdf&
    url=http://www.eurosource.se/beijing_2.xml
`</code>`

to test this with **curl** use the following format

`<code=css>`
curl -X GET "http://host:port/vscp/rest? 
    vscpsession=d1c13eb83f52f319f14d167962048521 & 
    format=xml|json|jsonp&
    op=11|mdf"&
    url=http://www.eurosource.se/beijing_2.xml
`</code>`

## HTTP Request with POST

`<code=css>`
curl -X POST "http://host:8080/vscp/rest" \
    -H "vscpsession: d1c13eb83f52f319f14d167962048521" \ 
    -d "op=11|mdf&format=xml|json|jsonp&url=http://www.eurosource.se/beijing_2.xml"     
`</code>`

## Demo

There is a a [demo app.](https///github.com/grodansparadis/vscp-ux/tree/master/rest) in the source tree, that demonstrates this functionality using JavaScript.

`<code=uri>`
http://demo.vscp.org:8080/vscp/rest?vscpuser=admin&vscpsecret=d50c3180375c27927c22e42a379c3f67&format=plain&op=1
`</code>`

and you will get a reply

	
	1 1 Success vscpsession=2a280db0de5d7c698faaee0e44a94314 nEvents=0


and now you use the returned VSCP sesson-key 

	
	2a280db0de5d7c698faaee0e44a94314 


in new calls. In this case

`<code=uri>`
http://localhost:8080/vscp/rest?vscpsession=b6d6e355124504cef7da7a6e97c09872&format=xml&op=mdf&url=http://www.eurosource.se/beijing_2.xml
`</code>`

to get the MDF file for the [Beijing node](http://www.grodansparadis.com/beijing/beijing.html).

## Responses

### Format=plain

Not supported.

	
	0 -1 Failure 
	
	General failure.


### Format=csv

Not supported.

	
	success-code,error-code,message,description
	0,-1,Failure,General failure.


### Format=xml

`<code=xml>`
`<!--  Ake Hedman, Grodans Paradis AB  -->`
`<vscp>`
    `<module>`
        `<name>`Beijing IO controller`</name>`
        `<model>`B`</model>`
        `<version>`1.0.4`</version>`
        `<changed>`2015-07-07`</changed>`
        
        .... bla bla bla bla
        
    `</module>`
`</vscp>`
`</code>`

### Format=json

`<code=css>`
{"vscp":
    {"module":{"name":"Beijing IO controller","model":"B","version":"1.0.4","changed":"2015-07-07",
    
    .... bla bla bla bla
    
        frequency0","@value":"$frequency"}}}}
    }
}
`</code>`

### Format=jsonp

`<code=css>`
typeof handler === 'function' && handler({"vscp":
    {"module":{"name":"Beijing IO controller","model":"B","version":"1.0.4","changed":"2015-07-07",
    
    .... bla bla bla bla
    
        frequency0","@value":"$frequency"}}}}
    }
});
`</code>`

\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
