# 海光DCU

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
git clone https://github.com/huggingface/transformers.git
```

- 容器镜像

```
docker pull image.sourcefind.cn:5000/dcu/admin/base/pytorch:2.1.0-ubuntu20.04-dtk24.04.1-py3.10
```

### 创建容器

```
# 进入transformers项目根目录
cd transformers
# 创建容器
docker run -dit --network=host \
--name=transformers \
--restart=on-failure:10 \
--privileged \
--device=/dev/kfd --device=/dev/dri \
--ipc=host --shm-size=32G --group-add video \
--cap-add=SYS_PTRACE --security-opt seccomp=unconfined \
-v $PWD:/transformers \
-v /data/model:/model \
-v /opt/hyhal:/opt/hyhal \
-u root --ulimit stack=-1:-1 --ulimit memlock=-1:-1 \
image.sourcefind.cn:5000/dcu/admin/base/pytorch:2.1.0-ubuntu20.04-dtk24.04.1-py3.10 \
bash
```

### 安装第三方库

```
# 进入容器项目根目录下
docker exec -it transformers bash
cd /transformers
```

然后安装该依赖包，

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple modelscope datasets tokenizers==0.13.3 transformers==4.33.1
```

验证transformers版本

```
python -c "import transformers; print(transformers.__version__)"
```

