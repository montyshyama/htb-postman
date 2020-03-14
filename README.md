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

The redis server (version 4.0.9) is running on port 6379. <a href="https://github.com/Avinash-acid/Redis-Server-Exploit">Here</a> is a working exploit for the same.
