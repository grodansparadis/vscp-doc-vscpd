# The VSCP Daemon


*  [ Start](start )

*  [ Introduction](introduction )

**Setup**


*  [ Setting up the system](setting_up_the_system )

*  [ Linux/Unix](setting_up_the_system_on_unix )

*  [ Windows](setting_up_the_system_on_windows )

*  [ Macintosh](setting_up_the_system_on_macintosh )

*  [ Rasperry Pi](setting_up_the_system_on_rasperry_pi )

*  [ Beaglebone](setting_up_the_system_on_beaglebone )

*  [ OpenWrt](setting_up_the_system_on_openwrt )

*  [ Carambola](setting_up_the_system_on_8devices_carambola )

*  [ ArchLinuxArm](setting_up_the_system_on_an embeded ArchLinuxArm system )

** Configure **


*  [ Files and directory structure ](files and directory structure )

*  [ Configuration file format](configuring_the_vscp_daemon )

*  [ Startup switches](vscp_daemon_startup_switches )

**Server/Service Discovery**


*  [ General](server_disovery )

*  [ High end server probe](server_disovery_probe )

*  [ Heartbeats](server_disovery_heartbeats )	

** Security **


*  [ General](security_general )

**Webserver**


*  [ Web Server Interface](web_server_interface )

*  [ Security](vscp_daemon_web_server_interface_security )

**UDP**


*  [ General](daemon_udp_protocol_description_general )

**Multicast**


*  [ General](daemon_multicast_protocol_description_general )

*  [ Announce](daemon_multicast_protocol_description_announce )

*  [ Channels](daemon_multicast_protocol_description_channels )

**TCP/IP Interface**
 

*  [ TCP/IP Control Interface](vscp_daemon_tcp_ip_control_interface )

*  [ Security](vscp_daemon_tcp_ip_control_interface_security )

**[ TCP/IP Protocol Description](vscp_daemon_tcp_ip_protocol_description )**


