# linux笔记

## 购买阿里云

> 买完阿里云服务器后

服务器是远程的linux系统。

1. 需要开通安全组设置；端口映射。

   ![image-20210309222644006](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210309222644006.png)

   一般需要开放的端口：

   - 8080：tomcat
   - 3306：MySQL服务默认端口
   - 39000-40000：FTP被动模式
   - 20：FTP主动模式数据端口
   - 22：SSH远程服务
   - 21：FTP协议默认的端口
   - 8888：宝塔面板默认端口
   - 80：网站默认端口

2. 修改实例名称何密码。

3. ![image-20210309222730847](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210309222730847.png)

4. 获取公网ip

**第一次修改要重启。**



> 用xshell远程连接

![image-20210309223042094](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210309223042094.png)

> 项目的部署

1. 傻瓜式（宝塔面板）

   ![image-20210309223503074](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210309223503074.png)

   安装教程：https://www.bt.cn/bbs/thread-19376-1-1.html

   连接linux后执行下列代码，安装宝塔面板，一直等待安装完成

   ```xml
   yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
   ```

   下载完成后得到一个地址：宝塔面板的管理地址。

   ![image-20210309224203209](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210309224203209.png)

   访问网址，输入账号密码即可：

   ![image-20210309231914861](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210309231914861.png)

   安装相应的环境：

   放入网站进行访问：

   比如tomcat就放到web apps目录下

**网站如果访问测试失败，一定是防火墙的问题（linux服务器，阿里云安全组面板）**

war直接丢到tomcat即可。

jar直接用java -jar 执行即可访问。

1. 命令式（原生的）

   学习linux】





## 学习路线

JavaSE、mysql、前端（html、Css、Js）、Java Web、SSM框架、Springboot、SpringCloud~、（MP Git）

Linux操作系统**(一切皆文件：文件就：读、写（权限）)**

消息队列(Kafka、RabbitMQ、RockeetMQ)、缓存(Redis)、搜索引擎、集群分布式！



## 为什么学习linux

![image-20210310100517566](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210310100517566.png)



## 常用命令

> 开机

开机启动很多程序，在win我们叫‘服务Service’，而Linux里面我们称之为“守护进程Daemon”

**不管是重启系统还是关闭系统，首先要运行 sync 命令，把内存中的数据写到磁盘中。**

> 关机

```bash
sync # 将数据由内存同步到硬盘中

shutdown # 关机指令

shutdown -h 10 #计算机10分钟后关机

shutdown -h now #计算机1立刻关机

shutdown -h 20：25 #计算机在今天20：25关机

shutdown -r now #系统立刻重启

shutdown -r +10 #系统10分钟后重启

reboot #重启  等同于 shutdown -r now

halt  #关闭系统，等同于shutdown -h now  和 poweroff
```

```bash
cd （切换目录）
pwd ( 显示目前所在的目录 )
mkdir 文件名（创建新目录）
```



处理目录的常用命令：

- ls: 列出目录
- cd：切换目录
- pwd：显示目前的目录
- mkdir：创建一个新的目录
- rmdir：删除一个空的目录
- cp: 复制文件或目录
- rm: 移除文件或目录
- mv: 移动文件与目录，或修改文件与目录的名称

**ls查看文件列表**

参数：

- -a ：全部的文件，连同隐藏文件( 开头为 . 的文件) 一起列出来(常用)
- -l ：长数据串列出，包含文件的属性与权限等等数据；(常用)

![image-20210310111459910](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210310111459910.png)

**创建文件**

![image-20210310111810346](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210310111810346.png)

**递归创建文件：**

![image-20210310112004571](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210310112004571.png)

**删除目录**

![image-20210310112430720](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210310112430720.png)

**递归删除同理：rmdir -p 删除的文件**

**拷贝文件**

语法：cp 文件  拷贝的位置

```bash
[root@iZbp1hbo1srus41nnad33sZ /]# ls
bin   dev  home        lib    media  opt   root  sbin  sys  usr  www
boot  etc  install.sh  lib64  mnt    proc  run   srv   tmp  var
[root@iZbp1hbo1srus41nnad33sZ /]# cp install.sh home/xiaozhang   #拷贝文件
cp: overwrite 'home/xiaozhang/install.sh'? y  #是否覆盖
```

> rm ( 移除文件或目录 )

语法：

```
rm [-fir] 文件或目录
```

选项与参数：

- -f ：就是 force 的意思，忽略不存在的文件，不会出现警告信息；
- -i ：互动模式，在删除前会询问使用者是否动作
- -r ：递归删除啊！最常用在目录的删除了！这是非常危险的选项！！！

测试：

```bash
# 将刚刚在 cp 的实例中创建的 install.sh删除掉！
[root@kuangshen home]# rm -i install.sh
rm: remove regular file ‘install.sh’? y
# 如果加上 -i 的选项就会主动询问喔，避免你删除到错误的档名！

# 尽量不要在服务器上使用 rm -rf /
```

> mv  ( 移动文件与目录，或修改名称 )

语法：

```
[root@www ~]# mv [-fiu] source destination
[root@www ~]# mv [options] source1 source2 source3 .... directory
```

选项与参数：

- -f ：force 强制的意思，如果目标文件已经存在，不会询问而直接覆盖；
- -i ：若目标文件 (destination) 已经存在时，就会询问是否覆盖！
- -u ：若目标文件已经存在，且 source 比较新，才会升级 (update)

测试：

```bash
# 复制一个文件到当前目录
[root@kuangshen home]# cp /root/install.sh /home

# 创建一个文件夹 test
[root@kuangshen home]# mkdir test

# 将复制过来的文件移动到我们创建的目录，并查看
[root@kuangshen home]# mv install.sh test
[root@kuangshen home]# ls
test
[root@kuangshen home]# cd test
[root@kuangshen test]# ls
install.sh

# 将文件夹重命名，然后再次查看！
[root@kuangshen test]# cd ..
[root@kuangshen home]# mv test mvtest
[root@kuangshen home]# ls
mvtest
```

> 文件重命名

```bash
[root@iZbp1hbo1srus41nnad33sZ home]# ls
test  test1  xiaozhang
[root@iZbp1hbo1srus41nnad33sZ home]# mv xiaozhang xaiozhang1
[root@iZbp1hbo1srus41nnad33sZ home]# ls
test  test1  xaiozhang1
```

> 基本属性

Linux系统是一种典型的多用户系统，不同的用户处于不同的地位，拥有不同的权限。为了保护系统的安全性，Linux系统对不同的用户访问同一文件（包括目录文件）的权限做了不同的规定。

