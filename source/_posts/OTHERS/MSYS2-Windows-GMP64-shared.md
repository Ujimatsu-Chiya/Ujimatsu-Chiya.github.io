---
title: 使用MSYS2在Windows编译GMP64位动态库
mathjax: true
date: 2022-07-17 14:02:25
tags:
---
<escape><!-- more --></escape>

# 下载并安装MSYS2

在[MSYS2官网](https://www.msys2.org/)下载[msys2-x86_64-20220603.exe](https://github.com/msys2/msys2-installer/releases/download/2022-06-03/msys2-x86_64-20220603.exe)，打开并直接完成安装。

如果官网太慢，可以在清华源下载[msys2-x86_64-20220603.exe](https://mirrors.tuna.tsinghua.edu.cn/msys2/distrib/x86_64/msys2-x86_64-20220603.exe)。

我将它安装在了`D:\msys64`下。

安装完成后会自动打开一个窗口，不用管它。

接下来需要将`D:\msys64\mingw64\bin`这个目录添加到**系统变量**`Path`中，如图：

![](p1.png)


# 下载GMP库

在[GMP官网](https://gmplib.org/)下载[gmp-6.2.1.tar.xz](https://gmplib.org/download/gmp/gmp-6.2.1.tar.xz)，文件解压后存放在`D:\msys64\home\admin\gmp-6.2.1`中，其中`admin`是用户名。

# 正式安装

打开msys2根目录下的**mingw64.exe**，打开后窗口如下：

![](p2.png)

注意红框是MINGW64.

如果执行命令时下载速度太慢，可以先参考[这里](https://mirrors.tuna.tsinghua.edu.cn/help/msys2/)将镜像源改成优先使用清华源，注意是**文件开头添加**。

1. 先更新软件源和软件

```bash
pacman -Syu
```

2. 安装如下内容

```bash
pacman -S mingw-w64-x86_64-gcc
pacman -S mingw-w64-x86_64-make
pacman -S mingw-w64-x86_64-libtool
pacman -S autoconf
pacman -S automake
pacman -S mingw-w64-x86_64-python3
pacman -S make
```

3. 跳转到解压后的GMP库的根目录，并进行动态库编译。

这一部分的命令需要执行相当长的时间，电脑约运行了约$6$个小时。
```
 cd gmp-6.2.1/
 ./configure --disable-static --enable-shared
make
make check
make install
```

执行完这些命令看到这个就可以了。

![](p3.png)

# 正式使用GMP库

如果直接使用命令行进行编译，那么编译命令需要添加多一个参数，如下：

```
g++ main.cpp -lgmp
```

## CodeBlocks使用

在Codeblocks中的设置——编译器——全局编译器设置——可执行工具链切换成msys2中的MinGW，如图

![](p4.png)

然后再在连接器设置这里添加一个参数-lgmp即可。

![](p5.png)


## Clion使用

同样也需要先在Clion切换成msys2中的MinGW，如图

![](p6.png)

如果发现这个红色警告Not Found，那么将`\msys64\mingw64`下的`include`
文件夹整个复制到`\msys64\mingw64\x86_64-w64-mingw32`下。


创建一个新的项目后，需要在`CMakeLists.txt`中添加如下代码。

```
target_link_libraries([Project-Name] D:\\\\msys64\\\\mingw64\\\\bin\\\\libgmp-10.dll)
```

其中`[Project-Name]`是项目的名称。

# 示例代码执行

```C++
# include <gmpxx.h>
int main(){
    mpz_t a,b;
    mpz_init_set_str(a,"1000000007",10);
    printf("1000000007 is prime? %d\n",mpz_probab_prime_p(a,50) > 0);
    mpz_set_str(a,"10000000007",10);
    printf("10000000007 is prime? %d\n",mpz_probab_prime_p(a,50) > 0);
    int n=199,m=200;
    //计算并输出199!和200!,199!+200!。
    mpz_set_si(a,1);
    mpz_init_set_si(b,1);
    for(int i=1;i<=n;i++)
        mpz_mul_si(a,a,i);
    for(int i=1;i<=m;i++)
        mpz_mul_si(b,b,i);
    gmp_printf("%d!= %Zd\n",n,a);
    gmp_printf("%d!= %Zd\n",m,b);
    mpz_add(a,a,b);
    gmp_printf("199!+200!= %Zd\n",a);
}
```

1. CodeBlocks执行结果

![](p7.png)

2. Clion执行结果

![](p8.png)


另附：GMP库的[文档](https://gmplib.org/gmp-man-6.2.1.pdf)。

相关参考：[[1]](http://www.javashuo.com/article/p-yhoxagck-ns.html)