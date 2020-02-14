---
layout: post
title: Basic Howto on IPTables on Centos
date: '2013-09-06T15:59:00.000-04:00'
author: DatsWorld
tags:
- firewall
- linux
- Centos
- IPtables
modified_time: '2013-09-25T15:09:24.777-04:00'
thumbnail: http://2.bp.blogspot.com/-yarqXxZc6ik/Uik6vCr9SvI/AAAAAAAAAB0/QfLtaI3zYtQ/s72-c/iptable_filter_table.jpg
blogger_id: tag:blogger.com,1999:blog-1770165193886521985.post-6354008807468838749
blogger_orig_url: http://blog.datsworld.com/2013/09/basic-howto-on-iptables-on-centos.html
---

IPTables is a firewall software tool used in Linux software distributions to administer IPv4 packet filtering and NAT. It can be used to set up, maintain, and inspect IP packet filter rules in the Linux kernel. Iptables is installed by default on all CentOS 5.x and 6.x.  
  
IPTables has 4 built-in tables the filter table, NAT table, mangle table and raw table. Each table contain chains and within each chain there are rules. The filter table is configured in CentOS 5.x and 6.x. There are 3 predefined chains in the filter table to which rules are added. The following are the chains in the filter table:  

> -   INPUT chain – Incoming to firewall. For packets coming to the local server.
> -   OUTPUT chain – Outgoing from firewall. For packets generated locally and going out of the local server.
> -   FORWARD chain – Packet for another NIC on the local server. For packets routed through the local server.