在Linux中我们可以使用`ll`或者`ls –l`命令来显示一个文件的属性以及文件所属的用户和组，如：

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7JGpeIS4j9q3B4LQhsQkFiauXAQN0qOnVCYvj7Cm1oQbvexVDFqPhUIeTe83BdAHlXCJhGoNabSFKQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

实例中，boot文件的第一个属性用"d"表示。"d"在Linux中代表该文件是一个目录文件。

在Linux中第一个字符代表这个文件是目录、文件或链接文件等等：

- 当为[ **d** ]则是目录
- 当为[ **-** ]则是文件；
- 若是[ **l** ]则表示为链接文档 ( link file )；
- 若是[ **b** ]则表示为装置文件里面的可供储存的接口设备 ( 可随机存取装置 )；
- 若是[ **c** ]则表示为装置文件里面的串行端口设备，例如键盘、鼠标 ( 一次性读取装置 )。

接下来的字符中，以三个为一组，且均为『rwx』 的三个参数的组合。

其中，[ r ]代表可读(read)、[ w ]代表可写(write)、[ x ]代表可执行(execute)。

要注意的是，这三个权限的位置不会改变，如果没有权限，就会出现减号[ - ]而已。

每个文件的属性由左边第一部分的10个字符来确定（如下图）：

