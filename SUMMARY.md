# Summary

* [Start](start.md)
* [Introduction](introduction.md)

## Setup

* [Setting up the system - intro](setting_up_the_system.md)
    * [Linux/Unix](setting_up_the_system_on_unix.md)
    * [Windows](setting_up_the_system_on_windows.md)
    * [Macintosh](setting_up_the_system_on_macintosh.md)
    * [Rasperry Pi](setting_up_the_system_on_rasperry_pi.md)
    * [Beaglebone](setting_up_the_system_on_beaglebone.md)
    * [OpenWrt](setting_up_the_system_on_openwrt.md)
    * [Carambola](setting_up_the_system_on_8devices_carambola.md)
    * [ArchLinuxArm](setting_up_the_system_on_an_embeded_archlinuxarm_system.md)

## Configure

* [Files and directory structure](files_and_directory_structure.md)
* [Configuration file format](configuring_the_vscp_daemon.md)
* [Startup switches](startup_switches.md)

## Server/Service Discovery

* [General](server_disovery.md)
* [High end server probe](server_disovery_probe.md)
* [Heartbeats](server_disovery_heartbeats.md)	

## Security

* [General](security_general.md)

## Decision Matrix

* [Decision Matrix](decision_matrix.md)
* [Actions](decision_matrix.md#actions)
* [Lua scripts](lua_callbacks.md)
* [JavaScript scripts](javascript_callbacks.md)
* [Escapes](decision_matrix.md#variable_substitution_for_)
* [Debugging](decision_matrix_debug.md)
* [Examples](decision_matrix_examples.md)

## Webserver

* [Web Server Interface](web_server_interface.md)
* [Security](web_server_interface_security.md)

## UDP

* [General](udp_protocol_description_general.md)

## Multicast  

* [General](multicast_protocol_description_general.md)
* [Announce](multicast_protocol_description_announce.md)
* [Channels](multicast_protocol_description_channels.md)

## TCPIP Interface

* [TCP/IP Control Interface](tcp_ip_control_interface.md)
* [Security](tcp_ip_control_interface_security.md)
* [TCP/IP Protocol Description](tcp_ip_protocol_description.md)

    ### TCP/IP commands
    
    * [noop](tcp_ip_protocol_description.md#noop)
    * [quit](tcp_ip_protocol_description.md#quit)
    * [help](tcp_ip_protocol_description.md#help)
    * [user](tcp_ip_protocol_description.md#use)
    * [pass](tcp_ip_protocol_description.md#pass)
    * [challenge](tcp_ip_protocol_description.md#challenge)
    * [restart](tcp_ip_protocol_description.md#restart)
    * [shutdown](tcp_ip_protocol_description.md#shutdown)
    * [send](tcp_ip_protocol_description.md#send_-_send_an_event)
    * [retr](tcp_ip_protocol_description.md#retr_-_retrieve)
    * [rcvloop](tcp_ip_protocol_description.md#rcvloop_-_send_)
    * [quitloop](tcp_ip_protocol_description.md#quitloop_-_qui)
    * [chkdata](tcp_ip_protocol_description.md#cdta_chkdata_-_che)
    * [clrall](tcp_ip_protocol_description.md#clra_clrall_-_clear_)
    * [stat](tcp_ip_protocol_description.md#stat_-_get_statistics)
    * [info](tcp_ip_protocol_description.md#info_-_get_st)
    * [chid](tcp_ip_protocol_description.md#chid_-_get_channel_id)
    * [setguid](tcp_ip_protocol_description.md#sgid_setguid_-_set)
    * [getguid](tcp_ip_protocol_description.md#ggid_getguid_-_get_g)
    * [vers](tcp_ip_protocol_description.md#vers_version_-_get_vsc)
    * [setfilter](tcp_ip_protocol_description.md#sflt_setfilter_-_)
    * [setmask](tcp_ip_protocol_description.md#smsk_setmask_-_set)
    * [wcyd](tcp_ip_protocol_description.md#wcyd_whatcanyoudo_-_as)
    * [measurement](tcp_ip_protocol_description.md#measurement_-_)

    * [driver](tcp_ip_protocol_description.md#driver)
        * [install](tcp_ip_protocol_description.md#driver_install)
        * [uninstall](tcp_ip_protocol_description.md#driver_)
        * [start](tcp_ip_protocol_description.md#driver_start)
        * [stop](tcp_ip_protocol_description.md#driver_stop)
        * [reload](tcp_ip_protocol_description.md#driver_reload)
        * [upgrade](tcp_ip_protocol_description.md#driver_upgrade)

    * [file](tcp_ip_protocol_description.md#file)
        * [dir](tcp_ip_protocol_description.md#dir)
        * [copy](tcp_ip_protocol_description.md#copy)
        * [move](tcp_ip_protocol_description.md#move)
        * [delete](tcp_ip_protocol_description.md#delete)
        * [list](tcp_ip_protocol_description.md#list)

    * [udp](tcp_ip_protocol_description.md#udp)
        * [enable](tcp_ip_protocol_description.md#enable)
        * [disable](tcp_ip_protocol_description.md#disable)
          
    * [remote](tcp_ip_protocol_description.md#remote)
        * [list](tcp_ip_protocol_description.md#list1)
        * [add](tcp_ip_protocol_description.md#add)
        * [remove](tcp_ip_protocol_description.md#remove)
        * [privelege](tcp_ip_protocol_description.md#privilege)
        * [password](tcp_ip_protocol_description.md#password)
        * [host-list](tcp_ip_protocol_description.md#host-list)
        * [event-list](tcp_ip_protocol_description.md#event-list)
        * [filter](tcp_ip_protocol_description.md#filter)
        * [mask](tcp_ip_protocol_description.md#mask)

    * [interface](tcp_ip_protocol_description.md#interface)
        * [list2](tcp_ip_protocol_description.md)
        * [close](tcp_ip_protocol_description.md)

    * [dm](tcp_ip_protocol_description.md#dm)
        * [enable](tcp_ip_protocol_description.md#enable1)
        * [disable](tcp_ip_protocol_description.md#disable1)
        * [list](tcp_ip_protocol_description.md#list3)
        * [add](tcp_ip_protocol_description.md#add1)
        * [delete](tcp_ip_protocol_description.md#delete1)
        * [reset](tcp_ip_protocol_description.md#reset)
        * [clrtrig](tcp_ip_protocol_description.md#clrtrig)
        * [clrerr](tcp_ip_protocol_description.md#clrerr)
        * [save](tcp_ip_protocol_description.md#save)
        * [load](tcp_ip_protocol_description.md#load)

    * [var](tcp_ip_protocol_description.md#var)
        * [list](tcp_ip_protocol_description.md#list4)
        * [write](tcp_ip_protocol_description.md#write)
        * [read](tcp_ip_protocol_description.md#read)
        * [readvalue](tcp_ip_protocol_description.md#readvalue)
        * [writevalue](tcp_ip_protocol_description.md#writevalue)
        * [readnote](tcp_ip_protocol_description.md#readnote)
        * [writenote](tcp_ip_protocol_description.md#writenote)
        * [reset](tcp_ip_protocol_description.md#reset1)
        * [readreset](tcp_ip_protocol_description.md#readreset)
        * [remove](tcp_ip_protocol_description.md#remove1)
        * [readremove](tcp_ip_protocol_description.md#readremove)
        * [length](tcp_ip_protocol_description.md#length)
        * [save](tcp_ip_protocol_description.md#save1)
        * [load](tcp_ip_protocol_description.md#load1)

        ## Table 
        * [table](tcp_ip_protocol_description.md#table)
        * [list all](tcp_ip_protocol_description.md#list5)
        * [list table](tcp_ip_protocol_description.md#list_table-)
        * [get](tcp_ip_protocol_description.md#get_table-name_from)
        * [getraw](tcp_ip_protocol_description.md#getraw_table-name)
        * [log](tcp_ip_protocol_description.md#log_table-name_value)
        * [logsql](tcp_ip_protocol_description.md#logsql_table-nam)
        * [records](tcp_ip_protocol_description.md#records_table-n)
        * [firstdate](tcp_ip_protocol_description.md#firstdate_tab)
        * [lastdate](tcp_ip_protocol_description.md#lastdate_table)
        * [sum](tcp_ip_protocol_description.md#sum_table-name_fr)
        * [sum](tcp_ip_protocol_description.md#sum_table-name_fro)
        * [min](tcp_ip_protocol_description.md#min_table-name_from)
        * [max](tcp_ip_protocol_description.md#max_table-name_from)
        * [average](tcp_ip_protocol_description.md#average_table-n)
        * [median](tcp_ip_protocol_description.md#median_table-nam)
        * [stddev](tcp_ip_protocol_description.md#stddev_table-name)  
        * [variance](tcp_ip_protocol_description.md#variance_table)
        * [mode](tcp_ip_protocol_description.md#mode_table-name_fro)
        * [lowerq](tcp_ip_protocol_description.md#lowerq_table-nam)
        * [upperq](tcp_ip_protocol_description.md#upperq_table-nam)
        * [clear](tcp_ip_protocol_description.md#clear_table-name_t)
        * [create](tcp_ip_protocol_description.md#create_table-name)

## Websocket interface
* [Websocket Interface](websocket_interface.md)
* [Security](websocket_interface_security.md)
* [Errors](websocket_protocol_description.md#errors)
* [Protocol Description](./websocket_protocol_description.md)

    ## Websocket Commands
    * [Send Events](websocket_protocol_description.md#send_events)
    * [NOOP](websocket_protocol_description.md#noop)
    * [CHALLENGE](websocket_protocol_description.md#challenge)
    * [ AUTH](websocket_protocol_description.md#auth )
    * [ OPEN](websocket_protocol_description.md#open )
    * [ CLOSE](websocket_protocol_description.md#close )
    * [ CLRQ](websocket_protocol_description.md#clrq )
    * [ SF](websocket_protocol_description.md#sf )
    * [ RVAR](websocket_protocol_description.md#rvar )
    * [ WVAR](websocket_protocol_description.md#wvar )
    * [ CVAR](websocket_protocol_description.md#cvar )
    * [ DELVAR](websocket_protocol_description.md#delvar )
    * [ LSTVAR](websocket_protocol_description.md#lstvar )
    * [ RSTVAR](websocket_protocol_description.md#rstvar )
    * [ LENVAR](websocket_protocol_description.md#lenvar )
    * [ LCVAR](websocket_protocol_description.md#lcvar )
    * [ GT](websocket_protocol_description.md#gt )
    * [ MEASUREMENT](websocket_protocol_description.md#measurement )

## REST interface

* [REST Interface](rest_interface.md)
* [Security](rest_interface_security.md)
* [REST Protocol Description](rest_protocol.md)

## Commands

* [ Open session](rest_interface_open.md)
* [ Close session](rest_interface_close.md)
* [ Get status](rest_interface_status.md)
* [ Send Event](rest_interface_sendevent.md)
* [ Read Event](rest_interface_readevent.md)
* [ Set Filter](rest_interface_setfilter.md)
* [ Clear Input queue](rest_interface_clearinqueue.md)
* [ Create variable](rest_interface_createvar.md)
* [ Delete variable](rest_interface_delvar.md)
* [ Read variable](rest_interface_readvar.md)
* [ Write variable](rest_interface_writevar.md)
* [ List variables](rest_interface_listvar.md)
* [ Send a measurement](rest_interface_measurement.md)
* [ Get Table](rest_interface_table.md)
* [ Get MDF](rest_interface_mdf.md)

## Tables

* [How to use tables](vscp-tables.md)

## Remote Variables

* [Variables Introduced](./remote_variables.md)
* [Variable Types](./remote_variables.md#variable_types)
* [Variable write format](./remote_variables.md#variable_types)
* [Variable persistent storage format](./remote_variables.md#persistent)

## Drivers

*  [Driver Interfaces](driver_interfaces.md)

    * [Level I Drivers](level_i_drivers.md)
        * [API](canal_interface_specification.md)
        * [8Devices USB2CAN Driver](level1_driver_usb2can.md)
        * [Apox Driver](level1_driver_apox.md)
        * [CAN4VSCP Driver](level1_driver_can4vscp.md)
        * [CCS CAN Driver](level1_driver_ccs.md)
        * [IXATT VCI Driver](level1_driver_ixxat.md)
        * [Lawicel CAN232 Driver](level1_driver_can232.md)
        * [level1_driver_canusb](level1_driver_canusb.md)
        * [LIRC Driver](level1_driver_lirc.md)
        * [Logger Driver](level1_driver_logger.md)
        * [PEAK CAN Adapter Driver](level1_driver_peak.md)
        * [Socketcan Driver](level1_driver_socketcan.md)
        * [Tellstick Driver](level1_driver_tellstick.md)
        * [Vector CAN Driver](level1_driver_vector.md)
        * [Zanthic CAN Driver](level1_driver_zanthic.md)

    * [Level II Drivers](level_ii_drivers.md)

        * [API](level_ii_driver_api.md)
        * [Bluetooth proximity driver](level2_driver_bluetooth_proximity.md)
        * [LM-sensors driver](level2_driver_lm_sensors.md)
        * [Logger driver](level2_driver_logger.md)
        * [MQTT driver](level2_driver_mqtt.md)
        * [Raw Ethernet driver](level2_driver_raw_ethernet.md)
        * [Socketcan driver](level2_driver_socketcan.md)
        * [TCP/IP link driver](level2_driver_tcpip_link.md)
        * [Linux 1-wire driver](level2_driver_wire1.md)
        * [Raspberry Pi Linux GPIO driver](level2_driver_rpigpio.md)
        * [Simulation driver](level2_driver_simulation.md)

**Appendix**

* [History](./history.md)
* [Variable persistent storage format](variable_persistent_storage_format.md)
* [Variable write format](variable_types.md)
* [CANAL](canal_interface_specification.md)
* [Test events](test_events.md)

## Other documentation

*  [VSCP Specification](https://grodansparadis.gitbooks.io/the-vscp-specification)
*  [VSCP Helper lib](https://www.vscp.org/docs/vscphelper/doku.php?id=start)
*  [VSCP Works](https://www.vscp.org/docs/vscpworks/doku.php?id=start)
*  [VSCP Firmware](https://www.vscp.org/docs/vscpfirmware/doku.php)
*  [VSCP L1 Framework](https://github.com/BlueAndi/vscp-framework/blob/master/README.md)
*  [VSCP Arduino](https://github.com/BlueAndi/vscp-arduino)
*  [VSCP Javascript lib.](https://grodansparadis.gitbooks.io/the-vscp-javascript-library/)
*  [VSCP HTML demo](https://www.vscp.org/docs/html5/doku.php)
*  [General VSCP wiki](https://www.vscp.org/wiki/doku.php)