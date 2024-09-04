# 安装

基于英伟达GPU加速卡适配vLLM框架

## 要求

- OS: Linux
- Python: 3.8 – 3.11
- GPU: 计算能力不低于7.0（比如V100、T4、 RTX20xx、A100、 L4 H100等）

## Pip

```
# 基于conda创建虚拟环境
conda create -n vllm python=3.10 -y
conda activate vllm
# 使用pip安装vllm包
pip install vllm
```

## 其他

- 官方安装文档：https://docs.vllm.ai/en/latest/getting_started/installation.html