![图片](https://mmbiz.qpic.cn/mmbiz_png/uJDAUKrGC7JGpeIS4j9q3B4LQhsQkFiauEybzG2XIdlOMLyO13lMfPKUWRpGJGgyxCAJ9mics9dTZ1qrWDIvleYQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

从左至右用0-9这些数字来表示。

第0位确定文件类型，第1-3位确定属主（该文件的所有者）拥有该文件的权限。第4-6位确定属组（所有者的同组用户）拥有该文件的权限，第7-9位确定其他用户拥有该文件的权限。

其中：

第1、4、7位表示读权限，如果用"r"字符表示，则有读权限，如果用"-"字符表示，则没有读权限；

第2、5、8位表示写权限，如果用"w"字符表示，则有写权限，如果用"-"字符表示没有写权限；

第3、6、9位表示可执行权限，如果用"x"字符表示，则有执行权限，如果用"-"字符表示，则没有执行权限。

对于文件来说，它都有一个特定的所有者，也就是对该文件具有所有权的用户。

同时，在Linux系统中，用户是按组分类的，一个用户属于一个或多个组。

文件所有者以外的用户又可以分为文件所有者的同组用户和其他用户。

因此，Linux系统按文件所有者、文件所有者同组用户和其他用户来规定了不同的文件访问权限。

在以上实例中，boot 文件是一个目录文件，属主和属组都为 root。

> 
> 修改文件属性

**1、chgrp：更改文件属组**

```
chgrp [-R] 属组名 文件名
```

-R：递归更改文件属组，就是在更改某个目录文件的属组时，如果加上-R的参数，那么该目录下的所有文件的属组都会更改。

**2、chown：更改文件属主，也可以同时更改文件属组**

```
chown [–R] 属主名 文件名
chown [-R] 属主名：属组名 文件名
```

**3、chmod：更改文件9个属性（必须要掌握）**

```
chmod [-R] xyz 文件或目录
```

Linux文件属性有两种设置方法，一种是数字，一种是符号。

Linux文件的基本权限就有九个，分别是owner/group/others三种身份各有自己的read/write/execute权限。

先复习一下刚刚上面提到的数据：文件的权限字符为：『-rwxrwxrwx』， 这九个权限是三个三个一组的！其中，我们可以使用数字来代表各个权限，各权限的分数对照表如下：

```
r:4     w:2         x:1
```

每种身份(owner/group/others)各自的三个权限(r/w/x)分数是需要累加的，例如当权限为：[-rwxrwx---] 分数则是：

- owner = rwx = 4+2+1 = 7
- group = rwx = 4+2+1 = 7
- others= --- = 0+0+0 = 0

```
chmod 770 文件名
```

### 文件搜索

#### 文件搜索`find`：在**硬盘**上查找。

```linux
find [搜索范围] [匹配的条件]

#在目录中/etc中通过名字的形式查找文件init
$find /etc -name init

#在根目录下通过大小查找大于204800的文件
$find / -size +204800

#在根目录下通过所有者为xiaozhang的文件
$find / -user xiaozhang

#在/etc目录下查找5分钟内被修改过属性的文件和目录
$find /etc -cmin -5
	-amin 访问时间access
	-cmin 文件属性change
	-mmin 文件内容modify
	
#在/etc目录下查找大于100小于200的文件
$find /etc -size +100 -a -size _200
	-a 类似于and两个条件同时满数。
	-o 类似于or满足任意一个条件即可。

-type  根据文件类型
	f:文件
	d:目录
	l:软连接文件
-inum  根据i节点查找

#查询/etc下查找init文件并显示其详情信息。
$find /etc -name init -exec ls -l {}\;
	
	-exec/ok 命令 {}\;  exec:execute执行
						ok:会询问信息，即是否执行

```

#### 文件搜索`locate`：在文件**资料库**中查找文件

locate:定位

```linux
#locate 文件名

$locate xiaozhang

#忽略大小写查找
$locate -i xiaozhang
updatedb 跟新资源库
```

#### 文件搜索`which`:搜索**命令所在的目录及别名信息**

```linux
$which ls
```

![image-20210514145036114](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210514145036114.png)

#### 文件搜索`whereis`：搜索**命令所在的目录及帮助文档路径(绝对路径)**

```linux
$whereis ls
```

![image-20210514145529563](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210514145529563.png)

#### 内容搜索`grep`：在文件中搜寻字符串匹配的行并输出

```linux
#grep -iv [自定字符串] [文件]
	-i:不区分大小写
	-v:排除指定字串
$grep mysql /root/install.log

#去掉以#开头发行(在Linux中#开头的都是注释)
$grep -v ^# /etc/inittab
```

### 帮助命令

#### 帮助命令：man:获得帮助信息

```linux
man [命令或者怕配置文件]
#查看ls命令的帮助信息
$man ls   1、一般看ls做什么用？ 2、ls中-ld的参数，即/-l。

#查看配置文件services的帮助信息
$man services  1、该配置文件是做什么的？ 2、配置文件的格式
```

**man查看时命令名和配置文件名相同，1表命令  5代表配置文件**

```linux
$man 1 passwd  通过命令查看帮助
$man 5 passwd  通过配置文件查看帮助
```

补充：

​	`whatis`:查看命令信息。

```linux
$whatis ls
```

​		注意：如果whatis不能使用，执行`mandb`。

​	`apropos`查看配置文件信息。

```linux
$apropos services
```

**命令 --help**:查看命令选项。例如：ls --help

#### 帮助命令help：获得shell内置命令的帮助信息

```linux
#help 命令 查看ls命令的帮助信息。
$help ls
```



### 压缩解压

#### 压缩命令：gzip:压缩文件,压缩后的文件格式：.gz

```linux
#gzip [文件]
```

gunzip [ 压缩文件]： 解压缩.gz的压缩文件

gzip -d [ 压缩文件]:   解压缩.gz的压缩文件

```linux
$gunzip abc.gz     解压abc.gz
$gzip -d abc.gz
```

**注意：1、只能压缩文件。	2、且不保留压缩前的文件。**



#### 压缩命令：tar:打包目录：压缩后的文件格式：.tar.gz

```linux
#tar [-zcf] [压缩后的文件名] [目录]
		-c: 打包
		-v: 显示详情信息
		-f: 指定文件名
		-z: 打包同时压缩
$tar -zcf abc.tar.gz abc
```

tar命令解压缩语法：

```linux
#tar [-xvfz] [解压的文件]
	-x:  解包
	-v:  详情信息
	-z:  解压缩
	-f:  指定解压的文件
$tar -zxvf abc.tar.gz
```



#### 压缩命令：zip:压缩文件或者目录：压缩后的文件格式：.zip

```linux
#zip [-r] [压缩后的文件名] [文件或者目录]
		-r: 压缩目录 
$tar -r abc.zip abc
```

**能保留源文件**

unzip命令解压缩。

```linux
#unzip [压缩文件]
$unzip abc.zip
```



#### 压缩命令：bzip2:压缩文件：压缩后的文件格式：.bz2

```linux
#bzip2 [-k] [文件]
		-k(keep): 产生压缩文件后保留原文件 
$bzip2 -k abc
$tar -cjf def.tar.bz2 def(文件夹)  这里把z换成j
```

**bzip2压缩比惊人。**

bunzip2命令解压缩。

```linux
#bunzip2 [-k] [压缩文件]
		-k: 解压缩后保留原文件
$bunzip2 -k abc.bz2
$bunzip2 -xjf def.tar.bz2
```









### 文件内容查看

> 概述

Linux系统中使用以下命令来查看文件的内容：

- **cat 由第一行开始显示文件内容，用来读文章，或者读取配置文件都用cat命令。**

  

  ![image-20210311195228536](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210311195228536.png)

- **tac 从最后一行开始显示，可以看出 tac 是 cat 的倒着写！**

- **nl  显示的时候，顺道输出行号！（常用）**

  

  ![image-20210311195135085](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210311195135085.png)

  

- **more 一页一页的显示文件内容（空格代表翻页，enter代表向下看一行， :f 显示行号）**

  ![image-20210311200129776](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210311200129776.png)

  

- **less 与 more 类似，但是比 more 更好的是，他可以往前翻页！（空格翻页，上下代表上下行！退出使用 q(quit) 命令。 /字符串向下查找字符串、？字符串是向上查找字符串，n向上询找，N向下询找）**

  ![image-20210311200514128](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210311200514128.png)

  

- **head 只看头几行( -n 参数显示能看几行）**

  ![image-20210311200742424](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210311200742424.png)

  ![image-20210311201251357](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210311201251357.png)

  

- **tail 只看尾巴几行**

  ![image-20210311200805698](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210311200805698.png)



**你可以使用 *man [命令]*来查看各个命令的使用文档，如 ：man cp。**

网络配置目录：`cd /etc/sysconfig/network-scripts/`

`ifconfig`命令查看网络配置

![image-20210311195052375](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210311195052375.png)





## Linux链接（了解）

Linux的链接分为两种：**硬链接**和**软连接**

**硬链接：**A---B，假设B是A的硬链接，那么他们两个指向了同一个文件！允许一个文件拥有多个路径，用户可以通过这种机制建立硬链接到一些重要文件上，防止误删！

**软链接：**类似win下的快捷方式，删除源文件后，快捷方式就不能使用了！

创建链接 ln 命令!

`touch`：创建文件

`echo`：写东西到文件中

![image-20210311204331929](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210311204331929.png)

![image-20210311205402065](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210311205402065.png)



## Linux基本目录

**一切皆文件**

**根目录 / ，所有的文件都挂在在这个节点下**

![image-20210310104153763](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210310104153763.png)

```
ls /
```

你会看到：

![image-20210310104426988](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210310104426988.png)

目录解释：

- **/bin**：bin是Binary的缩写, 这个目录存放着最经常使用的命令。
- **/boot：** 这里存放的是启动Linux时使用的一些核心文件，包括一些连接文件以及镜像文件。
- **/dev ：** dev是Device(设备)的缩写, 存放的是Linux的外部设备，在Linux中访问设备的方式和访问文件的方式是相同的。
- **/etc：** 这个目录用来存放所有的系统管理所需要的配置文件和子目录**比如Redis、tomcat的配置**。
- **/home：用户的主目录，在Linux中，每个用户都有一个自己的目录，一般该目录名是以用户的账号命名的。**
- **/lib**：这个目录里存放着系统最基本的动态连接共享库，其作用类似于Windows里的DLL文件。
- **/lost+found**：这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件**（存放电脑突然关机的文件）**。
- **/media**：linux系统会自动识别一些设备，例如U盘、光驱等等，当识别后，linux会把识别的设备挂载到这个目录下。
- **/mnt**：系统提供该目录是为了让用户临时挂载别的文件系统的，我们可以将光驱挂载在/mnt/上，然后进入该目录就可以查看光驱里的内容了。（我们可以把本地文件挂载到这个目录下）
- **/opt：这是给主机额外安装软件所摆放的目录。比如你安装一个ORACLE数据库则就可以放到这个目录下。默认是空的。（用来存放安装软件比如MySQL，redis）**
- **/proc**：这个目录是一个虚拟的目录，它是系统内存的映射，我们可以通过直接访问这个目录来获取系统信息。
- **/root：该目录为系统管理员，也称作超级权限者的用户主目录。**
- **/sbin**：s就是Super User的意思，这里存放的是系统管理员使用的系统管理程序。
- **/srv**：该目录存放一些服务启动之后需要提取的数据。
- **/sys**：这是linux2.6内核的一个很大的变化。该目录下安装了2.6内核中新出现的一个文件系统 sysfs 。
- **/tmp：这个目录是用来存放一些临时文件的。**
- **/usr："Unix Salftwre Resource"系统软件资源目录，这是一个非常重要的目录，用户的很多应用程序和文件都放在这个目录下，类似于windows下的program files目录。(本地目录)**
- **/usr/bin：** 系统用户使用的应用程序。
- **/usr/sbin：** 超级用户使用的比较高级的管理程序和系统守护程序。
- **/usr/src：** 内核源代码默认的放置目录。
- **/var：这个目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件。**
- **/run**：是一个临时文件系统，存储系统启动以来的信息。当系统重启时，这个目录下的文件应该被删掉或清除。
- **/www：** **存放服务器网站相关的资源，环境，网站的项目**



## 网络命令

```linux
#测试网络连通性
ping 选项 IP地址
	-c ：指定发送次数
	
#查看和设置网卡信息
ifconfig 网卡名称 IP地址
$ifconfig eth0 127.0.0.1

#mail 查看/发送电子邮件

#last 列出目前与过去登入系统的用户信息

#lastlog 检查某特定用户上次登录的时间
$lastlog -u 502(用户的标识符)

#traceroute 显示数据包到主机间的路径
$traceroute www.baudu.com

#netstat 显示网络相关信息
netstat [选项]
	-t: tcp协议
	-u: udp协议
	-r: 路由
	-l: 监听
	-n: 显示IP地址和端口号
$netstat -tlun:查看本机监听端口
$netstat -an:查看本机所有的网络连接
$netstat -rn:查看本机路由表


#setup 配置网络
setup

#mount 挂在命令       例如：安装U盘，windows会自动挂载，而Linux不会，需要手动挂载。分配盘符的过程就是挂载。
mount [-t 系统文件] 设备文件名 挂载点
$mount -t ios9660 /dev/sr0 /mnt/cdrom
#卸载挂载点
umount 设备文件名
$umount /dev/sr0
```









## Vim编辑器

> 什么是vim编辑器（程序开发工具）
>

Vim通过一些插件可以实现IDE一样的功能！

Vim可以代码补全、编译及错误跳转等方便的功能，在程序员中被广泛使用，尤其是Linux中必须要会使用Vim编辑器**（查看内容、编辑内容、保存内容！）**。

![image-20210317173347464](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317173347464.png)



> 三种使用模式

三种模式：

1. **命令模式（Command mode）**

   用户刚启动Vi/Vim，便进入命令模式。此状态下敲击键盘动作会被Vim识别为命令，而非输入的字符串。

   ![image-20210317171555111](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317171555111.png)

   ![image-20210317173643218](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317173643218.png)

   有以下几个常用命令：

   - i 切换到输入模式，以输入字符。
   - x 删除当前光标所处的字符。
   - ：切换到底线命令模式，以在最底一行输入命令。

   想要编辑文本：启动Vim，进入命令模式，按下i（insert） ,切换到输入模式（只有一些最基本的命令），因此仍要靠**底线命令模式**输入更多的命令。

2. **输入模式(Isnert mode)**

3. **底线命令模式(Last line mide)**

   在命令模式下按下 :(英文冒号)就进入底线命令模式。光标移动到最底下，可以执行一些底线命令。

   ![image-20210317172628487](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317172628487.png)

   在底线的基本命令 **:wq**(保存并退出)：

   - q 退出程序
   - w 保存文件



> Vim 按键说明

除了上面简易范例的 i, Esc, :wq 之外，其实 vim 还有非常多的按键可以使用。

**第一部分：一般模式可用的光标移动、复制粘贴、搜索替换等**

| 移动光标的方法     |                                                              |
| :----------------- | ------------------------------------------------------------ |
| h 或 向左箭头键(←) | 光标向左移动一个字符                                         |
| j 或 向下箭头键(↓) | 光标向下移动一个字符                                         |
| k 或 向上箭头键(↑) | 光标向上移动一个字符                                         |
| l 或 向右箭头键(→) | 光标向右移动一个字符                                         |
| [Ctrl] + [f]       | 屏幕『向下』移动一页，相当于 [Page Down]按键 (常用)          |
| [Ctrl] + [b]       | 屏幕『向上』移动一页，相当于 [Page Up] 按键 (常用)           |
| [Ctrl] + [d]       | 屏幕『向下』移动半页                                         |
| [Ctrl] + [u]       | 屏幕『向上』移动半页                                         |
| +                  | 光标移动到非空格符的下一行                                   |
| -                  | 光标移动到非空格符的上一行                                   |
| **数字< space>**   | 那个 表示『数字』，例如 20 。按下数字后再按空格键，光标会向右移动这一行的 数字个字符。 |
| 0 或功能键[Home]   | 这是数字『 0 』：移动到这一行的最前面字符处 (常用)           |
| $ 或功能键[End]    | 移动到这一行的最后面字符处(常用)                             |
| H                  | 光标移动到这个屏幕的最上方那一行的第一个字符                 |
| M                  | 光标移动到这个屏幕的中央那一行的第一个字符                   |
| L                  | 光标移动到这个屏幕的最下方那一行的第一个字符                 |
| G                  | 移动到这个档案的最后一行(常用)                               |
| nG                 | n 为数字。移动到这个档案的第 n 行。例如 20G 则会移动到这个档案的第 20 行(可配合 :set nu) |
| gg                 | 移动到这个档案的第一行，相当于 1G 啊！(常用)                 |
| **n< Enter>**      | n 为数字。光标向下移动 n 行(常用)                            |

| 搜索替换  |                                                              |
| :-------- | ------------------------------------------------------------ |
| **/word** | 向光标之下寻找一个名称为 word 的字符串。例如要在档案内搜寻 vbird 这个字符串，就输入 /vbird 即可！(常用) |
| ?word     | 向光标之上寻找一个字符串名称为 word 的字符串。               |
| **n**     | 这个 n 是英文按键。代表重复前一个搜寻的动作。举例来说， 如果刚刚我们执行 /vbird 去向下搜寻 vbird 这个字符串，则按下 n 后，会向下继续搜寻下一个名称为 vbird 的字符串。如果是执行 ?vbird 的话，那么按下 n 则会向上继续搜寻名称为 vbird 的字符串！ |
| **N**     | 这个 N 是英文按键。与 n 刚好相反，为『反向』进行前一个搜寻动作。例如 /vbird 后，按下 N 则表示『向上』搜寻 vbird 。 |

| 删除、复制与粘贴 |                                                              |
| :--------------- | ------------------------------------------------------------ |
| x, X             | 在一行字当中，x 为向后删除一个字符 (相当于 [del] 按键)， X 为向前删除一个字符(相当于 [backspace] 亦即是退格键) (常用) |
| nx               | n 为数字，连续向后删除 n 个字符。举例来说，我要连续删除 10 个字符， 『10x』。 |
| dd               | 删除游标所在的那一整行(常用)                                 |
| ndd              | n 为数字。删除光标所在的向下 n 行，例如 20dd 则是删除 20 行 (常用) |
| d1G              | 删除光标所在到第一行的所有数据                               |
| dG               | 删除光标所在到最后一行的所有数据                             |
| d$               | 删除游标所在处，到该行的最后一个字符                         |
| d0               | 那个是数字的 0 ，删除游标所在处，到该行的最前面一个字符      |
| yy               | 复制游标所在的那一行(常用)                                   |
| nyy              | n 为数字。复制光标所在的向下 n 行，例如 20yy 则是复制 20 行(常用) |
| y1G              | 复制游标所在行到第一行的所有数据                             |
| yG               | 复制游标所在行到最后一行的所有数据                           |
| y0               | 复制光标所在的那个字符到该行行首的所有数据                   |
| y$               | 复制光标所在的那个字符到该行行尾的所有数据                   |
| p, P             | p 为将已复制的数据在光标下一行贴上，P 则为贴在游标上一行！举例来说，我目前光标在第 20 行，且已经复制了 10 行数据。则按下 p 后， 那 10 行数据会贴在原本的 20 行之后，亦即由 21 行开始贴。但如果是按下 P 呢？那么原本的第 20 行会被推到变成 30 行。(常用) |
| J                | 将光标所在行与下一行的数据结合成同一行                       |
| c                | 重复删除多个数据，例如向下删除 10 行，[ 10cj ]               |
| u                | 复原前一个动作。(常用)                                       |
| [Ctrl]+r         | 重做上一个动作。(常用)                                       |

**第二部分：一般模式切换到编辑模式的可用的按钮说明**

| 进入输入或取代的编辑模式 |                                                              |
| :----------------------- | ------------------------------------------------------------ |
| **i, I**                 | 进入输入模式(Insert mode)：i 为『从目前光标所在处输入』， I 为『在目前所在行的第一个非空格符处开始输入』。(常用) |
| a, A                     | 进入输入模式(Insert mode)：a 为『从目前光标所在的下一个字符处开始输入』， A 为『从光标所在行的最后一个字符处开始输入』。(常用) |
| o, O                     | 进入输入模式(Insert mode)：这是英文字母 o 的大小写。o 为『在目前光标所在的下一行处输入新的一行』；O 为在目前光标所在处的上一行输入新的一行！(常用) |
| r, R                     | 进入取代模式(Replace mode)：r 只会取代光标所在的那一个字符一次；R会一直取代光标所在的文字，直到按下 ESC 为止；(常用) |
| **[Esc]**                | 退出编辑模式，回到一般模式中(常用)                           |

**第三部分：一般模式切换到指令行模式的可用的按钮说明**

| 指令行的储存、离开等指令                                     |                                                              |
| :----------------------------------------------------------- | ------------------------------------------------------------ |
| :w                                                           | 将编辑的数据写入硬盘档案中(常用)                             |
| :w!                                                          | 若文件属性为『只读』时，强制写入该档案。不过，到底能不能写入， 还是跟你对该档案的档案权限有关啊！ |
| :q                                                           | 离开 vi (常用)                                               |
| :q!                                                          | 若曾修改过档案，又不想储存，使用 ! 为强制离开不储存档案。    |
| 注意一下啊，那个惊叹号 (!) 在 vi 当中，常常具有『强制』的意思～ |                                                              |
| **:wq**                                                      | 储存后离开，若为 :wq! 则为强制储存后离开 (常用)              |
| ZZ                                                           | 这是大写的 Z 喔！若档案没有更动，则不储存离开，若档案已经被更动过，则储存后离开！ |
| :w [filename]                                                | 将编辑的数据储存成另一个档案（类似另存新档）                 |
| :r [filename]                                                | 在编辑的数据中，读入另一个档案的数据。亦即将 『filename』 这个档案内容加到游标所在行后面 |
| :n1,n2 w [filename]                                          | 将 n1 到 n2 的内容储存成 filename 这个档案。                 |
| :! command                                                   | 暂时离开 vi 到指令行模式下执行 command 的显示结果！例如 『:! ls /home』即可在 vi 当中看 /home 底下以 ls 输出的档案信息！ |
| **:set nu**                                                  | 显示行号，设定之后，会在每一行的前缀显示该行的行号           |
| :set nonu                                                    | 与 set nu 相反，为取消行号！                                 |





## 账号管理

> 简介

Linux系统是一个多用户多任务的分时操作系统，任何一个要使用系统资源的用户，都必须首先向系统管理员申请一个账号，然后以这个账号的身份进入系统。

用户的账号一方面可以帮助系统管理员对使用系统的用户进行跟踪，并控制他们对系统资源的访问；另一方面也可以帮助用户组织文件，并为用户提供安全性保护。

每个用户账号都拥有一个唯一的用户名和各自的口令。

用户在登录时键入正确的用户名和口令后，就能够进入系统和自己的主目录。

实现用户账号的管理，要完成的工作主要有如下几个方面：

- 用户账号的添加、删除与修改。
- 用户口令的管理。
- 用户组的管理。



> 用户账号的管理**（重要）**

用户账号的管理工作主要涉及到用户账号的添加、修改和删除。

添加用户账号就是在系统中创建一个新账号，然后为新账号分配用户号、用户组、主目录和登录Shell等资源。



> useradd 命令 添加用户

useradd -选项 用户名

- -m：自动创建这个用户的主目录/home/用户名

![image-20210317195418313](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317195418313.png)

参数说明：

- 选项 :

- - -c comment 指定一段注释性描述。
  - -d 目录 指定用户主目录，如果此目录不存在，则同时使用-m选项，可以创建主目录。
  - -g 用户组 指定用户所属的用户组。
  - -G 用户组，用户组 指定用户所属的附加组。
  - -m　使用者目录如不存在则自动建立。
  - -s Shell文件 指定用户的登录Shell。
  - -u 用户号 指定用户的用户号，如果同时有-o选项，则可以重复使用其他用户的标识号。

- 用户名 :

- - 指定新账号的登录名。



> 删除用户  userdel

userdel -r 用户名 删除用户的时候把目录一块删除。

![image-20210317195456348](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317195456348.png)



> 修改用户！usermod

修改用户 usermod 对应修改的内容  修改哪个用户

![image-20210317200355854](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317200355854.png)

修改完毕后查看配置文件....

![image-20210317200236594](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317200236594.png)



> 切换用户！

root用户

![image-20210317200834319](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317200834319.png)

1.切换用户的命令为：su username 【username是你的用户名哦】

![image-20210317201926949](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317201926949.png)



2.从普通用户切换到root用户，还可以使用命令：sudo su

3.在终端输入exit或logout或使用快捷方式ctrl+d，可以退回到原来用户，其实ctrl+d也是执行的exit命令

![image-20210317201926949](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317201926949.png)



4.在切换用户时，如果想在切换用户之后使用新用户的工作环境，可以在su和username之间加-，例如：【su - root】

$表示普通用户

\#表示超级用户，也就是root用户



> 用户密码设置问题！

一般是root用户在创建用户的时候设置密码。

![image-20210317203417098](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317203417098.png)

Linux上输入密码是不会显示的！

> 当前用户：who

**who:查看登录用户信息**

![image-20210514173003864](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210514173003864.png)

> 用户：w

**w:查看登录用户信息比who更详细:服务器运行时间、负载均衡、当前用户、执行操作等。**

![image-20210514174231674](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210514174231674.png)



> 锁定用户！

比如用户caohuihui辞职了，可以冻结这个账号。

```bash
passwd -l caohuihui  #锁定之后这个用户就不能登录了！
passwd -d caohuihui  # -d 会把密码清空，即使清空了也不能登录！
```

参数：

- -l :是锁的意思，冻结。
- -d : 密码清空。

**关于用户管理的基本命令，必须要掌握！**



## 用户组管理

每个用户都有一个用户组，系统可以对一个用户组中的所有用户进行集中管理。不同Linux 系统对用户组的规定有所不同，如Linux下的用户属于与它同名的用户组，这个用户组在创建用户时同时创建。

用户组的管理涉及用户组的添加、删除和修改。组的增加、删除和修改实际上就是对/etc/group文件的更新。

> 增加一个新的用户组使用groupadd命令

```
groupadd 选项 用户组
```

可以使用的选项有：

- -g GID 指定新用户组的组标识号（GID）。
- -o 一般与-g选项同时使用，表示新用户组的GID可以与系统已有用户组的GID相同。

实例1：

```
# groupadd group1
```

此命令向系统中增加了一个新组group1，新组的组标识号是在当前已有的最大组标识号的基础上加1。

实例2：

```
# groupadd -g 101 group2
```

此命令向系统中增加了一个新组group2，同时指定新组的组标识号是101。



> 如果要删除一个已有的用户组，使用groupdel命令

```
groupdel 用户组
```

例如：

```
# groupdel group1
```

此命令从系统中删除组group1。



> 修改用户组的属性使用groupmod命令

```
groupmod 选项 用户组
```

常用的选项有：

- -g GID 为用户组指定新的组标识号。
- -o 与-g选项同时使用，用户组的新GID可以与系统已有用户组的GID相同。
- -n新用户组 将用户组的名字改为新名字

```
# 此命令将组group2的组标识号修改为102。
groupmod -g 102 group2

# 将组group2的标识号改为10000，组名修改为group3。
groupmod –g 10000 -n group3 group2
```



> 切换组

如果一个用户同时属于多个用户组，那么用户可以在用户组之间切换，以便具有其他用户组的权限。

用户可以在登录后，使用命令newgrp切换到其他用户组，这个命令的参数就是目的用户组。例如：

```
$ newgrp root
```

这条命令将当前用户切换到root用户组，前提条件是root用户组确实是该用户的主组或附加组。



> /etc/passwd

完成用户管理的工作有许多种方法，但是每一种方法实际上都是对有关的系统文件进行修改。

与用户和用户组相关的信息都存放在一些系统文件中，这些文件包括/etc/passwd, /etc/shadow, /etc/group等。

下面分别介绍这些文件的内容。

**/etc/passwd文件是用户管理工作涉及的最重要的一个文件。**

```bash
用户名：口令（登录密码，我们不可见）：用户标识号：组标识号：注释行描述：主目录：登录shell
```

这个文件的每一行都代表一个用户，我们可以从这里查看出这个用户的主目录，属于哪个组。

```bash
[root@xiaozhang home]# cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:65534:65534:Kernel Overflow User:/:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
systemd-coredump:x:999:997:systemd Core Dumper:/:/sbin/nologin
systemd-resolve:x:193:193:systemd Resolver:/:/sbin/nologin
tss:x:59:59:Account used by the trousers package to sandbox the tcsd daemon:/dev/null:/sbin/nologin
polkitd:x:998:996:User for polkitd:/:/sbin/nologin
libstoragemgmt:x:997:995:daemon account for libstoragemgmt:/var/run/lsm:/sbin/nologin
unbound:x:996:993:Unbound DNS resolver:/etc/unbound:/sbin/nologin
setroubleshoot:x:995:991::/var/lib/setroubleshoot:/sbin/nologin
cockpit-ws:x:994:990:User for cockpit web service:/nonexisting:/sbin/nologin
cockpit-wsinstance:x:993:989:User for cockpit-ws instances:/nonexisting:/sbin/nologin
sssd:x:992:988:User for sssd:/:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
chrony:x:991:987::/var/lib/chrony:/sbin/nologin
rngd:x:990:986:Random Number Generator Daemon:/var/lib/rngd:/sbin/nologin
tcpdump:x:72:72::/:/sbin/nologin
nscd:x:28:28:NSCD Daemon:/:/sbin/nologin
caohuihui:x:1000:520::/home/caohuihui:/bin/bash
```

从上面的例子我们可以看到，/etc/passwd中一行记录对应着一个用户，每行记录又被冒号(:)分隔为7个字段，其格式和具体含义如下：

```bash
用户名:口令:用户标识号:组标识号:注释性描述:主目录:登录Shell
```

1）"用户名"是代表用户账号的字符串。

通常长度不超过8个字符，并且由大小写字母和/或数字组成。登录名中不能有冒号(:)，因为冒号在这里是分隔符。

为了兼容起见，登录名中最好不要包含点字符(.)，并且不使用连字符(-)和加号(+)打头。

2）“口令”一些系统中，存放着加密后的用户口令字。

虽然这个字段存放的只是用户口令的加密串，不是明文，但是由于/etc/passwd文件对所有用户都可读，所以这仍是一个安全隐患。因此，现在许多Linux 系统（如SVR4）都使用了shadow技术，把**真正的加密后的用户口令字存放到/etc/shadow文件中**，而在/etc/passwd文件的口令字段中只存放一个特殊的字符，例如“x”或者“*”。

3）“用户标识号”是一个整数，系统内部用它来标识用户。

一般情况下它与用户名是一一对应的。如果几个用户名对应的用户标识号是一样的，系统内部将把它们视为同一个用户，但是它们可以有不同的口令、不同的主目录以及不同的登录Shell等。

通常用户标识号的取值范围是0～65 535。0是超级用户root的标识号，1～99由系统保留，作为管理账号，普通用户的标识号从100开始。在Linux系统中，这个界限是500。

4）“组标识号”字段记录的是用户所属的用户组。

它对应着/etc/group文件中的一条记录。

5)“注释性描述”字段记录着用户的一些个人情况。

例如用户的真实姓名、电话、地址等，这个字段并没有什么实际的用途。在不同的Linux 系统中，这个字段的格式并没有统一。在许多Linux系统中，这个字段存放的是一段任意的注释性描述文字，用作finger命令的输出。

6)“主目录”，也就是用户的起始工作目录。

