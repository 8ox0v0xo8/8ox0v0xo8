# Caption

> 本机 IP: 10.10.16.5
>
> 目标 IP: 10.10.11.33

```shell
$ nmap -sSVC -p- 10.10.11.33
PORT     STATE SERVICE    VERSION
22/tcp   open  ssh        OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http
|_http-title: Did not follow redirect to http://caption.htb
8080/tcp open  http-proxy
|_http-title: GitBucket

$ vi /etc/host
[+] 10.10.11.33 caption.htb
```
