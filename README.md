# Nagios-Deployment-Guide
Nagios is a powerful, open-source monitoring tool widely used in IT infrastructure for real-time monitoring, alerting, and reporting. Nagios provides comprehensive insights into system health, helping organizations identify and resolve issues before they impact end users or critical business operations.

This repository provides a complete, step-by-step guide for deploying Nagios in a professional environment. It will cover the installation of Nagios Core, the open-source version of Nagios, on a Linux-based server, including initial configuration, setting up monitoring for key services, and configuring notifications.

In this tutorial, I will use Centos as my lab environment, you can pick any distribution you'd like. 
If you need help on how to set a Centos VM on Azure, please click [here](https://www.youtube.com/watch?v=cokJZ2gJhxY)

1. Install required Packages
   
   Ensure that the system has essential packages like gcc, glibc, make, wget, and openssl installed, there are more packages need to be installed.    :
   
   		dnf install httpd php gcc glibc glibc-common gd gd-devel make net-snmp unzip wget
   
   		

		
<p align="center"> </p>
<img src="https://imgur.com/odDHSSA.png" height="80%" width="80%" >
<br />    

2. Create Nagios User and Group
   In this step we want to create nagios user and assign it in the right group:
   
   		useradd nagios
   
   		groupadd nagcmd

		usermod -a -G nagcmd nagios

		usermod -a -G nagcmd apache
<p align="center"> </p>
<img src="https://imgur.com/dyjlKrD.png" height="80%" width="80%" >
<br />    

3. Download and Extract Nagios Core
   
   Changes to /tmp directory, dowload the nagios core file and extracts the downloaded tar.gz file.:
   
   		cd /tmp
   
   		wget -O nagios-4.5.4.tar.gz https://go.nagios.org/l/975333/2024-08-14/6dqd8

		tar xzf nagios-4.5.4.tar.gz

		cd nagios-4.5.4

<p align="center"> </p>
<img src="https://imgur.com/u1qI3Vz.png" height="80%" width="80%" > 
<p align="center"> </p>
<img src="https://imgur.com/CPnLFG7.png" height="80%" width="80%" >
<br />    

4. Configure Nagios Core
   
    Installs development libraries for SSL, needed for secure communication. Configures Nagios, specifying that the nagcmd group will manage command execution permissions:
   
   		dnf install openssl-devel
   
   		./configure --with-command-group=nagcmd

		
<p align="center"> </p>
<img src="https://imgur.com/WG230aF.png" height="80%" width="80%" >
<p align="center"> </p>
<img src="https://imgur.com/an83fsQ.png" height="80%" width="80%" >
<br />  

5.Install Nagios Core

  Compiles the nagios code, install its binaries and files, install script for nagios, configure Apache for nagios web interface:
   
   		make all
   
   		make install

		make install-commandmode
  
  		make install-init

		make install-config
  
  		make install-webconf
 


6. Download, Install Nagios Plugins
   
  There are many commands in this step, download the nagios plugins, extract the nagios plugins, configure the plugins for nagios, install the plugins. Set up a firewall rule allow 	 
  nagios to go through, I configured a firewall rule in my azure environment. :
   
   		cd /tmp
   
   		wget https://nagios-plugins.org/download/nagios-plugins-2.4.11.tar.g

		tar xzf nagios-plugins-2.4.11.tar.gz

		cd nagios-plugins-2.4.11

  		./configure --with-nagios-user=nagios --with-nagios-group=nagios

   		make

   		make install

   		
  <p align="center"> </p>
<img src="https://imgur.com/w0eDgSV.png" height="80%" width="80%" >
<p align="center"> </p>
<img src="https://imgur.com/WbqNO8B.png" height="80%" width="80%" >
 <p align="center"> </p>
<img src="https://imgur.com/92x1RzH.png" height="80%" width="80%" >
<br />   

7. Create Nagios Web Interface Password and Start and Enable Services
   
   Creates a password for nagiosadmin to access the Nagios web interface.:
   
   		htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
   
   		systemctl start httpd

		systemctl enable httpd

		systemctl start nagios

		systemctl enable nagios

		systemctl status nagios
<p align="center"> </p>
<img src="https://imgur.com/AbUZkYM.png" height="80%" width="80%" >
<br />    


8. Configure Hosts in Nagios
   
   Navigates to the directory where Nagios configuration files are stored. Opens hosts.cfg configuration files for editing,  Define monitoring settings for a specific host and a 
   specific service in your own environment :
   
   		cd /usr/local/nagios/etc/objects/
   
   		vi hosts.cfg

		define host {
 use linux-server
 host_name CentosServer
 alias My First Server
 address 192.168.100.162
 max_check_attempts 5
 check_period 24x7
 notification_interval 30
 notification_period 24x7
}
define service {
 use generic-service
 host_name CentosServer
 service_description PING
 check_command check_ping!100.0,20%!500.0,60%
 max_check_attempts 5
 normal_check_interval 5
 retry_check_interval 1
 check_period 24x7
 notification_interval 30
 notification_period 24x7
}



		

<p align="center"> </p>
<img src="https://imgur.com/vjCvrAK.png" height="80%" width="80%" >
<br />  

4. Configure Nagios Core
   
    Installs development libraries for SSL, needed for secure communication. Configures Nagios, specifying that the nagcmd group will manage command execution permissions:
   
   		dnf install openssl-devel
   
   		./configure --with-command-group=nagcmd

		
<p align="center"> </p>
<img src="https://imgur.com/WG230aF.png" height="80%" width="80%" >
<p align="center"> </p>
<img src="https://imgur.com/an83fsQ.png" height="80%" width="80%" >
<br />  
