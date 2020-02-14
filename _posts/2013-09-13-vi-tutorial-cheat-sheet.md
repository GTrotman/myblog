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

### Starting vi

  
To start vi at the prompt enter:  
  
>**[root@ts3 ~]#vi filename**  
  
If the file does not exist vi will create it for you.  
  

### Command Mode and Input Mode

  
When you first open a file with vi it takes you to command mode. To get to input mode type "i" :  
  
>**i**  
  
To return to command mode press the ESC key:  
  
**[Esc]**  
  

### Deleting Text

  
To delete text using the following commands you have to be in command mode:  
  
| Command | Function |
|--|--|
| **x** | Delete the character that the cursor is on |
| **[Shift] d** | Delete from the cursor to the end of the line. |
|**db**|Delete from the cursor to the beginning of the current word|
| **de** | Delete from the cursor to the end of the current word |
| **dd** | Delete the current line that the cursor is on |
|**d [Shift] g**|Delete the current line that the cursor is on to the bottom of the file|



### Undo

  
  
To undo  changes  or line deletions you have to be in command mode and type the following:  
  
>**u**  
  

### Goto

  
  
To go to a particular line a file go to command mode and type :linenumber :  
  
>**:14**  
  
You can also type in the line number followed by:  
  
>**[Shift] g**  
  
To see what line you are on:  
  
>**[Ctrl] [Shift] g**  
  
To display all the line numbers:  
>**:set number**  
  
To go to a particular line in a file while opening a file with vi:  
  
>**[root@ts3 ~]#vi +45 filename**  
  
To go to a particular pattern in a file while opening a file with vi:  
  
>**[root@ts3 ~]#vi +/pattern filename**  
  

### Search

  
  
To search forward for some text, use the / (forward slash) command:  
  
>**/pattern**  
  
To look for the next occurrence of that pattern:  
>**n**  
  
To look for the previous occurence of that pattern:  
  
>**[Shift] n**  
  
To find and replace that pattern:  
  
  

### Saving Work

  
  
To save changes go to command mode and type:  
  
>**:w**  
  
To save a file with a different filename:  
  
>**:w filename**  
  
To save and exit:  
>**:wq**  
  
To exit without saving:  
  
>**:q!**


> Written with [StackEdit](https://stackedit.io/).
