# FAQ

## Docker默认保存路径磁盘空间不足

默认情况下Docker默认保存路径为/var/lib/docker/，可以使用rsync来安全地复制整个目录到新的位置

创建新目录，此处以/data/docker为例

```
sudo mkdir /data/docker
```

使用rsync进行数据迁移

```
sudo rsync -aP /var/lib/docker/ /data/docker/
```

编辑配置文件

```
vim /etc/docker/daemon.json
```

在文件中添加或修改data-root项内容

```
{   
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

重启docker

```bash
sudo systemctl restart docker
```