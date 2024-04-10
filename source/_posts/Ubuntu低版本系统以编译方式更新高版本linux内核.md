---
title: Ubuntu低版本系统以编译方式更新高版本linux内核
date: 2024-01-22 11:01:15
tags: Ubuntu/Linux
categories: Ubuntu/Linux 
---

​		**因为低版本的Ubuntu系统（18.04）无法通过apt/deb二进制包形式，更新linux内核至较高版本，故计划通过本地编译高版本内核实现编译安装更新。**

# 以下为详细步骤：

1、前期准备

```
#解压对应版本内核，以6.4.3为例
tar -xavf  linux-6.4.3.tar.xz
#移动至/usr/src/目录
sudo mv linux-6.4.3  /usr/src
cd /usr/src/linux-6.4.3

```



2、环境准备

```
sudo apt-get install gcc make libncurses5-dev openssl libssl-dev 
sudo apt-get install build-essential
sudo apt-get install libelf-dev
sudo apt-get install libc6-dev
sudo apt-get install bison
sudo apt-get install flex
```



3、  配置编译配置

```
#清除编译过程中产生的所有中间文件
sudo make mrproper 
sudo make clean
#将已有的配置文件复制一份
sudo cp /boot/config-5.4.150-generic .config
#进入配置菜单，直接选择 exit，并 yes 保存
sudo make menuconfig
```



4、修改创建的 .config文件

```
sudo gedit .config
```

修改项为：

```
CONFIG_MODULE_SIG_KEY="certs/signing_key.pem"
CONFIG_SYSTEM_TRUSTED_KEYS=""
CONFIG_SYSTEM_BLACKLIST_HASH_LIST=""
CONFIG_SYSTEM_REVOCATION_KEYS=""
```

可选修改（有些内核版本太低，无法生成debug log，会报错）：

```
CONFIG_DEBUG_INFO_BTF=n
```



5、开始编译内核镜像（数字为物理线程数，我选择的是12线程加速）

```
 make modules -j12
```



6、安装内核模块

```cpp
make INSTALL_MOD_STRIP=1 modules_install
```



7、打包引导程序

作用是把/lib/modules/5.17.3中对应的.ko驱动打包到initrd.img文件中：

```csharp
mkinitramfs /lib/modules/6.4.3 -o /boot/initrd.img-6.4.3-generic
```



8、安装内核

这一步可以直接用sudo make install 替代

```
cp /usr/src/linux-6.4.3/arch/x86/boot/bzImage    /boot/vmlinuz-6.4.3-generic
cp  /usr/src/linux-6.4.3/System.map    /boot/System.map-6.4.3
```



9、根据需要修改grub引导bios

```
      cd /boot/grub
      chmod 777 grub.cfg
      #根据需要修改，优先级可先不设置
      sudo  gedit grub.cfg
      #更新grub
      update-grub2  
```



10、重启系统，大功完成

```
reboot
```



# **注意：如果无法启动ubuntu，先进入原有内核，执行：**

```
sudo apt install mokutil
sudo mokutil --disable-validation

```

然后输入一个密码，后面会用到

1. reboot重启
2. 四个选项，选择change secure boot state
3. 比如第一步设置的密码为123，则char[1] =1,char[2]
    =2,就是第几个字符的意思

5.选择yes

6.重启即可
