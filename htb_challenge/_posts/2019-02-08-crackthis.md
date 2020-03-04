---
title: CrackThis!
published: true
---
# CrackThis! 
- [CrackThis!](#crackthis)
  - [Description](#description)
  - [Work](#work)
## Description 
Crack the program and get the flag! We are given an EXE file that looks like possible dotnet 

## Work
Moving the file to Windows for ease of digging into after ida pro did not reveal much. The file was confused by ConfuserEX which is a .NET obfuscator to protect the source code of exe files. I used https://github.com/MindSystemm/ConfuserEx-Resources-Decryptor to decrypt the exe file. 

![](/htb_challenge/img/2020-03-04-08-51-27.png)

There was still an issue with the encoded obfuscation which can be solved with ConfuserEx Switch Killer

![](/htb_challenge/img/2020-03-04-08-56-07.png)

yet more obfuscation de4dot to fix that https://github.com/0xd4d/de4dot

Follow the methods for the password all the way to method0 which had obsure system and another string admin

DO NOT FOLLOW TICKCOUNT that is a trap of IFs

![](/htb_challenge/img/2019-02-20-15-32.png)


