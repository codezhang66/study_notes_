### git的安装和卸载：

```
卸载
先删除环境变量，在卸载软件

安装
在官网下载（一般比较慢，建议使用淘宝镜像），直接无脑下一步即可。
```

### git 的常用命令

```bash
cd  改变目录
cd ..  回到上一个目录
pwd   显示当前多所在的目录路径
ls(ll)   列出当前目录的所有文件，ll列出的内容更为详细。
touch  新建一个文件。如：touch index.js
rm  删除一个文件。
rm -r  删除一个文件夹
mkdir  新建一个文件夹。
mv  把一个文件移到另一个文件中。如mv index.js A:把index.js文件移到A文件夹中。
reset  重新初始化终端/清屏。
clear  清屏。
history  查看命令历史。
help  帮助。
exit  退出。
# 表示注释。
```



### 查看不同级别的配置文件：

```bash
#查看系统config
git config --system --list

#查看当前用户（global）配置
git config --global --list
```

### git相关的配置文件：

1)、Git\etc\gitconfig : Git安装目录下的gitconfig --system 系统级

2)、C:\User\Administrator\.gitconfig 只适用于当前登录用户的配置 --global全局这里可以直接编辑配置文件，通过命令设置后会响应到这里。

### 设置git用户的名字和mail

```bash
git config --global user.name "名字"

git config --global user.mail "邮件"
```

### git的基本理论（核心）

#### 四个工作区域:3个本地和一个远程

![image-20210204193421157](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210204193421157.png)

![image-20210204193716557](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210204193716557.png)

##### 3个本地:

```
工作目录(Working Directory):就是平常存放代码的地方。
暂存区(Stage/Index): 用于临时存放你的改动，事实上他只是个文件，保存即将提交到文件列表信息。
资源库(Repository或Git Directory):本地仓库， 就是安全存放数据的位置，这里有你提交的所有版本的数据。期中HEND指向最新放入仓库的版本。
```

##### 远程仓库：

```
git仓库(Remote Directory):远程仓库，托管代码的服务器，可以简单的认为是你项目组中的一台电脑用于远程数据交换。
```

![image-20210204193239112](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210204193239112.png)

### 本地仓库搭建

创建本地仓库有两种方式：创建一个全新的仓库 ，另一个是克隆远程仓库。

1、创建一个全新的仓库：

```bash
#在当前目录新建一个Git代码库
$ git init
```

2、克隆远程仓库

```bash
#克隆一个项目和他的整个代码历史（版本信息）
$ git clone [url]
```

### 文件4种状态

下述命令可以查看到文件的状态：

```bash
#查看指定文件的状态
git status [filename]

#查看所有文件的状态
git status

#git add .      添加所有文件到暂存区
#git commit -m "注释消息内容"  提交暂存区的内容到本地仓库  -m是一些提交信息
```

### 忽略文件

![image-20210204201743572](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210204201743572.png)



### 设置免密码登录

1、设置本机绑定SSH公匙，实现免密码登录！（免密码登录，很重要，码云是远程仓库，我们平常工作是在本地仓库！）

```bash
#进目录c:Users\\administrator\.ssh  
#生成公匙
ssh-keygen

#可以加密
ssh-keygen -t rsa
```

2、将公匙信息public key 添加到马云账户即可！

![image-20210205135754468](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210205135754468.png)

3、使用码云创建一个自己的仓库。

![image-20210205140303517](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210205140303517.png)

克隆到本地！

![image-20210205142610953](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210205142610953.png)



### IDEA集成Git

1、新建项目，绑定git.

​     将我们远程的git文件目录拷贝到项目中即可。

![image-20210205193451378](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210205193451378.png)

2、修改文件，使用idea操作git.

![image-20210205193854074](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210205193854074.png)

3、提交测试。

![image-20210205194225972](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210205194225972.png)

### 分支

```bash
#新建一个分支，但一依旧停留在当前分支
git branch [branch-name]

#新建一个分支，并切换到该分支
git checkout -b [branch]

#合并指定分支到当前分支
git merge [branch]

#删除分支
$ git branch -d [branch-name]

#删除远程分支
$ git push origin --delete [branch-name]
$ git branch -dr [remote/branch]
```



# 世界上没有笨人，只有懒人。跟对人，做对事。现在懒，吃小亏，以后吃大亏！