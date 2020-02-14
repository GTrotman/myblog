---
layout: post
title: GnuPG Cheat Sheet (command line)
date: '2015-01-17T14:53:00.000-05:00'
author: DatsWorld
tags:
- Security
- Ubuntu
- linux
- gpg
- configuration
- pgp
modified_time: '2015-01-24T13:24:37.528-05:00'
blogger_id: tag:blogger.com,1999:blog-1770165193886521985.post-8939872299589203254
blogger_orig_url: http://blog.datsworld.com/2015/01/gnupg-cheat-sheet-command-line.html
---
### Create a PGP Key Pair
```
trotman@glt:~$ gpg --list-keys

  
Output:  

gpg (GnuPG) 1.4.16; Copyright (C) 2013 Free Software Foundation, Inc.  
This is free software: you are free to change and redistribute it.  
There is NO WARRANTY, to the extent permitted by law.  
  
Please select what kind of key you want:  
   (1) RSA and RSA (default)  
   (2) DSA and Elgamal  
   (3) DSA (sign only)  
   (4) RSA (sign only)  
Your selection?1  

  
Select 1 if you want to enable both encryption and signing.  
  

RSA keys may be between 1024 and 4096 bits long.  
What keysize do you want? (4096)  
Requested keysize is 4096 bits  
Please specify how long the key should be valid.  
         0 = key does not expire  
      <n>  = key expires in n days  
      <n>w = key expires in n weeks  
      <n>m = key expires in n months  
      <n>y = key expires in n years  
Key is valid for? (0)   
Key does not expire at all  
Is this correct? (y/N) y  
  
You need a user ID to identify your key; the software constructs the user ID  
from the Real Name, Comment and Email Address in this form:  
    "Heinrich Heine (Der Dichter) <heinrichh@duesseldorf.de>"  
  
Real name: Garth Trotman  
Email address: garth.trotman@example.com  
Comment: Sample Key  
You selected this USER-ID:  
    "Garth Trotman (Sample Key) <garth.trotman@example.com>"  
  
Change (N)ame, (C)omment, (E)mail or (O)kay/(Q)uit? O  
You need a Passphrase to protect your secret key.  
  
We need to generate a lot of random bytes. It is a good idea to perform  
some other action (type on the keyboard, move the mouse, utilize the  
disks) during the prime generation; this gives the random number  
generator a better chance to gain enough entropy.  
  
Not enough random bytes available.  Please do some other work to give  
the OS a chance to collect more entropy! (Need 150 more bytes)  
...+++++  
gpg: key 30F394FB marked as ultimately trusted  
public and secret key created and signed.  
  
gpg: checking the trustdb  
gpg: 3 marginal(s) needed, 1 complete(s) needed, PGP trust model  
gpg: depth: 0  valid:   2  signed:   0  trust: 0-, 0q, 0n, 0m, 0f, 2u  
pub   4096R/30F394FB 2015-01-07  
      Key fingerprint = 0CC6 6C07 FDA9 2724 2690  054F 8AD8 84A4 30F3 94FB  
uid                  Garth Trotman (Sample Key) <garth.trotman@example.com>  
sub   4096R/0779F606 2015-01-07  
```
  

### Create a Revocation Certificate

gpg --output filename.asc --gen-revoke key_id

  
```
trotman@glt:~$ gpg --output revoke.asc --gen-revoke 30F394FB

  
Output:  

sec  4096R/30F394FB 2015-01-07 Garth Trotman (Sample Key) <garth.trotman@example.com>  
  
Create a revocation certificate for this key? (y/N)y  
Please select the reason for the revocation:  
  0 = No reason specified  
  1 = Key has been compromised  
  2 = Key is superseded  
  3 = Key is no longer used  
  Q = Cancel  
(Probably you want to select 1 here)  
Your decision? 0  
Enter an optional description; end it with an empty line:  
>   
Reason for revocation: No reason specified  
(No description given)  
Is this okay? (y/N) y  
  
You need a passphrase to unlock the secret key for  
user: "Garth Trotman (Sample Key) <garth.trotman@example.com>"  
4096-bit RSA key, ID 30F394FB, created 2015-01-07  
  
ASCII armored output forced.  
Revocation certificate created.  
  
Please move it to a medium which you can hide away; if Mallory gets  
access to this certificate he can use it to make your key unusable.  
It is smart to print this certificate and store it away, just in case  
your media become unreadable.  But have some caution:  The print system of  
your machine might store the data and make it available to others!  
```

### List PGP Public Keys
```
trotman@glt:~$ gpg --list-keys

  
Output:  

/home/trotman/.gnupg/pubring.gpg  
--------------------------------  
pub   4096R/30F394FB 2015-01-07  
uid                  Garth Trotman (Sample Key) <garth.trotman@example.com>  
sub   4096R/0779F606 2015-01-07  
```

### List PGP Secret Keys

```
trotman@glt:~$ gpg --list-secret-keys

  
Output:  

/home/trotman/.gnupg/secring.gpg  
--------------------------------  
sec   4096R/30F394FB 2015-01-07  
uid                  Garth Trotman (Sample Key) <garth.trotman@example.com>  
ssb   4096R/0779F606 2015-01-07  
```

### Export/Backup a Public key

gpg -ao filename.key --export key_id

 ``` 

trotman@glt:~$ gpg -ao public.key --export 30F394FB
```
  

### Export/Backup a Private key

gpg -ao filename.key --export-secret-key key_id

  
```
trotman@glt:~$ gpg -ao private.key --export-secret-key 30F394FB
```
  

### Import/Restore a Public key

gpg --import filename.key

  
```
trotman@glt:~$ gpg --import public.key

  ```

### Import/Restore a Private key

gpg --import filename.key

  ```

trotman@glt:~$ gpg --import private.key
```
  

### Delete a Private key

gpg --delete-secret-key key_id

  
```
trotman@glt:~$ gpg --delete-secret-key 30F394FB
```
  

### Delete a Public key

gpg --delete-key key_id

  
```
trotman@glt:~$ gpg --delete-key 30F394FB
```
  

### Create ASCII Armored Version of Public Key
```
trotman@glt:~$ gpg --output mykey.asc --export -a 30F394FB
```

> Written with [StackEdit](https://stackedit.io/).
