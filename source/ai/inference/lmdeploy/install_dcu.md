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
docker pull image.sourcefind.cn:5000/dcu/admin/base/pytorch:2.1.0-ubuntu20.04-dtk24.04.1-py3.10
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
image.sourcefind.cn:5000/dcu/admin/base/pytorch:2.1.0-ubuntu20.04-dtk24.04.1-py3.10 \
bash
```

### 安装依赖

```
# 进入容器项目根目录下
docker exec -it lmdeploy bash
cd /lmdeploy
# 需要更换transformers版本至4.41.2，否则qwen2的推理会报错
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple transformers==4.41.2
```

验证lmdeploy版本

```
python -c "import lmdeploy; print(lmdeploy.__version__)"
```