它是用户在登录到系统之后所处的目录。在大多数系统中，各用户的主目录都被组织在同一个特定的目录下，而用户主目录的名称就是该用户的登录名。各用户对自己的主目录有读、写、执行（搜索）权限，其他用户对此目录的访问权限则根据具体情况设置。

7)用户登录后，要启动一个进程，负责将用户的操作传给内核，这个进程是用户登录到系统后运行的命令解释器或某个特定的程序，即Shell。

Shell是用户与Linux系统之间的接口。Linux的Shell有许多种，每种都有不同的特点。常用的有sh(Bourne Shell), csh(C Shell), ksh(Korn Shell), tcsh(TENEX/TOPS-20 type C Shell), bash(Bourne Again Shell)等。

系统管理员可以根据系统情况和用户习惯为用户指定某个Shell。如果不指定Shell，那么系统使用sh为默认的登录Shell，即这个字段的值为/bin/sh。

用户的登录Shell也可以指定为某个特定的程序（此程序不是一个命令解释器）。

利用这一特点，我们可以限制用户只能运行指定的应用程序，在该应用程序运行结束后，用户就自动退出了系统。有些Linux 系统要求只有那些在系统中登记了的程序才能出现在这个字段中。

8)系统中有一类用户称为伪用户（pseudo users）。

