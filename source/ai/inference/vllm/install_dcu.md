# 安装

基于海光DCU加速卡适配vLLM框架

## 要求

- OS: Linux
- Python: 3.8 – 3.11
- DCU: K100AI、K100、Z100L、Z100
- 驱动: 5.7.1
- DTK: 24.04.1

## Docker（推荐）

- 拉取代码

```
git clone -b v0.5.0 https://github.com/vllm-project/vllm.git
```

- 拉取镜像

```
docker pull image.sourcefind.cn:5000/dcu/admin/base/pytorch:2.1.0-ubuntu20.04-dtk24.04.1-py3.10
```

- 创建容器

默认项目所依赖资源放置在/data目录下，可根据实际情况自行修改目录映射关系

```
docker run -dit \
       --network=host \
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

- 安装第三方库

先进行容器vllm项目根目录下，

```
docker exec -it vllm bash
cd /data/project/vllm
```

登录[光合开发者社区](https://cancon.hpccube.com:65024/4/main/vllm/DAS1.1.1)中下载对应版本vllm包，然后安装该依赖包，

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple vllm-0.5.0+das.opt1.3e2c63a.dtk2404.torch2.1.0-cp310-cp310-linux_x86_64.whl
```

- 额外步骤

对于一些特殊的模型需要安装额外的依赖包

【Baichuan1.0系列】

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple transformers==4.33.1
```

## Pip

未更新

## 其他

- 官方安装文档：https://docs.vllm.ai/en/latest/getting_started/installation.html
