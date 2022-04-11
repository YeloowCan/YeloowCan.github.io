title: 记录我的Hexo博客搭建过程
author: 黄罐头
tags: ['hexo', '博客搭建']
categories: blog
date: 2021-06-30 22:29:00
---
## 开始搭建
### 一.创建github仓库
 1. 在github下新建一个仓库，名为<span style="color: red">你的用户名.github.io</span>
 2. 配置ssh key，右键git bash here，分别执行如下命令

		git config --global user.name "你的GitHub用户名"
		git config --global user.email "你的GitHub注册邮箱"
    
 3. 生成ssh密钥文件

		ssh-keygen -t rsa -C "你的GitHub注册邮箱"

直接回车，在C:\Users\A\.ssh(以自己的目录为准)下生成<span style="color: red">id_rsa.pub</span>密钥，打开[GitHub_Settings_keys](https://github.com/settings/keys) 页面，新建new SSH Key，将<span style="color: red">id_rsa.pub</span>密钥复制进去。

### 二.博客的安装与部署
使用npm安装hexo:
```
npm install -g hexo-cli

```
初始化博客
```
hexo init blog
```
在blog目录下执行下面命令启动博客查看是否初始化成功，执行完可在[localhost:4000](http://localhost:4000)下查看
```
hexo g
hexo s
```
打开blog目录下得_config.yml文件，与github关联起来，滚到最后，修改为(repo填自己的仓库)：

	deploy:
	type: git
	repo: https://github.com/YeloowCan/YeloowCan.github.io
	branch: master

安装git部署插件
	
    npm install hexo-deployer-git --save

按顺序执行以下命令进行部署
		
    hexo clean
    hexo g
    hexo d

浏览器打开[yeloowcan.github.io](https://yeloowcan.github.io/)，可以访问到博客了

### 三.绑定域名
1. 可以在阿里云上购买的域名，我买的是[yellowcan.top](https://www.yellowcan.top/)，打开阿里云的域名控制台，添加一条A记录，记录值是ip地址（可以Ping仓库地址获取IP地址），再添加一条CNAME记录，记录值是博客地址，比如我的是：yeloowcan.github.io。
2. 再本地博客目录source文件夹下新建一个CNAME文件<span style="color: red">（！！！一定要保存为所有文件，不能保存为txt文件，可以先新建文本文档后将后缀名直接删掉直接把文件）</span>，里面写进你的域名，我的是：www.yellowcan.top
3. 再顺序执行以下命令进行部署

		hexo clean
   	 hexo g
   	 hexo d
4. 在浏览器里访问自己的域名，就可以访问到自己的博客啦。

### 四.修改主题
我用的是matery，在本地博客的theme文件下执行下面命令将主题下载下来：
		
        git clone https://github.com/blinkfox/hexo-theme-matery.git

然后打开博客的_config.yml文件，将theme改为hexo-theme-matery

			theme: hexo-theme-matery

最后再执行下面命令部署一下，就可以啦

			hexo clean
	        hexo g
	        hexo d

打开自己的域名，博客大功告成，我的博客地址：[yellowcan.top](http://yellowcan.top)