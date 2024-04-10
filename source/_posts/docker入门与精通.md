---
title: docker入门与精通
date: 2024-01-03 11:31:56
tags: docker
categories: docker相关
---

参考外部链接：http://www.dockerinfo.net/document

# 一、docker构成

## docker包含：

1、docker容器（可写层，主要为应用程序，广义上也可以将docker容器视作docker）

2、docker镜像（可读层，环境，镜像可以有父镜像）



## docker概念：

可理解为对操作系统的虚拟化，基于linux内核的 Linux 容器（LXC）等技术（抽象版自制内核），具备高可用性



# 二、docker镜像构造

## 1、通过自定义Dockerfile，来使用 docker build 命令构建，只要来源于本地系统环境

它将基于 Dockerfile 中的指令和上下文构建一个可运行的镜像。下面是 docker build 命令的基本用法：

```bash
docker build [OPTIONS] PATH
```

```bash
OPTIONS：是一些可选的参数，用于指定构建过程中的各种选项，例如镜像标签、构建缓存、网络设置等。常用的选项包括：
    -t, --tag：指定镜像的标签，格式为 <repository>:<tag>。
    --build-arg：传递构建时的参数给 Dockerfile。
    --no-cache：禁用构建过程中的缓存。
    --network：指定构建过程中使用的网络模式。

PATH：是包含 Dockerfile 的目录路径或 URL。这是构建上下文的路径，Docker 在构建过程中会将该路径下的文件和目录复制到镜像中。
```

在执行 docker build 命令时，Docker 会读取 Dockerfile 中的指令，按照指令的顺序执行构建过程。Dockerfile 是一个文本文件，其中包含了构建镜像所需的指令和配置。常见的 Dockerfile 指令包括：

| 参数    | 含义                                 |
| ------- | ------------------------------------ |
| FROM    | 指定基础镜像，用于构建新镜像的起点。 |
| RUN     | 在镜像中执行命令                     |
| COPY    | 将文件从构建上下文复制到镜像中       |
| WORKDIR | 设置工作目录                         |
| EXPOSE  | 声明容器运行时监听的端口             |
| CMD     | 指定容器启动后要执行的命令           |



## 2、通过已有的镜像/容器，使用 docker commit 命令构建，主要来源于远程仓库/可定制化已有容器

如在容器中添加 json 和 gem 两个应用：

```bash
   root@0b2616b0e5a8:/# gem install json
```

当结束后，我们使用 exit 来退出，现在我们的容器已经被我们改变了，使用 docker commit 命令来提交更新后的副本。

  

```bash
 $ sudo docker commit -m "Added json gem" -a "Docker Newbee" 0b2616b0e5a8 ouruser/sinatra:v2
   4f177bd27a9ff0f6dc2a830403925b5360bfe0b93d476f7fc3231110e7f71b1c
```

其中，-m 来指定提交的说明信息，跟我们使用的版本控制工具一样；-a 可以指定更新的用户信息；之后是用来创建镜像的容器的 ID；最后指定目标镜像的仓库名和 tag 信息。创建成功后会返回这个镜像的 ID 信息。

使用 docker images 来查看新创建的镜像。

```bash
   $ sudo docker images
   REPOSITORY          TAG     IMAGE ID       CREATED       VIRTUAL SIZE
   training/sinatra    latest  5bc342fa0b91   10 hours ago  446.7 MB
   ouruser/sinatra     v2      3c59e02ddd1a   10 hours ago  446.7 MB
   ouruser/sinatra     latest  5db5f8471261   10 hours ago  446.7 MB


```

之后，可以使用新的镜像来启动容器

```bash
   $ sudo docker run -t -i ouruser/sinatra:v2 /bin/bash
```



### 3、通过外部导入，使用 docker import 命令构建，主要为本地文件系统 



# 三、构建docker容器

构建 Docker 容器的命令是 docker run。
docker run 命令用于在 Docker 中创建和运行容器。下面是 docker run 命令的基本用法：

```bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```



```bash
OPTIONS：	是一些可选的参数，用于配置容器的各种选项，例如端口映射、环境变量、数据卷等。常用的选项包括：
    -d, --detach：	在后台运行容器。
    -p, --publish：	将容器的端口映射到主机的端口。
    -e, --env：	设置容器的环境变量。
    -v, --volume：	挂载主机的目录或数据卷到容器中。
    --name：	为容器指定一个名称。
    --network：	连接容器到指定的网络。

IMAGE：	指定要基于的镜像名称或镜像 ID。

COMMAND：	可选参数，用于在容器启动时执行的命令。

ARG...：	可选参数，传递给容器启动命令的参数。
```

通过执行 docker run 命令，Docker 会根据指定的镜像创建一个新的容器，并在容器内部运行指定的命令。容器可以是临时的，也可以是长期运行的。在容器内部，您可以运行应用程序、执行命令、访问文件系统等。
