# Nagios Installation on Amazon Linux EC2 
This guide provides step-by-step instructions to install Nagios on an Amazon Linux EC2 instance.

## Prerequisites

- An Amazon Linux EC2 instance
- SSH access to the instance
- sudo privileges
- Ensure your EC2 instance’s security group allows inbound traffic on port 80 (HTTP)


## Installation Steps

1. **Update the System**
     
    `yum update -y`

2. **Install Prerequisite Software Install Apache, PHP, and other required libraries**

    `yum install httpd php gcc glibc glibc-common gd gd-devel -y`

3. **Create account information, you need to setup a Nagios user**

    `adduser -m nagios`
   
    `passwd nagios`

  *Now it will ask to enter new password and provide any*

   *Now to add group enter these commands*

    `groupadd nagioscmd`
   
    `usermod -a -G nagioscmd nagios`
   
    `usermod -a -G nagioscmd apache`

4. **Download and Install Nagios Core and plugins, now create directories to store the downloaded files**
  
    `mkdir ~/downloads`
   
    `cd ~/downloads`   

5. **Download the source code tarballs of both nagios and the plugins**

    `wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.6.tar.gz`
   
    `wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz` 
     
6. **Extract the nagios source code tarball and install**

    `tar -zxvf nagios-4.4.6.tar.gz`
   
    `cd nagios-4.4.6`
   
7. **Run the configuration script with the name of the group which you have created in above step**

    `./configure --with-command-group=nagioscmd`

8. **Install binaries, init script, sample config files and set permission on the external command directly**

    `make all`
   
    `make install`
   
    `make install-init`
   
    `make install-config`
   
    `make install-commandmode`

9. **---Optional--- You can customize the configuration (e.g. email)**

     `vim /usr/local/nagios/etc/objects/contacts.cfg`   

10. **Configure the web interface**

     `make install-webconf`

11. **Create a `nagiosadmin` account for login into the nagios web interface & set password**

     `htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin`   
   
  
12. **Restart service**

     `service httpd restart`

13. **Compile and install the nagios plugins. Extract the nagios plugins. Source code tarball**

     `cd ~/downloads`

     `tar -zxvf nagios-plugins-2.3.3.tar.gz`
    
     `cd nagios-plugins-2.3.3`    

15. **Configure and install the nagios plugins**

     `./configure --with-nagios-user=nagios --with-nagios-group=nagios`
    
     `make`
    
     `make install`

16. **Enable and start the Nagios service**  
      
     `systemctl enable httpd`
    
     `systemctl start httpd`
    
     `systemctl enable nagios`
    
     `systemctl start nagios`

 18. **Verify the sample nagios configuration files (Optional)**

      `/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg`
          
 19. **You can now start NAGIOS**

      `service nagios start`
     
      `service httpd restart`
     
 21. Now copy the public IP of your ec2 instance and paste the URL on your browser like this *( 12.1.1.1/nagios )*

 22. Provide your username & password your set earlier then goooo.    




















