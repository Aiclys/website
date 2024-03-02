+++
title = 'Set up your website on the tor network'
author = 'Nyrs'
tags = ["how-to", "online privacy", "self host"]
date = 2024-02-28T19:42:33+01:00
+++

#### Setting up your own website on the Tor network has many benefits, one of them being that you only need a server and no domain name to set it up. Another benefit is the privacy provided by .onion domains and the Tor network in general. Most registrars publish your personal information, which can be viewed on the public [WHOIS database](https://who.is/), for everyone to view and access. Furthermore, it is very easy to set up if you already have a clearnet website like mine. If you already have a Nginx server set up and running you can skip all of the steps in the "Installing Nginx, the webserver" section.
&nbsp;
&nbsp;
## Install and set up Tor
#### To get the latest version of Tor you need to add the Tor repositories to your system. Before doing that you need to check if your CPU architecture is supported. Be sure that it is either arm64, amd64 or i386. To check that run:
        dpkg --print-architecture
#### Now add the Tor repos:
        apt install -y apt-transport-https gpg
        echo "deb     [signed-by=/usr/share/keyrings/tor-archive-keyring.gpg] https://deb.torproject.org/torproject.org $(lsb_release -cs) main
        deb-src [signed-by=/usr/share/keyrings/tor-archive-keyring.gpg] https://deb.torproject.org/torproject.org $(lsb_release -cs) main" > /etc/apt/sources.list.d/tor.list
#### Then, add the Tor GPG keys tor your keyring by typing this command:
        curl -s https://deb.torproject.org/torproject.org/A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89.asc | gpg --dearmor > /usr/share/keyrings/tor-archive-keyring.gpg
#### After doing all of this, install Tor (it is generally a good idea to do an update and upgrade before installing a new application):
        apt update
        apt upgrade
        apt install tor deb.torproject.org-keyring
#### Now that you installed Tor, you need to enable it. Do this by editing the /etc/tor/torrc file and uncommenting these lines:
        HiddenServiceDir /var/lib/tor/hidden_service/
        HiddenServicePort 80 127.0.0.1:80
#### Now enable the Tor service:
        systemctl enable tor
#### If you didn't encounter any errors, you should be having an active website on the Tor network. To get your default onion address type the following command:
         cat /var/lib/tor/hidden_service/hostname
#### If you want to use a custom one, read [this guide](/posts/custom-onion) which will show you how to do that.
&nbsp;
&nbsp;
## Installing Nginx, the webserver
#### Again, all of the installation instructions will be made for Debian based system. The installation steps can be replicated easily with any other system though. 
### Install Nginx
        apt update
        apt upgrade
        apt install nginx

### Configuring Nginx
#### Create the configuration file by using the following command:
        vim /etc/ngin/sites-available/torsite
#### Or type the following command if you use nano:
        nano /etc/nginx/sites-available/torsite
#### In this example I named the file torsite but you can give it whatever name you want. 
#### After creating the file you need to add the following content to it: 
        server {
            listen 127.0.0.1:80 ;
            root /var/www/website ;
            index index.html ;
            server_name example.onion ;
        }
#### Again, replace example.onion with your onion address (you can also create a customized one by following the steps in [this article](/posts/custom-onion)) and replace the path after root to the path to your website folder.
&nbsp;
&nbsp;
## Enabling the website
#### After saving the file, you need to tell nginx that the website should be enabled. To do that you need to create a symbolic link by typing this command:
        ln -s /etc/nginx/sites-available/website /etc/nginx/sites-enabled
#### Now you can restart the nginx service by typing one of these commands:
        systemctl restart nginx
        systemctl reload nginx
&nbsp;
&nbsp;
## Optional
#### If you have a clearnet website and want to advertise your onion mirror to Tor users, add the following code snippet to your nginx configuration file to add to onion-location header:
        server {
                ...
                add_header Onion-Location http://example.onion$request_uri;
        }
&nbsp;
&nbsp;
## Maintenance
#### Always update all of your packages on a regular basis! To do this type the following command:
        apt update
        apt upgrade
&nbsp;
&nbsp;
## [Go back](/posts/postsintro)
