---
title: 怎样迁移hexo博客
date: 2024-04-10 14:31:37
tags: 一切的开始
categories: 碎碎念
---

# 备份

预先备份好文件:

*_config.fluid.yml, _config.yml,  themes, source, scaffolds, package.json, .gitignore*



# 步骤



1. 新建blog文件夹，复制进去相关备份文件
2. 安装nodejs、以及相关包管理工具npm、cnpm
3. 配置好本地SSH，并在github上填充key
4. 安装hexo脚手架、安装相关依赖、安装hexo插件hexo-depolyer-git：

```bash

	sudo npm install -g hexo-cli@版本号
	npm install
    npm install hexo-deployer-git --save
	
	
```