这些用户在/etc/passwd文件中也占有一条记录，但是不能登录，因为它们的登录Shell为空。它们的存在主要是方便系统管理，满足相应的系统进程对文件属主的要求。

常见的伪用户如下所示：

```bash
伪 用 户 含 义
bin 拥有可执行的用户命令文件
sys 拥有系统文件
adm 拥有帐户文件
uucp UUCP使用
lp lp或lpd子系统使用
nobody NFS使用
```

> /etc/shadow

**1、除了上面列出的伪用户外，还有许多标准的伪用户，例如：audit, cron, mail, usenet等，它们也都各自为相关的进程和文件所需要。**

由于/etc/passwd文件是所有用户都可读的，如果用户的密码太简单或规律比较明显的话，一台普通的计算机就能够很容易地将它破解，因此对安全性要求较高的Linux系统都把加密后的口令字分离出来，单独存放在一个文件中，这个文件是/etc/shadow文件。有超级用户才拥有该文件读权限，这就保证了用户密码的安全性。

**2、/etc/shadow中的记录行与/etc/passwd中的一一对应，它由pwconv命令根据/etc/passwd中的数据自动产生**

它的文件格式与/etc/passwd类似，由若干个字段组成，字段之间用":"隔开。这些字段是：

```
登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志
```

