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
git clone -b v0.5.0 https://github.com/vllm-project/vllm.git
```

- 容器镜像

```
docker pull image.sourcefind.cn:5000/dcu/admin/base/pytorch:2.1.0-ubuntu20.04-dtk24.04.1-py3.10
```

### 创建容器

```
# 创建容器
docker run -dit --network=host \
--name=vllm \
--restart=on-failure:10 \
--privileged \
--device=/dev/kfd --device=/dev/dri \
--ipc=host --shm-size=32G --group-add video \
--cap-add=SYS_PTRACE --security-opt seccomp=unconfined \
-v /data:/data \
-v /opt/hyhal:/opt/hyhal \
-u root --ulimit stack=-1:-1 --ulimit memlock=-1:-1 \
image.sourcefind.cn:5000/dcu/admin/base/pytorch:2.1.0-ubuntu20.04-dtk24.04.1-py3.10 \
bash
```

### 安装第三方库

```
# 进入容器项目根目录下
docker exec -it vllm bash
cd /data/project/vllm
```

登录[光合开发者社区资源下载中心的DAS](https://cancon.hpccube.com:65024/4/main/vllm/DAS1.1.1)中下载对应版本vllm包，然后安装该依赖包，

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple vllm-0.5.0+das.opt1.3e2c63a.dtk2404.torch2.1.0-cp310-cp310-linux_x86_64.whl
# 降低transformers包版本至4.33.1，否则baichuan模型会报错；其他模型需要版本4.43.4
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple transformers==4.33.1
```

验证vllm版本

```
python -c "import vllm; print(vllm.__version__)"
```

