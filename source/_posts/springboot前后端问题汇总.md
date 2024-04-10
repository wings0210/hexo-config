---
title: springboot前后端问题汇总
date: 2024-01-05 13:36:29
tags: Spring
categories: SpringBoot前后端问题汇总
---



# 一、Springboot后端问题汇总

1、导入开源项目步骤

*1）*每个项目单独配置 **maven的仓库conf** 和 **本地仓库的地址**

*2）*每个项目单独配置项目结构下的jdk



2、maven的依赖配置文件**pom.xml**中 的 **project头文件** 报红问题

解决方案：

在	设置->架构和DTD->忽略的模式和DTD	下：

新增：http://maven.apache.org/POM/4.0.0





## 二、VUE前端项目启动部署步骤

1、进入项目所在文件夹，执行：

```bash
npm install --registry=https://registry.npmmirror.com
```

如果已经通过npm/cnpm 安装过节点，先删除出错的node_modules



2、接着执行启动命令：

```bash
npm run dev
```

或者

```bash
npm run serve
```

