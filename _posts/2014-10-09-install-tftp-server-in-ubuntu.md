---
layout: post
title: 'Install TFTP Server in Ubuntu '
date: '2014-10-09T21:02:00.000-04:00'
author: DatsWorld
tags:
- Ubuntu
- linux
- tftp
- cisco
modified_time: '2014-10-09T21:02:15.472-04:00'
blogger_id: tag:blogger.com,1999:blog-1770165193886521985.post-1559103359176289543
blogger_orig_url: http://blog.datsworld.com/2014/10/install-tftp-server-in-ubuntu.html
---

Configure TFTP server under Ubuntu Linux server to backup configuration files and IOS from networking devices. In this tutorial I am going to install and configure tftpd-hpa. <br /><ol><li><h3><span style="color: #29aae1;">Install the tftpd-hpa package</span></h3></li><pre class="pre1">[root@glt ~]# sudo apt-get install tftpd-hpa</pre><li><h3><span style="color: #29aae1;">Edit tftpd-hpa config file</span></h3></li><pre class="pre1">[root@glt ~]# sudo vi /etc/default/tftpd-hpa</pre><code class="codeblock" style="background-color: #dedede; border: 0px solid rgb(85, 153, 102); color: #242424; display: block; font-family: Courier; font-size: small; line-height: 18px; margin: 0.75em 0px; padding: 5px;"># /etc/default/tftpd-hpa<br /><br />TFTP_USERNAME="tftp"<br />TFTP_DIRECTORY="/tftpboot"<br />TFTP_ADDRESS="0.0.0.0:69"<br />TFTP_OPTIONS="-s -c -4"<br /></code>-s Prevents the remote host from passing along the directory as part of the transfer.<br />-c Allow new files to be created.<br />-4 Connect with IPv4 only.<br /><li><h3><span style="color: #29aae1;">Create TFTP folder.</span></h3></li><pre class="pre1">[root@glt ~]# sudo mkdir /tftpboot<br />[root@glt ~]# $ sudo chmod -R 777 /tftpboot<br />[root@glt ~]# $ sudo chown -R nobody /tftpboot<br /></pre><li><h3><span style="color: #29aae1;">Restart the tftpd-hpa service.</span></h3></li><pre class="pre1">[root@glt ~]# sudo service tftpd-hpa restart</pre><li><h3><span style="color: #29aae1;">Verify that the tftpd-hpa service is running.</span></h3></li><pre class="pre1">[root@glt ~]# ps -ef | grep tftp</pre><pre class="pre1">root     16177     1  0 20:42 ?        00:00:00 /usr/sbin/in.tftpd --listen --user tftp --address 0.0.0.0:69 -s -c -4 /tftpboot</pre></ol><br />