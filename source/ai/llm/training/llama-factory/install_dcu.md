# 安装

基于海光DCU加速卡适配LLaMA-factory训练平台

## 要求

- OS: Linux
- Python: 3.8 – 3.11
- DCU: K100AI、K100、Z100L、Z100
- 驱动: 5.7.1
- DTK: 24.04.1

## Docker（推荐）

- 拉取代码

```
git clone https://github.com/hiyouga/LLaMA-Factory.git
```

- 拉取镜像

```
docker pull image.sourcefind.cn:5000/dcu/admin/base/pytorch:2.1.0-ubuntu20.04-dtk24.04.1-py3.10
```

- 创建容器

默认项目所依赖资源放置在/data目录下，可根据实际情况自行修改目录映射关系

```
docker run -dit --network=host \
       --name=llama-factory \
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

```
# 进入容器项目根目录下
docker exec -it llama-factory bash
cd LLaMA-Factory
# 安装第三方库
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -r requirements.txt
# 该镜像需卸载自带vllm，否则会有错误
pip uninstall vllm
```

登录[光合开发者社区](https://cancon.hpccube.com:65024/4/main/deepspeed/DAS1.1)中下载对应版本deepspeed包，然后安装该依赖包，

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple deepspeed-0.12.3+das1.0+gita724046.abi0.dtk2404.torch2.1.0-cp310-cp310-manylinux2014_x86_64.whl
```

如需使用llamafactory-cli命令，请执行如下安装

```
cd /LLaMA-Factory
pip install -e ".[torch,metrics]"
```

## Pip

暂未更新

## 其他

- 官方安装文档：https://github.com/hiyouga/LLaMA-Factory/blob/main/README_zh.md
