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

Conﬁgurations file for network interfaces are located in <b>/etc/sysconﬁg/network-scripts/ifcfg-iface</b>. To configure a static IP address on interface eth0 in CentOS the following changes have to be made to the <b>/etc/sysconfig/network-scripts/ifcfg-eth0</b> file: <br /><code class="codeblock" style="background-color: #dedede; border: 0px solid rgb(85, 153, 102); color: #242424; display: block; font-family: Courier; font-size: small; line-height: 18px; margin: 0.75em 0px; padding: 5px;">DEVICE=eth0<br />HWADDR=08:00:27:65:8E:AE<br />TYPE=Ethernet<br />UUID=2d9f0a42-8d66-4a5b-a50d-b10016262c5a<br /># activate interface at startup<br />ONBOOT=yes<br />NM_CONTROLLED=yes<br /># static IP, do not use a boot protocol<br />BOOTPROTO=no<br />NETMASK=255.255.255.0<br />IPADDR=192.168.1.204<br />GATEWAY=192.168.1.1<br /># do not allow users to enable and disable<br />USERCTL=no<br /></code> To conifgure a <acronym title="Domain Name Server">DNS</acronym> server the <b>/etc/resolv.conf</b> file has to be modified:<br /><code class="codeblock" style="background-color: #dedede; border: 0px solid rgb(85, 153, 102); color: #242424; display: block; font-family: Courier; font-size: small; line-height: 18px; margin: 0.75em 0px; padding: 5px;">nameserver 8.8.8.8<br />nameserver 8.8.4.4<br /></code>For changes to take effect restart the network service:<br /><code class="codeblock" style="background-color: #dedede; border: 0px solid rgb(85, 153, 102); color: #242424; display: block; font-family: Courier; font-size: small; line-height: 18px; margin: 0.75em 0px; padding: 5px;">service network restart</code> <marquee behavior="alternate" scrolldelay="250"><article></article></marquee>