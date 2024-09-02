# vLLM

## 简介

vLLM是一个开源的LLM推理和服务引擎。

## 安装

[基于GPU](./install_gpu.md)

[基于DCU](./install_dcu.md)

## 快速开始

- 项目代码

```
git clone https://github.com/vllm-project/vllm.git
```

- 准备模型

下载模型至服务器/data/model文件夹下，此处以[Qwen2-7B-Instruct](https://www.modelscope.cn/models/qwen/Qwen2-7B-Instruct)为例。

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

## Benchmark

进入项目benchmark目录下，

```
cd vllm/benchmarks
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

## 模型支持

|                             系列                             |      模型       | 备注 |
| :----------------------------------------------------------: | :-------------: | :--: |
| [Qwen](https://www.modelscope.cn/organization/qwen?tab=model) | 7B、14B、72B等  |      |
| [Qwen2](https://www.modelscope.cn/organization/qwen?tab=model) | 0.5B、7B、72B等 |      |

## 参考

- 官方链接：[https://github.com/vllm-project/vllm](https://github.com/vllm-project/vllm)