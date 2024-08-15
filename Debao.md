# Debao ovo

- [Debao ovo](#debao-ovo)
  - [Git](#git)
  - [配置 Docker 镜像](#配置-docker-镜像)
  - [Nessus Docker](#nessus-docker)

## Git

```bash
sudo apt install git
git config --global user.name "ox0v0xo"
git config --global user.email "xxx"
git config --global --unset http.proxy
git config --global --unset https.proxy
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
