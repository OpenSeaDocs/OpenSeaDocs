# vLLM

## 简介

vLLM是一个开源的LLM推理和服务引擎。

## 前置准备

- 项目代码

```
git clone https://github.com/vllm-project/vllm.git
```

- 模型

下载模型至服务器/data/model文件夹下，此处以[Qwen2-7B-Instruct](https://www.modelscope.cn/models/qwen/Qwen2-7B-Instruct)为例。

## 环境安装

[安装-海光DCU](./install_dcu.md)

## 快速开始

### benchmark

#### throughput

```
python benchmark_throughput.py \
--backend vllm \
--dtype float16 \
--model "/model/Qwen2-7B-Instruct" \
--num-prompts 32 \
--input-len 128 \
--output-len 1024 \
--seed 1100 \
--tensor-parallel-size 4
```



## 参考

- 官方链接：https://github.com/vllm-project/vllm
