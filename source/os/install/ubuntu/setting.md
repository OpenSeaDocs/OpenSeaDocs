# 系统设置

## ssh远程连接

- 安装openssh-server

```
sudo apt install openssh-server
```

- 检查ssh server的状态

```
systemctl status sshd
```

确认状态是active(running）

- 设置ssh server开机启动

```
sudo systemctl enable ssh
```

