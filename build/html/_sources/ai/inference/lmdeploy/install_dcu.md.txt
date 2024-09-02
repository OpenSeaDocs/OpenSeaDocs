# 安装-海光DCU

## 基于Docker

以下以K100AI为例，介绍项目运行环境搭建过程。

### 环境依赖

- DCU驱动
- DTK
- Docker
- Git

### 前置准备

- 项目代码

拉取官方项目代码

```
git clone https://github.com/InternLM/lmdeploy.git
```

- 容器镜像

```
docker pull image.sourcefind.cn:5000/dcu/admin/base/custom:lmdeploy1.0-dtk23.10-torch1.13-py38-latest
```

### 创建容器

```
# 进入lmdeploy项目根目录
cd lmdeploy
# 创建容器
docker run -dit --network=host \
--name=lmdeploy \
--restart=on-failure:10 \
--privileged \
--device=/dev/kfd --device=/dev/dri \
--ipc=host --shm-size=32G --group-add video \
--cap-add=SYS_PTRACE --security-opt seccomp=unconfined \
-v $PWD:/lmdeploy \
-v /data/model:/model \
-v /opt/hyhal:/opt/hyhal \
-u root --ulimit stack=-1:-1 --ulimit memlock=-1:-1 \
image.sourcefind.cn:5000/dcu/admin/base/custom:lmdeploy1.0-dtk23.10-torch1.13-py38-latest \
bash
```

### 安装依赖

```
# 进入容器项目根目录下
docker exec -it lmdeploy bash
cd /lmdeploy
```

验证lmdeploy版本

```
python -c "import lmdeploy; print(lmdeploy.__version__)"
```

