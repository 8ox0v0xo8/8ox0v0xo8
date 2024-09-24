# Trickster

> 本机 IP: 10.10.16.3
>
> 目标 IP: 10.10.11.34

```shell
$ nmap -sS -A -T5 -v 10.10.11.34
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.52
|_http-title: Did not follow redirect to http://trickster.htb/
| http-methods:
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.52 (Ubuntu)
Aggressive OS guesses: Linux 4.15 - 5.8 (95%), Linux 5.3 - 5.4 (95%), Linux 2.6.32 (95%), Linux 5.0 - 5.5 (95%), Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%), Linux 5.0 (93%)

$ vi /etc/hosts
[+] 10.10.11.34 trickster.htb
# 访问 http://trickster.htb/，有个 shop.trickster.htb 无法访问，加入 hosts
[+] 10.10.11.34 shop.trickster.htb
```