1. "登录名"是与/etc/passwd文件中的登录名相一致的用户账号
2. "口令"字段存放的是加密后的用户口令字，长度为13个字符。如果为空，则对应用户没有口令，登录时不需要口令；如果含有不属于集合 { ./0-9A-Za-z }中的字符，则对应的用户不能登录。
3. "最后一次修改时间"表示的是从某个时刻起，到用户最后一次修改口令时的天数。时间起点对不同的系统可能不一样。例如在SCO Linux 中，这个时间起点是1970年1月1日。
4. "最小时间间隔"指的是两次修改口令之间所需的最小天数。
5. "最大时间间隔"指的是口令保持有效的最大天数。
6. "警告时间"字段表示的是从系统开始警告用户到用户密码正式失效之间的天数。
7. "不活动时间"表示的是用户没有登录活动但账号仍能保持有效的最大天数。
8. "失效时间"字段给出的是一个绝对的天数，如果使用了这个字段，那么就给出相应账号的生存期。期满后，该账号就不再是一个合法的账号，也就不能再用来登录了。









## 磁盘管理

> 概述

Linux磁盘管理好坏直接关系到整个系统的性能问题。

Linux磁盘管理常用命令为 df、du。

- df ：列出文件系统的整体磁盘使用量
- du：检查磁盘空间使用量



