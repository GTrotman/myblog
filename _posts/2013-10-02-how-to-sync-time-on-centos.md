---
layout: post
title: How to Sync Time on CentOS
date: '2013-10-02T22:22:00.003-04:00'
author: DatsWorld
tags:
- NTP
- linux
- time server
- Centos
modified_time: '2013-10-05T23:22:37.218-04:00'
blogger_id: tag:blogger.com,1999:blog-1770165193886521985.post-8224467365845999388
blogger_orig_url: http://blog.datsworld.com/2013/10/how-to-sync-time-on-centos.html
---

To ensure that your system is always using the correct time, you can sync the hardware clock with a remote time server. This can be done in CentOS by using the <annotate title="Network Time Protocol">NTP</annotate> service which is not installed by default. <br /><ol><li><h3><span style="color: #29aae1;">Install <annotate title="Network Time Protocol">NTP</annotate> service</span></h3></li><br /><pre class="pre1">[root@glt ~]# yum install ntp</pre><br /><li><h3><span style="color: #29aae1;">Turn on service</span></h3></li><br /><pre class="pre1">[root@glt ~]# chkconfig ntpd on</pre><br /><li><h3><span style="color: #29aae1;">Synchronize with time server in your zone</span></h3></li><table align="center" border="1" cellpadding="1" cellspacing="1" style="height: 252px; width: 482px;"><tbody><tr bgcolor="#6E6E6E" style="color: #29aae1;"><td>Continental Zones</td><td><annotate title="Uniform Resource Locator">URL</annotate></td></tr><tr><td>Europe </td><td>europe.pool.ntp.org </td></tr><tr><td>Asia </td><td>asia.pool.ntp.org </td></tr><tr><td>Oceania </td><td>oceania.pool.ntp.org </td></tr><tr><td>North America </td><td>north-america.pool.ntp.org </td></tr><tr><td>South America </td><td>south-america.pool.ntp.org </td></tr><tr><td>Africa </td><td>africa.pool.ntp.org </td></tr></tbody></table><br /><pre class="pre1">[root@glt ntp]# ntpdate  north-america.pool.ntp.org<br /> 1 Oct 22:30:26 ntpdate[14429]: adjust time server 72.14.183.239 offset 0.011128 sec</pre><br /><li><h3><span style="color: #29aae1;">Start the <annotate title="Network Time Protocol">NTP</annotate> service</span></h3></li><br /><pre class="pre1">[root@glt ~]# /etc/init.d/ntpd start</pre><br /><li><h3><span style="color: #29aae1;">Verify that the <annotate title="Network Time Protocol">NTP</annotate> service is working </span></h3></li><br /><pre class="pre1">[root@glt ntp]#  ntpq -pn<br />     remote           refid      st t when poll reach   delay   offset  jitter<br />==============================================================================<br /> +198.58.100.237  127.67.113.92    2 u   40   64    1   58.513   -0.780   0.002<br /> +151.236.20.4    193.190.230.65   2 u   39   64    1  260.159    5.373   0.002<br /> *66.175.216.101  127.67.113.92    2 u   38   64    1   81.630   -5.700   0.002<br /></pre></ol>