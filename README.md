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
 


5. Verify NFS Server installation
   
   Enter the following command to verify the installation of NFS, port 2049 listening state, check if there is anything shared out. I will not provide screenshot on this step.:
   
   		dkpg -l | grep -i nfs
   
   		ss -ntulp | grep 2049

		showmount -e
  <p align="center"> </p>
<img src="https://imgur.com/fMs0z5V.png" height="80%" width="80%" >
<br />   

6. Download, Install Nagios Plugins
   
   
There are many commands in this step, download the nagios plugins, extract the nagios plugins, configure the plugins for nagios, install the plugins. Set up a firewall rule allow nagios to go through, I configure a firewall rule in my azure. :
   
   		dkpg -l | grep -i nfs
   
   		ss -ntulp | grep 2049

		showmount -e
<p align="center"> </p>
<img src="https://imgur.com/fMs0z5V.png" height="80%" width="80%" >
<br />    