> df

df命令参数功能：检查文件系统的磁盘空间占用情况。可以利用该命令来获取硬盘被占用了多少空间，目前还剩下多少空间等信息。

语法：

```
df [-ahikHTm] [目录或文件名]
```

选项与参数：

- -a ：列出所有的文件系统，包括系统特有的 /proc 等文件系统；
- -k ：以 KBytes 的容量显示各文件系统；
- -m ：以 MBytes 的容量显示各文件系统；
- -h ：以人们较易阅读的 GBytes, MBytes, KBytes 等格式自行显示；
- -H ：以 M=1000K 取代 M=1024K 的进位方式；
- -T ：显示文件系统类型, 连同该 partition 的 filesystem 名称 (例如 ext3) 也列出；
- -i ：不用硬盘容量，而以 inode 的数量来显示

![image-20210319151057265](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210319151057265.png)



> du

Linux du命令也是查看使用空间的，但是与df命令不同的是Linux du命令是对文件和目录磁盘使用的空间的查看，还是和df命令有一些区别的，这里介绍Linux du命令。

语法：

```bash
du [-ahskm] 文件或目录名称
```

选项与参数：

- -a ：列出所有的文件与目录容量，因为默认仅统计目录底下的文件量而已。
- -h ：以人们较易读的容量格式 (G/M) 显示；
- -s ：列出总量而已，而不列出每个各别的目录占用容量；
- -S ：不包括子目录下的总计，与 -s 有点差别。
- -k ：以 KBytes 列出容量显示；
- -m ：以 MBytes 列出容量显示；

