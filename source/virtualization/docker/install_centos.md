# 安装

## 要求

- OS: Centos7+

## 在线安装

卸载旧版本

```
sudo yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine
```

### 一键安装

```
sudo curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
```

### 手动安装

安装依赖包

```bash
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

配置国内镜像源

```bash
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

安装最新版

```bash
sudo yum install docker-ce docker-ce-cli containerd.io
```

若报错，则执行下述语句，

```bash
sudo wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
sudo yum -y install docker-ce
```

创建数据保存目录

```
sudo mkdir /data/docker
```

编辑配置文件

```
sudo vim /etc/docker/daemon.json
```

写入下述内容并保存

```
{   
    "registry-mirrors": ["https://f3wa7uij.mirror.aliyuncs.com"],
    "data-root": "/data/docker"
}
```

重载配置文件

```bash
sudo systemctl daemon-reload
```

启动docker

```bash
sudo systemctl start docker
```

查看docker运行状态

```bash
sudo systemctl status docker
```

设置开机自动启动

```bash
sudo systemctl enable docker
```

重启docker

```bash
sudo systemctl restart docker
```

