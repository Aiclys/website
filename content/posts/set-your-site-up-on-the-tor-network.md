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
