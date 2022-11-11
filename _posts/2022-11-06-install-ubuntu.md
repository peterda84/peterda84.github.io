---
title: "Installing Ubuntu Server"
categories:
  - post
tags:
  - portfolio
---

I have always wanted to try some OS on my RPi 4 that is not Raspberry Pi OS. In this post I will show you how easy is to install Ubuntu Server on this hardware.

Step1: Download the official Raspberry Pi Imager [from here](https://www.raspberrypi.com/software/).

![image1](/assets/images/ubuntu/rpi_imager01.png)

Step2: Install the software in 2 easy steps as follows.

![image2](/assets/images/ubuntu/rpi_imager02.png)

![image3](/assets/images/ubuntu/rpi_imager03.png)

Step3: Insert an SD card into your computer. Open the Imager and click on the button 'Choose OS'.

![image4](/assets/images/ubuntu/rpi_imager04.png)

Step4: On the popping menu choose the item 'Other general-purpose OS'.

![image5](/assets/images/ubuntu/rpi_imager05.png)

Step5: On the next step choose 'Ubuntu'.

![image6](/assets/images/ubuntu/rpi_imager06.png)

Step6: Choose the OS version according to your needs. I have opted for Ubuntu Server 22.04 LTS (64-bit).

![image7](/assets/images/ubuntu/rpi_imager07.png)

Step7: Click on the button 'Choose Storage'.

![image8](/assets/images/ubuntu/rpi_imager08.png)

Step8: Choose the SD card you want to install the OS on.

![image9](/assets/images/ubuntu/rpi_imager09.png)

Step9: Click on the small gear icon on the left bottom for Advanced options. Modify the setting as your needs. I have enabled SSH and set a password since I use my Raspberry Pi as a headless server.

![image10](/assets/images/ubuntu/rpi_imager10.png)

Step 10: Click on the button 'Write' and wait until the installation process is done.

![image11](/assets/images/ubuntu/rpi_imager11.png)

Step 11: That's all, you can remove the SD card with the fresh OS installed on it. Insert it into the RPi and start to use.

![image12](/assets/images/ubuntu/rpi_imager12.png)

Step12: Ssh into your server using the credentials you have set in the Imager

```console
C:\Users\david>ssh pi@192.168.88.100
The authenticity of host '192.168.88.100 (192.168.88.100)' can't be established.
ECDSA key fingerprint is SHA256:r55Ed3ca4XO3+xDo2YigYkd1QtRbrTC5SMzhDZKqDJs.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.88.100' (ECDSA) to the list of known hosts.
pi@192.168.88.100's password:
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-1012-raspi aarch64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sun Nov  6 19:28:21 UTC 2022

  System load:  2.14306640625     Temperature:           44.8 C
  Usage of /:   7.6% of 28.94GB   Processes:             149
  Memory usage: 5%                Users logged in:       0
  Swap usage:   0%                IPv4 address for eth0: 192.168.88.100

0 updates can be applied immediately.


The list of available updates is more than a week old.
To check for new updates run: sudo apt update


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
```
