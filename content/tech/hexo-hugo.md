+++
title = "Hexo迁移hugo"
date = "2020-08-21 10:17:25"
tags = ["hugo"]
gitinfo = true
dropCap = false
toc = true
+++


## 前言
对于博客搭建，[hexo](https://hexo.io/zh-cn/)怕是大家都耳熟能详，但是[hugo](https://gohugo.io/)是比较新的一种搭建方式，Hugo是由Go语言实现的静态网站生成器。简单、易用、高效、易扩展、快速部署。  
两者的文章书写方式都是MarkDown的语法，对于迁移有很大的帮助。hugo的快速和MemE让我眼前一亮，以下是我通过hexo迁移hugo历程

## windows安装

针对于不同的操作系统，安装过程会有所不同，我以windows为例，通过[hugo releases地址](https://github.com/gohugoio/hugo/releases) 选择相关系统的压缩包  
提示:1、下载带有`extended`的扩展版包 2、在windows的环境变量Path中配置hugo路径

### Hugo的使用
先查看hugo版本，然后进行博客站点的创建
```sh
 hugo version
 hugo new site blog
```
命令执行之后生成目录结构及与Hexo的目录结构差异性对比
    
```
.                     # 说明             Hexo
├── archetypes/     # 文章模板          scaffolds/
├── assets/         # Hugo 管道
├── config.toml     # 配置文件          _config.yml
├── content/        # 文章目录          source/_posts/
├── data/           # Hugo 数据文件     source/_data/
├── layouts/        # 布局模板
├── public/         # 生成的静态文件     public/
├── resources/      # Hugo 缓存
├── static/         # 网站的静态文件     source/
└── themes/         # 主题目录          themes/
```
### 安装MemE主题
进入blog站点博客目录,进行主题的安装，例如我选择的`MemE`主题

```sh
cd blog
git init
git submodule add --depth 1 https://github.com/reuixiy/hugo-theme-meme.git themes/meme
```

## hugo的blog开始之路

1️、替换 `config.toml`

对于简体中文用户，可以通过一下命令替换 `config.toml` 文件，替换成简体中文版本

```sh
 rm config.toml && cp themes/meme/config-examples/zh-cn/config.toml config.toml
```

2️、 新建文章
```sh
hugo new "posts/hello-world.md"
hugo new "about/_index.md"
```
在`content`目录会生成相对应的文件，例如`posts/hello-world.md`文件，`about/_index.md`文件，_index.md文件是主页，可以直接在浏览器打开  
在hexo迁移hugo中可以把原来hexo的文件`source`目录下的文章cp过来

3、起本地服务
```sh
hugo server 
```

build很快，出现 <http://localhost:1313/>，可以直接打开浏览器访问，随意更新md文章，博客站点内容会自动更新，很酷😄


## 定制

相关配置可在config.toml文件中进行配置  
你想要自定义样式，推荐在assets目录下创建`assets/scss/custom/_custom.scss` 文件,不修改theme文件下的样式文件(当时使用hexo就是在theme修改☹️)，以以覆盖theme目录下的样式文件

