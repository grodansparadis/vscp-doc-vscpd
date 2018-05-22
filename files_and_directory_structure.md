# Files and directory structure


{{::vscpd_directory_structure.png|}}

This picture above show the default directory structure for files for a VSCP server. The default installation folder is **/srv/vscp**.


## Folder content

 | Folder      | Content                                                                                                                                                                            | 
 | ------      | -------                                                                                                                                                                            | 
 | **certs**   | Contains SSL certificate and other security related data                                                                                                                           | 
 | **web**     | The default root for the built in web server                                                                                                                                       | 
 | **drivers** | All drivers are here. Level I (CANAL) drives in the **Level I folder** and Level II drivers in  the **Level II folder**. Uploading drivers use these folders and no others.        | 
 | **actions** | The actions folder hold external execution scripts that an be executed from the DM (decision matrix). They all need to recognize action parameters.                                | 
 | **scripts** | JavaScript and Lua scripts are stored here.                                                                                                                                        | 
 | **tables**  | All VSCP tables is  store in this folder.                                                                                                                                          | 
 | **logs**    | Logfiles are here.                                                                                                                                                                 | 
 | **ux**      | User interface packages.                                                                                                                                                           | 
 | **upload**  | Uploaded files goes here. This can be driver, scripts, DM-content, web-content and other content packed in an zip file with a XML manifest that tells how the file should be used. | 

## Databases

### vscpd-database /srv/vscp/vscpd.sqlite3

This is the main configuration file for the VSCP server. It holds discovery information as well as many other things.

If the vscpd server crash for some reason this database may be left locked by the crashed instance. To release the lock firts issue

    fuser /srv/vscp/vscpd.sqlite3

this will list something like

    /srv/vscp/vscpd.sqlite3:   960 12807

the two numbers are process id's. The last is the program we are running and reported the lock. We terminate this program and issue

    kill -9 960

which removes the lock (sends **SIGKILL**). You can read [about signals here](https///en.wikipedia.org/wiki/Signal_(IPC)#List_of_signals).


### log-database /srv/vscp/logs/vscpd_log.sqlite3

Log messages is logged into this database. It can be held at a fixed size with the [logdays switch](https///www.vscp.org/docs/vscpd/doku.php?id=configuring_the_vscp_daemon#logdays) in the configuration file or grow to infinity if left out. 

You can check entries in the log in the admin web interface or you can use the sqlite command line tool. To install this tool use

    sudo apt-get install sqlite 
 
then to open the log database

   sudo sqlite /srv/vscp/logs/vscpd_log.sqlite3  
 

dump the content with

    .dump
 
And jelp giveshelp.

    .help
 
But best is to use sql. To list everything use

    select * from log;

To list a specific log type use

    select date,message from log where type=1;

To list a specific log type between two datestimes use

    select date,message from log where ( date BETWEEN '2018-03-19T00:00:00' AND '2018-03-19T23:23:59' )  AND type=1;

Well you got the drill.

    


