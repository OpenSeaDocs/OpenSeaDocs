# lmdeploy

## 简介

LMDeploy 由 [MMDeploy](https://github.com/open-mmlab/mmdeploy) 和 [MMRazor](https://github.com/open-mmlab/mmrazor) 团队联合开发，是涵盖了 LLM 任务的全套轻量化、部署和服务解决方案。

## 前置准备

- 项目代码

```
git clone https://github.com/InternLM/lmdeploy.git
```

- 模型

下载模型至服务器/data/model文件夹下，此处以[Qwen2-7B-Instruct](https://www.modelscope.cn/models/qwen/Qwen2-7B-Instruct)为例。

## 环境安装

[安装-海光DCU](./install_dcu.md)

## 快速开始

LMDeploy 默认从 HuggingFace 上面下载模型，如果要从 ModelScope 上面下载模型，请通过命令 `pip install modelscope` 安装ModelScope，并设置环境变量：

```
export LMDEPLOY_USE_MODELSCOPE=True
```

### 离线批处理

```
import lmdeploy
pipe = lmdeploy.pipeline("/model/Qwen2-7B-Instruct")
response = pipe(["Hi, pls intro yourself", "Shanghai is"])
print(response)
```

## benchmark

### throughput



## 参考

- 官方项目链接：https://github.com/InternLM/lmdeploy