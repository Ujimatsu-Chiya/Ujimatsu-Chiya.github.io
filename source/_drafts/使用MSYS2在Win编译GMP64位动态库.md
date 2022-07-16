---
title: 使用MSYS2在Win编译GMP64位动态库
tags:
---

# 下载并安装MSYS2

在[MSYS2官网](https://www.msys2.org/)下载 [msys2-x86_64-20220603.exe](https://github.com/msys2/msys2-installer/releases/download/2022-06-03/msys2-x86_64-20220603.exe)，打开并直接完成安装。

我将它安装在了D:\msys64下。

# 下载GMP库

在[GMP官网](https://gmplib.org/)下载[gmp-6.2.1.tar.xz](https://gmplib.org/download/gmp/gmp-6.2.1.tar.xz)，文件解压后存放在D:\msys64\home\Administrator\gmp-6.2.1中，其中Administrator是用户名。

# 正式安装

打开msys2根目录下的**mingw64.exe**，打开后窗口如下：


1. 先更新软件源和软件

```bash
sudo pacman -Syu  #更新软件源并更新软件
```

2. 安装如下内容

```bash
pacman -S mingw-w64-x86_64-gcc
pacman -S mingw-w64-x86_64-make
pacman -S mingw-w64-x86_64-libtool
pacman -S autoconf
pacman -S automake
pacman -S mingw-w64-x86_64-python3
```

3. 跳转到解压后的GMP库的根目录，并进行动态库编译。

```
 cd gmp-6.2.1/
 ./configure --disable-static --enable-shared
make
make check
make install
```


Clion使用
```
target_link_libraries(C2 D:\\\\msys64\\\\mingw64\\\\bin\\\\libgmp-10.dll)
```