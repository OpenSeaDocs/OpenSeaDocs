# LLaMA-factory

## 项目背景

​	开源大模型如LLaMA，Qwen，Baichuan等主要都是使用通用数据进行训练而来，其对于不同下游的使用场景和垂直领域的效果有待进一步提升，衍生出了微调训练相关的需求，包含预训练（pt），指令微调（sft），基于人工反馈的对齐（rlhf）等全链路。但大模型训练对于显存和算力的要求较高，同时也需要下游开发者对大模型本身的技术有一定了解，具有一定的门槛。

​        LLaMA-Factory项目的目标是整合主流的各种高效训练微调技术，适配市场主流开源模型，形成一个功能丰富，适配性好的训练框架。项目提供了多个高层次抽象的调用接口，包含多阶段训练，推理测试，benchmark评测，API Server等，使开发者开箱即用。同时借鉴 Stable Diffsion WebUI相关，本项目提供了基于gradio的网页版工作台，方便初学者可以迅速上手操作，开发出自己的第一个模型。

## 前置准备

- 项目代码

```
git clone https://github.com/hiyouga/LLaMA-Factory.git
```

- 模型

下载模型至服务器，此处以[Qwen2-7B-Instruct](https://www.modelscope.cn/models/qwen/Qwen2-7B-Instruct)为例。

## 环境安装

[DCU](./install_dcu.md)

## 快速开始

以Qwen2-7B-Instruct模型的Lora微调为例。

创建配置文件，

```
# 复制一个官方给出的配置文件模版
cd /LLaMA-Factory/examples/train_lora
cp llama3_lora_sft.yaml qwen2_lora_sft.yaml
```

修改配置文件中的model_name_or_path模型路径，

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
