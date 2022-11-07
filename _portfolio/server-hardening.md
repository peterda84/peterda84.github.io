---
title: "Server hardening"
header:
  overlay_image: /assets/images/boinc/HERE_COMES_AN_IMAGE
  overlay_color: "#000"
  overlay_filter: "0.1"
excerpt: "Increase the security of an off-the-shelf server"
---

## Apt update and apt upgrade

```console
peterda@ubuntu:~$ sudo apt update
[sudo] password for peterda:
Hit:1 http://ports.ubuntu.com/ubuntu-ports jammy InRelease
Get:2 http://ports.ubuntu.com/ubuntu-ports jammy-updates InRelease [114 kB]
Get:3 http://ports.ubuntu.com/ubuntu-ports jammy-backports InRelease [99.8 kB]
Get:4 http://ports.ubuntu.com/ubuntu-ports jammy-security InRelease [110 kB]
Get:5 http://ports.ubuntu.com/ubuntu-ports jammy-updates/main arm64 Packages [650 kB]
Get:6 http://ports.ubuntu.com/ubuntu-ports jammy-updates/main Translation-en [159 kB]
Get:7 http://ports.ubuntu.com/ubuntu-ports jammy-updates/main arm64 c-n-f Metadata [10.6 kB]
Get:8 http://ports.ubuntu.com/ubuntu-ports jammy-updates/restricted arm64 Packages [155 kB]
Get:9 http://ports.ubuntu.com/ubuntu-ports jammy-updates/restricted Translation-en [63.1 kB]
Get:10 http://ports.ubuntu.com/ubuntu-ports jammy-updates/restricted arm64 c-n-f Metadata [424 B]
Get:11 http://ports.ubuntu.com/ubuntu-ports jammy-updates/universe arm64 Packages [638 kB]
Get:12 http://ports.ubuntu.com/ubuntu-ports jammy-updates/universe Translation-en [122 kB]
Get:13 http://ports.ubuntu.com/ubuntu-ports jammy-updates/multiverse arm64 Packages [8892 B]
Get:14 http://ports.ubuntu.com/ubuntu-ports jammy-updates/multiverse Translation-en [4228 B]
Get:15 http://ports.ubuntu.com/ubuntu-ports jammy-backports/main arm64 Packages [3012 B]
Get:16 http://ports.ubuntu.com/ubuntu-ports jammy-backports/main Translation-en [1432 B]
Get:17 http://ports.ubuntu.com/ubuntu-ports jammy-backports/main arm64 c-n-f Metadata [272 B]
Get:18 http://ports.ubuntu.com/ubuntu-ports jammy-backports/restricted arm64 c-n-f Metadata [116 B]
Get:19 http://ports.ubuntu.com/ubuntu-ports jammy-backports/universe arm64 Packages [6748 B]
Get:20 http://ports.ubuntu.com/ubuntu-ports jammy-backports/universe Translation-en [9360 B]
Get:21 http://ports.ubuntu.com/ubuntu-ports jammy-backports/universe arm64 c-n-f Metadata [352 B]
Get:22 http://ports.ubuntu.com/ubuntu-ports jammy-backports/multiverse arm64 c-n-f Metadata [116 B]
Get:23 http://ports.ubuntu.com/ubuntu-ports jammy-security/main arm64 Packages [420 kB]
Get:24 http://ports.ubuntu.com/ubuntu-ports jammy-security/main Translation-en [101 kB]
Get:25 http://ports.ubuntu.com/ubuntu-ports jammy-security/restricted arm64 Packages [145 kB]
Get:26 http://ports.ubuntu.com/ubuntu-ports jammy-security/restricted Translation-en [57.4 kB]
Get:27 http://ports.ubuntu.com/ubuntu-ports jammy-security/universe arm64 Packages [499 kB]
Get:28 http://ports.ubuntu.com/ubuntu-ports jammy-security/universe Translation-en [76.6 kB]
Fetched 3456 kB in 5s (642 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
94 packages can be upgraded. Run 'apt list --upgradable' to see them.
```

```console
peterda@ubuntu:~$ sudo apt upgrade
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
The following packages were automatically installed and are no longer required:
  libflashrom1 libftdi1-2
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  linux-headers-5.15.0-1017-raspi linux-image-5.15.0-1017-raspi linux-modules-5.15.0-1017-raspi
  linux-raspi-headers-5.15.0-1017 python3-magic systemd-hwe-hwdb
The following packages will be upgraded:
  apt apt-utils bind9-dnsutils bind9-host bind9-libs binutils binutils-aarch64-linux-gnu binutils-common cloud-init
  cryptsetup cryptsetup-bin cryptsetup-initramfs curl dbus dbus-user-session distro-info-data dmidecode flash-kernel
  fwupd gcc-12-base git git-man gzip isc-dhcp-client isc-dhcp-common libapt-pkg6.0 libbinutils libcryptsetup12
  libctf-nobfd0 libctf0 libcurl3-gnutls libcurl4 libdbus-1-3 libfwupd2 libfwupdplugin5 libgcc-s1 libksba8 libldap-2.5-0
  libldap-common libnftables1 libnss-systemd libntfs-3g89 libpam-systemd libpcre2-8-0 libperl5.34 libpython3-stdlib
  libpython3.10 libpython3.10-minimal libpython3.10-stdlib libssl3 libstdc++6 libsystemd0 libudev1 libxslt1.1
  linux-firmware linux-headers-raspi linux-image-raspi linux-raspi nftables ntfs-3g open-vm-tools openssl perl perl-base
  perl-modules-5.34 python3 python3-distupgrade python3-distutils python3-gdbm python3-jwt python3-lib2to3
  python3-minimal python3-oauthlib python3-software-properties python3-twisted python3.10 python3.10-minimal snapd
  software-properties-common sosreport sudo systemd systemd-sysv systemd-timesyncd tzdata ubuntu-advantage-tools
  ubuntu-release-upgrader-core udev vim vim-common vim-runtime vim-tiny xxd zlib1g
94 upgraded, 6 newly installed, 0 to remove and 0 not upgraded.
52 standard security updates
Need to get 377 MB of archives.
After this operation, 278 MB of additional disk space will be used.
Do you want to continue? [Y/n]
...
```