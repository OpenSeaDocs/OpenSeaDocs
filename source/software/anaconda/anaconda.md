# Anaconda

## 简介

Anaconda 是一个用于科学计算的 Python 发行版，支持 Linux, Mac, Windows, 包含了众多流行的科学计算、数据分析的 Python 包。

## 安装

- 下载安装包

下载所需版本安装包，并上传至服务器

Anaconda 安装包下载地址：https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/ 

Miniconda 安装包下载地址：https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/

- 软件安装

此处以Miniconda3-py310_24.7.1-0-Linux-x86_64.sh为例

```
# 下载安装包
sudo wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-py310_24.7.1-0-Linux-x86_64.sh
# 执行安装
sudo bash Miniconda3-py310_24.7.1-0-Linux-x86_64.sh
```

- 激活环境变量

```
sudo source ~/.bashrc
```

- 验证

```
conda -V
```

可输出conda版本号即安装完成

- 配置国内镜像源

创建用户目录下的 `.condarc` 文件来使用 TUNA 镜像源（Windows 用户无法直接创建名为 `.condarc` 的文件，可先执行 `conda config --set show_channel_urls yes` 生成该文件之后再修改）

```
sudo vim ~/.condarc
```

并写入如下内容

```
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch-lts: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  deepmodeling: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/
```

清除索引缓存

```
conda clean -i
```

## 快速开始

查看conda版本

```
conda -V
```

创建一个名为py10的虚拟环境

```
conda create -n py10 python=3.10
```

给予py10环境克隆一个名为py10_cp的虚拟环境

```
conda create -n py10_cp --clone py10
```

删除一个名为py10的虚拟环境

```
conda remove -n py10 --all 
```

激活py10虚拟环境

```
conda activate py10
```

退出当前虚拟环境

```
conda deactivate
```

查看当前所有虚拟环境

```
conda env list
```

## 参考

- 参考文档：https://blog.csdn.net/2402_84205067/article/details/140143471