# Nagios Installation on Amazon Linux EC2 
This guide provides step-by-step instructions to install Nagios on an Amazon Linux EC2 instance.

## Prerequisites

- An Amazon Linux EC2 instance
- SSH access to the instance
- `sudo` privileges
- All port


## Installation Steps

1. **Update the System**
     
   yum update -y

2. **Install Prerequisite Software Install Apache, PHP, and other required libraries**

   yum install httpd php gcc glibc glibc-common gd gd-devel -y

3. **Create account information, you need to setup a Nagios user**

   adduser -m nagios
   
   passwd nagios

  *Now it will ask to enter new password and provide any*

   **Now to add group enter these commands**

   groupadd nagioscmd
   
   usermod -a -G nagioscmd nagios
   
   usermod -a -G nagioscmd apache

4. **Download and Install Nagios Core and plugins, now create directories to store the downloaded files**
  
   mkdir ~/downloads
   
   cd ~/downloads    

6. **Download the source code tarballs of both nagios and the plugins**

   wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.6.tar.gz
   
   wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz 
     
8. **Extract the nagios source code tarball and install**

   tar -zxvf nagios-4.4.6.tar.gz
   
   cd nagios-4.4.6
   
10. **Run the configuration script with the name of the group which you have created in above step**

   ./configure --with-command-group=nagiocmd

   *Compile the nagios source code, run the below command*

    make all

11. **Install binaries, init script, sample config files and set permission on the external command directly**

   make all
   
   make install
   
   make install-init
   
   make install-config
   
   make install-commandmode

11. **Configure the web interface**

   make install-webconf
  
11.  





















