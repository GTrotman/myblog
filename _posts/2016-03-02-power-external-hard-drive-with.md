---
layout: post
title: Power External Hard Drive with Raspberry Pi B+
date: '2016-03-02T09:53:00.000-05:00'
author: DatsWorld
tags:
- raspbian
- linux
- raspberrypi
- configuration
modified_time: '2016-03-02T14:02:55.276-05:00'
blogger_id: tag:blogger.com,1999:blog-1770165193886521985.post-1318669750651486482
blogger_orig_url: http://blog.datsworld.com/2016/03/power-external-hard-drive-with.html
---

To power a USB portable 2.5″ hard drive on a Raspberry Pi Model B+ the GPIO pin 38 has to be turned on (has to be set to 1). By default it is off :<br /><br /><pre class="pre1">root@raspberrypi:~# gpio -g read 38<br />0</pre><br />While the hard drive is connected to the Pi and the blkid command is issued the drive does not appear:<br /><br /><pre class="pre1">root@raspberrypi:~# blkid<br />/dev/mmcblk0p1: SEC_TYPE="msdos" LABEL="boot" UUID="35ED-46FE" TYPE="vfat" PARTUUID="6603105a-01"<br />/dev/mmcblk0p2: UUID="443559ba-b80f-4fb6-99d9-ddbcd6138fbd" TYPE="ext4" PARTUUID="6603105a-02"<br /></pre><br />To turn on the&nbsp; GPIO&nbsp; pin 38 the config.txt file located in /boot has to be edited:<br /><br /><pre class="pre1">root@raspberrypi:~# nano /boot/config.txt</pre><br />Add the following line to the bottom of the file:<br /><br /><code class="codeblock" style="background-color: #dedede; border: 0px solid rgb(85, 153, 102); color: #242424; display: block; font-family: Courier; font-size: small; line-height: 18px; margin: 0.75em 0px; padding: 5px;">max_usb_current=1</code><br />Reboot the Pi:<br /><br /><pre class="pre1">root@raspberrypi:~# reboot</pre><br />Check to see if the GPIO pin 38 is set to on:<br /><br /><pre class="pre1">root@raspberrypi:~# gpio -g read 38<br />1</pre><br />Check to see if the drive is visible:  <br /><pre class="pre1">root@raspberrypi:~# blkid<br />/dev/mmcblk0p1: SEC_TYPE="msdos" LABEL="boot" UUID="35ED-46FE" TYPE="vfat" PARTUUID="6603105a-01"<br />/dev/mmcblk0p2: UUID="443559ba-b80f-4fb6-99d9-ddbcd6138fbd" TYPE="ext4" PARTUUID="6603105a-02"<br />/dev/sda1: LABEL="SAMSUNG" UUID="3C2C1AB02C1A6564" TYPE="ntfs" PARTUUID="efad9a84-01"<br />/dev/mmcblk0: PTUUID="6603105a" PTTYPE="dos"<br /></pre>