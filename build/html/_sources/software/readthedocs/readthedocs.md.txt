# ReadTheDocs

## 简介

Read the Docs 是一个托管和自动化文档生成的服务，旨在帮助开发者轻松创建、更新和发布项目文档。

## 本地操作

以下通过如何将本文档部署到线上为例，对操作流程进行介绍。

### 1.环境依赖

请自行安装好以下软件

- [Python3](https://www.python.org/)

- [Git](https://git-scm.com/)

注册以下网站账号

- [GitHub](https://github.com/)
- [readthedocs](https://about.readthedocs.com/)

### 2.创建文件夹配置

```cmd
mkdir readthedocs
cd readthedocs
```

### 3.生成Sphinx项目

安装sphinx包，

```
pip install sphinx sphinx-autobuild
```

设置文档信息

```
sphinx-quickstart
```

![1](../../imgs/software_readthedocs_sphinx.jpg)

此时，项目路径如下图所示


![2](../../imgs/software_readthedocs_tree.jpg)
### 4.编译部署

部署http服务

```
sphinx-autobuild source build/html
```

此时打开`http://127.0.0.1:8000`即可看到对应的页面。

### 5.更换主题

可到如下[链接](https://sphinx-themes.org/)查看选择一个你喜欢的主题，并使用pip安装该主题，

```
pip install sphinx-rtd-theme
```

修改Sphinx文档的配置文件`./source/conf.py`中的html_theme值

```
html_theme = 'sphinx_rtd_theme'
```

### 6.配置内容

#### 6.1 markdown依赖

安装markdown依赖包

```bash
pip install recommonmark sphinx_markdown_tables
```

在`./source/conf.py`中配置`extention`项

```
extensions = ['recommonmark','sphinx_markdown_tables']
```

#### 6.2 **配置文档内容**

通过修改`./source/index.rst`文件配置文档内容，可参考[官方配置说明文档](https://zh-sphinx-doc.readthedocs.io/en/latest/rest.html)

## 远程托管

### 1.依赖包文件

项目根目录下创建依赖包文件requirements.txt，内容如下如果有安装其他主题包，也需要添加进来）

```
anyio==4.3.0
astor==0.8.1
certifi==2024.2.2
decorator==5.1.1
h11==0.14.0
httpcore==1.0.4
httpx==0.26.0
idna==3.6
numpy==1.26.4
opt-einsum==3.3.0
pillow==10.2.0
protobuf==3.20.2
sniffio==1.3.0
sphinx 
sphinx-autobuild
recommonmark
sphinx_markdown_tables
sphinx_rtd_theme
```

### 2.配置文件

在项目根目录下创建一个`.readthedocs.yaml`文件，其内容如下

```
version: 2

build:
  os: ubuntu-22.04
  tools:
    python: "3.10"

sphinx:
  configuration: source/conf.py

python:
  install:
    - requirements: requirements.txt
```

### 3.创建GitHub项目

创建一个GitHub项目，项目名可与本项目名相同，然后推送本地项目至GitHub

```
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/MJdoc/readthedocs.git
git push -u origin main
```

## ReadTheDocs导入项目

使用github账号登录[ReadTheDocs官网](https://readthedocs.org/)，并导入项目


![3](../../imgs/software_readthedocs_importproject.jpg)


填写项目信息后，依次点击“下一步-----完成”，


![4](../../imgs/software_readthedocs_project.png)
最后，点击”build version“按钮创建版本，完成后点击“阅读文档”即可看到线上文档了。
