---
layout: post
title: Vi Editor Tutorial Cheat Sheet
date: '2013-09-13T18:27:00.002-04:00'
author: DatsWorld
tags:
- linux
- Centos
modified_time: '2013-10-22T15:49:02.662-04:00'
blogger_id: tag:blogger.com,1999:blog-1770165193886521985.post-3951556756810458174
blogger_orig_url: http://blog.datsworld.com/2013/09/vi-tutorial-cheat-sheet.html
---

<h3><span style="color: #29aae1;">Starting vi</span></h3><br />To start vi at the prompt enter:<br /><br /><b>[root@ts3 ~]#vi filename</b><br /><br />If the file does not exist vi will create it for you.<br /><br /><h3><span style="color: #29aae1;">Command Mode and Input Mode</span></h3><br />When you first open a file with vi it takes you to command mode. To get to input mode type "i" :<br /><br /><b>i</b><br /><br />To return to command mode press the ESC key:<br /><br /><b>[Esc] </b><br /><br /><h3><span style="color: #29aae1;">Deleting Text</span></h3><br />&nbsp;To delete text using the following commands you have to be in command mode:<br /><br /><table align="center" border="1" cellpadding="1" cellspacing="1" style="height: 252px; width: 482px;"><tbody><tr><td>Command&nbsp; </td><td>Function</td></tr><tr><td><b>x </b></td><td>Delete the character that the cursor is on</td></tr><tr><td><b>[Shift] d</b></td><td>Delete from the cursor to the end of the line.</td></tr><tr><td><br /><b>db</b></td><td>Delete from the cursor to the beginning of the current word</td></tr><tr><td><b>de</b> </td><td>Delete from the cursor to the end of the current word</td></tr><tr><td><b>dd</b> </td><td>Delete the current line that the cursor is on</td></tr><tr><td><b>d [Shift] g </b></td><td>Delete the current line that the cursor is on to the bottom of the file</td></tr></tbody></table><br /><br /><h3><span style="color: #29aae1;">Undo</span></h3><br /><br />To undo<b> </b>changes<b> </b>or line deletions you have to be in command mode and type the following:<br /><br /><b>u</b><br /><br /><h3><span style="color: #29aae1;">Goto</span></h3><br /><br />to go to a particular line a file go to command mode and type :linenumber :<br /><br /><b>:14</b><br /><br />You can also type in the line number followed by: <br /><br /><b>[Shift] g</b><br /><br />To see what line you are on:<br /><br /><b>&nbsp;[Ctrl] [Shift] g</b><br /><br />To display all the line numbers:<br /><b><br /></b><b>:set number</b><br /><br />To go to a particular line in a file while opening a file with vi:<br /><br /><b>[root@ts3 ~]#vi&nbsp; +45 filename</b><br /><br />To go to a particular pattern in a file while opening a file with vi:<br /><br /><b>[root@ts3 ~]#vi&nbsp; +/pattern filename</b><br /><br /><h3><span style="color: #29aae1;">Search </span></h3><br /><br />To search forward for some text, use the  /  (forward  slash) command:<br /><br /><b>/pattern</b><br /><br />To look for the next occurrence of that pattern:<br /><b><br /></b><b>n</b><br /><br />To look for the previous occurence of that pattern:<br /><br /><b>[Shift] n</b><br /><br />To find and replace that pattern: &nbsp; <br /><br /><br /><h3><span style="color: #29aae1;">Saving Work</span></h3><br /><br />To save changes go to command mode and type:<br /><br /><b>:w</b><br /><br />To save a file with a different filename:<br /><br /><b>:w filename</b><br /><br />To save and exit:<br /><b><br /></b><b>:wq</b><br /><br />To exit without saving:<br /><br /><b>:q! </b><marquee behavior="alternate" scrolldelay="250"><article></article></marquee>