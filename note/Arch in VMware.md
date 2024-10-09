# Arch in VMware

- [Arch in VMware](#arch-in-vmware)
  - [安装](#安装)
    - [NAT 连接配置静态 IP](#nat-连接配置静态-ip)
  - [使用](#使用)
    - [pacman](#pacman)
    - [.bashrc](#bashrc)
    - [过程](#过程)

## 安装

### NAT 连接配置静态 IP

> VMware NAT 虚拟机, 设置 IP 地址为 192.168.8.8

Windows 10 (主机): 设置 -> 网络和 Internet -> 状态 -> 更改适配器选项 -> 右键 VMnet8 -> 属性 -> Internet 协议版本 4 -> 属性

> 使用下面的 IP 地址 & DNS 服务器地址

|   NAME   |       IP        |      INFO      |
| :------: | :-------------: | :------------: |
| IP 地址  |   192.168.8.1   |    主机 IP     |
| 子网掩码 |  255.255.255.0  |    子网掩码    |
| 默认网关 |   192.168.8.2   |   虚拟机网关   |
| 首选 DNS |     8.8.8.8     | 虚拟机首选 DNS |
| 备用 DNS | 114.114.114.114 | 虚拟机备用 DNS |

> VMware

VMware Workstation: 编辑 -> 虚拟网络编辑器 -> VMnet8 -> 更改设置 -> VMnet8 -> 子网 IP: 192.168.8.0 -> 勾选使用本地 DHCP 服务将 IP 地址分配给虚拟机 -> DHCP 设置 -> 起始 IP 地址: 192.168.8.8 -> 确定

进入 Arch Linux 后使用 archinstall 进行安装, 选择手动配置网络

## 使用

### pacman

```shell
# 更新系统 ; -y:标记刷新 ; -yy：标记强制刷新 ; -u：标记升级动作
$ sudo pacman -Syu

# 查看是否安装包 xxx ; -Q：查询本地软件包数据库
$ sudo pacman -Q | grep xxx

# 卸载软件 xxx
$ sudo pacman -Rns xxx
```

### .bashrc

```bash
#
# ~/.bashrc
#

# If not running interactively, don't do anything
[[ $- != *i* ]] && return

alias ls='ls --color=auto'
alias grep='grep --color=auto'
PS1='[\u@\h \W]\$ '

# ---------- ADD ---------- #
alias la='ls -al'

export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
export PATH=$JAVA_HOME/bin:$PATH
# ---------- source ~/.bashrc ---------- #
```

### 过程

```shell
# ---------- ssh ---------- #
$ sudo pacman -S openssh
$ sudo systemctl enable sshd
$ sudo systemctl start sshd
$ sudo systemctl status sshd
# ---------- ssh ---------- #

# ---------- python ---------- #
$ sudo pacman -S python python-pip
$ python --version
$ pip --version
# ---------- python ---------- #

# ---------- jdk17 ---------- #
$ sudo pacman -S jdk17-openjdk

$ readlink -f $(which java) | sed "s:bin/java::"
/usr/lib/jvm/java-17-openjdk/

# 修改 ~/.bashrc
[+] export JAVA_HOME=/usr/lib/jvm/java-17-openjdk
[+] export PATH=$JAVA_HOME/bin:$PATH

# 重新加载配置文件
$ source ~/.bashrc

# 安装 Maven
$ sudo pacman -S maven
$ mvn -version
# ---------- jdk17 ---------- #

# ---------- docker ---------- #
$ sudo pacman -S docker
# 当前用户添加到 docker 组 ; 重启
$ sudo usermod -aG docker $USER

$ sudo systemctl enable docker
$ sudo systemctl start docker
$ sudo systemctl status docker

# 添加镜像源
$ sudo mkdir -p /etc/docker
$ sudo touch /etc/docker/daemon.json
$ echo '{
  "registry-mirrors": [
    "https://registry.docker-cn.com",
    "http://hub-mirror.c.163.com",
    "https://docker.mirrors.ustc.edu.cn",
    "https://dockerhub.azk8s.cn",
    "https://mirror.ccs.tencentyun.com",
    "https://registry.cn-hangzhou.aliyuncs.com",
    "https://docker.mirrors.ustc.edu.cn",
    "https://docker.1panel.live",
    "https://atomhub.openatom.cn/",
    "https://hub.uuuadc.top",
    "https://docker.anyhub.us.kg",
    "https://dockerhub.jobcher.com",
    "https://dockerhub.icu",
    "https://docker.ckyl.me",
    "https://docker.awsl9527.cn"
  ],
  "live-restore": true
}' | sudo tee /etc/docker/daemon.json
$ sudo systemctl restart docker
$ docker info
# ---------- docker ---------- #

# ---------- git ---------- #
$ sudo pacman -S git
$ git --version
$ git config --global user.name "ox0v0xo"
$ git config --global user.email "ox0v0xo@outlook.com"
# ---------- git ---------- #

# ---------- rust ---------- #
$ sudo pacman -S rust
$ rustc --version
# ---------- rust ---------- #

# ---------- golang ---------- #
$ sudo pacman -S go
$ go version
# ---------- golang ---------- #

# ---------- vim ---------- #
$ sudo pacman -S vim
# ---------- vim ---------- #
```
