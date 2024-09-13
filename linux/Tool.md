# Tool

> 目标 IP: 11.11.11.11

- [Tool](#tool)
  - [find](#find)
  - [nmap](#nmap)
    - [OPTION](#option)
  - [nessus (Docker)](#nessus-docker)
  - [curl](#curl)
  - [hydra](#hydra)
    - [OPTION](#option-1)
  - [vi](#vi)
    - [命令模式](#命令模式)

## find

- find / -perm -u=s -type f 2>/dev/null

## nmap

```shell
sudo apt install nmap

# 查看版本
nmap --version
```

### OPTION

- -C:"服务检测"功能
- -Pn:直接进行端口扫描，不发送 ICMP Echo 请求（ping）来检测目标主机是否在线
- -sS:SYN 半开连接扫描
- -sV:服务版本探测
- -V:显示详细输出

## nessus (Docker)

```bash
# 拉取镜像
docker pull ramisec/nessus

docker run -itd --name=ramisec_nessus -p 28834:8834 ramisec/nessus
```

修改容器中的`nessus/update.sh`,将`update_url`修改为:

```bash
https://plugins.nessus.org/v2/nessus.php?f=all-2.0.tar.gz&u=56b33ade57c60a01058b1506999a2431&p=1ee9c89d5379a119a56498f2d5dff674
```

进入容器 bash 运行 update.sh 进行更新

```bash
./update.sh

# 更新编译完成后, 进入 /opt/nessus/sbin/ 修改 admin 密码(admin)
cd /opt/nessus/sbin/
./nessuscli chpasswd admin
```

网址: `https://192.168.8.8:28834`

## curl

```bash
sudo apt install curl
```

## hydra

```bash
sudo apt install hydra

# ssh
sudo hydra -l root -P /usr/share/wordlists/rockyou.txt -F ssh://192.168.25.150
```

### OPTION

- -l : 用户名
- -P : 密码字典
- -F : 成功后停止

## vi

- `Esc`：退出插入模式，返回命令模式

### 命令模式

- i: 进入插入模式

- a：进入插入模式，在当前光标后的位置开始编辑

- o：在当前行的下方新开一行并进入插入模式

- dd：删除当前行
