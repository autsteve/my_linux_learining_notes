# Linux系统学习笔记
&emsp;&emsp;新装了deepin v23系统,结果磁盘没设置好，玩崩了，百度半天修复不了，看看韩顺平老师的Linux操作课程，做做笔记(只记录对自己有用的)。
&emsp;&emsp;[B站网址](https://www.bilibili.com/video/BV1Sv411r7vd/?spm_id_from=333.999.0.0)

## 基础篇·Linux系统结构抽象
&emsp;&emsp;Linux系统可以抽象为三个层次，顶层为用户进程，中间层为系统内核，底层为硬件设备。
> 用户进程
> `图形用户界面` `服务器` `命令行`  

> Linux内核
> `系统调用` `进程管理` `内存管理` `设备驱动程序` 

> 硬件层
> `CPU(中央处理器)` `RAM(内存)` `磁盘` `网络端口`

## 基础篇·Linux目录结构

* **基本介绍**

> Linux文件系统采用级层式的树状目录结构.结构中的最上层是根目录```/```,根目录下是系统创建的其他目录。

&emsp;&emsp;打开deepin-V23系统，键盘输入`ctrl alt t`进入终端，输入如下命令，就可以查看根目录下的子目录。
```bash
ls -l / 
```
```
lrwxrwxrwx   1 root root     7 11月  7 13:32 bin -> usr/bin
drwx------   6 root root  4096 11月 21 22:00 boot
drwxr-xr-x  19 root root  4520 11月 23 14:56 dev
drwxr-xr-x 123 root root 12288 11月 23 14:56 etc
drwxr-xr-x   4 root root  4096 11月 21 22:00 home
lrwxrwxrwx   1 root root     7 11月  7 13:32 lib -> usr/lib
lrwxrwxrwx   1 root root     9 11月  7 13:32 lib32 -> usr/lib32
lrwxrwxrwx   1 root root     9 11月  7 13:32 lib64 -> usr/lib64
lrwxrwxrwx   1 root root    10 11月  7 13:32 libx32 -> usr/libx32
drwx------   2 root root 16384 11月 21 21:55 lost+found
drwxr-xr-x   5 root root  4096 11月 21 22:00 media
drwxr-xr-x   2 root root  4096 11月  7 13:32 mnt
drwxr-xr-x   6 root root  4096 11月 21 23:28 opt
dr-xr-xr-x 406 root root     0 11月 23 10:54 proc
drwx------  14 root root  4096 11月 22 21:40 root
drwxr-xr-x  31 root root   860 11月 23 14:56 run
lrwxrwxrwx   1 root root     8 11月  7 13:32 sbin -> usr/sbin
drwxr-xr-x   2 root root  4096 11月  7 13:32 srv
dr-xr-xr-x  13 root root     0 11月 23 10:54 sys
drwxrwxrwt  20 root root  4096 11月 23 20:34 tmp
drwxr-xr-x  15 root root  4096 10月 11 14:38 usr
drwxr-xr-x  12 root root  4096 11月 21 22:01 var
```
|目录名称|  目录内容简介 |
|:--:|:--|
| / |  根目录|
|/boot|启动 Linux 时使用的一些核心文件，包括一些连接文件以及镜像文件|
|/usr|usr 是 unix shared resources(共享资源) 的缩写，这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于 windows 下的 program files 目录|
|/bin|bin 是 Binaries (二进制文件) 的缩写, 存放着最经常使用的命令，在deepin系统中，bin是/usr/bin的软链接|
|/lib|ib 是 Library(库) 的缩写,包含目标文件(object files)与库，在deepin系统中，/lib是/usr/lib的软链接|
|/lib32|包含32位的目标文件和库，在deepin系统中，/lib是/usr/lib32的软链接|
|/lib64|包含64位的目标文件和库，在deepin系统中，/lib是/usr/lib64的软链接|
|/libx32|libx32是面向x32 ABI的目标文件和库。x32 ABI使用着32位地址空间，但是可以使用一些x86-64的特性.在deepin系统中，/lib是/usr/libx32的软链接|
|/sbin|s 就是 Super User 的意思，是 Superuser Binaries (超级用户的二进制文件) 的缩写，这里存放的是系统管理员使用的系统管理程序，deepin系统中sbin时usr/sbin的软链接|
|/etc|etc 是 Etcetera(等等) 的缩写,这个目录用来存放所有的系统管理所需要的配置文件和子目录|
|/root|系统管理员，也称作超级权限者的用户主目录|
|/home|用户主目录，在 Linux 系统中每新建一个用户，默认在/home下新建一个以用户为名的子目录|
|/dev| dev是Device(设备) 的缩写, 该目录下存放的是 Linux 的外部设备，在 Linux 中访问设备的方式和访问文件的方式是相同的|
|/media|Linux系统识别设备(如U盘、光驱)后将设备挂载到/media目录下进行处理|
|/mnt|用于临时挂载其他文件系统，可以将外部存储挂载在/mnt上，并进入该目录查看相关内容|
|/opt|opt 是 optional(可选) 的缩写，默认为空目录，ORACLE数据库等软件可以安装在/opt下|
|/proc|**不建议修改** proc 是 Processes(进程) 的缩写虚拟目录，是系统内存映射，访问该目录可以获取系统信息|
|srv|**不建议修改** 该目录存放一些服务启动之后需要提取的数据|
|sys|**不建议修改** 安装文件系统 sysfs 。sysfs 文件系统集成了下面3种文件系统的信息：针对进程信息的 proc 文件系统、针对设备的 devfs 文件系统以及针对伪终端的 devpts 文件系统。该文件系统是内核设备树的一个直观反映。当一个内核对象被创建的时候，对应的文件和目录也在内核对象子系统中被创建|
|/var|var 是 variable(变量) 的缩写，这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件|
|/run|是一个临时文件系统，存储系统启动以来的信息。当系统重启时，这个目录下的文件应该被删掉或清除。如果你的系统上有 /var/run 目录，应该让它指向 run|
|/lost+found|一般情况下为空目录，当系统非法关机后，存放相关文件|

## 实操篇·Linux网络入门指令
* **查看主机`ip`地址，`inet`为本机`ip`地址，`inet6`为`ipv6`地址** 
```bash
ip addr  
ifconfig  #windows系统使用ipconfig 
```
* **测试主机网络连接情况，键入`ctrl  C`终止该进程**
```shell
ping www.baidu.com # 测试与百度的连接情况
ping 113.96.140.93 # 测试与ip地址113.96.140.93的连接情况
```

* **查看主机名**  
```bash
hostname
```

* **修改`/etc/hostname`文件可以更改主机名**
```bash
source /etc/hostname # 更改主机名后使用此命令生效
```
* **设置host映射**

> 在/etc/host配置文件末尾填写 `113.96.140.93  bbs.nga.cn`，以后在浏览器上填写`bbs.nga.com`会自动链接到ip地址`113.96.140.93`


## 实操篇·Vim的使用

&emsp;&emsp;vim编辑器是Linux系统自带的编辑器，在终端中输入`vim /hello.c`或`vi hello.c`就可以在根目录下新建`hello.c`文件。

* 一般模式 刚进入vi 时的默认模式。这个模式下能够进行:移动光标、整行的复制粘贴、整行删除等基本操作。  
![一般模式](https://img-blog.csdnimg.cn/b20951efc3e940219f23c14919f161fc.png#pic_center)
* 编辑模式 在一般模式下,按`a` `i` `o`均可进入编辑模式。此模式下能够进行:文本的输入、删除。输入`esc`进入一般模式  
![插入模式](https://img-blog.csdnimg.cn/40aba164f3dd49ad9b5aaa9fd6977518.png#pic_center)
* 命令行模式(末行模式) 在一般指令模式下,按“:”“/” “?” 均可进入命令行模式，在命令行模式下，键盘输入会出现在文件末尾，因此也称为末行模式。输入```esc```进入正常模式  
![命令行模式](https://img-blog.csdnimg.cn/48751f0a08ae4f4b852bae4acf35fc89.png#pic_center)
### vim快捷键
* **一般模式**

> 拷贝当前行 `yy`
> 拷贝当前行向下的5行 ```5yy```
> 粘贴```p```
  
   
> 删除当前行 `dd`
> 删除当前行向下的5行 `5dd`

> 在文件查找某个单词，如`is`  键入`/is` `enter`确认查找 按`n`查找下一个

> 进入文件正数第一行 `gg`

> 进入文件倒数第一行 `G`

> 进入文件某一行,输入行号和G，如 ```20 G```

> 撤销上一步输入 ```u```

> 复原上一步输入 ```ctrl r```

* **命令行模式**
>  设置行号
>  ```bash
>  set nu
> ```
> 取消设置行号
> ```bash
> set nonu
> ```
> 设置缩进为4空格
> ```bash
> set tabstop=4
>```
* **vim快捷键示意图**
![vim快捷键示意图](https://img-blog.csdnimg.cn/b48a711d999a43be83e24b2a3f49ac31.gif#pic_center)
## 实操篇·关机重启
在关闭或者重启计算机之前，最好把内存数据同步到磁盘，为此，需要在终端输入`sync`命令，一般来说，系统在重启或关机之前会自动执行`sync`指令，但为保万全，还是执行一下。
```bash
sync
```
* **关机命令**
```bash
init 0  # 设置运行级别为0,即关机  

shutdown # 1分钟后关机

shutdown -h now # 立刻关机

shutdown -h 10   # 10分钟后关机

shutdown -r now # 立刻重启计算机

halt # 关机
```
* **重启命令**
```bash
reboot # 重启
```
## 实操篇·登录注销
```bash
useradd hotel # 增加用户hotel,默认该用户的目录在/home/hotel下

useradd -d # 指定目录 用户名

passwd hotel # 修改用户hotel的密码

pwd #显示当前用户所在目录

userdel hotel #用root权限操作,删除用户hotel,但/home/hotel还存在

userdel -r hotel #用户权限操作，彻底删除用户hotel一切信息
```
## 实操篇·用户管理
* **查询用户信息**

```bash
id 用户名 #查询用户名信息

id root #查询root信息
```
```
用户id=0(root) 组id=0(root) 组=0(root)
```
* **切换用户信息**

&emsp;&emsp;在操作Linux时，如果当前用户权限不够，可以通过su -指令，切换到高权限用户，比如root
```bash
su root # 切换到root
sudo #临时切换为高级权限
```
>  从权限高的用户切换到权限低的用户，不需要输入密码，反之需要。
>  当需要返回原来用户时，使用```exit/logout```指令

* **查询当前用户信息** 
```bash
whoami
```
###  用户组

> 用户组类似于角色，系统可以对有共性/权限的多个用户进行统一管理。  

* **新增用户组**
```bash
groupadd 组名
```
*  **删除用户组**
```bash
groupdel 组名
```
*  **增加用户，并添加进组**
```bash
useradd -g 组名 用户名
```
*  **修改用户的组**
```bash
usermod -g 组名 用户名
```

### 用户组相关文件

* `/etc/passwd`
> 用户(user)的配置文件，记录用户信息,包括 `用户名:口令:用户标识号:组标识号:注释性描述:主目录:登录shell`

* `/etc/shadow`
> 口令配置文件，包括`登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志`

* `/etc/group`
> 组配置文件，包括 `组名:口令:组标识号:组内用户列表`

## 实操·常用shell指令
### 运行级别
* **运行级别说明**  
> 
> 0  关机  
> 1  单用户(找回丢失密码)  
> 2  多用户状态(无网络服务)  
> 3  多用户状态(有网络服务)  
> 4  系统未使用保留给用户  
> 5  图形界面  
> 6  系统重启  

&emsp;&emsp;Linux系统常用运行级别是 3 和 5 ，通过```init```可以切换运行级别

```bash
init 0 # 关机
init 3 # 进入多用户状态(有网络服务)
init 5 # 进入图形界面
systemctl get-default # 查看当前运行级别
systemctl set-default multi-user.target #设置运行级别为多用户状态(无网络服务)，以后开机自动进入多用户状态(无网络服务)
systemctl set-defatlt graphic.target #设置运行级别为图形界面，以后开机自动进入图形界面
```
#### 如何找回root密码？ 

* 启动系统，进入开机界面，按`e`进入编辑界面

* 使用键盘 $\quad\uparrow\quad\downarrow\quad$键移动光标，找到以`Linux16`开头的行，在最后输入`init = /bin/sh`

* `ctrl x`进入单用户模式

* 输入指令`mount -o remount,rw /`, 按`enter`确认

* 输入`passwd`,键入`Enter`,输入密码，按`Enter`确认,重新输入密码，按`Enter`确认。

* 屏幕显示`passwd ...`,修改成功。

* 输入`touch /.autorelabel`,按`enter`确认

* 输入`exit /sbin/init`, 按`enter`确认, 系统会自动修改密码，完成后自动重启，新密码生效。

### 帮助指令 
* help 获得shell内置指令的帮助信息
```bash
help cd #获得内置指令cd的帮助信息
```
* man 获得帮助信息,按`q`退出
```bash
man ls  #查询指令ls的用法和参数
```

### 文件目录类指令
* file(查看文件格式)
```bash
file 1.txt # 查看1.txt的内容
```
```
1.txt: UTF-8 Unicode text
```
* diff (对比文件区别)
```bash
diff file1 file2 # 对比文件 file1 和 file2之间的区别
```

* pwd (显示当前目录的绝对路径)  
```bash
pwd
```
* ls (显示当前目录文件和目录， 参数 -l 代表以列表形式展现，参数 -a 代表显示所有目录和文件)
```bash
ls 
```
* cd (移动到某目录下)
```bash
cd .. #回到当前目录的上一级目录
cd /root #通过绝对路径进入root文件夹
cd ../../root #通过相对路径进入root文件夹
cd /home/tom/Desktop # 移动到用户Tom的桌面
```

* mkdir (创建目录 参数 -p 创建多级目录)
```bash
mkdir /home/dog #在home目录下创建dog目录
mkdir -p /home/animal/dog #在home目录下创建animal目录，在animal目录下创建dog目录
```
* rmdir (删除空目录 )
```bash
rmdir /home/dog #删除home目录下的dog目录
```
* rm  (删除目录或文件，-r 全部删除 -f 强制删除)
```bash
rm /home/user/Desktop/a.txt #删除用户桌面的a.txt文件
rm -rf /home/user/Desktop/learn #强制删除用户桌面的learn文件夹及其子文件
```
* touch (创建空文件，并更新文件状态)
```bash
touch /hello.c #在根目录下创建hello.c文件
```
* cp (拷贝指令) 拷贝文件到指定目录
```bash
cp /home/hello.txt /home/bbb # 将home目录下的hello.txt文件复制到 /home/bbb目录下
cp -r /home/bbb /home/aaa # 将bbb及bbb下的所有文件及目录拷贝到/home/aaa目录下 
\cp -r /home/bbb /opt # 将bbb及bbb下的所有文件及目录覆盖拷贝到/opt下
```

* mv (移动文件或目录 | 重命名文件或目录)
```bash
mv oldfilename newfilename # 给文件改名
mv /temp/movefile /tagetfolder # 移动文件 
```

* cat (查看文件内容 -n 显示行号)
```bash
cat /hello.c # 显示根目录下的hello.c中的内容
```
![hello.c](https://img-blog.csdnimg.cn/ff5da5fcac52478388229f329ca02da2.png#pic_center)
&emsp;&emsp;  `cat`只能浏览文件，而不能修改文件，面对一些大文件为了浏览方便，一般利`| more`命令浏览。
&emsp;&emsp; `|`管道命令`more`基于vi编辑器的文本过滤器，以全屏幕形式按页显示文本文件内容。
```bash
cat /1.txt | more # 在终端展示1.txt的内容
```
![](https://img-blog.csdnimg.cn/0624626f15b44e09b5f28c304e5173e5.png#pic_center)
* more  
>  按`space`向下翻一页  
> 按`enter`向下翻一行  
> 按`q`退出  
> 按`ctrl B`返回上一屏  
> 按`ctrl F`向下滚动一屏幕  
> 按`=`输出当前行号  
> 按`:f`输出文件名和当前行号  

* less (分屏查看，支持各种显示终端，根据现实需要加载内容，对于显示文件具有较高的效率)
> 按`space`向下翻一页  
> 按 `PgDn`向下翻一行  
> 按`PgUp`向上翻一行  
> 按`/str`向下搜索字符串，  按`n`向下查,按`N`向上查 
> 按`？str`向上搜索字符串， 按`N`向上查, 按`n`向上查
> 按`q`输出当前行号  

* echo (输出内容到控制台)
```bash
echo $HOSTNAME #在终端输出主机名称
echo "hello world！" # 在终端输出hello world! 
```
* head (显示文件开头部分，默认显示文件前10行)
```bash
head /1.txt
```
![1.txt](https://img-blog.csdnimg.cn/89c816bd2be640ba8859408b3344775f.png#pic_center)
```bash
head -n 6 # 显示文件前6行
```
![1.txt](https://img-blog.csdnimg.cn/4c86983e09804b6f8db561225f6ba1ff.png#pic_center)
* tail (显示文件结尾部分，默认显示文件最后10行)
```bash
tail /1.txt

tail -n 6 /1.txt # 显示文件最后6行

tail -f /1.txt #实时跟踪文件内容
```
* ```>```输出重定向(覆盖写入)   
* ```>>```在文件中追加内容
```bash
ls -l > a.txt # 将本目录内容输入a.txt(覆盖写入)
ls -al >> a.txt # 将本目录内容追加到a.txt的末尾
cat a.txt > b.txt # 将a.txt的内容覆盖到b.txt中
echo "内容" >> b.txt # 将内容写入b.txt
```
* ln (软链接也称为符号链接，类似于Windows的快捷方式，主要存放链接其他文件的路径)
```bash
ln -s /root myroot # 创造一个软链接，在当前目录链接到/root目录，文件名叫myroot
rm -rf myroot #删除软链接myroot
```
* history (查看已经执行过的历史命令)

```bash
history #显示已执行过的命令
history 10 # 显示最近的10条指令
history 
!5 #执行第5条指令
```

### 时间日期类指令 
* date (显示当前日期  参数 ```+%Y```显示当前年份 ```+%m```显示当前月份 ```+%d```显示当前是哪一天)
```bash
date 
2022年 11月 23日 星期三 18:39:50 CST

date +%Y-%m-%d-%H:%M:%S 
2022-11-23-18:40:25

```
* **cal (查看日历) deepin系统没有cal命令**

### 搜索查找类指令

* find (从指定目录向下递归地遍历各个子目录，将满足条件地文件或者目录显示在终端)
```bash
find /home -name hello.txt # 在home文件夹下寻找名为hello.txt的文件
find /opt -user nobody #在/opt文件夹下寻找用户nobody的所有文件
find /-size +200M # 寻找系统中大于200MB的文件(+n 代表大于n -代表小于n ,单位有k,指kB,M,指MB,G,指GB)
```

* **updatedb (更新系统数据库)deepin系统没有该指令**
* **locate (快速定位文件路径) deepin系统没有该指令**

* which (查看命令所在目录)
```bash
which ls # 查看ls在哪个目录
/usr/bin/ls
```

* grep (过滤查找)
```bash
cat a.txt | grep "deepin" >> b.txt # 在a.txt中查找包含"deepin"的行，并定向输入到b.txt 
cat a.txt | grep "deepin" -n # 在a.txt中寻找包含“deepin”的行，在终端中标注行号并显示相关内容
grep -n "deepin" a.txt # a.txt中寻找包含“deepin”的行，在终端中标注行号并显示相关内容
```

### 压缩解压类命令 

* **gzip/gunzip (gzip压缩文件为.gz模式，gunzip解压.gz文件)**

* **zip/unzip (zip压缩文件为.zip模式，unzip解压.zip文件)**
```bash
unzip ax.zip -d /opt # 将ax.zip文件解压缩到/opt文件夹下
```
* tar (打包指令，将大文件打包为.tar.gz文件)
```bash
tar -c #产生打包文件
tar -v #显示详细信息
tar -f #指定压缩文件名
tar -z #打包同时压缩
tar -x #解包tar.gz文件

tar -zcvf pc.tar.gz /home/Desktop/a.txt /home/Desktop/b.txt #将/home/Desktop 下的a.txt和b.txt压缩为pc.tar.gz文件

tar -zxvf pc.tar.gz -C /opt/tmp # 将pc.tar.gz 文件解压到/opt/tmp文件夹
```
## 实操篇·权限管理 

&emsp;&emsp;Linux系统每建立一个用户，或者同时建立一个组，或者为用户指定一个组。  
&emsp;&emsp;Linux系统中的文件都有以下3个概念：
> * 所有者
> * 所在组
> * 其他组

### 文件/目录所有者
&emsp;&emsp;文件/目录创建者自然成为该文件的所有者。  

* 查看文件所有者
```bash
ls -ahl # 查看当前目录下文件所有者
```
![a](https://img-blog.csdnimg.cn/90ccbda3741e48288726306f5a9a9d28.png#pic_center)
&emsp;&emsp;如图所示，apple.txt文件的所有者是rock，其所在组是root

* 修改文件所有者
```bash
chown  rock apple.txt  # 将apple.txt的所有者改为rock
```
### 组的创建
```bash
groupadd allan # 创建allan组

useradd -g allan fox # 创建用户fox,并将用户fox指定为allan组的成员
```
### 文件/目录所在组
* 查看文件/目录所在组
```bash
ls -lha # 查看当前目录下文件所有者
```
![b](https://img-blog.csdnimg.cn/ce42133aad114c2d97dcf1ace267fdf4.png#pic_center)
```bash
chgrp rock apple.txt # 将apple.txt文件所在组更改为rock,该命令可能需要高级权限
ls -alh # 查看文件信息
```
![1](https://img-blog.csdnimg.cn/d17c6d864302422284ec213f392036ca.png#pic_center)
### 其他组 
&emsp;&emsp;对于Linux文件来说，除了文件的所有者和文件所在组的用户以外，系统其他用户都是文件的其他组。  

* 改变用户所在组
```bash
usermod -g root rock # 将用户rock添加到root组中
usermod -d /home/xyz rock # 将用户rock登录的初始界面放在/home/xyz中，该用户需要具有进入该目录的权限
```
### 权限管理 
&emsp;&emsp;Linux某个目录中，在终端中输入```ls -l```指令，显示如下：  

![在这里插入图片描述](https://img-blog.csdnimg.cn/0c2b8247d5d443b39e0332ae8504b9ab.png#pic_center)

&emsp;&emsp;以上数据分别代表 `权限(文件属性) 文件个数(普通文件：硬链接数 目录：子目录数) 文件所有者 文件所在组  文件大小 最后修改时间 文件名`

&emsp;&emsp;权限(文件属性)即`-rw-r--r--`,从0到9，共包含10位，以下为具体说明：  
* 0 确定文件类型
> d 目录  
> \- 文件  
> l 链接  
> c 字符设备，如鼠标、键盘  
> b 块设备，如硬盘 

* 123 文件所有者拥有的权限
> r 读  
> w 写  
> x 执行  
> \- 无对应权限  

* 456 文件所在组成员拥有的权限
> r 读  
> w 写  
> x 执行  
> \- 无对应权限  

* 789 其他组成员拥有的权限
> r 读  
> w 写  
> x 执行  
> \- 无对应权限  

#### rwx权限详解 
* rwx作用到文件
> 1.[r] 代表可读(read)，可以读取、查看。  
> 2.[w] 代表可写(write),可以修改文件内容，但不代表可以删除该文件，可以删除文件的前提是对该文件所在目录有可写权限，才能删除该文件。  
> 3.[x] 代表可执行(execute)，可以执行文件。
  
* rwx作用到目录
> 1.[r] 代表可读(read)，可以读取,```ls```查看目录内容。  
> 2.[w] 代表可写(write),可以修改目录，对目录内容进行创建、删除、重命名。  
> 3.[x] 代表可执行(execute)，可以进入该目录。  

#### 修改权限
* chmod (修改文件和目录的权限)
* u = 文件所有者 g = 文件所在组成员 o = 其他组成员 a = 所有组成员  

```
权限可以用数字代表：
x = 1
w = 2
wx = 2 + 1 = 3
r = 4 
rx = 4 + 1 = 5
rw = 4 + 2 = 6
rwx = 4 + 2 + 1 = 7
```
```bash
chmod u=rwx,g=rx,o=x 文件名/目录名 # 给文件所有者读、写、执行权限，给组成员读、执行权限，给其他组执行权限。  
chmod o+w 文件名/目录名 # 给其他组成员赋予写权限  
chmod a-x 文件名/目录名 # 所有组成员取消执行权限
chmod -R 777 文件名/目录名 # 强制执行：文件所有者：赋予全部权限 文件所在组成员：赋予全部权限 其他组成员：赋予全部权限
```
#### 修改文件所有者 
* chown newowner         (更改文件所有者)
* chown newoner:newgroup (更改文件所有者和文件所在组)
* -R 如果是目录，则使其下所有子文件或目录递归生效

```bash
chown rock a.txt # 将a.txt的所有者改为rock
chown rock:root a.txt #将a.txt的所有者改为rock,文件所在组改为root
```
#### 修改文件/目录所在组 
```bash
chgrp newgroup 文件/目录 # 修改文件/目录所在组(不包括目录下子目录和子文件)
chgrp -R newgroup 文件/目录 # 修改文件/目录所在组(包括目录下子目录和子文件)
```
## 实操篇·任务调度

* 概述

> 任务调度：系统在某个时间执行特定的命令或程序

> 任务调度分类：1.系统工作：有些重要工作任务必须周而复始地执行，如病毒扫描等。2.个别用户工作：个别用户可能希望执行某些程序，比如备份mysql数据库备份。

* crontab 
> -e 编辑crontab定时任务  
> -l 查询crontab任务  
> -r 删除当前用户所有的crontab任务  
> -i 在删除当前用户的crontab任务之前给予提示

```
参数说明
 第一个* 一小时中的第几分钟 (0-29)
 第二个* 一天中的第几小时 (0-23)
 第三个* 一个月中的第几天（1-31）
 第四个* 一年中的第几月(1-12)
 第五个* 一周中的星期几(1-7)

特殊符号说明
 * 代表任何时间，第一个*代表一小时中每分钟都执行一次
 , 代表不连续的时间，比如0 8,12,16 *,就代表每天的8：00，12：00，16:00 都执行一次命令
 - 代表连续的时间范围，比如 0 5 * * * 1-6 就代表 每周的周一到周六的5：00执行一次命令
 */n 代表每隔多久执行一次，比如*/10 * * * * 就代表每隔10分钟执行一次命令
```
```bash
crontab -e # 编辑crontab定时任务
*/1**** ls -l /etc/ > /tmp/to.txt # 每小时的第一分钟将/etc目录下的内容覆盖输入到/tmp文件夹的to.txt文件中  
```
* **at (deepin V23 系统没有at命令)**
## 实操篇·分区挂载

* **原理介绍**
> 1. Linux系统只有一个根目录，一个独立且唯一的文件结构，Linux每个分区都是用来组成文件系统的一部分  
> 2. Linux系统采用"载入"的处理方法，整个文件系统中包含了一整套文件和目录。且将分区和目录联系起来，每个磁盘分区的存储空间都被挂载到某个目录下。

* 查看计算机磁盘挂载情况
```bash
lsblk # 查看所有设备挂载情况  
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/b16d14f50f97439db3a771927ea108b1.png#pic_center)
```bash
lsblk -f
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/df8b9e938511403fb904a0f82232cf6b.png#pic_center)


* 硬盘分区

>  采用IDE接口的硬盘叫做IDE和,采用SCSI接口的硬盘叫做SCSI硬盘，采用nvme接口的硬盘叫做nvme硬盘。  

> 对于IDE硬盘，驱动器标识符为"hdx~"  
> 其中,"hd"表明分区所在设备的类型(hd代表IDE)，"x"为盘号(a基本盘，b基本从属盘,c辅助主盘,d辅助从属盘)  
> "~"代表分区，前4个分区用数字1—4表示，是主分区或扩展分区。从5开始是逻辑分区。例如，hda3代表第一个IDE硬盘的第三个主分区或扩展分区，hdb2表示第二块IDE硬盘的第二个主分区或者扩展分区。  

> SCSI硬盘标识符为"sdx~"
> 其中"sd"表明分区所在设备的类型(sd代表SCSI)，"x"为盘号  
> "~"表示分区。

> nvme硬盘，标识为nvme0n1p~,p1分区挂载/boot/efi,p2分区挂载/boot,p3分区挂载根目录/,p4分区为swap,无挂载，p5分区挂载/home

### 如何挂载一块硬盘？

* 添加硬盘(物理安装)

```bash
lsblk # 查看当前主机识别出的硬盘
```

* 硬盘分区

```bash
fdisk /dev/sda
```
显示如下内容

```
Welcome to fdisk (util-linux 2.38).                        
Changes will remain in memory only, until you decide to write them.                  
Be careful before using the write command.
```

键入```m```查看帮助目录
```
GPT
   M   enter protective/hybrid MBR

  Generic
   d   delete a partition
   F   list free unpartitioned space
   l   list known partition types
   n   add a new partition
   p   print the partition table
   t   change a partition type
   v   verify the partition table
   i   print information about a partition

  Misc
   m   print this menu
   x   extra functionality (experts only)

  Script
   I   load disk layout from sfdisk script file
   O   dump disk layout to sfdisk script file

  Save & Exit
   w   write table to disk and exit
   q   quit without saving changes

  Create a new label
   g   create a new empty GPT partition table
   G   create a new empty SGI (IRIX) partition table
   o   create a new empty DOS partition table
   s   create a new empty Sun partition table

```
键入```n```新建分区,提示
```
Partition number (2-128, default 2):  

# 此处应该是我的电脑已经建过一个分区了，因此显示分区可以建2-128个，大概吧
```
键入```2```新建2个分区,提示
```
First sector (1953521664-1953525134, default 1953521664): 
```
键入```enter```或数字确认
```
Last sector, +/-sectors or +/-size{K,M,G,T,P} (1953521664-1953525134, default 1953523711): 
```
键入```enter```或数字确认，提示
```
Created a new partition 2 of type 'Linux filesystem' and of size 1 MiB.
```
键入```w```保存设置。  
键入```q```退出,之前更改作废。
* 格式化磁盘  
```bash
mkfs -t ext4 /dev/sda1 # 格式化磁盘sda1
lsblk -f # 查看是否格式化成功
```
* 挂载/卸载磁盘 
```bash
mount /dev/sda1 /home # 将sda1挂载在/home目录下。
umount /dev/sda1 
```
* 永久挂载
> 修改etc/fstab实现挂载
```bash
vi /etc/fstab
```
```
UUID=d8162e69-5c41-4e25-81a7-d04592f36556   /home     ext4 defaults  0 0   
```
> 执行```mount -a```实现挂载
```bash
mount -a 
```
### 实操篇·进程管理

* Linux系统中，每个执行的程序都称为1个进程，每一个进程都分配一个ID号(pid进程号)  

* 每个进程都可能以两种方式存在：前台与后台。所谓前台进程就是用户屏幕上可以操作的。后台进程是在系统中执行，但不显示在屏幕上的。  

* 系统服务一般以后台进程方式存在，常驻系统，关机结束。

### 进程管理相关指令

* `ctrl C` 不论是否有输入输出，立即终止当前进程

* `ctrl D` 终止当前终端标准输入，并终止命令

* ps (显示系统执行进程)
```bash
ps -a # 显示终端所有进程信息
ps -u # 以用户格式显示进程信息
ps -x # 显示后台进程运行的参数
ps -ef #以全格式显示当前所有进程

```
![进程](https://img-blog.csdnimg.cn/3f4c7d6b7e434e9db71454b62497fa37.png#pic_center)
`USER`用户 
`PID`进程号 
`%CPU`占用CPU百分比 
`%MEM`占用物理内存百分比 
`VSZ`占用虚拟内存的百分比 
`TTY`终端信息  
`STAT`运行状态 
`START`执行开始时间 
`TIME`进程占用CPU时间 
`COMMAND`进程名，命令名

* kill (终止进程)
* killall 进程名(终止进程及子进程) -9表示强迫进程终止。
```bash
kill 11421 # 终止PID为11421的进程
```
* pstree (以树状图模式展示系统执行进程)
```bash
pstree -u # 显示用户名
pstree -p # 显示进程号
```
* top (显示系统当前状态,每秒更新一次)
```bash
top 
```
## 实操篇·apt软件安装
* `/etc/apt/sources.list`中存放了软件安装服务器地址(大部分服务器地址在美国)
* `APT`通过指令可以完成软件安装、更新、卸载。
```bash
cat /etc/apt/sources.list 
```
```
## Generated by deepin-installer
deb https:#community-packages.deepin.com/beige/ beige main commercial community
#deb-src https:#community-packages.deepin.com/beige/ beige main commercial community
```
* 通过修改`/etc/apt/sources.list`可以更换软件源
```bash
sudo apt-get update #更新软件源
sudo apt-get install package #安装包
sudo apt-get remove package #卸载包

sudo apt-cache search package #搜索包
sudo apt-cache show package #获取包的相关信息，说明、大小、版本等

sudo apt-get install package --reinstall #重新安装包 
sudo apt-get -f install package #修复安装
sudo apt-get remove package --purge #删除包，包括配置文件
sudo apt-get build-dep package #安装相关编译环境

sudo apt-get upgrade #更新已安装的包
sudo apt-get dist-upgrade #升级系统
sudo apt-cache depends package #了解使用包依赖哪些包
sudo apt-cache rdepends package #查看该包被哪些包依赖
sudo apt-get source package #下载包源代码
```