测试：

```bash
# 只列出当前目录下的所有文件夹容量（包括隐藏文件夹）:
# 直接输入 du 没有加任何选项时，则 du 会分析当前所在目录的文件与目录所占用的硬盘空间。
[root@kuangshen home]# du
16./redis
8./www/.oracle_jre_usage  # 包括隐藏文件的目录
24./www
48.                        # 这个目录(.)所占用的总量
# 将文件的容量也列出来
[root@kuangshen home]# du -a
4./redis/.bash_profile
4./redis/.bash_logout    
....中间省略....
4./kuangstudy.txt # 有文件的列表了
48.
# 检查根目录底下每个目录所占用的容量
[root@kuangshen home]# du -sm /*
0/bin
146/boot
.....中间省略....
0/proc
.....中间省略....
1/tmp
3026/usr  # 系统初期最大就是他了啦！
513/var
2666/www
```

通配符 * 来代表每个目录。

与 df 不一样的是，du 这个命令其实会直接到文件系统内去搜寻所有的文件数据。



> 磁盘挂载与卸除

根文件系统之外的其他文件要想能够被访问，都必须通过“关联”至根文件系统上的某个目录来实现，此关联操作即为“挂载”，此目录即为“挂载点”,解除此关联关系的过程称之为“卸载”

Linux 的磁盘挂载使用mount命令，卸载使用umount命令。

磁盘挂载语法：

```bash
mount [-t 文件系统] [-L Label名] [-o 额外选项] [-n] 装置文件名 挂载点
```

测试：

```bash
# 将 /dev/hdc6 挂载到 /mnt/hdc6 上面！
[root@www ~]# mkdir /mnt/hdc6
[root@www ~]# mount /dev/hdc6 /mnt/hdc6
[root@www ~]# df
Filesystem           1K-blocks     Used Available Use% Mounted on
/dev/hdc6              1976312     42072   1833836   3% /mnt/hdc6
```

磁盘卸载命令 umount 语法：

```bash
umount [-fn] 装置文件名或挂载点
选项与参数：
```

- -f ：强制卸除！可用在类似网络文件系统 (NFS) 无法读取到的情况下；
- -n ：不升级 /etc/mtab 情况下卸除。

卸载/dev/hdc6

```bash
[root@www ~]# umount /dev/hdc6
```





## 进程管理

> 基本概念

1. 在Linux中，每一个程序都有自己的一个进程，每个进程都有一个id号！
2. 每一个进曾都有一个父进程
3. 进程可以有两种方式：前台！和后台运行
4. 一般的话服务都是后台运行，基本的程序都是前台运行的。！

> 命令

**ps** 查看当前系统中正在执行的各种进程的信息！

ps -xx：

-  -a :显示当前终端运行的所有进程信息(当前进程一个)！
- -u：以用户的信息显示进程。
- -x：显示后台运行进程的参数！

```bash
#ps -aux 查看所有进程
ps -aux|grep

#例如 ps -aux|grep mysql  只查看MySQL进程
#例如 ps -aux|grep reids  只查看reids进程

# | 在Linux这个叫做管道符   A|B
# grep 查找文件中符合条件的字符串！
```

**ps -ef：可以查看父进程的信息。**

```bash
ps -ef|grep mysql  #看父进程我们一般可以通过目录树结构查看！

#进程树！
pstree -pu
	-p 显示父id
	-u 显示用户
```

**结束进程**

一般用于平常写Java代码时出现了死循环，才会杀死进程！

```bash
kill -9 进程的id
```

**表示强制结束该进程！**



**总结：Linux中一切皆文件**

​		**（文件：读写执行（查看、创建、删除、移动、复制、编辑），权限（用户、用户组），系统（磁盘、进程））！**





## 软件包管理

![image-20210517140034907](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517140034907.png)

![image-20210517141102743](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517141102743.png)

![image-20210517141719152](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517141719152.png)

### RPM安装

**rpm -ivh 全包名**

​	-i（install）        安装

​	-v（verbose）   显示详细信息

​	-h（hash）         显示进度

​	--nodeps             检测依赖性



**RPM包升级**

rpm  -Uvh  包全名

​	-U（upgrade）  升级



**RPM卸载**

rpm -e 包名

​	-e（erase）       卸载

​	--nodeps           不检查依赖性



**1、检查是否安装**

![image-20210517144337289](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517144337289.png)

**2、查询软件包的详细信息**

![image-20210517145506093](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517145506093.png)

**3、查询包中文件安装位置**

![image-20210517145914446](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517145914446.png)

**4、查询系统文件属于哪个RPM包**

![image-20210517150300678](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517150300678.png)

**5、查询软件包的依赖性**

![image-20210517150517527](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517150517527.png)



### RPM校验

**1、RPM包校验**

![image-20210517150959617](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517150959617.png)

![image-20210517151247748](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517151247748.png)

![image-20210517151420568](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517151420568.png)



**2、RPM包中文件的提取**

主要用来解决文件误删问题。

![image-20210517152657497](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517152657497.png)

![image-20210517153055494](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517153055494.png)



### RPM的yum安装

#### 1、IP地址配置	![image-20210517154112306](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517154112306.png)

#### 2、网络yum源

![image-20210517154938797](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517154938797.png)

![image-20210517154306392](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517154306392.png)

#### 3、常用yum命令

**1、查询**

![image-20210517155628970](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517155628970.png)

**2、安装**

![image-20210517174253296](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517174253296.png)

**3、升级**

![image-20210517174552937](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517174552937.png)

**注意：update后面一定要加升级的包名，如果不加则升级所有包和Linux内核导致系统无法启动。**

**4、卸载**

![image-20210517174818309](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517174818309.png)

**注意：用什么装什么，尽量不要卸载，更不要使用yum卸载，会导致依赖包同时卸载，造成系统崩溃。**

#### 4、yum软件组管理命令

![image-20210517175610082](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517175610082.png)

**需要什么功能就安装什么软件组即可，例如输入法，安装输入法的软件组。**

#### 5、搭建本地yum源步骤

![image-20210517182642570](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517182642570.png)

![image-20210517183004854](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210517183004854.png)

### 源码包管理

35