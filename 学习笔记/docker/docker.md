# Docker-study

## docker简介





## docker和虚拟机对比



![image-20210609223424185](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210609223424185.png)



## docker的安装

![image-20210609225043908](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210609225043908.png)

**注意：sudo加不加都行**



## docker核心概念



![image-20210610075219963](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210610075219963.png)



## docker镜像配置



![image-20210610085955183](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210610085955183.png)



## docker入门案例



![image-20210610092254371](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210610092254371.png)



## docker镜像相关命令



![image-20210610100918279](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210610100918279.png)



## docker容器相关命令



![image-20210610104357816](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210610104357816.png)

![image-20210610104313665](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210610104313665.png)

![image-20210610104502063](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210610104502063.png)

![image-20210610132846743](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210610132846743.png)

![image-20210610142037247](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210610142037247.png)



## docker镜像分层原理



![image-20210610145529647](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210610145529647.png)





## docker容器中网络的通信机制





P12





## docker数据卷

```bash
#：ro是挂载数据卷的时候是只读。
docker run -d -p 8080:8080 --name tomcat01 -v /root/apps:/usr/local/tomcat/webapps:ro tomcat:8.0-jre8
```

![image-20210612185112990](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210612185112990.png)



## docker核心架构图

![image-20210612185730346](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210612185730346.png)



## docker安装服务



### 安装mysql服务

![image-20210612202006567](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210612202006567.png)

### 安装tomcat服务

![image-20210613100612640](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210613100612640.png)

注意：**一般修改了配置文件后直接重启即可（docekr restart  容器id），但注意修改端口后一定要重新运行一个新的tomcat容器。**

![image-20210613222128602](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210613222128602.png)

### 安装redis服务



![image-20210614002441190](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210614002441190.png)

