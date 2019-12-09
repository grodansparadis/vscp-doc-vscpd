# Execute the heyu program to control X10 devices

The external program [heyu](http://heyu.tanj.com/) is used to control X10 devices. Here we want to turn on a group of lamps at 18:00 each night except during the summer. But never do this on Saturdays.


*  Set filter/Mask so only the CLASS2.VSCPD Type=6, Minute event is interesting. 

*  allowed_from is set to "2010-10-01"  and allowed_to is set to 2011-4-01 to 

*  allowed_weekdays is set to mtswtf-s to allow the action to take place all days except Saturdays. 

*  allowed_time is "*" as we have no timing constraints.

*  The action code is set to __Run external program at specific time__. 

*  The action parameter is set to the path to the heyu program plus program argument to heyu, in this case “on A13” to turn on switch addressed as A13. 
    
allow the action to occur from October first to April first. 


```xml
<dm>
    <row enabled="true" groupid="example">
 
    <!-- Mask to trigger row -->     
    <mask 
        priority="0" 
        class="0xFFFF" 
        type="0xFF" 
        guid="00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00">
    </mask>
 
    <!-- Filter to trigger row -->
    <filter
        priority="0" 
        class="65532" 
        type="6" 
        guid="00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00">
    </filter>
 
    <!-- Date and time from which action should trigger -->    
    <allowed_from>2010-10-01</allowed_from>
 
    <!-- Date and time up to which action should trigger -->     
    <allowed_to>2011-10-01</allowed_to>
 
    <!-- List of weekdays which action should trigger --> 
    <allowed_weekdays>mtwtf-s</allowed_weekdays>    
 
    <!-- A specific time (or pattern) when the action should trigger -->
    <allowed_time></allowed_time>
    
    <!-- Zone to check -->
    <zone>33</zone>
 
    <!-- Subzone to check -->
    <subzone>1</subzone>
 
    <!-- Action code -->
    <action>0x10</action>
 
    <!-- Action parameter -->
    <param>/usr/local/bin/heyu on A13</param>
 
    <!-- Comment for decision matrix row -->
    <comment>
    Turn on a A13 group of lamps at 18:00 each night except during the summer. But 
    never do this on Saturdays.
    </comment>
 
</row>

</dm>

```


[filename](./bottom_copyright.md ':include')
