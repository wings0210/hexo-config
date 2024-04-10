---
title: ubuntu安装VUE相关
date: 2024-01-03 11:49:51
tags: VUE
categories: VUE相关
---



# 前提：已经安装好web容器nodejs和相关包管理工具，可参考hexo安装



# 一、全局安装Vue.js的脚手架工具vue-cli

```bash
sudo npm install -g @vue/cli
```

# 二、第一个Vue项目

先设置npm注册表使用淘宝镜像

```bash
sudo npm config set registry https://registry.npm.taobao.org
```

1、在需要创建项目的目录下：(查看项目链接vue版本：sudo npm list vue)

```bash
sudo vue create "项目名"
```

2、进入所在目录下，如：

```bash
cd my_vue_project
```

3、启动

```bash
sudo npm run serve
```

（若启动vue3项目出错，尝试在项目目录使用命令：sudo npm i vue@3.3.4，将项目vue版本升级）



# 三、进行Vue部署，安装代理服务器nginx

1、先安装nginx

```bash
sudo apt update
sudo apt install nginx
```

2、查看nginx状态

```bash
sudo systemctl status nginx
```

其中nginx 相关命令：

| 指令                         | 含义      |
| ---------------------------- | --------- |
| sudo systemctl stop nginx    | 停止      |
| sudo systemctl start nginx   | 启动      |
| sudo systemctl restart nginx | 重启      |
| sudo systemctl reload nginx  | 重新加载  |
| sudo systemctl disable nginx | 禁用Nginx |
| sudo systemctl enable nginx  | 启用      |
