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
To power a USB portable 2.5″ hard drive on a Raspberry Pi Model B+ the GPIO pin 38 has to be turned on (has to be set to 1). By default it is off :  
  
```
root@raspberrypi:# gpio -g read 38  
0
```
  
While the hard drive is connected to the Pi and the blkid command is issued the drive does not appear:  
  
```
root@raspberrypi:# blkid  
/dev/mmcblk0p1: SEC_TYPE="msdos" LABEL="boot" UUID="35ED-46FE" TYPE="vfat" PARTUUID="6603105a-01"  
/dev/mmcblk0p2: UUID="443559ba-b80f-4fb6-99d9-ddbcd6138fbd" TYPE="ext4" PARTUUID="6603105a-02"  
```
  
To turn on the GPIO pin 38 the config.txt file located in /boot has to be edited:  
  
```
root@raspberrypi:# nano /boot/config.txt
```
  
Add the following line to the bottom of the file:  

>`max_usb_current=1` 



Reboot the Pi:  
  
```
root@raspberrypi:# reboot
```
  
Check to see if the GPIO pin 38 is set to on:  
  
```
root@raspberrypi:# gpio -g read 38  
1
```
  
Check to see if the drive is visible:  
```
root@raspberrypi:# blkid  
/dev/mmcblk0p1: SEC_TYPE="msdos" LABEL="boot" UUID="35ED-46FE" TYPE="vfat" PARTUUID="6603105a-01"  
/dev/mmcblk0p2: UUID="443559ba-b80f-4fb6-99d9-ddbcd6138fbd" TYPE="ext4" PARTUUID="6603105a-02"  
/dev/sda1: LABEL="SAMSUNG" UUID="3C2C1AB02C1A6564" TYPE="ntfs" PARTUUID="efad9a84-01"  
/dev/mmcblk0: PTUUID="6603105a" PTTYPE="dos"
```

> Written with [StackEdit](https://stackedit.io/).
