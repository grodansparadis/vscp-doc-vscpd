# The 5 second I don't want to read a shit walk through

 1.  Start VSCP daemon
 2.  Start VSCP Works, open a session to the localhost. Se events from simulated driver.
 3.  Open Browser. [http://localhost:8080](http://localhost:8080) and test websocket samples. Data is from the simulation driver.
 4.  Open browser. [http://localhost:8080/vscp](http://localhost:8080/vscp) check the built in administrative interface.

Read on or uninstall.

# Setting up the system on Windows

The VSCP server (the VSCP daemon) is no longer maintained in a special version for Windows. However it runs very well in the bash mode of Windows. Follow the instructions [here](https///www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/) to enable bash and then follow the [Linux/Unix installation](http://www.vscp.org/docs/vscpd/doku.php?id=setting_up_the_system_on_unix) process.


Installing VSCP & Friends for windows is done by installing the latest installation package. All packages are available for download at [Sourceforge](https///sourceforge.net/projects/m2m/files/VSCP%20Software/). All you need to do is to download the file and then run it and the system will be installed for you. 

__From VSCP & Friends version 1.0.0 windows 7 or larger version of Windows is a requirement.__

If you want to compile the package yourself [download the source](https///sourceforge.net/projects/m2m/files/VSCP%20Software/) and read the __BUILD_WIN32.txt__ file in the root of the source folder on how to build the system. You find the source in the same folder as the installation packages. The source for the system is also available on [GitHub](https///github.com/grodansparadis/vscp_software) if you want to use unstable code or just prefers GitHub.

The daemon comes in two flavors on windows. Either **vscpservice** which installs as a service on windows and runs in the background or as **vscpd** which is a standard windows application which opens in a window. The first can be useful for a deployed system while the other is good when you are testing a system or developing new drivers or other components.

A sample configuration file for Windows is [here](https///github.com/grodansparadis/vscp_software/blob/master/config_examples/vscpd.conf_windows_distro) and a sample configuration file is installed for you (see files below).

The two programs which are most important is the **VSCP daemon** and **VSCP Works**. You find them under **VSCP & Friends** under the program menu.  There are many other files in the installation folder which you normally find at

    c:\Program Files (x86)\VSCP

Here is a short description of what you find in this folder.

 | File/Folder        | Description                                                                                                                                                                                                                                                                                                                              | 
 | -----------        | -----------                                                                                                                                                                                                                                                                                                                              | 
 | **vscpd.exe**      | The VSCP Daemon described in this document.                                                                                                                                                                                                                                                                                              | 
 | **vscpworks.exe**  | VSCP Works described [here](http://www.vscp.org/docs/vscpworks/doku.php?id=start)                                                                                                                                                                                                                                                        | 
 | **iflist.exe**     | This little utility can be used to find the id for the raw ethernet driver.                                                                                                                                                                                                                                                              | 
 | **mkpasswd.exe**   | With this utility you can calculate the password hash for users. The hash is constructed by calculating an md5 checksum over **"username:auth-domain:password"**. The auth-domain is set in the vscpd.conf configuration file and is [described here](http://www.vscp.org/docs/vscpd/doku.php?id=configuring_the_vscp_daemon#webserver). | 
 | **uninstall.exe**  | You can uninstall VSCP & Friends with this command                                                                                                                                                                                                                                                                                       | 
 | **drivers\level1** | Contains level I drivers that you can use with the VSCP daemon. They are described [here](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_level_i_drivers).                                                                                                                                                                       | 
 | **drivers\level2** | Contains level II drivers that you can use with the VSCP daemon. They are described her [here](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_level_ii_drivers).                                                                                                                                                                 | 
 | **include**        | This folder contains include files for program development using the [helper lib](http://www.vscp.org/docs/vscphelper/doku.php?id=start).                                                                                                                                                                                                | 
 | **lib**            | This folder contains the helper dll and include lib used for program development using the [helper lib](http://www.vscp.org/docs/vscphelper/doku.php?id=start).                                                                                                                                                                          | 

The other folder that is important to know about is the data and configuration folder. This folder is normally found at 

    c:\ProgramData\VSCP

after an installation. Here is a short description of what you can expect to find in this folder.

 | File/Folder       | Description                                                                                                                                                                                                                                                                                                                                                                     | 
 | -----------       | -----------                                                                                                                                                                                                                                                                                                                                                                     | 
 | **actions**       | This folder contains action scripts run from the [decision matrix](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_decision_matrix)                                                                                                                                                                                                                                      | 
 | **certs**         | Contains som sample certs for SSL                                                                                                                                                                                                                                                                                                                                               | 
 | **logs**          | This is the default location for log files. If you have problems this is the first place to look.                                                                                                                                                                                                                                                                               | 
 | **tables**        | This is the default location for **tables**. VSCP tables is a type of databases where time is one axis and a measurement such as a temperature is another. Can be used to display diagrams or datatables or be used for further data processing. When VSCP & Friends is installed the folder contains three sample tables.                                                      | 
 | **web**           | This is the default web root folder. The folder contains the sample pages from the VSCP [HTML5 project](https///github.com/grodansparadis/vscp_html5) after a fresh installation and demos some of the HTML5 websocket components. This part of the VSCP project is evolving fast so you way want to replace the files here with the ones on github to get the latest greatest. | 
 | **dm.xml**        | This is a sample decision matrix file. You can read more about the decision matrix [here](http://www.vscp.org/docs/vscpd/doku.php?id=vscp_daemon_decision_matrix). The default content in it updates a remote mysql database with measurements and then there is three entries that log data to the sample tables.                                                              | 
 | **variables.xml** | This is a sample persistent variable file. You can read more about VSCP variables [here](http://www.vscp.org/docs/vscpd/doku.php?id=decision_matrix_varaibles). Default content is just some test variables.                                                                                                                                                                    | 
 | **vscp.conf**     | This is the configuration file for the VSCP Daemon. It is described [here](http://www.vscp.org/docs/vscpd/doku.php?id=configuring_the_vscp_daemon).                                                                                                                                                                                                                             | 

## Taking your newly installed system for a test ride

    
To take a newly installed VSCP & Friends system on a test ride [go to this page](new system install test ride).


## vscpd

The vscpd application is just run from it's place in the menu or from it's install location. A window will open after that and display some debug information according to set log level. Quit the VSCP daemon by closing the window.

### Command line switches for vscpd

 | Short switch | Long switch   | Description                                                                                                                                                                                                                                                               | 
 | ------------ | -----------   | -----------                                                                                                                                                                                                                                                               | 
 | -h           | –help       | Give information about available switches and what they do                                                                                                                                                                                                                | 
 | -g           | –gnu        | Gives copyright information.                                                                                                                                                                                                                                              | 
 | -v           | –verbose    | Give extra information useful for debugging                                                                                                                                                                                                                               | 
 | -c           | –configpath | Tell where the program should look for the configuration file. \\ Default is to look for this information in the general “application data” folder in a folder called vscp. \\ Typically this is c:/documents and settings/all users/application data/vscp/vscpd.conf | 
 | -d           | –debuglevel | Set the debug level (0-9). Higher value more output. Default=0                                                                                                                                                                                                            | 
 | -w           | –hide       | Hide the console window. Can be useful if running the app. in a “service way”.                                                                                                                                                                                        | 

## vscpservice

** Version 1.0.0 of VSCP & Friends does not have the Windows service activated. We expect to have this program back in next version. **

When you install VSCP & Friends with the installation software both vscpservice and vscpd will be installed. If you want to run the service you just go to the control panel (//Control Panel/System and Security/Local Services//) and start it there. When it is installed it is set to be started manually and you can also change that at this location so the server is started when windows is started.

### Command line switches for vscpservice

 | Switch    | Description                        | 
 | ------    | -----------                        | 
 | no switch | Start the VSCP daemon as a service | 
 | -i        | Install the service                | 
 | -u        | Uninstall the service              | 
 | -v        | Display service information        | 
 | -? or -h  | Display help                       | 


##### Manually installing the services

The service can be installed with (this is done automatically by the setup program)
    vscpservice -i
Uninstalled with
    vscpservice -u
More info about different switches and the available options can be retrieved by
    vscpservice -? or vscpservice -h
The service has a variable called start at
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\vscpservice
that should be set to 2 (autostart). It is set to 3 (manual) after installation so that you have the option to select which server/service to use.
This can also be done in the service applet (//Control Panel/System and Security/Local Services//).

\\ 
----
{{  ::copyright.png?600  |}}

`<HTML>``<p style="color:red;text-align:center;">``<a href="http://www.grodansparadis.com">`Grodans Paradis AB`</a>``</p>``</HTML>`
 
