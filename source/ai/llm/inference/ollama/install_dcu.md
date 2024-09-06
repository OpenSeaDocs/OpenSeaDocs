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
git clone http://developer.hpccube.com/codes/wangkx1/ollama_dcu.git -b v0.3.5
cd ollama_dcu
cp -r /opt/hyhal ./
tar -zxvf cmake-3.29.3.tgz
```

- 容器镜像

```
docker load < ollama_k100ai_v0.3.5.tgz
```

### 创建容器

```
# 进入ollama_dcu项目根目录
cd ollama_dcu
# 创建容器
docker run -dit --network=host \
--name=ollama \
--restart=on-failure:10 \
--privileged \
--device=/dev/kfd --device=/dev/dri \
--ipc=host --shm-size=32G --group-add video \
--cap-add=SYS_PTRACE --security-opt seccomp=unconfined \
-v $PWD:/ollama \
-v /data/model:/model \
-v /opt/hyhal:/opt/hyhal \
-u root --ulimit stack=-1:-1 --ulimit memlock=-1:-1 \
ollama_k100ai_v0.3.5_debug:latest \
bash
```

### 配置环境变量

```
# 进入容器项目根目录下
docker exec -it ollama bash
vim ~/.bashrc
```

在配置文件后面添加以下内容，

```
# export HIP_VISIBLE_DEVICES=0  # 不指定的话, 会默认使用所有卡。
# 将28120替换为自己选择的端口号
export OLLAMA_HOST="0.0.0.0:28120"
export PATH=/app/ollama:$PATH
# 如果有迁移的本地模型仓库, 需要增加环境变量
#export OLLAMA_MODELS=/local—model-path
```

保存后，激活环境变量

```
source ~/.bashrc
```

启动ollama服务

```
ollama serve &
```

拉取模型

```
ollama pull qwen2:0.5b
```

运行模型

```
ollama run qwen2:0.5b
```



## 附录

- 
