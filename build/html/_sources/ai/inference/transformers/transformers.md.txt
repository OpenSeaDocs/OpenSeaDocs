# transformers

## 简介





## 前置准备





## 环境安装





## 快速开始

```
from transformers import AutoTokenizer, AutoModel

tokenizer = AutoTokenizer.from_pretrained("/model/internvl2-40b", trust_remote_code=True)
model = AutoModel.from_pretrained("/model/internvl2-40b", trust_remote_code=True)

inputs = tokenizer("Hello world!", return_tensors="pt")
outputs = model(**inputs)
```



## 参考