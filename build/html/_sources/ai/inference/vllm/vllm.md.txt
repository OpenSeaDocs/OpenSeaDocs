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

vLLM 默认从 HuggingFace 上面下载模型，如果要从 ModelScope 上面下载模型，请通过命令 `pip install modelscope` 安装ModelScope，并设置环境变量：

```
export VLLM_USE_MODELSCOPE=True
```

### 离线批量推理

```
from vllm import LLM, SamplingParams

prompts = [
    "Hello, my name is",
    "The president of the United States is",
    "The capital of France is",
    "The future of AI is",
]
sampling_params = SamplingParams(temperature=0.8, top_p=0.95)

llm = LLM(model="/model/Qwen2-7B-Instruct")

outputs = llm.generate(prompts, sampling_params)

# Print the outputs.
for output in outputs:
    prompt = output.prompt
    generated_text = output.outputs[0].text
    print(f"Prompt: {prompt!r}, Generated text: {generated_text!r}")
```

## benchmark

基准测试代码位于/vllm/benchmarks目录下

```
cd /vllm/benchmarks
```

### throughput

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

