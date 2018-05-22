# Logging measurement data to a MySQL database 

The sample here logs temperature values into a remote MySQL database. You may fist ask  **why do it this way?**. 

Yes your "thingi" can easily log directly to the database. In it's own format etc. But there are advantages to using the VSCP Daemon as a middleman solution. 

 1.  The data from your sensor is standardized using the well accepted SI system.
 2.  Other "thingis" know and understand what you sent. 
 3.  It is easy to configure/change and adopt over time what happens to your measurement. It might, as here, be stored in a database for later use, but may equally be used by some other hardware or software in a live way or be presented on a web page or on a desktop or in a live diagram.   

In the end of course the decision is yours. Is it worth the effort to learn a new framework and adopt the way it looks at the world or not. Only you can make that decision from your own needs.

Also note the built in [table functionality of the VSCP Daemon](http://www.vscp.org/docs/vscpd/doku.php?id=configuring_the_vscp_daemon#tables). It may be a good solution instead of a full database for many situations where you want to log time series for display or later analysis.

----

The database is simple and have the following definition

	
	--
	-- Table structure for table `temperature`
	--
	
	CREATE TABLE IF NOT EXISTS `temperature` (
	  `id` int(11) NOT NULL AUTO_INCREMENT,
	  `GUID` text NOT NULL,
	  `sensorindex` int(11) NOT NULL DEFAULT '0',
	  `Date` datetime NOT NULL,
	  `Value` double NOT NULL DEFAULT '0',
	  PRIMARY KEY (`id`),
	  KEY `Date` (`Date`)
	) ENGINE=InnoDB  DEFAULT CHARSET=utf8 AUTO_INCREMENT=75857 ;


Simple enough. It has a unique **id** for each record. The **GUID** to identify the device that sens the measurement. **SensorIndex** to identify the sensor on that device. And then **date** to time stamp the measurement that is named **value**.

Even if this is a temperature measurement example it works for all [measurement types](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.measurement) of course. As all SI units is defined everything can be logged with a bunch of standard events in a well defined way and everyone will understand what we talk about. 

You may notice that we don't use a **unit** field in this database. This would indicate that we store values using the default unit which is **Kelvin** for a temperature measurement but we are a bit sloppy in this sample as we only is interested in Celsius readings and therefore just store values in degrees Celsius. In a general case that would be a bad idea but this is just an example and as all of them they need to leave som room for improvements.



## Step 1

You first need to install the MySQL package. If you just want to use a remote server select one of the zips's on [this page](http://dev.mysql.com/downloads/mysql/) and unpack it to a folder.

On Linux you install with 

    sudo apt-get install mysql-client-5.5

The version may of course be another when you read this.

## Step 2

You now need to add a decision matrix entry. You can either do this by editing the **dm.xml** file, which usually is in *c:\programdata\vscp*, by hand or use the the daemon interface of the VSCP daemon. In the first case you add the following to your dm-xml file

`<code=xml>`
`<row enable="true" groupid="" >`
    `<mask  priority="0"  class="65535"  type="65535"  GUID=" 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:FF" >` `</mask>`
    `<filter  priority="0"  class="10"  type="6"  GUID=" 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:01" >` `</filter>`
    `<control>`0x0`</control>`
    `<action>`0x10`</action>`
    `<param>`C:\mysql-5.6.21-winx64\bin\mysql.exe -uyour-username -pyour-password -hyour-host your-database -e"INSERT INTO temperature(GUID,SensorIndex,Date,Value) VALUES ('%event.guid',%measurement.index,'%isodate  %isotime', %measurement.float )";`</param>`
    `<comment>``</comment>`
    `<allowed_from>`0000-01-01 00:00:00`</allowed_from>`
    `<allowed_to>`9999-12-31 23:59:59`</allowed_to>`
    `<allowed_weekdays>`mtwtfss`</allowed_weekdays>`
    `<allowed_time>`-*-* *:*:`</allowed_time>`
    `<index measurementindex="true">`1`</index>`
    `</row>`
`</code>`

If you prefer to use the VSCP Daemon admin web interface You enter data as in the following screens

{{:dm:actions:mysql:2014-11-13_12-17-06.png?700|}}
----

**Note:** The select of *Check Index* in the control fields and *Index* set equal to 1 and the select of *Use measurement index* which just logs measurement from sensor 1 of the device. Unselect the *Check Index* to store measurements from all sensors of the device in the database.

and

{{:dm:actions:mysql:2014-11-08_18-31-32.jpg?700|}}
----

looking like this 

{{:dm:actions:mysql:dm_600.png|}}
----

On Linux and other OS's the path to the executable should be different of course. On Linux it is normally located in 

    /usr/bin/mysql


Your own user information goes in here as 
 | User info     | Description                                           | 
 | ---------     | -----------                                           | 
 | your-username | The username you use to log in to the remote database | 
 | your-password | The password you use to log in to the remote database | 
 | your-host     | The host the remote database is located on            | 
 | your-database | The name of your database                             | 

**Note 1:** It may be bad to have username and passwords on a command line  if the configuration file (dm.xml in this case) is not protected. There are other options that are [described here](http://dev.mysql.com/doc/refman/5.0/en/option-files.html).

**Note 2:** The full path with extension is used for the executable. This must always be set that way as the file is checked for existence (and checked if it is really an executable) before  it is executable.


## Step 3

Oh well there is no step 3. That is all that is needed.   What you need now is events that trigger the DM-row. In this case temperature events [CLASS1.MEASUREMENT, Type=6,Temperature](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.measurement#type_6_0x06_temperature) from a unit with nickname 1 on any interface. Notice the GUID mask which only says the LSB of the GUID should be checked. In a live situation you probably should check the full GUID of course. 

And the end result is data filled into your database.

{{:dm:actions:mysql:2014-11-08_18-25-23.jpg?700|}}



\\ 
----
Copyright (c) 2000-2017 [Åke Hedman](mailto/akhe@grodansparadis.com), [Paradise of the Frog / Grodans Paradis AB](http://www.grodansparadis.com)
