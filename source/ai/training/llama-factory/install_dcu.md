# 基于海光DCU搭建项目运行环境

## 基于Docker搭建

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
git clone https://github.com/hiyouga/LLaMA-Factory.git
```

- 容器镜像

```
docker pull image.sourcefind.cn:5000/dcu/admin/base/pytorch:2.1.0-ubuntu20.04-dtk24.04.1-py3.10
```

### 创建容器

```
# 进入LLaMA-Factory项目根目录
cd LLaMA-Factory
# 创建容器
docker run -dit --network=host \
--name=llama-factory \
--restart=on-failure:10 \
--privileged \
--device=/dev/kfd --device=/dev/dri \
--ipc=host --shm-size=32G --group-add video \
--cap-add=SYS_PTRACE --security-opt seccomp=unconfined \
-v $PWD:/LLaMA-Factory \
-v /opt/hyhal:/opt/hyhal \
-u root --ulimit stack=-1:-1 --ulimit memlock=-1:-1 \
image.sourcefind.cn:5000/dcu/admin/base/pytorch:2.1.0-ubuntu20.04-dtk24.04.1-py3.10 \
bash
```

### 安装第三方库

```
# 进入容器项目根目录下
docker exec -it llama-factory bash
cd /LLaMA-Factory
# 安装第三方库
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -r requirements.txt
# 该镜像需卸载自带vllm，否则会有错误
pip uninstall vllm
```

登录[光合开发者社区资源下载中心的DAS](https://developer.hpccube.com/tool)中下载对应版本deepspeed包，然后安装该依赖包，

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple deepspeed-0.12.3+das1.0+gita724046.abi0.dtk2404.torch2.1.0-cp310-cp310-manylinux2014_x86_64.whl
```

如需使用llamafactory-cli命令，请执行如下安装

```
cd /LLaMA-Factory
pip install -e ".[torch,metrics]"
```

