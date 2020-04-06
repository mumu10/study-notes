# NET 5.0 安装

## 1. 关于NET 5.0

虽然职业的大部分时间都没有用微软家的平台，但是最近对于微软一系列开源和跨平台的操作非常看好，同样的，对于.NET平台也越发感兴趣起来。

早在去年，就知道NET 5的计划：[《Introducing .NET 5》](https://devblogs.microsoft.com/dotnet/introducing-net-5/)。今年三月份，微软家总算发布了试用版：[《Announcing .NET 5 Preview 1》](https://devblogs.microsoft.com/dotnet/announcing-net-5-0-preview-1/)，于是迫不及待地想看看究竟怎么回事。

## 2. 安装NET 5.0

NET 5.0提供多种平台安装，为了体验它的跨平台特性，准备在Linux安装。家里的笔记本自带win10家庭版，之前就安装了[Docker Desktop on Windows](https://docs.docker.com/docker-for-windows/)。因此打算在docker中的Linux系统安装。

Win10上要使用Linux有多种方式：

* 基于`Hyper-V`安装虚拟机
* 安装Docker Desktop on Windows
* 使用WSL 1
* 使用WSL 2

我用的是第二种方式。

## 2.1 WIN10中DOCKER的安装与使用

主要参考了[《WIN10中DOCKER的安装与使用》](https://blog.csdn.net/hunan961/article/details/79484098#%E7%8E%AF%E5%A2%83%E5%87%86%E5%A4%87)这篇文章。

这里有几点额外的可以参考：

1. 安装之前，需要打开`Hyper-V`，可以参考[《Win10家庭版中使用Hyper-V》
](https://zhuanlan.zhihu.com/p/51939654)。

2. 在Start Docker之前可以把Virual Hard Disks从默认的C盘切换到其它盘，免得随着使用，C盘容量不够。Start->Windows管理工具->Hyper-V Manager->Virual Hard Disks。

3. 配置阿里云镜像。

## 2.2 Docker上安装NET 5.0

按[《NET5.0 SDK的安装说明》](https://github.com/dotnet/core/blob/master/release-notes/5.0/preview/5.0.0-preview.2-install-instructions.md)即可。

几点需要注意的地方：

1. 请务必使用centos。不知道为什么，ubuntu镜像中安装snapd一直没有成功。

2. 运行centos的命令请参考 [《docker 容器使用 systemctl 命令是报错》](https://www.cnblogs.com/infoo/p/11900607.html)中的命令：

    ```
    docker run -itd   --privileged --name myCentos centos /usr/sbin/init
    
    //创建完成后: 请使用以下命令进入容器
    docker exec -it myCentos /bin/bash
    ```
3. 按照官方文档[《使用 .NET Core CLI 实现 .NET Core 入门》
](https://docs.microsoft.com/zh-cn/dotnet/core/tutorials/cli-create-console-app)中的`Hello World`示例运行，如果成功，表明按照成功了。


## 3. 使用VS Code进行Remote Debug

随着跨平台需求，云平台开发的需求的兴起，似乎一夜之间各家IDE都开始支持跨平台调试了。作为微软家的产品VS Code，自然是能够跨平台调试.NET程序的。

### 3.1 Start CentOS in Docker

这个时候假设已经在CentOS in Docker安装好.NET 5的SDK了，重新开始工作的步骤如下：

1. Start Docker for Windows

2. 通过 `docker ps -a` 查看之前的docker image的状态

3. 运行 `docker start {docker image name}` 重新运行centos的docker image

4. 运行 `docker exec -it {docker image name} /bin/bash` 进入容器centos的bash

### 3.2 Start VS Code 并且安装Docker扩展

安装完Docker扩展后，可以在Docker扩展界面发现正在运行的centos，点击右键菜单`attach virtual studio code`选项，即可start另外一个VS Code instance，此VS Code instance已经attche到remote了。在此VS Code安装C#扩展，即可开始编辑、编译、debug .NET程序。