[![](https://camo.githubusercontent.com/20c17d52858974b533132705e3d47ab8af7ba3f6/687474703a2f2f322e62702e626c6f6773706f742e636f6d2f2d7961727158785a6336696b2f55696b36764372395376492f41414141414141414142302f51664c746149337a5974512f733332302f69707461626c655f66696c7465725f7461626c652e6a7067)](http://2.bp.blogspot.com/-yarqXxZc6ik/Uik6vCr9SvI/AAAAAAAAAB0/QfLtaI3zYtQ/s1600/iptable_filter_table.jpg)

###   

### List rules in the filter table

  
The following displays the list of rules in the filter table. The -n option show the numeric format of the IP address and port number, the -v option displays the packet count, the -L list the ruleset and the --line-numbers option list the line number of the rule:  
  
iptables -nvL --line-numbers  
  
```
[root@glt ~]# iptables -nvL --line-numbers  
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
1    3777K 5463M ACCEPT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           state RELATED,ESTABLISHED  
2       80  2837 ACCEPT     icmp --  *      *       0.0.0.0/0            0.0.0.0/0  
3       10   440 ACCEPT     all  --  lo     *       0.0.0.0/0            0.0.0.0/0  
4      186 10820 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0           state NEW tcp dpt:22  
5      900 60201 REJECT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited  
  
Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
1        0     0 REJECT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited  
  
Chain OUTPUT (policy ACCEPT 2329K packets, 141M bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
```
###   

### Appending Rules

  
The following adds a Rule at the end of the specified chain of IPTables. The -A option appends the rule, -p is used to select the protocol, --dport indicates the destination port and -j ACCEPT simply means jumps to ACCEPT :  
  
iptables -A INPUT -p tcp --dport 80 -j ACCEPT  
  
```
[root@glt ~]# iptables -A INPUT -p tcp --dport 80 -j ACCEPT  
[root@glt ~]# iptables -nvL --line-numbers  
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
1    3777K 5463M ACCEPT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           state RELATED,ESTABLISHED  
2       80  2837 ACCEPT     icmp --  *      *       0.0.0.0/0            0.0.0.0/0  
3       10   440 ACCEPT     all  --  lo     *       0.0.0.0/0            0.0.0.0/0  
4      186 10820 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0           state NEW tcp dpt:22  
5      901 60241 REJECT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited  
6        0     0 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0           tcp dpt:80  
  
Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
1        0     0 REJECT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited  
  
Chain OUTPUT (policy ACCEPT 4 packets, 512 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
[root@glt ~]#
```
###   

### Deleting Rules

  
To delete a Rule, you must know its position in the chain and use the -D option:  
  
iptables -D INPUT 6  
  
```
[root@glt ~]# iptables -D INPUT 6  
[root@glt ~]# iptables -nvL --line-numbers  
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
1    3777K 5463M ACCEPT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           state RELATED,ESTABLISHED  
2       80  2837 ACCEPT     icmp --  *      *       0.0.0.0/0            0.0.0.0/0  
3       10   440 ACCEPT     all  --  lo     *       0.0.0.0/0            0.0.0.0/0  
4      186 10820 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0           state NEW tcp dpt:22  
5      903 60369 REJECT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited  
  
Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
1        0     0 REJECT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited  
  
Chain OUTPUT (policy ACCEPT 55 packets, 5156 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
```
###   

### Inserting Rules

  
The following commands inserts a rule using the -I option:  
  
iptables -I INPUT 5 -p tcp --dport 80 -j ACCEPT  
iptables -I INPUT 6 -p tcp --dport 443 -j ACCEPT  
  
```
[root@glt ~]# iptables -I INPUT 5 -p tcp --dport 80 -j ACCEPT  
[root@glt ~]# iptables -I INPUT 6 -p tcp --dport 443 -j ACCEPT  
[root@glt ~]# iptables -nvL --line-numbers  
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
1    3777K 5463M ACCEPT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           state RELATED,ESTABLISHED  
2       82  2954 ACCEPT     icmp --  *      *       0.0.0.0/0            0.0.0.0/0  
3       10   440 ACCEPT     all  --  lo     *       0.0.0.0/0            0.0.0.0/0  
4      186 10820 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0           state NEW tcp dpt:22  
5        0     0 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0           tcp dpt:80  
6        0     0 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0           tcp dpt:443  
7      905 60465 REJECT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited  
  
Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
1        0     0 REJECT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited  
  
Chain OUTPUT (policy ACCEPT 52 packets, 4976 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
[root@glt ~]#  
```
###   

### Replacing Rules

  
Using the -R option existing rules can be replaced in the chain:  
  
iptables -R INPUT 5 -p tcp -s 192.168.0.0/24 --dport 80 -j ACCEPT  
  
```
[root@glt ~]# iptables -R INPUT 5 -p tcp -s 192.168.0.0/24 --dport 80 -j ACCEPT  
[root@glt ~]# iptables -nvL --line-numbers  
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
1    3777K 5463M ACCEPT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           state RELATED,ESTABLISHED  
2       83  3015 ACCEPT     icmp --  *      *       0.0.0.0/0            0.0.0.0/0  
3       10   440 ACCEPT     all  --  lo     *       0.0.0.0/0            0.0.0.0/0  
4      186 10820 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0           state NEW tcp dpt:22  
5        0     0 ACCEPT     tcp  --  *      *       192.168.0.0/24       0.0.0.0/0           tcp dpt:80  
6        0     0 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0           tcp dpt:443  
7      917 61834 REJECT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited  
  
Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
1        0     0 REJECT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited  
  
Chain OUTPUT (policy ACCEPT 3 packets, 436 bytes)  
num   pkts bytes target     prot opt in     out     source               destination
```
  
Other example: replacing rule on line 2 that allows ICMP to blocking ICMP  
  
```
[root@glt ~]# iptables -R INPUT 2 -p icmp --icmp-type echo-request -j DROP  
[root@glt ~]# iptables -nvL --line-numbers  
Chain INPUT (policy ACCEPT 0 packets, 0 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
1    3782K 5464M ACCEPT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           state RELATED,ESTABLISHED  
2        0     0 DROP       icmp --  *      *       0.0.0.0/0            0.0.0.0/0           icmp type 8  
3       10   440 ACCEPT     all  --  lo     *       0.0.0.0/0            0.0.0.0/0  
4      503 29488 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0           state NEW tcp dpt:22  
5        0     0 ACCEPT     tcp  --  *      *       192.168.0.0/24       0.0.0.0/0           tcp dpt:80  
6        8   348 ACCEPT     tcp  --  *      *       0.0.0.0/0            0.0.0.0/0           tcp dpt:443  
7     1530  101K REJECT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited  
  
Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
1        0     0 REJECT     all  --  *      *       0.0.0.0/0            0.0.0.0/0           reject-with icmp-host-prohibited  
  
Chain OUTPUT (policy ACCEPT 40 packets, 3952 bytes)  
num   pkts bytes target     prot opt in     out     source               destination  
[root@glt ~]#
```
### Saving changes to the filter table

  
The iptables Rules changes using CLI commands will be lost upon system reboot if not saved. The command iptables-save can be used to save changes. The utility iptables-restore can be used to restore the table if a dump file is created:  
  
iptables-save > iptables.dump  
  
```
[root@glt ~]#  iptables-save > iptables.dump  
[root@glt ~]# ls  
anaconda-ks.cfg                      install.log  
HoneyDrive_0.2_Nectar_edition.ova    install.log.syslog  
HoneyDrive_0.2_Nectar_edition.ova.1  iptables.dump  
[root@glt ~]# cat iptables.dump  

Generated by iptables-save v1.4.7 on Thu Sep  5 22:48:36 2013  
*filter  
:INPUT ACCEPT [0:0]  
:FORWARD ACCEPT [0:0]  
:OUTPUT ACCEPT [23:4220]  
-A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT  
-A INPUT -p icmp -j ACCEPT  
-A INPUT -i lo -j ACCEPT  
-A INPUT -p tcp -m state --state NEW -m tcp --dport 22 -j ACCEPT  
-A INPUT -s 192.168.0.0/24 -p tcp -m tcp --dport 80 -j ACCEPT  
-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT  
-A INPUT -j REJECT --reject-with icmp-host-prohibited  
-A FORWARD -j REJECT --reject-with icmp-host-prohibited  
COMMIT  
Completed on Thu Sep  5 22:48:36 2013  
```

> Written with [StackEdit](https://stackedit.io/).
