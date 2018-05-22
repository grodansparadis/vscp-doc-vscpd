# vscpws_speedometerCelsius

The vscpws_speedometerCelsius is a widget that can be used to display temperature values in an analog way. It is very easy to use and with just one line of code you can have a dynamic thermometer on your web page without any programming knowledge.

## Construction of a vscpws_speedometerCelsius

`<code=javascript>`
vscpws_speedometerCelsius( username,          // username                                                      
                             passwordhash,    // passwordhash, 
                             url, 	     // url to VSCP websocket i/f
                             canvasName, // Placeholder for widget
                             widgetType, // Widget type
                             vscpclass,  // Event class 10/60/65
                             vscptype,   // Event type
                             sensorIndex,// Datacoding sensor index
                             bNumeric,   // Add numeric printout
                             guid )      // GUID we are interested in
`</code>`

### username

Username to logon to the websocket server.

### passwordhash

Password hash to logon to the websocket server

### url

Url to the websocket server. This typically is on the form 

    "ws://192.168.1.20:8080"
    
or

    "wss://192.168.1.20:8080" 
    
if SSL is used.  

With all widgets having there own user/password/url specified for the websocket server it is possible to create web pages that control nodes/units/hardware that are located in different locations from the same page. 

### canvasName

This is the name of the canvas element where the button should be placed. Typically this is defined on the form

`<code=javascript>`
<canvas id="mythermometer1"    
	style="z-index: 1;       
	position:absolute;       
	left:100px;       
	top:200px;" >    
	Your browser does not support HTML5 Canvas. 
`</canvas>`
`</code>`

The id is the parameter that goes for the canvasName. This name is also used to create the instance name for the button and the name set is preceded with vscpws_. The canvas specifies the position for the widget, size is set by to the widgets size. Also z-order is possible to define so that objects can be placed behind, or partially behind each other to get nice visual effects. 

### widgetType

This is the appearance of the widget. Zero i the default value. The following widgets is defined.

**Type = 0 (Default)** \\ 
{{:html5:speedometer:speedometer1.png?nolink|}} 

### vscpclass

This is the the VSCP class of the event we are interested in. This parameter should be set to one of the measurement events 

    VSCP_CLASS1_MEASUREMENT=10 (default), 
    VSCP_CLASS1_DATA=15,
    VSCP_CLASS1_MEASUREMENT64=60 or 
    VSCP_CLASS1_MEASUREZONE=65. 

Set to -1 for don't care. Default is VSCP_CLASS1_MEASUREMENT.

### vscptype

This is the the VSCP type of the event we are interested in. This is normally set to VSCP_TYPE_MEASUREMENT_TEMPERATURE=6 , Set to -1 for don't care. Default is VSCP_TYPE_MEASUREMENT_TEMPERATURE=6.

### sensorindex

This is the sensor index for the sensor in the device sending out the event. This information is part of the datacoding and can be a value 0,1,2,3,4,5,6,7. Set to -1 for don't care. Default=0.

### bNumeric

Set to true to get a numerical representation of the temperature printed out as well. Default=true.

### guid

This can be used to match a specific GUID the event should come from. Default is "" meaning events from all sensors are of interest.

## Methods

       
###  setExtraParameters

To use the vscpws_simpleTextEvent widget with events in class VSCP_CLASS1_MEASUREZONE and VSCP_CLASS1_SETVALUEZONE you may want to filter on more than sensorindex and guid. This method allows the extra info available in these classes to be checked as well. 

**Usage**
`<code=javascript>`
setExtraParameters( index,      // Index if applicable 
                      zone,     // Zone if applicable 
                      subzone)  // Subzone if applicable 
`</code>`

#####  index

This can be used to match a specific index. Default is -1 meaning don't care. Only VSCP_CLASS1_MEASUREZONE and VSCP_CLASS1_SETVALUEZONE have an index to check among the measurement classes.

##### zone

This can be used to match a specific zone. Default is -1 meaning don't care. Only VSCP_CLASS1_MEASUREZONE and VSCP_CLASS1_SETVALUEZONE have a zone to check among the measurement classes.

#####  subzone

This can be used to match a specific subzone. Default is -1 meaning don't care. Only VSCP_CLASS1_MEASUREZONE and VSCP_CLASS1_SETVALUEZONE have a subzone to check among the measurement classes.

### setMonitorVariable

With this method one can set a VSCP daemon variable that should be monitored with a specific interval. The current value of the variable will be written.

**Usage**
`<code=javascript>`
setMonitorVariable( variablename, // variable name 
                     interval )   // monitoring interval in milliseconds
`</code>`

##### variablename

The name for the VSCP daemon boolean variable. 

##### interval

The interval in milliseconds between variable reads. Set to zero to disable. Default=1000 (one second). To test try to set the variable name to "temp1" and issue

    variable write temp1,,,20.5

and

    variable write temp1,,,-12

in the VSCP daemon TCP/IP interface to see the change in your browser page.


## Using the vscpws_speedometerCelsius widget


All vscpws controls have a sample in the **vscp_html5/testws** folder of the
repository [VSCP HTML5 code](http://github.com/grodansparadis/vscp_html5). For the  vscpws_speedometerCelsius control this sample is  
[here](http://github.com/grodansparadis/vscp_html5/blob/master/testws/speedometer.html).

It's very easy to use this widget. Set up a data source that send temperature events on even intervals and then tell the temperature widget to look for them. As always you also need to position your widget somewhere and you do that in the canvas definition. A working example looks like this

`<code=javascript>`
<canvas id="mythermometer2"
   style="z-index: 1;
      position:absolute;
      left:200px;
      top:200px;" >
   Your browser does not support HTML5 Canvas.
`</canvas>`

var temp2 = new vscpws_speedometerCelsius( "ws://192.168.1.20:7681", 
                                              "mythermometer2", 
                                              0,
                                              VSCP_CLASS1_MEASUREMENT,
                                              VSCP_TYPE_MEASUREMENT_TEMPERATURE, 
                                              2 ); 
temp2.setDecimals(0);
`</code>`

which displays measurement temperature data with a widget of type=0 from sensor 2 and the numerics are printed out by default. Also no decimals is printed out

{{:html5:speedometer:speedometer2.png?nolink|}}


No GUID is set here and should normally be added do distinguish data from different sources. 

\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
