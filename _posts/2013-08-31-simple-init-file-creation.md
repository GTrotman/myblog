---
layout: post
title: 'Simple init.d file creation: A basic example'
date: '2013-08-31T08:23:00.001-04:00'
author: DatsWorld
tags:
- linux
modified_time: '2013-09-09T16:21:17.691-04:00'
blogger_id: tag:blogger.com,1999:blog-1770165193886521985.post-6120943402920544446
blogger_orig_url: http://blog.datsworld.com/2013/08/simple-init-file-creation.html
---

Init scripts are essentially shell scripts. They can be invoked manually, or automatically by the system. To invoke an init script manually, the syntax is: /etc/init.d/service parameter .The following steps walk you through the creation of a simple init script:  

 1. **Define the interpreter.** You need to specify which interpreter will be used to execute this script. The first line of an init
    script should always be:

    
 

>    #! /bin/sh

    
  
2.  **Define init info.** These lines are needed by chkconfig. They specify what initial runlevels are active and what priority for the start-and-stop script execution order.  
    Under Centos, the following default runlevels are supported:  



|  |  |
|--|--|
| 0. |System Halt|
| 1. |Single-user mode|
| 2. |Multiuser, without NFS|
| 3. |Complete multiuser mode|
| 4. |User defined|
| 5. |X11 (XDM login)|
| 6. |Reboot|

    

>     # chkconfig: 2345 90 10  
>     # description: Starts and stops EXAMPLE daemon

    
  
3.  **Define the control parameters for the service.** This is were the start, stop, and other control parameters for bar are defined.  
    

>       case "$1" in  
>       start)  
>         echo "Starting example"  
>         ## run application you want to start  
>         python /usr/local/sbin/EXAMPLE &  
>         ;;  
>       stop)  
>         echo "Stopping example"  
>         ## kill application you want to stop  
>         killall EXAMPLE  
>         ;;  
>       *)  
>         ## If no parameters are given, print which are avaiable.  
>         echo "Usage: /etc/init.d/example{start|stop}"  
>         exit 1  
>         ;;  
>     esac  
>        
>     exit 0

    
  
4.  **Make init script executable.**  
  
    

>     chmod 0755 /etc/init.d/example_init

    
  
5.  **Enable init script.** Once the script has the appropriate execute permissions and the required chkconfig comments, it needs to be added to the chkconfig configuration.  
    


>     chkconfig --add example_init

    
  
6.  **Verify your addition to chkconfig.**  
    

>     chkconfig --list | grep example_init  
>     oracle        0:off     1:off   2:on   3:on   4:on   5:on  6:off  
>       
>       
>     find /etc/rc.d -name '*example_init' -print  
>     /etc/rc.d/rc5.d/S90example_init  
>     /etc/rc.d/rc3.d/S90example_init  
>     /etc/rc.d/rc2.d/S90example_init  
>     /etc/rc.d/rc4.d/S90example_init  
>     /etc/rc.d/rc1.d/K10example_init  
>     /etc/rc.d/rc6.d/K10example_init  
>     /etc/rc.d/rc0.d/K10example_init  
>     /etc/rc.d/init.d/example_init



Written with [StackEdit](https://stackedit.io/).
