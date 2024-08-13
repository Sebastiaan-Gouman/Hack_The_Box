## Meow

Start the vpn with typing `sudo openvpn 'filename.ovpn'` in the command line
For some reason it needs sudo to work
Hit Spawn Machine in HTB
Open new terminal and ping IP to see if it works

Scan ports with nmap: `sudo nmap -sV {target_IP}`
Use service detection flag `-sV` to determine the name and description of the identified services.


What does the acronym VM stand for? 
- Virtual Machine

What tool do we use to interact with the operating system in order to issue commands via the command line, such as the one to start our VPN connection? It's also known as a console or shell. 
- Terminal

What service do we use to form our VPN connection into HTB labs? 
- Open VPN

What tool do we use to test our connection to the target with an ICMP echo request? 
- Ping

What is the name of the most common tool for finding open ports on a target? 
- nmap

What service do we identify on port 23/tcp during our scans? 
- telnet

What username is able to log into the target over telnet with a blank password? 
- root

Root flag 
- b40abdfe23665f766f9c61ecba8a4c19
