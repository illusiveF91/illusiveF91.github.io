---
title: 如何使用Hexo+Github部署个人博客
date: 2025-03-26 15:32:44
tags:
---

## 安装Hexo
安装Hexo 需要以下应用

- [Node.js](https://nodejs.org/) (Node.js 版本需不低于 10.13，建议使用 Node.js 12.0 及以上版本)
- [Git](http://git-scm.com/)

### 安装Git

下载并安装 [git](https://git-scm.com/downloads/win)

### 安装Node.js

Node.js 为大多数平台提供了官方的 [安装程序](https://nodejs.org/zh-cn/download/)。

安装完成后打开cmd 输入

~~~ shell
npm -v 
~~~

试一下 如果有返回版本号就ok了

### 安装Nexo

所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。

~~~shell
npm install -g hexo-cli
~~~



## 建站

安装 Hexo 完成后，执行以下命令，Hexo 将会在指定文件夹中新建所需要的文件。

~~~shell
hexo init <folder>
cd <folder>
npm install
~~~

<folder> 是你指定的文件夹

初始化后，项目文件夹将如下所示：

```
.
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes
```

### _config.yml

网站的 [配置](https://hexo.io/zh-cn/docs/configuration) 文件。 

### package.json

应用程序的信息。

~~~Json
{
  "name": "hexo-site",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "build": "hexo generate",
    "clean": "hexo clean",
    "deploy": "hexo deploy",
    "server": "hexo server"
  },
  "hexo": {
    "version": "7.3.0"
  },
  "dependencies": {
    "hexo": "^7.3.0",
    "hexo-deployer-git": "^4.0.0",
    "hexo-generator-archive": "^2.0.0",
    "hexo-generator-category": "^2.0.0",
    "hexo-generator-index": "^4.0.0",
    "hexo-generator-tag": "^2.0.0",
    "hexo-renderer-ejs": "^2.0.0",
    "hexo-renderer-marked": "^7.0.0",
    "hexo-renderer-pug": "^3.0.0",
    "hexo-renderer-stylus": "^3.0.1",
    "hexo-server": "^3.0.0",
    "hexo-theme-landscape": "^1.0.0"
  }
}
~~~

### scaffolds

[模版](https://hexo.io/zh-cn/docs/writing#模版（Scaffold）) 文件夹。 新建文章时，Hexo 会根据 scaffold 创建文件

### source

资源文件夹。 是存放用户资源的地方。 除 `_posts` 文件夹之外，开头命名为 `_` (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。 Markdown 和 HTML 文件会被解析并放到 `public` 文件夹，而其他文件会被拷贝过去。

### themes

[主题](https://hexo.io/zh-cn/docs/themes) 文件夹。 Hexo 会根据主题来生成静态页面。



## 本地启动服务

建好网站之后通过以下命令在本地启动服务器

~~~shell
hexo serve
~~~

默认端口为4000， 使用`http://localhost:4000/` 进行访问



## 安装主题

hexo提供了很多主题，在[官网](https://hexo.io/themes/)上可以找到

本教程使用redifine

首先打开git bash

使用以下命令进入到网站文件夹

~~~ git
cd <folder>
~~~

使用以下命令将主题github仓库下载到theme文件夹下（以redifine为例）

~~~git
git clone https://github.com/EvanNotFound/hexo-theme-redefine.git themes/redefine
~~~

打开_config.yml 文件，找到theme配置项,增加redefine

~~~ yaml
theme:redefine
~~~

这个地方填写的名称对应themes文件夹下各主题的文件夹名称

本地启动看下效果，如果没问题就ok了

~~~shell
hexo serve
~~~



## 部署github

如果没有github账号的话，需要首先注册一个，有邮箱就能注册

注册完github账号后需要创建一个[github page](https://pages.github.com/)的仓库

创建完仓库之后，安装git部署插件

~~~shell
npm install hexo-deployer-git --save
~~~

安装完成之后，打开_config.yml 文件，配置远程部署

~~~yaml
deploy:
  type: git
  repo: https://github.com/username/username.github.io.git
  branch: main
~~~

type是远程部署的类型，我们是github page所以填git

repo是仓库地址，在你的仓库里找到

![](D:\Blog\source\images\where_to_find_git_repo_url.png)

branch是你的分支，默认main就行

配置完之后执行以下命令将网站部署到github上

~~~shell
hexo clean
hexo generate
hexo deploy
~~~

hexo clean 会清理缓存文件，和已生成的静态文件

hexo generate 会根据当前配置生成新的静态文件

hexo deploy 部署网站

部署完成后 使用你配置的repourl 上去看看 https://username.github.io/

至此，网站部署完成，后续写文章啥的可以自己去hexo上看文档，或者等我在写一个教程🤣
