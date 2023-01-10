---
title: "Pi-hole"
#header:
#  overlay_image: /assets/images/pihole/pihole_logo.png
#  overlay_color: "#000"
#  overlay_filter: "0.1"
#  caption: "Photo credit: [**Wikipedia**](https://en.wikipedia.org/wiki/Pi-hole)"
excerpt: "Install Docker Pi-hole on a Raspberry Pi"
---

According to Wikipedia, Pi-hole is a Linux network-level advertisement and Internet tracker blocking application which acts as a DNS sinkhole and optionally a DHCP server, intended for use on a private network. It is designed for low-power embedded devices with network capability, such as the Raspberry Pi, but can be installed on almost any Linux machine.

Installation steps, variable descriptions, tips and much more can be found on the project's [Github repo](https://github.com/pi-hole/docker-pi-hole/) and [Documentation page](https://docs.pi-hole.net).

## Quick start

Let's have a first attempt, without DHCP and any additional extra configuration. We are using Ubuntu on the Raspberry Pi:

```console
peterda@ubuntu:~$ cat /etc/issue
Ubuntu 22.04.1 LTS \n \l
```

The first step is to create a ```docker-compose.yml``` file with the following content:

```
version: "3"

services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "80:80/tcp"
    environment:
      TZ: 'America/Argentina/Buenos_Aires'
    volumes:
      - './etc-pihole:/etc/pihole'
      - './etc-dnsmasq.d:/etc/dnsmasq.d'
    restart: unless-stopped
```

Then run ```docker compose up -d``` to build and start pi-hole:

```console
peterda@ubuntu:~/scripts/docker_pihole$ sudo docker compose up -d
[+] Running 10/10
 ⠿ pihole Pulled                                                                                                    55.1s
   ⠿ 4b7f5b2a3113 Pull complete                                                                                     40.9s
   ⠿ 7e9169f3f9b4 Pull complete                                                                                     47.9s
   ⠿ 4f4fb700ef54 Pull complete                                                                                     48.0s
   ⠿ 4ce7bf7952c5 Pull complete                                                                                     48.2s
   ⠿ fb82e4c56a4f Pull complete                                                                                     48.5s
   ⠿ a2e7afb87663 Pull complete                                                                                     48.7s
   ⠿ e142cbff6d10 Pull complete                                                                                     51.6s
   ⠿ 3856f68e7375 Pull complete                                                                                     51.8s
   ⠿ b4add2ae2554 Pull complete                                                                                     52.0s
[+] Running 1/2
 ⠿ Network docker_pihole_default  Created                                                                            0.2s
 ⠿ Container pihole               Starting                                                                          25.6s
Error response from daemon: driver failed programming external connectivity on endpoint pihole (a3e99f68b887ec4a2b671b98a91bceec7f0884d557f7308096cf15ce9e5c0632): Error starting userland proxy: listen tcp4 0.0.0.0:53: bind: address already in use
```

Here I realized that port 53 is already in use. In the same Github repo there is an explanation and solution for the problem on https://github.com/pi-hole/docker-pi-hole/#installing-on-ubuntu-or-fedora

The problem is that Ubuntu 17.10+ includes ```systemd-resolved``` which is configured by default to implement a caching DNS stub resolver. This will prevent pi-hole from listening on port 53. The stub resolver should be disabled with:

```console
peterda@ubuntu:~/scripts/docker_pihole$ sudo sed -r -i.orig 's/#?DNSStubListener=yes/DNSStubListener=no/g' /etc/systemd/resolved.conf
```

Please note the ```-i.orig``` option that make a backup of the ```resolved.conf``` file with .orig extension then edits the file in place.
Then we need to restart systemd-resolved:

```console
peterda@ubuntu:~/scripts/docker_pihole$ sudo systemctl restart systemd-resolved
```

Since we have not configured the ```WEBPASSWORD``` variable in our .yml file, we must run this command to find our random password to the admin page:

```console
peterda@ubuntu:~/scripts/docker_pihole$ sudo docker logs pihole | grep random
s6-rc: info: service s6rc-oneshot-runner: starting
s6-rc: info: service s6rc-oneshot-runner successfully started
s6-rc: info: service fix-attrs: starting
s6-rc: info: service fix-attrs successfully started
s6-rc: info: service legacy-cont-init: starting
s6-rc: info: service legacy-cont-init successfully started
s6-rc: info: service cron: starting
s6-rc: info: service cron successfully started
s6-rc: info: service _uid-gid-changer: starting
s6-rc: info: service _uid-gid-changer successfully started
s6-rc: info: service _startup: starting
  [i] Assigning random password: jd87LF4P
s6-rc: info: service _startup successfully started
s6-rc: info: service pihole-FTL: starting
s6-rc: info: service pihole-FTL successfully started
s6-rc: info: service lighttpd: starting
s6-rc: info: service lighttpd successfully started
s6-rc: info: service _postFTL: starting
s6-rc: info: service _postFTL successfully started
s6-rc: info: service legacy-services: starting
s6-rc: info: service legacy-services successfully started
```

In order to access the admin page, visit http://IP_ADDRESS_OF_YOUR_SERVER/admin. To log in, use the password found in the previous step. You will see something like this:

![image1](/assets/images/pihole/admin_site.jpg)
