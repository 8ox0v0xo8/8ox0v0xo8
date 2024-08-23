# Debao ovo

- [Debao ovo](#debao-ovo)
  - [配置 NAT 虚拟机 IP](#配置-nat-虚拟机-ip)
  - [Git](#git)
  - [配置 Docker 镜像](#配置-docker-镜像)
  - [Nessus Docker](#nessus-docker)

## 配置 NAT 虚拟机 IP

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

## Git

```bash
sudo apt install git
git config --global user.name "8ox0v0xo8"
git config --global user.email "ox0v0xo@outlook.com"
git config --global --unset http.proxy
git config --global --unset https.proxy
# To solve the problem: SSL certificate problem: unable to get local issuer certificate
git config --global http.sslVerify false
```

## 配置 Docker 镜像

```json
// sudo vi /etc/docker/daemon.json
{
  "registry-mirrors": ["https://docker.1panel.live/"]
}
```

重启 docker: `sudo systemctl restart docker`

## Nessus Docker

```bash
# 拉取镜像
docker pull ramisec/nessus

docker run -itd --name=ramisec_nessus -p 28834:8834 ramisec/nessus
```

修改容器中的`nessus/update.sh`,将`update_url`修改为`https://plugins.nessus.org/v2/nessus.php?f=all-2.0.tar.gz&u=56b33ade57c60a01058b1506999a2431&p=1ee9c89d5379a119a56498f2d5dff674`

进入容器 bash 运行 update.sh 进行更新

更新编译完成后，进入 /opt/nessus/sbin/ ，运行`./nessuscli chpasswd admin`修改 admin 密码(admin)

访问网址 https://127.0.0.1:28834 即可
