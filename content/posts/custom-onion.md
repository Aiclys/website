+++
title = 'How to generate a customized .onion address'
author = 'Nyrs'
tags = ["how-to", "online privacy", "self host"]
date = 2024-02-19T19:42:33+01:00
+++

#### After following [this guide](/posts/set-your-site-up-on-the-tor-network) you should have a working tor .onion site. This .onion domain will be generated randomly and most likely won't have anything to do with the actual domain name of your clearnet site. To changes this you can use a tool called [mkp224o](https://github.com/cathugger/mkp224o) to generate a vanity tor onion v3 address. This guide will be for Debian users but it's pretty easy to do it on any other os, you just have to know the name of the packages in the repos of you distro and change the command a little bit to fit your package manager.

### Install dependencies
```
sudo apt install gcc libc6-dev libsodium-dev make autoconf
```

### Clone the Git repo
```
git clone https://github.com/cathugger/mkp224o.git
```

### Change into the mkp224o directory
```
cd mkp224o
```

### Building mkp224o
```
./autogen.sh
./configure
make
```

### Generating the vanity address
#### Replace "desired-key" with the key you want, for example the first 5 letters of your clearnet domain. The shorter the key, the less time it will take to generate it. You also need to replace "number-of-threads" with the number of threads you want to use for this operation (the more threads you use, the faster it will generate the address).
```
./mkp224o desired-key -v -n 1 -d -d ~/new_onion -t number-of-threads
```

###  Copying the address to the tor hidden service directory
```
cp -r ~/new_onion/name-of-your-address/ /var/lib/tor/hidden_service
cd /var/lib/tor/hidden_service/name-of-your-address/
cp * /var/lib/tor/hidden_service/
```

### Restarting tor
```
sudo systemctl restart tor
```

#### To check if everything worked correctly use this command:
```
cat /var/lib/tor/hidden_service/hostname
```
#### If this now outputs the correct .onion address, it worked just fine.
&nbsp;
&nbsp;
## [Go back](/posts/postsintro)
