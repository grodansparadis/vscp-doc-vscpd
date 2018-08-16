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
    
    * [noop](tcp_ip_protocol_description.md#tcpip-noop)
    * [quit](tcp_ip_protocol_description.md#tcpip-quit)
    * [help](tcp_ip_protocol_description.md#tcpip-help)
    * [user](tcp_ip_protocol_description.md#tcpip-use)
    * [pass](tcp_ip_protocol_description.md#tcpip-pass)
    * [challenge](tcp_ip_protocol_description.md#tcpip-challenge)
    * [restart](tcp_ip_protocol_description.md#tcpip-restart)
    * [shutdown](tcp_ip_protocol_description.md#tcpip-shutdown)
    * [send](tcp_ip_protocol_description.md#tcpip-send)
    * [retr](tcp_ip_protocol_description.md#tcpip-retr)
    * [rcvloop](tcp_ip_protocol_description.md#tcpip-rcvloop)
    * [quitloop](tcp_ip_protocol_description.md#tcpip-quitloop)
    * [chkdata](tcp_ip_protocol_description.md#tcpip-chkdata)
    * [clrall](tcp_ip_protocol_description.md#tcpip-clrall)
    * [stat](tcp_ip_protocol_description.md#tcpip-stat)
    * [info](tcp_ip_protocol_description.md#tcpip-info)
    * [chid](tcp_ip_protocol_description.md#tcpip-chid)
    * [setguid](tcp_ip_protocol_description.md#tcpip-setguid)
    * [getguid](tcp_ip_protocol_description.md#tcpip-getguid)
    * [vers](tcp_ip_protocol_description.md#tcpip-version)
    * [setfilter](tcp_ip_protocol_description.md#tcpip-setfilter)
    * [setmask](tcp_ip_protocol_description.md#tcpip-setmask)
    * [wcyd](tcp_ip_protocol_description.md#tcpip-whatcanyoudo)
    * [measurement](tcp_ip_protocol_description.md#tcpip-measurement)

    * [driver](tcp_ip_protocol_description.md#tcpip-driver)
        * [install](tcp_ip_protocol_description.md#tcpip-driver-install)
        * [uninstall](tcp_ip_protocol_description.md#tcpip-driver-uninstall_)
        * [start](tcp_ip_protocol_description.md#tcpip-driver-start)
        * [stop](tcp_ip_protocol_description.md#tcpip-driver-stop)
        * [reload](tcp_ip_protocol_description.md#tcpip-driver-reload)
        * [upgrade](tcp_ip_protocol_description.md#tcpip-driver-upgrade)

    * [file](tcp_ip_protocol_description.md#tcpip-file)
        * [dir](tcp_ip_protocol_description.md#tcpip-file-dir)
        * [copy](tcp_ip_protocol_description.md#tcpip-file-copy)
        * [move](tcp_ip_protocol_description.md#tcpip-file-move)
        * [delete](tcp_ip_protocol_description.md#tcpip-file-delete)
        * [list](tcp_ip_protocol_description.md#tcpip-file-list)

    * [udp](tcp_ip_protocol_description.md#tcpip-udp)
        * [enable](tcp_ip_protocol_description.md#tcpip-udp-enable)
        * [disable](tcp_ip_protocol_description.md#tcpip-udp-disable)
          
    * [remote](tcp_ip_protocol_description.md#tcpip-remote)
        * [list](tcp_ip_protocol_description.md#tcpip-remote-list)
        * [add](tcp_ip_protocol_description.md#tcpip-remote-add)
        * [remove](tcp_ip_protocol_description.md#tcpip-remote-remove)
        * [privelege](tcp_ip_protocol_description.md#tcpip-remote-privilege)
        * [password](tcp_ip_protocol_description.md#tcpip-remote-password)
        * [host-list](tcp_ip_protocol_description.md#tcpip-remote-host-list)
        * [event-list](tcp_ip_protocol_description.md#tcpip-remote-event-list)
        * [filter](tcp_ip_protocol_description.md#tcpip-remote-filter)
        * [mask](tcp_ip_protocol_description.md#tcpip-remote-mask)

    * [interface](tcp_ip_protocol_description.md#tcpip-interface)
        * [list2](tcp_ip_protocol_description.md#tcpip-interface-list)
        * [close](tcp_ip_protocol_description.md#tcpip-interface-close)

    * [dm](tcp_ip_protocol_description.md#tcpip-dm)
        * [enable](tcp_ip_protocol_description.md#tcpip-dm-enable)
        * [disable](tcp_ip_protocol_description.md#tcpip-dm-disable)
        * [list](tcp_ip_protocol_description.md#tcpip-dm-list)
        * [add](tcp_ip_protocol_description.md#tcpip-dm-add)
        * [delete](tcp_ip_protocol_description.md#tcpip-dm-delete)
        * [reset](tcp_ip_protocol_description.md#tcpip-dm-reset)
        * [clrtrig](tcp_ip_protocol_description.md#tcpip-dm-clrtrig)
        * [clrerr](tcp_ip_protocol_description.md#tcpip-dm-clrerr)
        * [save](tcp_ip_protocol_description.md#tcpip-dm-save)
        * [load](tcp_ip_protocol_description.md#tcpip-dm-load)

    * [var](tcp_ip_protocol_description.md#tcpip-var)
        * [list](tcp_ip_protocol_description.md#tcpip-var-list)
        * [write](tcp_ip_protocol_description.md#tcpip-var-write)
        * [read](tcp_ip_protocol_description.md#tcpip-var-read)
        * [readvalue](tcp_ip_protocol_description.md#tcpip-var-readvalue)
        * [writevalue](tcp_ip_protocol_description.md#tcpip-var-writevalue)
        * [readnote](tcp_ip_protocol_description.md#tcpip-var-readnote)
        * [writenote](tcp_ip_protocol_description.md#tcpip-var-writenote)
        * [reset](tcp_ip_protocol_description.md#tcpip-var-reset)
        * [readreset](tcp_ip_protocol_description.md#tcpip-var-readreset)
        * [remove](tcp_ip_protocol_description.md#tcpip-var-remove)
        * [readremove](tcp_ip_protocol_description.md#tcpip-var-readremove)
        * [length](tcp_ip_protocol_description.md#tcpip-var-length)
        * [save](tcp_ip_protocol_description.md#tcpip-var-save)
        * [load](tcp_ip_protocol_description.md#tcpip-var-load)

        ## Table 
        * [table](tcp_ip_protocol_description.md#tcpip-table)
        * [list all](tcp_ip_protocol_description.md#tcpip-table-list)
        * [list table](tcp_ip_protocol_description.md#tcpip-table-list-name)
        * [get](tcp_ip_protocol_description.md#tcpip-table-get)
        * [getraw](tcp_ip_protocol_description.md#tcpip-table-getraw)
        * [log](tcp_ip_protocol_description.md#tcpip-table-log)
        * [logsql](tcp_ip_protocol_description.md#tcpip-table-logsql)
        * [records](tcp_ip_protocol_description.md#tcpip-table-records)
        * [firstdate](tcp_ip_protocol_description.md#tcpip-table-firstdate)
        * [lastdate](tcp_ip_protocol_description.md#tcpip-table-lastdate)
        * [sum](tcp_ip_protocol_description.md#tcpip-table-sum)
        * [sum](tcp_ip_protocol_description.md#tcpip-table-sum)
        * [min](tcp_ip_protocol_description.md#tcpip-table-min)
        * [max](tcp_ip_protocol_description.md#tcpip-table-max)
        * [average](tcp_ip_protocol_description.md#tcpip-table-average)
        * [median](tcp_ip_protocol_description.md#tcpip-table-median)
        * [stddev](tcp_ip_protocol_description.md#tcpip-table-stddev)  
        * [variance](tcp_ip_protocol_description.md#tcpip-table-variance)
        * [mode](tcp_ip_protocol_description.md#tcpip-table-mode)
        * [lowerq](tcp_ip_protocol_description.md#tcpip-table-lowerq)
        * [upperq](tcp_ip_protocol_description.md#tcpip-table-upperq)
        * [clear](tcp_ip_protocol_description.md#tcpip-tcpip-table-clear)
        * [create](tcp_ip_protocol_description.md#tcpip-tcpip-table-create)

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
*  [VSCP Helper lib](https://grodansparadis.gitbooks.io/the-vscp-helper-library)
*  [VSCP Works](https://www.vscp.org/docs/vscpworks/doku.php?id=start)
*  [VSCP Firmware](https://grodansparadis.gitbooks.io/vscp-firmware/)
*  [VSCP L1 Framework](https://github.com/BlueAndi/vscp-framework/blob/master/README.md)
*  [VSCP Arduino](https://github.com/BlueAndi/vscp-arduino)
*  [VSCP Javascript lib.](https://grodansparadis.gitbooks.io/the-vscp-javascript-library/)
*  [VSCP HTML demo](https://www.vscp.org/docs/html5/doku.php)
*  [General VSCP wiki](https://www.vscp.org/wiki/doku.php)