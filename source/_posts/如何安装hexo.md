---
title: 如何安装hexo
date: 2023-12-28 16:31:01
tags: 一切的开始
categories: 碎碎念
---

# 一、前置环境安装

## 1、已经安装好**nodejs**(包括包管理工具**npm**、**cnpm**)、**git**（以上ubuntu系统下，均可以通过二进制apt-get安装）



## 附nodejs安装教程：

先安装nodejs的管理工具：

```bash
npm install n -g
```

相关参数指令（全局操作需要加上sudo）：

| 指令含义                   | 指令               |
| -------------------------- | ------------------ |
| 安装最新长期支持版node     | n lts              |
| 版本检查                   | node -v            |
| 安装指定版本               | n 版本号           |
| 安装最新稳定版             | n lts              |
| 卸载指定版本node           | n rm 0.9.4 v0.10.0 |
| 查看已有的node版本，并切换 | n                  |
|                            |                    |

## 2、接着准备安装hexo脚架环境：

```bash
sudo cnpm install -g hexo-cli@版本号
```



# 二、开始安装

新建一个文件夹用于保存hexo博客对象node（有关于npm的操作，建议都使用cnpm操作代替）：

```bash
mkdir		build
cd				build
hexo		 init
```

如果遇到无法安装依赖的问题，输入：	

```bash
rm -rf node_modules && npm install --force	
```

​		

# 三、本地部署（不想要本地部署，可跳过）

```bash
hexo g		#静态生成文件
hexo s		#启动
#如果遇到4000端口被占用情况，输入：
hexo 	s 	-p 		端口号
```



------------------------------------------------------------------------------------------------------------------------------


四、远程部署
==============================================================================================================================


前置工作：完成github对本地主机间的RSA SSL密钥设置（远程仓库设置rsa公钥），保证后续git操作成功，并新建一个远程仓库

## 修改配置文件和安装Git部署插件

1、进入Blog文件夹，找到_config.yml,

下滑到文件底部，填上如下内容：

```
deploy:
  type: git
  repository: git@github.com:wings0210/wings0210.github.io.git
  branch: main
```



2、接着输入：

```bash
cnpm install hexo-deployer-git --save
```

# 五、安装Fluid主题

1、通过 npm/cnpm 直接安装，进入博客目录执行命令：

```bash
npm/cnpm install --save hexo-theme-fluid
```



2、粘贴覆盖_config.fluid.yml和 _config.yml



3、粘贴覆盖Blog/themes/fluid/source/img



## 生成静态文件和远程部署（后续更新修改，都是这三步）

```bash
hexo	clean
hexo	g
hexo	d
```

## 访问和绑定域名

参考：https://zhuanlan.zhihu.com/p/103813944



# 五、后续环节

相关markdown编辑器下载，
linux：	

```bash
wget https://file.babudiu.com/f/yXCL/Typora_Linux_0.11.18_amd64.deb
```

windows：

```

```



设置和优化相关主题参考：https://zhuanlan.zhihu.com/p/105584373

