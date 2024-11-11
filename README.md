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

5. Verify NFS Server installation
   
   Enter the following command to verify the installation of NFS, port 2049 listening state, check if there is anything shared out:
   
   		dkpg -l | grep -i nfs
   
   		ss -ntulp | grep 2049

		showmount -e
<p align="center"> </p>
<img src="https://imgur.com/fMs0z5V.png" height="80%" width="80%" >
<br />    


5. Verify NFS Server installation
   
   Enter the following command to verify the installation of NFS, port 2049 listening state, check if there is anything shared out:
   
   		dkpg -l | grep -i nfs
   
   		ss -ntulp | grep 2049

		showmount -e
<p align="center"> </p>
<img src="https://imgur.com/fMs0z5V.png" height="80%" width="80%" >
<br />    


5. Verify NFS Server installation
   
   Enter the following command to verify the installation of NFS, port 2049 listening state, check if there is anything shared out:
   
   		dkpg -l | grep -i nfs
   
   		ss -ntulp | grep 2049

		showmount -e
<p align="center"> </p>
<img src="https://imgur.com/fMs0z5V.png" height="80%" width="80%" >
<br />    


5. Verify NFS Server installation
   
   Enter the following command to verify the installation of NFS, port 2049 listening state, check if there is anything shared out:
   
   		dkpg -l | grep -i nfs
   
   		ss -ntulp | grep 2049

		showmount -e
<p align="center"> </p>
<img src="https://imgur.com/fMs0z5V.png" height="80%" width="80%" >
<br />    

5. Verify NFS Server installation
   
   Enter the following command to verify the installation of NFS, port 2049 listening state, check if there is anything shared out:
   
   		dkpg -l | grep -i nfs
   
   		ss -ntulp | grep 2049

		showmount -e
<p align="center"> </p>
<img src="https://imgur.com/fMs0z5V.png" height="80%" width="80%" >
<br />    
