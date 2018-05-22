
## Execute a program with argument when TurnOn event is received


*  Set filter to trigger only on the CLASS1.CONTROL, type=5/TurnOn. And it should do so when event is for zone="33", subzone="1" 

*  The action code is set to __Run external program at specific time__.  

*  Action parameter is path to program. 


`<code=xml>`
`<dm>`
    `<row enabled="true" groupid="example">`     
 
    `<!-- Mask to trigger row -->`            
    <mask 
        priority="0" 
        class="0xFFFF" 
        type="0xFF" 
        guid="00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00">
    `</mask>`         
 
    `<!-- Filter to trigger row -->`         
    <filter
        priority="0" 
        class="30" 
        type="5" 
        guid="00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00">
    `</filter>`         
 
    `<!-- Date and time from which action should trigger -->`         
    `<allowed_from>``</allowed_from>`         
 
    `<!-- Date and time up to which action should trigger -->`         
    `<allowed_to>``</allowed_to>`         
 
    `<!-- List of weekdays which action should trigger -->`        
    `<allowed_weekdays>``</allowed_weekdays>`         
 
    `<!-- A specific time (or pattern) when the action should trigger -->`
    `<allowed_time>``</allowed_time>` 
 
    `<!-- Action code -->`         
    `<action>`0x10`</action>`         
 
    `<!-- Action parameter -->`         
    `<param>`/usr/local/bin/killerapp "Hello World!" `</param>`         
 
    `<!-- Comment for decision matrix row -->`         
    `<comment>`
    Execute a program with argument when the ON event is received
    `</comment>`   
 
`</row>` 

`</dm>`
`</code>`



\\ 
----
Copyright (c) 2000-2014 [Åke Hedman](mailto/akhe@grodansparadis.com), [Paradise of the Frog / Grodans Paradis AB](http://www.grodansparadis.com)
