---
layout: post
title: 'Configure Static IP Address in CentOS: Quick Howto'
date: '2013-09-09T19:24:00.001-04:00'
author: DatsWorld
tags:
- linux
- Centos
modified_time: '2013-10-07T23:15:56.921-04:00'
blogger_id: tag:blogger.com,1999:blog-1770165193886521985.post-4396308130394296398
blogger_orig_url: http://blog.datsworld.com/2013/09/configure-static-ip-address-in-centos.html
---

Conﬁgurations file for network interfaces are located in **/etc/sysconﬁg/network-scripts/ifcfg-iface**. To configure a static IP address on interface eth0 in CentOS the following changes have to be made to the **/etc/sysconfig/network-scripts/ifcfg-eth0** file:  
```
DEVICE=eth0HWADDR=08:00:27:65:8E:AE
TYPE=Ethernet
UUID=2d9f0a42-8d66-4a5b-a50d-b10016262c5a
# activate interface at startup
ONBOOT=yes
NM_CONTROLLED=yes
# static IP, do not use a boot protocol
BOOTPROTO=no
NETMASK=255.255.255.0
IPADDR=192.168.1.204
GATEWAY=192.168.1.1
# do not allow users to enable and disable
USERCTL=no` 
```
To conifgure a DNS server the **/etc/resolv.conf** file has to be modified:  
```
nameserver 8.8.8.8
nameserver 8.8.4.4
```


For changes to take effect restart the network service: 
``` 
 service network restart` 
```

> Written with [StackEdit](https://stackedit.io/).