*  [ NOOP](vscp_daemon_tcp_ip_protocol_description#noop_-_no_operation )

*  [ QUIT](vscp_daemon_tcp_ip_protocol_description#quit_-_close_the_connection )

*  [ HELP](vscp_daemon_tcp_ip_protocol_description#help_-_give_help )

*  [ USER](vscp_daemon_tcp_ip_protocol_description#user_-_username_for_login )

*  [ PASS](vscp_daemon_tcp_ip_protocol_description#pass_-_password_for_login )

*  [ CHALLENGE](vscp_daemon_tcp_ip_protocol_description#challenge_-_get_challenge_session_id )

*  [ RESTART](vscp_daemon_tcp_ip_protocol_description#restart )

*  [ SHUTDOWN](vscp_daemon_tcp_ip_protocol_description#shutdown )

*  [ SEND](vscp_daemon_tcp_ip_protocol_description#send_-_send_an_event )

*  [ RETR](vscp_daemon_tcp_ip_protocol_description#retr_-_retrieve_one_or_several_event_s )

*  [ RCVLOOP](vscp_daemon_tcp_ip_protocol_description#rcvloop_-_send_events_to_client_as_soon_as_they_arrive )

*  [ QUITLOOP](vscp_daemon_tcp_ip_protocol_description#quitloop_-_quit_receiving_loop )

*  [ CHKDATA](vscp_daemon_tcp_ip_protocol_description#cdta_chkdata_-_check_if_there_are_events_to_retrieve )

*  [ CLRALL](vscp_daemon_tcp_ip_protocol_description#clra_clrall_-_clear_all_events_in_in-queue )

*  [ STAT](vscp_daemon_tcp_ip_protocol_description#stat_-_get_statistics_information )

*  [ NFO](vscp_daemon_tcp_ip_protocol_description#info_-_get_status_information )

*  [ CHID](vscp_daemon_tcp_ip_protocol_description#chid_-_get_channel_id )

*  [ SETGUID](vscp_daemon_tcp_ip_protocol_description#sgid_setguid_-_set_guid_for_channel )

*  [ GETGUID](vscp_daemon_tcp_ip_protocol_description#ggid_getguid_-_get_guid_for_channel )

*  [ VERS](vscp_daemon_tcp_ip_protocol_description#vers_version_-_get_vscp_daemon_version )

*  [ SETFILTER](vscp_daemon_tcp_ip_protocol_description#sflt_setfilter_-_set_incoming_event_filter )

*  [ SETMASK](vscp_daemon_tcp_ip_protocol_description#smsk_setmask_-_set_incoming_event_mask )

*  [ WCYD](vscp_daemon_tcp_ip_protocol_description#wcyd_whatcanyoudo_-_ask_the_capabilities_of_this_server )

*  [ MEASUREMENT](vscp_daemon_tcp_ip_protocol_description#measurement_-_send_a_measurement )

**[ DRIVER](vscp_daemon_tcp_ip_protocol_description#driver )**


*  [ INSTALL](vscp_daemon_tcp_ip_protocol_description#driver_install )

*  [ UNINSTALL](vscp_daemon_tcp_ip_protocol_description#driver_uninstall )

*  [ START](vscp_daemon_tcp_ip_protocol_description#driver_start )

*  [ STOP](vscp_daemon_tcp_ip_protocol_description#driver_stop )

*  [ RELOAD](vscp_daemon_tcp_ip_protocol_description#driver_reload )

*  [ UPGRADE](vscp_daemon_tcp_ip_protocol_description#driver_upgrade )

**[ FILE](vscp_daemon_tcp_ip_protocol_description#file )**


*  [ DIR](vscp_daemon_tcp_ip_protocol_description#dir )

*  [ COPY](vscp_daemon_tcp_ip_protocol_description#copy )

*  [ MOVE](vscp_daemon_tcp_ip_protocol_description#move )

*  [ DELETE](vscp_daemon_tcp_ip_protocol_description#delete )

*  [ LIST](vscp_daemon_tcp_ip_protocol_description#list )

**[UDP](vscp_daemon_tcp_ip_protocol_description#udp)**


*  [ ENABLE](vscp_daemon_tcp_ip_protocol_description#enable )

*  [ DISABLE](vscp_daemon_tcp_ip_protocol_description#disable )

**[ REMOTE](vscp_daemon_tcp_ip_protocol_description#remote )**


*  [ LIST](vscp_daemon_tcp_ip_protocol_description#list1 )

*  [ ADD](vscp_daemon_tcp_ip_protocol_description#add )

*  [ REMOVE](vscp_daemon_tcp_ip_protocol_description#remove )

*  [ PRIVELEGE](vscp_daemon_tcp_ip_protocol_description#privilege )

*  [ PASSWORD](vscp_daemon_tcp_ip_protocol_description#password )

*  [ HOST-LIST](vscp_daemon_tcp_ip_protocol_description#host-list )

*  [ EVENT_LIST](vscp_daemon_tcp_ip_protocol_description#event-list )

*  [ FILTER](vscp_daemon_tcp_ip_protocol_description#filter )

*  [ MASK](vscp_daemon_tcp_ip_protocol_description#mask )

**[ INTERFACE](vscp_daemon_tcp_ip_protocol_description#interface )**


*  [ list2 ](vscp_daemon_tcp_ip_protocol_description )

*  [ close ](vscp_daemon_tcp_ip_protocol_description )

**[ DM](vscp_daemon_tcp_ip_protocol_description#dm )**


*  [ ENABLE](vscp_daemon_tcp_ip_protocol_description#enable1 )

*  [ DISABLE](vscp_daemon_tcp_ip_protocol_description#disable1 )

*  [ LIST](vscp_daemon_tcp_ip_protocol_description#list3 )

*  [ ADD](vscp_daemon_tcp_ip_protocol_description#add1 )

*  [ DELETE](vscp_daemon_tcp_ip_protocol_description#delete1 )

*  [ RESET](vscp_daemon_tcp_ip_protocol_description#reset )

*  [ CLRTRIG](vscp_daemon_tcp_ip_protocol_description#clrtrig )

*  [ CLRERR](vscp_daemon_tcp_ip_protocol_description#clrerr )

*  [ SAVE](vscp_daemon_tcp_ip_protocol_description#save )

*  [ LOAD](vscp_daemon_tcp_ip_protocol_description#load )

**[ VAR](vscp_daemon_tcp_ip_protocol_description#var )**


*  [ LIST](vscp_daemon_tcp_ip_protocol_description#list4 )

*  [ WRITE](vscp_daemon_tcp_ip_protocol_description#write )

*  [ READ](vscp_daemon_tcp_ip_protocol_description#read )

*  [ READVALUE](vscp_daemon_tcp_ip_protocol_description#readvalue )

*  [ WRITEVALUE](vscp_daemon_tcp_ip_protocol_description#writevalue )

*  [ READNOTE](vscp_daemon_tcp_ip_protocol_description#readnote )

*  [ WRITENOTE](vscp_daemon_tcp_ip_protocol_description#writenote )

*  [ RESET](vscp_daemon_tcp_ip_protocol_description#reset1 )

*  [ READRESET](vscp_daemon_tcp_ip_protocol_description#readreset )

*  [ REMOVE](vscp_daemon_tcp_ip_protocol_description#remove1 )

*  [ READREMOVE](vscp_daemon_tcp_ip_protocol_description#readremove )

*  [ LENGTH](vscp_daemon_tcp_ip_protocol_description#length )

*  [ SAVE](vscp_daemon_tcp_ip_protocol_description#save1 )

*  [ LOAD](vscp_daemon_tcp_ip_protocol_description#load1 )

**[ TABLE](vscp_daemon_tcp_ip_protocol_description#table )**


*  [ LIST all](vscp_daemon_tcp_ip_protocol_description#list5 )

*  [ LIST table](vscp_daemon_tcp_ip_protocol_description#list_table-name )

*  [ GET](vscp_daemon_tcp_ip_protocol_description#get_table-name_from_to_full )

*  [ GETRAW](vscp_daemon_tcp_ip_protocol_description#getraw_table-name_from_to )

*  [ LOG](vscp_daemon_tcp_ip_protocol_description#log_table-name_value_datetime )

*  [ LOGSQL](vscp_daemon_tcp_ip_protocol_description#logsql_table-name_sql )

*  [ RECORDS](vscp_daemon_tcp_ip_protocol_description#records_table-name_from_to )

*  [ FIRSTDATE](vscp_daemon_tcp_ip_protocol_description#firstdate_table-name_from_to )

*  [ LAStDATE](vscp_daemon_tcp_ip_protocol_description#lastdate_table-name_from_to )

*  [ SUM](vscp_daemon_tcp_ip_protocol_description#sum_table-name_from_to )

*  [ SUM](vscp_daemon_tcp_ip_protocol_description#sum_table-name_from_to )

*  [ MIN](vscp_daemon_tcp_ip_protocol_description#min_table-name_from_to )

*  [ MAX](vscp_daemon_tcp_ip_protocol_description#max_table-name_from_to )

*  [ AVERAGE](vscp_daemon_tcp_ip_protocol_description#average_table-name_from_to )

*  [ MEDIAN](vscp_daemon_tcp_ip_protocol_description#median_table-name_from_to )

*  [ STDDEV](vscp_daemon_tcp_ip_protocol_description#stddev_table-name_from_to )

*  [ VARIANCE](vscp_daemon_tcp_ip_protocol_description#variance_table-name_from_to )

*  [ MODE](vscp_daemon_tcp_ip_protocol_description#mode_table-name_from_to )

*  [ LOWERQ](vscp_daemon_tcp_ip_protocol_description#lowerq_table-name_from_to )

*  [ UPPERQ](vscp_daemon_tcp_ip_protocol_description#upperq_table-name_from_to )

*  [ CLEAR](vscp_daemon_tcp_ip_protocol_description#clear_table-name_to_from )

*  [ CREATE](vscp_daemon_tcp_ip_protocol_description#create_table-name_create-parameters )


**Websocket**


*  [ Websocket Interface](vscp_daemon_vscp_websocket_interface )

*  [ Security](vscp_daemon_websocket_interface_security )

*  [ Protocol Description](vscp_daemon_websocket_protocol_description )

**Websocket Commands**


*  [ Send Events](vscp_daemon_websocket_protocol_description#send_events )

*  [ NOOP](vscp_daemon_websocket_protocol_description#noop )

*  [ CHALLENGE](vscp_daemon_websocket_protocol_description#challenge )

*  [ AUTH](vscp_daemon_websocket_protocol_description#auth )

*  [ OPEN](vscp_daemon_websocket_protocol_description#open )

*  [ CLOSE](vscp_daemon_websocket_protocol_description#close )

*  [ CLRQ](vscp_daemon_websocket_protocol_description#clrq )

*  [ SF](vscp_daemon_websocket_protocol_description#sf )

*  [ RVAR](vscp_daemon_websocket_protocol_description#rvar )

*  [ WVAR](vscp_daemon_websocket_protocol_description#wvar )

*  [ CVAR](vscp_daemon_websocket_protocol_description#cvar )

*  [ DELVAR](vscp_daemon_websocket_protocol_description#delvar )

*  [ LSTVAR](vscp_daemon_websocket_protocol_description#lstvar )

*  [ RSTVAR](vscp_daemon_websocket_protocol_description#rstvar )

*  [ LENVAR](vscp_daemon_websocket_protocol_description#lenvar )

*  [ LCVAR](vscp_daemon_websocket_protocol_description#lcvar )

*  [ GT](vscp_daemon_websocket_protocol_description#gt )

*  [ MEASUREMENT](vscp_daemon_websocket_protocol_description#measurement )


*  [ Errors](vscp_daemon_websocket_protocol_description#errors )

*  [ Widgets and Javascript library](vscp_daemon_widgets_and_javascript_library )

**Widgets**


*  [ vscpws_Event](vscpws_event )

*  [ vscpws_Variable](vscpws_variable )

*  [ vscpws_stateButton](vscpws_statebutton )

*  [ vscpws_simpleText](vscpws_simpletext )

*  [ vscpws_thermometerCelsius](vscpws_thermometercelsius )

*  [ vscpws_speedometerCelsius](vscpws_speedometercelsius )

**REST interface**


*  [ REST Interface](vscp_daemon_vscp_daemon_rest_interface )

*  [ Security](vscp_daemon_rest_interface_security )

*  [ REST Protocol Description](vscp_daemon_rest_protocol )

*  **Commands**

*  [ Open session](vscp_daemon_rest_interface_open )

*  [ Close session](vscp_daemon_rest_interface_close )

*  [ Get status](vscp_daemon_rest_interface_status )

*  [ Send Event](vscp_daemon_rest_interface_sendevent )

*  [ Read Event](vscp_daemon_rest_interface_readevent )

*  [ Set Filter](vscp_daemon_rest_interface_setfilter )

*  [ Clear Input queue](vscp_daemon_rest_interface_clearinqueue )

*  [ Create variable](vscp_daemon_rest_interface_creatvar )

*  [ Delete variable](vscp_daemon_rest_interface_delvar )

*  [ Read variable](vscp_daemon_rest_interface_readvar )

*  [ Write variable](vscp_daemon_rest_interface_writevar )

*  [ List variables](vscp_daemon_rest_interface_listvar )

*  [ Send a measurement](vscp_daemon_rest_interface_measurement )

*  [ Get Table](vscp_daemon_rest_interface_table )

*  [ Get MDF](vscp_daemon_rest_interface_mdf )

**Decision Matrix**


*  [ Decision Matrix](vscp_daemon_decision_matrix )

*  [ Actions](vscp_daemon_decision_matrix#actions )

*  [ Lua scripts](lua_callbacks )

*  [ JavaScript scripts](javascript_callbacks )

*  [ Escapes](vscp_daemon_decision_matrix#variable_substitution_for_parameters_escapes )

*  [ Debugging](vscp_daemon_decision_matrix_debug )

*  [ Examples](decision_matrix_examples )

**Tables**


*  [ How to use tables](vscp-tables )

**Remote Variables**


*  [ Variables Introduced](decision_matrix_varaibles )

*  [ Variable Types](decision_matrix_varaibles#variable_types )

*  [ Variable write format](decision_matrix_varaibles#variable_types )

*  [ Variable persistent storage format](decision_matrix_varaibles#persistent_storage_format )

**Drivers**


*  [ Driver Interfaces](vscp_daemon_driver_interfaces )

**[ Level I Drivers](vscp_daemon_level_i_drivers )**


*  [ API](canal_interface_specification )

*  [ 8Devices USB2CAN Driver](level1_driver_usb2can )

*  [ Apox Driver](level1_driver_apox )

*  [ CAN4VSCP Driver](level1_driver_can4vscp )

*  [ CCS CAN Driver](level1_driver_ccs )

*  [ IXATT VCI Driver](level1_driver_ixxat )

*  [ Lawicel CAN232 Driver](level1_driver_can232 )

*  [[level1_driver_canusb | Lawicel CANUSB DriverV

*  [ LIRC Driver](level1_driver_lirc )

*  [ Logger Driver](level1_driver_logger )

*  [ PEAK CAN Adapter Driver](level1_driver_peak )

*  [ Socketcan Driver](level1_driver_socketcan )

*  [ Tellstick Driver](level1_driver_tellstick )

*  [ Vector CAN Driver](level1_driver_vector )

*  [ Zanthic CAN Driver](level1_driver_zanthic )

**[ Level II Drivers](vscp_daemon_level_ii_drivers )**


*  [ API](vscp_daemon_level_ii_driver_api )

*  [ Bluetooth proximity driver](level2_driver_bluetooth_proximity )

*  [ LM-sensors driver](level2_driver_lm_sensors )

*  [ Logger driver](level2_driver_logger )

*  [ MQTT driver](level2_driver_mqtt )

*  [ Raw Ethernet driver](level2_driver_raw_ethernet )

*  [ Socketcan driver](level2_driver_socketcan )

*  [ TCP/IP link driver](level2_driver_tcpip/link )

*  [ Linux 1-wire driver](level2_driver_wire1 )

*  [ Raspberry Pi Linux GPIO driver](level2_driver_rpigpio )

*  [ Simulation driver](level2_driver_simulation )
 

**Appendix**


*  [ History](history )

*  [ Variable persistent storage format](vscp_daemon_variable_persistent_storage_format )

*  [ Variable write format](vscp_daemon_variable_string_write_format )>

*  [ CANAL](canal_interface_specification )

*  [Test events](Test events)

**Other documentation**


*  [ VSCP Specification](https///www.vscp.org/docs/vscpspec/doku.php?id=start )

*  [ VSCP Helper lib](https///www.vscp.org/docs/vscphelper/doku.php?id=start )

*  [ VSCP Works](https///www.vscp.org/docs/vscpworks/doku.php?id=start )

*  [ VSCP Firmware](https///www.vscp.org/docs/vscpfirmware/doku.php )

*  [ VSCP L1 Framework](https///github.com/BlueAndi/vscp-framework/blob/master/README.md )

*  [ VSCP Arduino](https///github.com/BlueAndi/vscp-arduino )

*  [ HTML & Javascript](https///www.vscp.org/docs/html5/doku.php )

*  [ General VSCP wiki ](https///www.vscp.org/wiki/doku.php )


