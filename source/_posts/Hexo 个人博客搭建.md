---
title: Hexo个人博客搭建
tags: [hexo]
published: true
hideInList: false
isTop: false
date: 
feature:
sticky: 101
top: 101
category: 学习 # 分类 MATLAB
---
---
# Hexo个人博客搭建

$a$

---

1. 安装nodejs、git

首先、需要安装 Node.js(http://nodejs.cn/download/) 和 Git(https://git-scm.com/downloads)，大家尽量去下载.exe扩展名的可执行文件，这样的好处是一键安装、省去了一些配置。安装版本也可以安装最新的版本。如果有问题卸载安装旧版。 

`验证安装是否成功`，打开CMD

```python
验证Node.js的方法
node -v
npm -v
输入后能够显示版本说明安装成功
```



1. 在文件夹中右击 `Git Bash Here` 

2. 使用npm命令安装Hexo，输入：

   ```python
   npm install -g hexo-cli # 安装hexo可略过
   hexo init
   hexo new 我的新博客
   hexo g #生成
   hexo s #启动服务预览
   git config --global user.name "wbupt"
   git config --global user.email "34@qq.com"
   npm install hexo-deployer-git --save # 安装上传文件
   npm install hexo-renderer-pug hexo-renderer-stylus # 安装 butterfly插件
   npm install hexo-generator-index-pin-top --save # 文章置顶插件
   npm install hexo-hide-posts --save # 隐藏文章
   npm install hexo-math --save # 安装公式
   npm i hexo-renderer-pandoc  # 不要安装 容易报错
   npm uninstall hexo-renderer-pandoc	# 卸载
   npm install hexo-wordcount --save # 安装字数统计
   
   
   hexo s -p  5000 # 更改localhost值
   hexo d #部署
   # 打开浏览器输入地址
   localhost:4000
   hexo clean #清除缓存，若是网页正常情况下可以忽略这条命令
   ```

   隐藏文章地址https://www.cnblogs.com/yangstar/articles/16690342.html

   ```python
   ssh-keygen -t rsa -C "34@qq.com"
   # 创建一个 ssh key, 用准备好的email作为标签
   Generating public/private rsa key pair.
   Enter file in which to save the key (/c/Users/you/.ssh/id_rsa): [Press enter]
   ```

   

3. ## 配置网站

进入根目录里的themes文件夹，里面也有个`_config.yml`文件

```python
deploy:
  type: git
  repo: git@github.com:仓库名/仓库名.github.io.git
  branch: main 
```

- 安装Git部署插件

```python
npm install hexo-deployer-git --save # 安装上传文件
hexo clean 
hexo g 
hexo d
```

```python
ssh-keygen -t rsa -f  ~/.ssh/wbupt -C "34@qq.com"
ssh -T [34@qq.com protected]
ssh -T git@wbupt.github.com #新的ssh_key验证

git config --global user.name Github_name
git config --global user.email ww@163.com
ssh-keygen -t rsa -C wz@163.com
```

## 配置文件设置：

`_config.yml`

```python
skip_render: #跳过文件
  - "HTML/*"
  - "about/*"
banner_img: ""
```

```python
---
title: Hexo个人博客搭建
tags: [Gridea,Hexo,Python] # 标题
published: true
hideInList: false
isTop: true
abbrlink: 20929
date: 2023-03-14 10:19:08
feature:
sticky: 101
top: 101
---
```

## 跳过文件

```python
skip_render: 
  - "HTML/*"
  - "about/*"
banner_img: ""
```

## Hexo 顶面配置

```python
title: Hexo个人博客搭建
tags: [Gridea,Hexo,Python] # 标签
published: true # 未知
hidden: false
hide: false
isTop: true # ?
abbrlink: 20929 # ?
date: 2023-03-14 10:19:08 # time
feature:
sticky: 101
top: 101
category: Hexo # 分类 category
```



