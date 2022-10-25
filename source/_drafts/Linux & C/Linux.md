---
title: Linux
tags:
---

/bin：
bin 是 Binaries (二进制文件) 的缩写, 这个目录存放着最经常使用的命令。

/boot：
这里存放的是启动 Linux 时使用的一些核心文件，包括一些连接文件以及镜像文件。

/dev ：
dev 是 Device(设备) 的缩写, 该目录下存放的是 Linux 的外部设备，在 Linux 中访问设备的方式和访问文件的方式是相同的。

/etc：
etc 是 Etcetera(等等) 的缩写,这个目录用来存放所有的系统管理所需要的配置文件和子目录。

/home：
用户的主目录，在 Linux 中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的，如上图中的 alice、bob 和 eve。

/lib：
lib 是 Library(库) 的缩写这个目录里存放着系统最基本的动态连接共享库，其作用类似于 Windows 里的 DLL 文件。几乎所有的应用程序都需要用到这些共享库。

/lost+found：
这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件。

/media：
linux 系统会自动识别一些设备，例如U盘、光驱等等，当识别后，Linux 会把识别的设备挂载到这个目录下。

/mnt：
系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在 /mnt/ 上，然后进入该目录就可以查看光驱里的内容了。

/opt：
opt 是 optional(可选) 的缩写，这是给主机额外安装软件所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认是空的。

/proc：
proc 是 Processes(进程) 的缩写，/proc 是一种伪文件系统（也即虚拟文件系统），存储的是当前内核运行状态的一系列特殊文件，这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。
这个目录的内容不在硬盘上而是在内存里，我们也可以直接修改里面的某些文件，比如可以通过下面的命令来屏蔽主机的ping命令，使别人无法ping你的机器：

`echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all`

/root：
该目录为系统管理员，也称作超级权限者的用户主目录。

/sbin：
s 就是 Super User 的意思，是 Superuser Binaries (超级用户的二进制文件) 的缩写，这里存放的是系统管理员使用的系统管理程序。

/selinux：
 这个目录是 Redhat/CentOS 所特有的目录，Selinux 是一个安全机制，类似于 windows 的防火墙，但是这套机制比较复杂，这个目录就是存放selinux相关的文件的。

/srv：
 该目录存放一些服务启动之后需要提取的数据。

/sys：

这是 Linux2.6 内核的一个很大的变化。该目录下安装了 2.6 内核中新出现的一个文件系统 sysfs 。

sysfs 文件系统集成了下面3种文件系统的信息：针对进程信息的 proc 文件系统、针对设备的 devfs 文件系统以及针对伪终端的 devpts 文件系统。

该文件系统是内核设备树的一个直观反映。

当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中被创建。

/tmp：
tmp 是 temporary(临时) 的缩写这个目录是用来存放一些临时文件的。

/usr：
 usr 是 unix shared resources(共享资源) 的缩写，这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于 windows 下的 program files 目录。

/usr/bin：
系统用户使用的应用程序。

/usr/sbin：
超级用户使用的比较高级的管理程序和系统守护程序。

/usr/src：
内核源代码默认的放置目录。

/var：
var 是 variable(变量) 的缩写，这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件。

/run：
是一个临时文件系统，存储系统启动以来的信息。当系统重启时，这个目录下的文件应该被删掉或清除。如果你的系统上有 /var/run 目录，应该让它指向 run。

终端利用ssh登录远程服务器

安装ssh：

yum install ssh
启动ssh：

service sshd start
登录远程服务器：

ssh -p 50022 my@127.0.0.1
输入密码：
my@127.0.0.1:
-p 后面是端口

my 是服务器用户名

127.0.0.1 是服务器 ip

回车输入密码即可登录

在 Linux 中我们可以使用 ll 或者 `ls –l` 命令来显示一个文件的属性以及文件所属的用户和组.

文件权限相关：https://www.runoob.com/linux/linux-file-attr-permission.html
（涉及chown,chgrp,chmod命令）。chmod命令用的最多。
`chmod 666 xxx.txt`的意思是将文件xxx.txt改成所有人都可读可写。


文件操作相关：https://www.runoob.com/linux/linux-file-content-manage.html
（涉及ls,cd,pwd,mkdir,rmdir,cp,rm,mv等处理目录命令，cat,tac,nl,more,less,head,tail等文件内容查看命令）。

可以使用 man [命令]来查看各个命令的使用文档，如 ：man cp。

磁盘管理相关：https://www.runoob.com/linux/linux-filesystem.html
（涉及命令df,du,fdisk）

vim相关：https://www.runoob.com/linux/linux-vim.html

三种模式：命令模式，输入模式，底线命令模式。

模式切换表：
|||
|-|-|
|命令->输入|i|
|命令->底线命令|:|
|输入->命令|esc|
|底线命令->命令|换行结束命令|
|保存|:w|
|退出|:q|