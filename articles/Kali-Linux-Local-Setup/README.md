# Kali Linux Local Docker Setup
Kali Linux is of course an incredibly popular Linux distribution among the infosec community.
It is configured to leverage many of the popular pen testing and hacking tools such as 
MetaSploit, Nitko, Nmap and more.
When it comes to becoming introduced to pen testing tools, Kali is essential.

For those less familiar with the specifics of deploying bare metal Linux VMs, 
or who wish to deploy Kali in the cloud, using the containerized version of Kali
is an easy way to get started.

Since Kali Linux is such a critical tool it is nice to have a container setup locally
on your laptop or home computer for testing.

First install docker engine for your OS and particular client computer setup.
You can check [Docker Installation Instructions](https://docs.docker.com/engine/install/)
for the details.


The latest Kali Linux image can be pulled onto the machine using

```
sudo docker pull kalilinux/kali-rolling
```

You can view the local images on your machine using 

```
docker images
```

to confirm the kalilinux image has been retrieved.

A Kali container can be spun up by running 

```
sudo docker run -t -d --name kali -i kalilinux/kali-rolling
```

You should get the Kali prompt
```
┌──(root💀49306b781eaa)-[/]
└─#        
```

The running container can be viewed with

```
sudo docker ps -a
```

Note the id of the new Kali container.
You can access a shell of the running container using

```
sudo docker exec -it <container_id> /bin/bash
```

As described in the [official Kali Docker Documentation](https://www.kali.org/docs/containers/official-kalilinux-docker-images/)
you will probably want to install many of the common Kali Linux packages.
This can be achieved by running 

```
apt update && apt -y install kali-linux-headless
```

from inside the Kali container.
Answer the prompted questions as appropriate.
You can check by running the popular vulnerability scanner `nikto`.

```
Processing triggers for php7.4-cli (7.4.21-1+deb11u1+b1) ...
Processing triggers for libapache2-mod-php7.4 (7.4.21-1+deb11u1+b1) ...
Processing triggers for libgdk-pixbuf-2.0-0:arm64 (2.42.6+dfsg-2) ...

┌──(root💀49306b781eaa)-[/]
└─# nikto
- Nikto v2.1.6
---------------------------------------------------------------------------
+ ERROR: No host or URL specified

       -config+            Use this config file
       -Display+           Turn on/off display outputs
       -dbcheck            check database and other key files for syntax errors
       -Format+            save file (-o) format
       -Help               Extended help information
       -host+              target host/URL
       -id+                Host authentication to use, format is id:pass or id:pass:realm
       -list-plugins       List all available plugins
       -output+            Write output to this file
       -nossl              Disables using SSL
       -no404              Disables 404 checks
       -Plugins+           List of plugins to run (default: ALL)
       -port+              Port to use (default 80)
       -root+              Prepend root value to all requests, format is /directory
       -ssl                Force ssl mode on port
       -Tuning+            Scan tuning
       -timeout+           Timeout for requests (default 10 seconds)
       -update             Update databases and plugins from CIRT.net
       -Version            Print plugin and database versions
       -vhost+             Virtual host (for Host header)
   		+ requires a value

```

Congratulations if you made it this far you now have a local Kali Linux container that is ready for
exploit testing!

As always

```
We trust you have received the usual lecture from the local
System Administrator. It usually boils down to these three things:

#1) Respect the privacy of others.

#2) Think before you type.

#3) With great power comes great responsibility.
```
