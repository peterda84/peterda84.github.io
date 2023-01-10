---
title: "Pi-hole"
#header:
#  overlay_image: /assets/images/TO_BE_FILLED
#  overlay_color: "#000"
#  overlay_filter: "0.1"
#  caption: "Photo credit: [**Wikipedia**](https://en.wikipedia.org/wiki/Pi-hole)"
excerpt: "Install Docker Pi-hole on a Raspberry Pi"
---

According to Wikipedia, Pi-hole is a Linux network-level advertisement and Internet tracker blocking application which acts as a DNS sinkhole and optionally a DHCP server, intended for use on a private network. It is designed for low-power embedded devices with network capability, such as the Raspberry Pi, but can be installed on almost any Linux machine.


Installation steps on https://github.com/pi-hole/docker-pi-hole/

Let's have a first attempt, without DHCP and any additional extra configuration

First step is to create a ```docker-compose.yml``` file

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
