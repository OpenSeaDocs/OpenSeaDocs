# LLaMA-factory

## 简介

LLaMA Factory 是一个简单易用且高效的大型语言模型（Large Language Model）训练与微调平台。通过 LLaMA Factory，可以在无需编写任何代码的前提下，在本地完成上百种预训练模型的微调。

## 前置准备

- 项目代码

```
git clone https://github.com/hiyouga/LLaMA-Factory.git
```

- 模型

下载模型至服务器/data/model文件夹下，此处以[Qwen2-7B-Instruct](https://www.modelscope.cn/models/qwen/Qwen2-7B-Instruct)为例。

## 环境安装

[安装-海光DCU](./install_dcu.md)

## 快速开始

以Qwen2-7B-Instruct模型的Lora微调为例。

创建配置文件，

```
# 复制一个官方给出的配置文件模版
cd /LLaMA-Factory/examples/train_lora
cp llama3_lora_sft.yaml qwen2_lora_sft.yaml
```

修改配置文件中的model_name_or_path模型路径，关于配置文件的参数含义可参考[官方文档](https://llamafactory.readthedocs.io/zh-cn/latest/)

```
vim qwen2_lora_sft.yaml
```

接下来就可以执行Lora微调了，

```
cd /LLaMA-Factory
# 默认多卡
llamafactory-cli train examples/train_lora/qwen2_lora_sft.yaml
# DCU指定卡
HIP_VISIBLE_DEVICES=0,1 llamafactory-cli train examples/train_lora/qwen2_lora_sft.yaml
# GPU指定卡
CUDA_VISIBLE_DEVICES=0,1 llamafactory-cli train examples/train_lora/qwen2_lora_sft.yaml
```

## 参考

1. 官方项目链接：https://github.com/hiyouga/LLaMA-Factory
2. 官方教程文档：https://zhuanlan.zhihu.com/p/695287607
