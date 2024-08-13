Ping host to check if reachable: `ping 10.129.61.254`

Run nmap to detect ports: `sudo nmap 10.129.61.254`

Run nmap with version info: `sudo nmap -sV 10.129.61.254`

```
PORT   		STATE 	SERVICE 	VERSION
21/tcp 		open  	ftp     vsftpd 3.0.3
Service Info: OS: Unix
```

Logging into the FTP with anonymus account, password can be anything since it will be disregarded: 
`ftp 10.129.61.254`
``` 
Connected to 10.129.61.254.
220 (vsFTPd 3.0.3)
Name (10.129.61.254:sebastiaan): anonymous
331 Please specify the password.
Password: 
230 Login successful.
```

Checked the content of the folder, found the flag.txt file

```
ftp> ls
229 Entering Extended Passive Mode (|||34390|)
150 Here comes the directory listing.
-rw-r--r--    1 0        0              32 Jun 04  2021 flag.txt
226 Directory send OK.
```

Download the flag file to local machine

```
ftp> get flag.txt
local: flag.txt remote: flag.txt
226 Transfer complete.
32 bytes received in 00:00 (0.87 KiB/s)
ftp> bye
221 Goodbye.
```

Opening flag file 
```
cat flag.txt
035db21c881520061c53e0536e44f815 
```


What does the 3-letter acronym FTP stand for? 
- File Transfer protocol

Which port does the FTP service listen on usually? 
- 21

FTP sends data in the clear, without any encryption. What acronym is used for a later protocol designed to provide similar functionality to FTP but securely, as an extension of the SSH protocol? 
- SFTP

What is the command we can use to send an ICMP echo request to test our connection to the target? 
- Ping

From your scans, what version is FTP running on the target? 
- vsftpd 3.0.3 

From your scans, what OS type is running on the target?
- Unix

What is the command we need to run in order to display the 'ftp' client help menu? 
- ftp -?

What is username that is used over FTP when you want to log in without having an accou
- anonymus

What is the response code we get for the FTP message 'Login successful'? 
- 230

There are a couple of commands we can use to list the files and directories available on the FTP server. One is dir. What is the other that is a common way to list files on a Linux system. 
- ls

What is the command used to download the file we found on the FTP server? 
- get

Root flag 
- 035db21c881520061c53e0536e44f815 
