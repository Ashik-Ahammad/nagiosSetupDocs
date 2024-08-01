# Nagios Installation on Amazon Linux EC2 
Welcome to the Nagios Installation Guide repository! This repository provides a comprehensive guide to installing Nagios on an Amazon Linux EC2 instance. Whether you’re a seasoned sysadmin or a newcomer devops engineer to monitoring systems, this guide will help you set up Nagios efficiently and effectively.

# About Nagios
Nagios is a powerful open-source monitoring system that enables organizations to identify and resolve IT infrastructure problems before they affect critical business processes. With Nagios, you can monitor your entire IT infrastructure, detect problems before they occur, and ensure that your systems, applications, services, networks and business processes are functioning properly.


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

 4. **Now to add group enter these commands**

    `groupadd nagioscmd`
   
    `usermod -a -G nagioscmd nagios`
   
    `usermod -a -G nagioscmd apache`

5. **Download and Install Nagios Core and plugins, now create directories to store the downloaded files**
  
    `mkdir ~/downloads`
   
    `cd ~/downloads`   

6. **Download the source code tarballs of both nagios and the plugins**

    `wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.6.tar.gz`
   
    `wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz` 
     
7. **Extract the nagios source code tarball and install**

    `tar -zxvf nagios-4.4.6.tar.gz`
   
    `cd nagios-4.4.6`
   
8. **Run the configuration script with the name of the group which you have created in above step**

    `./configure --with-command-group=nagioscmd`

9. **Install binaries, init script, sample config files and set permission on the external command directly**

    `make all`
   
    `make install`
   
    `make install-init`
   
    `make install-config`
   
    `make install-commandmode`

10. **---Optional--- You can customize the configuration (e.g. email)**

     `vim /usr/local/nagios/etc/objects/contacts.cfg`   

11. **Configure the web interface**

     `make install-webconf`

12. **Create a *nagiosadmin* account for login into the nagios web interface & set password**

     `htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin`   
   
  
13. **Restart service**

     `service httpd restart`

14. **Compile and install the nagios plugins. Extract the nagios plugins. Source code tarball**

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

 17. **Verify the sample nagios configuration files (Optional)**

      `/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg`
          
 18. **You can now start NAGIOS**

      `service nagios start`
     
      `service httpd restart`
     
 19. Now copy the public IP of your ec2 instance and paste the URL on your browser like this *( 12.1.1.1/nagios )*

 20. Provide your username & password your set earlier then goooo.    



  ##### Contributions are welcome! Feel free to fork this repository, make improvements, and submit pull requests. Your contributions will help others and enhance the quality of this guide. And if you find this helpful, send me a star ⭐ on GitHub. Your support will be appreciated very much!!!


<h3 align="center">
  <a href="https://git.io/typing-svg">
    <img src="https://readme-typing-svg.herokuapp.com/?lines=Ashik+Ahammad...;&center=true&size=30">
  </a>
</h3>














