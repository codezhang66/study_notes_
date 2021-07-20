# Redis

### 什么是NoSQL

> NoSQL

Not Only SQL(不仅仅是SQL)。

解决问题：用户的个人信息，社交网络，地理位置。用户自己产生的数据，用户日志等等爆发式的增长!

当今大数据环境下发展的十分迅速，Redis是发展最快的。

用户的个人信息，社交网络，地理位置(这些信息的存储不需要固定的格式)，不需要多余的操作就能横向扩展。NoSQL的表现   Map<String,Object>  使用键值对来控制

NoSQL特点：

解耦！

1. 方便扩展（数据之间没有关系，很好扩展！）

2. 大数据量高性能（Redis一秒写8万次，读取11万，Nosql的缓存记录级，是一种颗粒度的缓存，性能比较高。）

3. 数据类型是多样型的！（不需要事先设计数据库！随取随用！）

4. 传统的RDBMS（关系型数据库）和Nosql

   ```
   传统的RDBMS
   - 结构化组织
   - SQL
   - 数据和关系都存在单独的表中
   - 操作数据定义语言
   - 严格的一致性
   - 基础的事务
   ```

   ```
   NoSQL
   - 不仅仅是数据
   - 没有固定的查询语言
   - 键值对存储，列存储，文档存储，图形数据库（社交关系）
   - 最终一致性
   - CAP理论和BASE理论（异地多活）
   - 高性能，高可用，高可扩
   ```

   

### NoSQL的四大分类

**KV键值对：**

- 新浪：Redis
- 美团：Redis + Tair
- 阿里、百度： Redis + memecache

**文档型数据库（bson格式和json格式一样）：**

- MongoDB(一般必须要掌握)
  - MongoDB：是一个基于分布式文件存储的数据库，c++编写，主要用来处理大量的文档。
  - MongoDB是一个介于关系型和非关系型数据库之间的数据库，MongoDB是非关系型数据库中功能最丰富的、最像关系型数据库。

- ConthDB(国外的不做了解)

**列存储数据库**

- HBase
- 分布式文件系统

**图关系数据库**

- 它不是存放图片，存放的是关系。比如：朋友圈社交网络，广告推荐！
- Neo4j，infoGrid;

![img](https://img-blog.csdnimg.cn/20200410144538483.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L01vZGVzdHlfQm95,size_16,color_FFFFFF,t_70)



### Redis概述

Redis（Remote Dictionary Server )，即**远程字典服务**！

是一个开源的使用ANSI [C语言](https://baike.baidu.com/item/C语言)编写、支持网络、可基于内存亦可持久化的日志型、Key-Value[数据库](https://baike.baidu.com/item/数据库/103728)，并提供多种语言的API。

免费开源，是当下最热门的NoSQL技术之一！也被称之为结构化数据库。

> Redis能干什么？

1. 内存存储、持久化，内存中是断电即失，所以说持久化很重要（rdb,aof）;
2. 效率高，可以用于告诉缓存；
3. 发布订阅系统
4. 地图信息分析
5. 计时器，计数器（浏览量！）

> 特性：

1. 多样的事务类型
2. 持久化
3. 集群
4. 事务

> 学习中需要用到的东西

1. 中文官网：http://www.redis.cn/

![image-20210309211308698](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210309211308698.png)

注意：**windows在Github上下载（停止更新！）**

Redis推荐都是在Linux服务器上搭建的。

### linux下安装Redis

1. 下载安装包！

2. 解压Redis的安装

   把压缩包放入/opt目录下，解压即可!`tar -zxvf 解压的文件`

   ![image-20210319170412874](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210319170412874.png)

3. 进入解压后的文件，一般操作它时记得备份一个！

   ![image-20210319170814582](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210319170814582.png)

   

4.基本的环境安装

```bash
yum install gcc-c++

make

make install
```

5.redis 的默认安装路径：`/usr/local/bin`



6.将redis 的配置文件复制到当前目录下。



7.redis 的配置文件默认不是后台启动，修改配置文件！`daemonize yes`  设置为守护进程



8.启动redis服务 `redis-server zhangconfig/redis.conf`



9.启动客户端 `redis-cli -p 6379`



10.查看进程`ps -ef | grep redis`查看关于redis的进程



11.关闭服务  `shutdown`即可。



### 性能测试

redis-benchmark 压力测试工具。（官方自带的性能测试工具）

redis-benchmark  命令参数

redis 性能测试工具可选参数如下所示：

| 序号 | 选项      | 描述                                       | 默认值    |
| ---- | --------- | ------------------------------------------ | --------- |
| 1    | **-h**    | 指定服务器主机名                           | 127.0.0.1 |
| 2    | **-p**    | 指定服务器端口                             | 6379      |
| 3    | **-s**    | 指定服务器 socket                          |           |
| 4    | **-c**    | 指定并发连接数                             | 50        |
| 5    | **-n**    | 指定请求数                                 | 10000     |
| 6    | **-d**    | 以字节的形式指定 SET/GET 值的数据大小      | 2         |
| 7    | **-k**    | 1=keep alive 0=reconnect                   | 1         |
| 8    | **-r**    | SET/GET/INCR 使用随机 key, SADD 使用随机值 |           |
| 9    | **-P**    | 通过管道传输 <numreq> 请求                 | 1         |
| 10   | **-q**    | 强制退出 redis。仅显示 query/sec 值        |           |
| 11   | **--csv** | 以 CSV 格式输出                            |           |
| 12   | **-l**    | 生成循环，永久执行测试                     |           |
| 13   | **-t**    | 仅运行以逗号分隔的测试命令列表。           |           |
| 14   | **-I**    | Idle 模式。仅打开 N 个 idle 连接并等待。   |           |

```bash
#测试100并发请求100000个请求。
redis-benchmark -h localhost -p 6379 -n 100000 -c 100
```

![image-20210519180121233](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210519180121233.png)

### 基础知识

redis默认16个数据库，默认使用的第0个数据库，

![image-20210519180625757](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210519180625757.png)

切换第二个数据库`select 2`。

![image-20210519181239817](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210519181239817.png)

`dbsize`可以查看数据库的大小。

![image-20210519181201045](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210519181201045.png)

清除当前数据库` flushdb`

清除所有的数据库`flushall`



> redis是单线程的！

**redis单线程为什么还那么快？**

1、误区1：认为高性能的服务器一定是多线程的。

2、误区2：多线程（根CPU调度有关）一定比单线程效率高。

**核心：**redis是将所有的数据全部放入到内存中的，所以说使用单线程操作效率最高！（多线程上线文切换消耗内存！）对于内存系统来说，没有上线文切换效率就是最高的！多次读写都是在一个CPU上的



### 五大数据类型

#### redis-key

```bash
keys *

exists name               #判断是否存在name

expire name 秒数			#设置name过期时间   expire到期

ttl name                 #查看name的倒计时  ttl(time to live)

move name 数据库          #移动name到指定的数据库

del key                  #通过key删除键和值

type key                 #查看当前key的类型
```



#### 1、String

```bash
########################################################

append key value       #往key后面追加一个值   如果key不存在就相当于创建一个key和value

strlen key            #获取key的长度

set view 0           #设置浏览量为0
incr view            #view会自动加1
decr view            #view会自动减1
incrby view 10       #view会增加10 设置步长

########################################################

字符串范围 range   setrange和getrange先当与截取和替换字符串
getrange key1 2 3   #获取字符串范围[2，3]
getrange key1 0 -1   #获取全部字符串，和getkey一样
setrange key2 1 xx   #

########################################################

#setex (set with expire)   设置过期时间，例如setex keys 10 "hahahah"
#setnx (set if not exists)  不存在再设置（再在分布式锁中常常使用），例如setnx key3 hello

########################################################

mset key value [key value ...]		#同时设置一个或多个 key-value 对。
mget key1 [key2..]					#获取所有(一个或多个)给定 key 的值。 
msetnx key value [key value ...]    #原子性操作。

########################################################

#对象
set user:1 {name:xiaozhang,age:23}   #设置一个user:1对象，值为json字符串

#巧妙的设置对象
127.0.0.1:6379> mset user:1:name "xiaozhang" user:1:age "23"
OK
127.0.0.1:6379> mget user:1:name user:1:age
1) "xiaozhang"
2) "23"

########################################################

getset key value			#将给定 key 的值设为 value ，并返回 key 的旧值(old value)。不存在时返回null，并且设置键和值。
127.0.0.1:6379> getset db redis
(nil)
127.0.0.1:6379> get db
"redis"
127.0.0.1:6379> getset db mysql
"redis"
127.0.0.1:6379> get db
"mysql"

########################################################
```

**string应用场景：**

- 计数器
- 统计多单位的数量

#### 2、List

在redis里面，我们可以把list玩成栈、队列、阻塞队列。

所有的list命令都是以**l**开头的。redis不区分大小写命令。

```bash
#########################################

lpop key				#移出并获取列表的第一个元素
lpush key value1 [value2]	#将一个或多个值插入到列表头部
lrange key start stop    #获取列表指定范围内的元素
llen key				#获取列表长度
lindex key index		#通过索引获取列表中的元素


127.0.0.1:6379> lpush list one
(integer) 1
127.0.0.1:6379> lpush list two
(integer) 2
127.0.0.1:6379> lpush list three
(integer) 3
127.0.0.1:6379> lrange list 0 -1
1) "three"
2) "two"
3) "one"
127.0.0.1:6379> llen list
(integer) 3
127.0.0.1:6379> lpush list2 123 456
(integer) 2
127.0.0.1:6379> lrange list2 0 -1
1) "456"
2) "123"

#########################################

127.0.0.1:6379> rpush list four #从最后边插入
(integer) 4
127.0.0.1:6379> lrange list 0 -1
1) "three"
2) "two"
3) "one"
4) "four"
127.0.0.1:6379> lpop list2 		#移除list2的左边第一个元素
"456"
127.0.0.1:6379> lrange list2 0 -1
1) "123"
127.0.0.1:6379> rpop list		#移除list右边元素
"four"


#########################################

lrem key count value		#移除列表元素  list中可以存储相同的元素，该count是要移除元素的个数
lset key index value		#通过索引设置列表元素的值
ltrim key start stop		#对一个列表进行修剪(trim)，就是说，让列表只保留指定区间内的元素，不在指定区间之内的元素都将被删除。

127.0.0.1:6379> lrem list 1 three
(integer) 1
127.0.0.1:6379> lrange list 0 -1
1) "two"
2) "one"


#########################################

rpoplpush source destination	#移除列表的最后一个元素，并将该元素添加到另一个列表并返回
127.0.0.1:6379> lrange list 0 -1
1) "two"
2) "one"
127.0.0.1:6379> lrange list2 0 -1
1) "123"
127.0.0.1:6379> rpoplpush list list2
"one"
127.0.0.1:6379> lrange list2 0 -1
1) "one"
2) "123"

#########################################

lset key index value	#通过索引设置列表元素的值
127.0.0.1:6379> lset list 0 five  #给第一个元素设置值
OK
#########################################

linsert key before|after pivot value	#在列表的元素前或者后插入元素
127.0.0.1:6379> lrange list 0 -1
1) "xiaoyu"
2) "xiaozhang"
127.0.0.1:6379> 
127.0.0.1:6379> linsert list before xiaozhang wan
(integer) 3
127.0.0.1:6379> lrange list 0 -1
1) "xiaoyu"
2) "wan"
3) "xiaozhang"

#########################################
```

![image-20210520132119143](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210520132119143.png)

#### 3、Set

set中的值不能重复

```bash
#####################################################

127.0.0.1:6379> sadd myset "xiaozhang" "xiaoyu"		#向集合添加一个或多个成员
(integer) 2
127.0.0.1:6379> sadd myset "xiaozhang"
(integer) 0

#####################################################

127.0.0.1:6379> scard myset				#获取集合的成员数
(integer) 2

#####################################################

127.0.0.1:6379> smembers myset			#返回集合中的所有成员
1) "xiaozhang"
2) "xiaoyu"

#####################################################

127.0.0.1:6379> sismember myset "xiaozhang"		#判断 member 元素是否是集合 key 的成员
(integer) 1

#####################################################

127.0.0.1:6379> spop myset				#移除并返回集合中的一个随机元素
"xiaozhang"
127.0.0.1:6379> sadd myset "xiaozhang"
(integer) 1

#####################################################

127.0.0.1:6379> srandmember myset			#返回集合中一个或多个随机数
"xiaoyu"
127.0.0.1:6379> srandmember myset
"xiaoyu"
127.0.0.1:6379> srandmember myset
"xiaozhang"

#####################################################

127.0.0.1:6379> srem myset "xiaozhang"		#移除集合中一个或多个成员
(integer) 1
127.0.0.1:6379> sadd myset "xiaozhang"
(integer) 1
127.0.0.1:6379> sadd myset2 "haha"
(integer) 1

#####################################################

127.0.0.1:6379> sunion myset myset2			#返回所有给定集合的并集
1) "xiaozhang"
2) "xiaoyu"
3) "haha"

#####################################################

127.0.0.1:6379> sscan myset 0				#迭代集合中的元素
1) "0"
2) 1) "xiaozhang"
   2) "xiaoyu"
127.0.0.1:6379> sscan myset 1
1) "0"
2) 1) "xiaoyu"
127.0.0.1:6379> sscan myset 0
1) "0"
2) 1) "xiaozhang"
   2) "xiaoyu"
127.0.0.1:6379> sscan myset 0 match R*
1) "0"
2) (empty list or set)

#####################################################
```



#### 4、Hash

Map集合，key-Map集合==》key-<key,value>。

```bash
#############################################

127.0.0.1:6379> hset myhash name "xiaozhang"	#将哈希表 key 中的字段 field 的值设为 value 。
(integer) 1
127.0.0.1:6379> hset myhash aeg "23"
(integer) 1

#############################################

127.0.0.1:6379> hget myhash name			#获取存储在哈希表中指定字段的值。
"xiaozhang"

#############################################

127.0.0.1:6379> hkeys myhash				#获取所有哈希表中的字段
1) "name"
2) "aeg"

#############################################

127.0.0.1:6379> hvals myhash				#获取哈希表中所有值。
1) "xiaozhang"
2) "23"

#############################################

127.0.0.1:6379> hexists myhash name			#查看哈希表 key 中，指定的字段是否存在。
(integer) 1

#############################################

127.0.0.1:6379> hgetall myhash				#获取在哈希表中指定 key 的所有字段和值
1) "name"
2) "xiaozhang"
3) "aeg"
4) "23"

#############################################

127.0.0.1:6379> hlen myhash					#获取哈希表中字段的数量
(integer) 2
127.0.0.1:6379> hmget myhash name age
1) "xiaozhang"
2) (nil)

#############################################

127.0.0.1:6379> hmget myhash name			#获取所有给定字段的值
1) "xiaozhang"
127.0.0.1:6379> hmget myhash age
1) (nil)

#############################################

127.0.0.1:6379> hmset myhash age "24" addr "henan"	#同时将多个 field-value (域-值)对设置到哈希表 key 中
OK

#############################################

127.0.0.1:6379> hsetnx myhash age "23"		#只有在字段 field 不存在时，设置哈希表字段的值。
(integer) 0

#############################################

127.0.0.1:6379> hdel myhash aeg			#删除一个或多个哈希表字段
(integer) 1
127.0.0.1:6379> hgetall myhash
1) "name"
2) "xiaozhang"
3) "age"
4) "24"
5) "addr"
6) "henan"

#############################################
```



#### 5、Zset(有序集合)

再set的基础上，增加了一个值，即`set k1 score1 v1 `有点像list和set的结合体。

```bash
##################################################

127.0.0.1:6379> zadd myset 1 one	#添加一个值
(integer) 1
127.0.0.1:6379> zadd myset 2 two 3 three	#添加多个值
(integer) 2
127.0.0.1:6379> zrange myset 0 -1
1) "one"
2) "two"
3) "three"

##################################################

127.0.0.1:6379> zadd salary 3000 xiaozhang			#设置三个用户的工资
(integer) 1
127.0.0.1:6379> zadd salary 2500 xiaoyu
(integer) 1
127.0.0.1:6379> zrangebyscore salary -inf +inf withscores	#按照工资从低到高查询全部
1) "xiaoyu"
2) "2500"
3) "xiaozhang"
4) "3000"
127.0.0.1:6379> zrangebyscore salary -inf 2500 withscores
1) "xiaoyu"
2) "2500"

##################################################

127.0.0.1:6379> zrange salary 0 -1 withscores
1) "xiaoyu"
2) "2500"
3) "xiaozhang"
4) "3000"
127.0.0.1:6379> zrem salary xiaoyu				#移除指定用户
(integer) 1
127.0.0.1:6379> zrange salary 0 -1 withscores
1) "xiaozhang"
2) "3000"

##################################################

127.0.0.1:6379> zrank salary xiaoyu		#获取xiaoyu的索引
(integer) 0
127.0.0.1:6379> zrank salary zhangsan
(integer) 2
127.0.0.1:6379> zrange salary 0 -1 withscores
1) "xiaoyu"
2) "2500"
3) "xiaozhang"
4) "3000"
5) "zhangsan"
6) "5000"
7) "wangwu"
8) "6000"
127.0.0.1:6379> zremrangebyscore salary 2600 3000	#移除scores2600-3000的用户
(integer) 1
127.0.0.1:6379> zrange salary 0 -1 withscores
1) "xiaoyu"
2) "2500"
3) "zhangsan"
4) "5000"
5) "wangwu"
6) "6000"

##################################################
```



### 三种特殊类型

#### geospatial地理位置

朋友的定位、附近的人、打车距离计算

Redis的Geo，可以推算出地理位置信息，两地之间的距离，方圆几里的人。

相关命令

- GEOADD   
- GEODIST 
- GEOHASH
- GEOPOS 
- GEORADIUS   
- GEORADIUSBYMEMBER 

> geoadd

```bash
#添加地理位置
#地球的两极无法添加，一般会下载城市数据，直接通过Java程序直接导入。
#有效的经度从-180度到180度。
#有效的纬度从-85.05112878度到85.05112878度。
geoadd key value(经度、纬度、名称) ...
127.0.0.1:6379> geoadd china:city 114.66 33.65 zhoukou
(integer) 1
127.0.0.1:6379> geoadd china:city 113.65 34.72 zhengzhou
(integer) 1
127.0.0.1:6379> geoadd china:city 115.61 34.44 shangqiu
(integer) 1
```

> geopos

获得当前定位：一定是一个坐标值

```bash
#GEOPOS 命令返回一个数组， 数组中的每个项都由两个元素组成： 第一个元素为给定位置元素的经度， 而第二个元素则为给定位置元素的纬度。当给定的位置元素不存在时， 对应的数组项为空值。
geopos china:city member
127.0.0.1:6379> geopos china:city beijing
1) 1) "116.23000055551528931"
   2) "40.2200010338739844"
```

> geodist

两人之间的距离！

```bash
#返回两个给定位置之间的距离。

#如果两个位置之间的其中一个不存在， 那么命令返回空值。

#指定单位的参数 unit 必须是以下单位的其中一个：
#    m 表示单位为米。
#    km 表示单位为千米。
#    mi 表示单位为英里。
#    ft 表示单位为英尺。

127.0.0.1:6379> geodist china:city shangqiu kaifeng
"121729.6375"
127.0.0.1:6379> geodist china:city shangqiu kaifeng km
"121.7296"
```

> georadius

以给定的经纬度为中心， 返回键包含的位置元素当中， 与中心的距离不超过给定最大距离的所有位置元素。

范围可以使用以下其中一个单位：

- **m** 表示单位为米。
- **km** 表示单位为千米。
- **mi** 表示单位为英里。
- **ft** 表示单位为英尺。

在给定以下可选项时， 命令会返回额外的信息：

- `WITHDIST`: 在返回位置元素的同时， 将位置元素与中心之间的距离也一并返回。 距离的单位和用户给定的范围单位保持一致。
- `WITHCOORD`: 将位置元素的经度和维度也一并返回。
- `WITHHASH`: 以 52 位有符号整数的形式， 返回位置元素经过原始 geohash 编码的有序集合分值。 这个选项主要用于底层应用或者调试， 实际中的作用并不大。

命令默认返回未排序的位置元素。 通过以下两个参数， 用户可以指定被返回位置元素的排序方式：

- `ASC`: 根据中心的位置， 按照从近到远的方式返回位置元素。
- `DESC`: 根据中心的位置， 按照从远到近的方式返回位置元素。

```bash
127.0.0.1:6379> 
127.0.0.1:6379> georadius china:city 114.66 33.65 500 km withcoord withdist
1) 1) "shangqiu"
   2) "124.0415"
   3) 1) "115.61000257730484009"
      2) "34.4400003325985935"
2) 1) "zhengzhou"
   2) "150.9939"
   3) 1) "113.64999979734420776"
      2) "34.72000084018613109"
3) 1) "kaifeng"
   2) "129.9637"
   3) 1) "114.34999734163284302"
      2) "34.78999969972243633"
##############################################################
127.0.0.1:6379> georadius china:city 114.66 33.65 500 km withcoord withdist desc
1) 1) "zhengzhou"
   2) "150.9939"
   3) 1) "113.64999979734420776"
      2) "34.72000084018613109"
2) 1) "kaifeng"
   2) "129.9637"
   3) 1) "114.34999734163284302"
      2) "34.78999969972243633"
3) 1) "shangqiu"
   2) "124.0415"
   3) 1) "115.61000257730484009"
      2) "34.4400003325985935"
```

> georadiusbymember

这个命令和 GEORADIUS 命令一样， 都可以找出位于指定范围内的元素， 但是 `GEORADIUSBYMEMBER` 的中心点是由给定的位置元素决定的， 而不是像 GEORADIUS 那样， 使用输入的经度和纬度来决定中心点。指定成员的位置被用作查询的中心。

```bash
127.0.0.1:6379> georadiusbymember china:city shangqiu 500 km withcoord withdist asc
1) 1) "shangqiu"
   2) "0.0000"
   3) 1) "115.61000257730484009"
      2) "34.4400003325985935"
2) 1) "kaifeng"
   2) "121.7296"
   3) 1) "114.34999734163284302"
      2) "34.78999969972243633"
3) 1) "zhengzhou"
   2) "182.1687"
   3) 1) "113.64999979734420776"
      2) "34.72000084018613109"
```

> geohash(了解即可)

返回一个或多个位置元素的 Geohash表示。**（相当于把经纬度转换为11位字符串）**

```bash
127.0.0.1:6379> geohash china:city shangqiu
1) "ww45yv8es30"
```

> GEO的底层实现原理是Zset!可以使用Zset命令操作GEO

```bash
127.0.0.1:6379> zrange china:city 0 -1
1) "hangzhou"
2) "shangqiu"
3) "zhengzhou"
4) "kaifeng"
5) "beijing"
127.0.0.1:6379> zrem china:city beijing
(integer) 1
```



#### Hyperloglog

基数统计的算法！

> 什么是基数？基数就是不重复的元素。

A{1，2，3，4，5，6}  基数？ 6

A{1，2，，3，，2，3}  基数？ 1	

**优点**：占用的内存是固定的，2^64不同的元素，只需要12kb的内存！

![image-20210520172049570](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210520172049570.png)

```bash
127.0.0.1:6379> pfadd my a b c d e f g
(integer) 1
127.0.0.1:6379> pfcount my
(integer) 7
127.0.0.1:6379> pfadd my2 g t y w r 
(integer) 1
127.0.0.1:6379> pfcount my2
(integer) 4
127.0.0.1:6379> pfcount my my2
(integer) 10
127.0.0.1:6379> pfmerge my3 my my2		#合并my和my2为my3
OK
127.0.0.1:6379> pfcount my3
(integer) 10
```



#### BitMaps

![image-20210520190059659](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210520190059659.png)

使用bitmap记录一周的打卡。

![image-20210520185425494](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210520185425494.png)

```bash
127.0.0.1:6379> setbit daka 1 0	
(integer) 0
127.0.0.1:6379> setbit daka 2 1
(integer) 0
127.0.0.1:6379> setbit daka 3 0
(integer) 0
127.0.0.1:6379> setbit daka 4 1
(integer) 0
127.0.0.1:6379> setbit daka 5 1
(integer) 0
127.0.0.1:6379> setbit daka 6 1
(integer) 0
127.0.0.1:6379> setbit daka 0 1
(integer) 0
127.0.0.1:6379> getbit daka 6		#查看周6是否打卡
(integer) 1
127.0.0.1:6379> bitcount daka		#统计打卡天数
(integer) 5
```



### 事务

redis事务本质：就是一组命令的集合！一个事务中所有的命令都会被序列化，在事务执行的过程中，按照顺序执行。一次性、排他性、顺序性！执行一些列的命令！

redis的所有命令再事务中，并没有直接执行！只有发起执行命令的时候才会执行。Exec

**redis事务没有隔离级别的概念。**

**Redis单条命令保存原子性的，但事务不保证原子性。**

redis的事务：

- 开启事务（multi）
- 命令入队（要执行的mingling）
- 执行事务（exec）

**忘了？去看官网。**



### RedisTemplate自定义模板

```java
@Configuration
public class RedisConfig {

	//自定义的RedisTemplate的模板可以直接使用
	@Bean
	@SuppressWarnings("all")
	public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory factory) {

		//我么为了自己开发方便，一般直接使用<String,Object>
		RedisTemplate<String, Object> template = new RedisTemplate();
		template.setConnectionFactory(factory);

		//Json序列化配置
		Jackson2JsonRedisSerializer objectJackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);
		ObjectMapper om = new ObjectMapper();
		om.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
		om.enableDefaultTyping(ObjectMapper.DefaultTyping.NON_FINAL);
		objectJackson2JsonRedisSerializer.setObjectMapper(om);

		//String的序列化
		StringRedisSerializer stringRedisSerializer = new StringRedisSerializer();

		//key采用String的序列化方式
		template.setKeySerializer(stringRedisSerializer);
		//hash的key的序列化方式
		template.setHashKeySerializer(stringRedisSerializer);
		//value的序列化方式
		template.setValueSerializer(objectJackson2JsonRedisSerializer);
		//hash的value的序列化方式
		template.setHashValueSerializer(objectJackson2JsonRedisSerializer);
		template.afterPropertiesSet();

		return template;
	}

}
```

### RedisUtil

```java
@Component
public class RedisUtil {
	@Autowired
	private RedisTemplate<String, Object> redisTemplate;

	// =============================common============================

	/**
	 * 26
	 * 指定缓存失效时间
	 * 27
	 *
	 * @param key  键
	 *             28
	 * @param time 时间(秒)
	 *             29
	 * @return 30
	 */

	public boolean expire(String key, long time) {
		try {
			if (time > 0) {
				redisTemplate.expire(key, time, TimeUnit.SECONDS);
			}
			return true;
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 44
	 * 根据key 获取过期时间
	 * 45
	 *
	 * @param key 键 不能为null
	 *            46
	 * @return 时间(秒) 返回0代表为永久有效
	 * 47
	 */

	public long getExpire(String key) {
		return redisTemplate.getExpire(key, TimeUnit.SECONDS);
	}

	/**
	 * 53
	 * 判断key是否存在
	 * 54
	 *
	 * @param key 键
	 *            55
	 * @return true 存在 false不存在
	 * 56
	 */

	public boolean hasKey(String key) {
		try {
			return redisTemplate.hasKey(key);
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 67
	 * 删除缓存
	 * 68
	 *
	 * @param key 可以传一个值 或多个
	 *            69
	 */

	@SuppressWarnings("unchecked")
	public void del(String... key) {
		if (key != null && key.length > 0) {
			if (key.length == 1) {
				redisTemplate.delete(key[0]);
			} else {
				redisTemplate.delete((Collection<String>) CollectionUtils.arrayToList(key));
			}
		}
	}

	// ============================String=============================

	/**
	 * 83
	 * 普通缓存获取
	 * 84
	 *
	 * @param key 键
	 *            85
	 * @return 值
	 * 86
	 */

	public Object get(String key) {
		return key == null ? null : redisTemplate.opsForValue().get(key);
	}

	/**
	 * 92
	 * 普通缓存放入
	 * 93
	 *
	 * @param key   键
	 *              94
	 * @param value 值
	 *              95
	 * @return true成功 false失败
	 * 96
	 */

	public boolean set(String key, Object value) {
		try {
			redisTemplate.opsForValue().set(key, value);
			return true;
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 109
	 * 普通缓存放入并设置时间
	 * 110
	 *
	 * @param key   键
	 *              111
	 * @param value 值
	 *              112
	 * @param time  时间(秒) time要大于0 如果time小于等于0 将设置无限期
	 *              113
	 * @return true成功 false 失败
	 * 114
	 */

	public boolean set(String key, Object value, long time) {
		try {
			if (time > 0) {
				redisTemplate.opsForValue().set(key, value, time, TimeUnit.SECONDS);
			} else {
				set(key, value);
			}
			return true;
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 130
	 * 递增
	 * 131
	 *
	 * @param key   键
	 *              132
	 * @param delta 要增加几(大于0)
	 *              133
	 * @return 134
	 */

	public long incr(String key, long delta) {
		if (delta < 0) {
			throw new RuntimeException("递增因子必须大于0");
		}
		return redisTemplate.opsForValue().increment(key, delta);
	}

	/**
	 * 143
	 * 递减
	 * 144
	 *
	 * @param key   键
	 *              145
	 * @param delta 要减少几(小于0)
	 *              146
	 * @return 147
	 */

	public long decr(String key, long delta) {
		if (delta < 0) {
			throw new RuntimeException("递减因子必须大于0");
		}
		return redisTemplate.opsForValue().increment(key, -delta);
	}

	// ================================Map=================================

	/**
	 * 157
	 * HashGet
	 * 158
	 *
	 * @param key  键 不能为null
	 *             159
	 * @param item 项 不能为null
	 *             160
	 * @return 值
	 * 161
	 */

	public Object hget(String key, String item) {
		return redisTemplate.opsForHash().get(key, item);
	}

	/**
	 * 167
	 * 获取hashKey对应的所有键值
	 * 168
	 *
	 * @param key 键
	 *            169
	 * @return 对应的多个键值
	 * 170
	 */

	public Map<Object, Object> hmget(String key) {
		return redisTemplate.opsForHash().entries(key);
	}

	/**
	 * 176
	 * HashSet
	 * 177
	 *
	 * @param key 键
	 *            178
	 * @param map 对应多个键值
	 *            179
	 * @return true 成功 false 失败
	 * 180
	 */

	public boolean hmset(String key, Map<String, Object> map) {
		try {
			redisTemplate.opsForHash().putAll(key, map);
			return true;
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 192
	 * HashSet 并设置时间
	 * 193
	 *
	 * @param key  键
	 *             194
	 * @param map  对应多个键值
	 *             195
	 * @param time 时间(秒)
	 *             196
	 * @return true成功 false失败
	 * 197
	 */

	public boolean hmset(String key, Map<String, Object> map, long time) {
		try {
			redisTemplate.opsForHash().putAll(key, map);
			if (time > 0) {
				expire(key, time);
			}
			return true;
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 212
	 * 向一张hash表中放入数据,如果不存在将创建
	 * 213
	 *
	 * @param key   键
	 *              214
	 * @param item  项
	 *              215
	 * @param value 值
	 *              216
	 * @return true 成功 false失败
	 * 217
	 */

	public boolean hset(String key, String item, Object value) {
		try {
			redisTemplate.opsForHash().put(key, item, value);
			return true;
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 229
	 * 向一张hash表中放入数据,如果不存在将创建
	 * 230
	 *
	 * @param key   键
	 *              231
	 * @param item  项
	 *              232
	 * @param value 值
	 *              233
	 * @param time  时间(秒) 注意:如果已存在的hash表有时间,这里将会替换原有的时间
	 *              234
	 * @return true 成功 false失败
	 * 235
	 */

	public boolean hset(String key, String item, Object value, long time) {
		try {
			redisTemplate.opsForHash().put(key, item, value);
			if (time > 0) {
				expire(key, time);
			}
			return true;
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 250
	 * 删除hash表中的值
	 * 251
	 *
	 * @param key  键 不能为null
	 *             252
	 * @param item 项 可以使多个 不能为null
	 *             253
	 */

	public void hdel(String key, Object... item) {
		redisTemplate.opsForHash().delete(key, item);
	}

	/**
	 * 259
	 * 判断hash表中是否有该项的值
	 * 260
	 *
	 * @param key  键 不能为null
	 *             261
	 * @param item 项 不能为null
	 *             262
	 * @return true 存在 false不存在
	 * 263
	 */

	public boolean hHasKey(String key, String item) {
		return redisTemplate.opsForHash().hasKey(key, item);
	}

	/**
	 * 269
	 * hash递增 如果不存在,就会创建一个 并把新增后的值返回
	 * 270
	 *
	 * @param key  键
	 *             271
	 * @param item 项
	 *             272
	 * @param by   要增加几(大于0)
	 *             273
	 * @return 274
	 */

	public double hincr(String key, String item, double by) {
		return redisTemplate.opsForHash().increment(key, item, by);
	}

	/**
	 * 280
	 * hash递减
	 * 281
	 *
	 * @param key  键
	 *             282
	 * @param item 项
	 *             283
	 * @param by   要减少记(小于0)
	 *             284
	 * @return 285
	 */

	public double hdecr(String key, String item, double by) {
		return redisTemplate.opsForHash().increment(key, item, -by);
	}

	// ============================set=============================

	/**
	 * 292
	 * 根据key获取Set中的所有值
	 * 293
	 *
	 * @param key 键
	 *            294
	 * @return 295
	 */

	public Set<Object> sGet(String key) {
		try {
			return redisTemplate.opsForSet().members(key);
		} catch (Exception e) {
			e.printStackTrace();
			return null;
		}
	}

	/**
	 * 306
	 * 根据value从一个set中查询,是否存在
	 * 307
	 *
	 * @param key   键
	 *              308
	 * @param value 值
	 *              309
	 * @return true 存在 false不存在
	 * 310
	 */

	public boolean sHasKey(String key, Object value) {
		try {
			return redisTemplate.opsForSet().isMember(key, value);
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 321
	 * 将数据放入set缓存
	 * 322
	 *
	 * @param key    键
	 *               323
	 * @param values 值 可以是多个
	 *               324
	 * @return 成功个数
	 * 325
	 */

	public long sSet(String key, Object... values) {
		try {
			return redisTemplate.opsForSet().add(key, values);
		} catch (Exception e) {
			e.printStackTrace();
			return 0;
		}
	}

	/**
	 * 336
	 * 将set数据放入缓存
	 * 337
	 *
	 * @param key    键
	 *               338
	 * @param time   时间(秒)
	 *               339
	 * @param values 值 可以是多个
	 *               340
	 * @return 成功个数
	 * 341
	 */

	public long sSetAndTime(String key, long time, Object... values) {
		try {
			Long count = redisTemplate.opsForSet().add(key, values);
			if (time > 0)
				expire(key, time);
			return count;
		} catch (Exception e) {
			e.printStackTrace();
			return 0;
		}
	}

	/**
	 * 355
	 * 获取set缓存的长度
	 * 356
	 *
	 * @param key 键
	 *            357
	 * @return 358
	 */

	public long sGetSetSize(String key) {
		try {
			return redisTemplate.opsForSet().size(key);
		} catch (Exception e) {
			e.printStackTrace();
			return 0;
		}
	}
	/**
	 * 369
	 * 移除值为value的
	 * 370
	 *
	 * @param key    键
	 *               371
	 * @param values 值 可以是多个
	 *               372
	 * @return 移除的个数
	 * 373
	 */

	public long setRemove(String key, Object... values) {
		try {
			Long count = redisTemplate.opsForSet().remove(key, values);
			return count;
		} catch (Exception e) {
			e.printStackTrace();
			return 0;

		}

	}

	// ===============================list=================================

	/**
	 * 386
	 * 获取list缓存的内容
	 * 387
	 *
	 * @param key   键
	 *              388
	 * @param start 开始
	 *              389
	 * @param end   结束 0 到 -1代表所有值
	 *              390
	 * @return 391
	 */

	public List<Object> lGet(String key, long start, long end) {
		try {
			return redisTemplate.opsForList().range(key, start, end);
		} catch (Exception e) {
			e.printStackTrace();
			return null;
		}
	}

	/**
	 * 402
	 * 获取list缓存的长度
	 * 403
	 *
	 * @param key 键
	 *            404
	 * @return 405
	 */

	public long lGetListSize(String key) {
		try {
			return redisTemplate.opsForList().size(key);
		} catch (Exception e) {
			e.printStackTrace();
			return 0;
		}
	}

	/**
	 * 416
	 * 通过索引 获取list中的值
	 * 417
	 *
	 * @param key   键
	 *              418
	 * @param index 索引 index>=0时， 0 表头，1 第二个元素，依次类推；index<0时，-1，表尾，-2倒数第二个元素，依次类推
	 *              419
	 * @return 420
	 */

	public Object lGetIndex(String key, long index) {
		try {
			return redisTemplate.opsForList().index(key, index);
		} catch (Exception e) {
			e.printStackTrace();
			return null;
		}
	}

	/**
	 * 431
	 * 将list放入缓存
	 * 432
	 *
	 * @param key   键
	 *              433
	 * @param value 值
	 *              434
	 * @return 436
	 */

	public boolean lSet(String key, Object value) {
		try {
			redisTemplate.opsForList().rightPush(key, value);
			return true;
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 将list放入缓存
	 *
	 * @param key   键
	 * @param value 值
	 * @param time  时间(秒)
	 * @return
	 */

	public boolean lSet(String key, Object value, long time) {
		try {
			redisTemplate.opsForList().rightPush(key, value);
			if (time > 0)
				expire(key, time);
			return true;
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 467
	 * 将list放入缓存
	 * 468
	 *
	 * @param key   键
	 *              469
	 * @param value 值
	 *              470
	 * @return 472
	 */

	public boolean lSet(String key, List<Object> value) {
		try {
			redisTemplate.opsForList().rightPushAll(key, value);
			return true;
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 484
	 * 将list放入缓存
	 * 485
	 * <p>
	 * 486
	 *
	 * @param key   键
	 *              487
	 * @param value 值
	 *              488
	 * @param time  时间(秒)
	 *              489
	 * @return 490
	 */

	public boolean lSet(String key, List<Object> value, long time) {
		try {
			redisTemplate.opsForList().rightPushAll(key, value);
			if (time > 0)
				expire(key, time);
			return true;
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 504
	 * 根据索引修改list中的某条数据
	 * 505
	 *
	 * @param key   键
	 *              506
	 * @param index 索引
	 *              507
	 * @param value 值
	 *              508
	 * @return 509
	 */

	public boolean lUpdateIndex(String key, long index, Object value) {
		try {
			redisTemplate.opsForList().set(key, index, value);
			return true;
		} catch (Exception e) {
			e.printStackTrace();
			return false;
		}
	}

	/**
	 * 521
	 * 移除N个值为value
	 * 522
	 *
	 * @param key   键
	 *              523
	 * @param count 移除多少个
	 *              524
	 * @param value 值
	 *              525
	 * @return 移除的个数
	 * 526
	 */

	public long lRemove(String key, long count, Object value) {
		try {
			Long remove = redisTemplate.opsForList().remove(key, count, value);
			return remove;
		} catch (Exception e) {
			e.printStackTrace();
			return 0;
		}
	}
}
```



### Redis.conf详解

启动的时候通过配置文件启动！

> 单位

![image-20210521101228466](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521101228466.png)1、**配置文件文件unit单位对大小写不敏感。**

> 包含

![image-20210521101457084](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521101457084.png)

就好比spring的import、include。**可以导入其他的配置文件。**

> 网络配置

```bash
bind 127.0.0.1		#绑定的ip
protected-mode yes	#是否受保护的，一般要开启。
port 6379			#端口
```

![image-20210521101953470](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521101953470.png)



> 通用配置

```bash
daemonize yes		#守护线程，yes是以守护进程的方式后台运行  默认no 
pidfile /var/run/redis_6379.pid	#如果以后台运行的方式，我们那就需要指定一个pid文件。

#日志
# Specify the server verbosity level.
# This can be one of:
# debug (a lot of information, useful for development/testing)
# verbose (many rarely useful info, but not a mess like the debug level)
# notice (moderately verbose, what you want in production probably)生产环境使用
# warning (only very important / critical messages are logged)
loglevel notice		#日志级别
logfile ""			#生成的日志文件名
databases 16		#默认16个数据库
always-show-logo yes	#是否总是显示redis的logo

```

> 快照

持久化，在规定的时间内，执行了多少次操作，则会持久化到文件 .rdb  和 .aof

redis是内存数据库，断电既失。如果没有持久化数据库就会消失。

```bash
#如果900s内，至少有一个key进行了修改，我们就进行持久化操作。
save 900 1
#如果300s内，至少有10个key进行了修改，我们就进行持久化操作。
save 300 10
#如果60s内，至少有10000个key进行了修改，我们就进行持久化操作。
save 60 10000

stop-writes-on-bgsave-error yes		#持久化工作出现错误是，是否继续工作
rdbcompression yes					#是否压缩rdb文件，需要消耗cpu的资源。
rdbchecksum yes						#保存rdb文件的时候，是否进行错误的检查校验。
dir ./								#保存文件的路径，默认当前目录下。
```



> Replication  复制





> 安全Security



![image-20210521104456158](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521104456158.png)



> 限制

```bash
# maxclients 10000		#设置能连接redis的最大的客户端数量
# maxmemory <bytes>		#redis最大内存容量
# maxmemory-policy noeviction	#内存满了之后的处理策略。
```





> APPEND ONLY 模式  aof配置

```bash
appendonly no			#默认不开启aof的配置，默认使用的rdb模式的进行持久化。
appendfilename "appendonly.aof"		#持久化的文件的名字

# appendfsync always				每次修改都会同步  消耗性能
appendfsync everysec				#每秒都同步一下
# appendfsync no					不会同步
```



### 持久化



#### RDB(redis Database)

> 什么是RDB？

![image-20210521113806570](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521113806570.png)

![image-20210521113920340](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521113920340.png)



![image-20210521113242145](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521113242145.png)

基本上默认的配置就够用了！

**RDB的优点**

- RDB是一个非常紧凑的文件,它保存了某个时间点得数据集,非常适用于数据集的备份,比如你可以在每个小时报保存一下过去24小时内的数据,同时每天保存过去30天的数据,这样即使出了问题你也可以根据需求恢复到不同版本的数据集.
- RDB是一个紧凑的单一文件,很方便传送到另一个远端数据中心或者亚马逊的S3（可能加密），非常适用于灾难恢复.
- RDB在保存RDB文件时父进程唯一需要做的就是fork出一个子进程,接下来的工作全部由子进程来做，父进程不需要再做其他IO操作，所以RDB持久化方式可以最大化redis的性能.
- 与AOF相比,在恢复大的数据集的时候，RDB方式会更快一些.
- **RDB的缺点**
- 如果你希望在redis意外停止工作（例如电源中断）的情况下丢失的数据最少的话，那么RDB不适合你.虽然你可以配置不同的save时间点(例如每隔5分钟并且对数据集有100个写的操作),是Redis要完整的保存整个数据集是一个比较繁重的工作,你通常会每隔5分钟或者更久做一次完整的保存,万一在Redis意外宕机,你可能会丢失几分钟的数据.
- RDB  需要经常fork子进程来保存数据集到硬盘上,当数据集比较大的时候,fork的过程是非常耗时的,可能会导致Redis在一些毫秒级内不能响应客户端的请求.如果数据集巨大并且CPU性能不是很好的情况下,这种情况会持续1秒,AOF也需要fork,但是你可以调节重写日志文件的频率来提高数据集的耐久度.

![image-20210521113722044](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521113722044.png)



#### AOF（Append Only File）

**将我们所有的命令都记录下来！history,恢复的时候就是把这个文件里的命令执行一遍。**

![image-20210521144616920](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521144616920.png)

AOF持久化方式记录每次对服务器写的操作,当服务器重启的时候会重新执行这些命令来恢复原始的数据,AOF命令以redis协议追加保存每次写的操作到文件末尾.Redis还能对AOF文件进行后台重写,使得AOF文件的体积不至于过大.

**Aof保存的是appendonly.aof文件**

![image-20210521150821177](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521150821177.png)

默认是不开启的，我们只需要将appendonly  yes。重启redis既可以生效。

如果aof文件有错误就会导致无法启动redis，我们需要修复这个aof文件`redis-check-aof --fix appendonly.aof`。

**AOF 优点**

- 使用AOF 会让你的Redis更加耐久:  你可以使用不同的fsync策略：无fsync,每秒fsync,每次写的时候fsync.使用默认的每秒fsync策略,Redis的性能依然很好(fsync是由后台线程进行处理的,主线程会尽力处理客户端请求),一旦出现故障，你最多丢失1秒的数据.
- AOF文件是一个只进行追加的日志文件,所以不需要写入seek,即使由于某些原因(磁盘空间已满，写的过程中宕机等等)未执行完整的写入命令,你也也可使用redis-check-aof工具修复这些问题.
- Redis 可以在 AOF 文件体积变得过大时，自动地在后台对 AOF 进行重写： 重写后的新 AOF  文件包含了恢复当前数据集所需的最小命令集合。 整个重写操作是绝对安全的，因为 Redis 在创建新 AOF  文件的过程中，会继续将命令追加到现有的 AOF 文件里面，即使重写过程中发生停机，现有的 AOF 文件也不会丢失。 而一旦新 AOF  文件创建完毕，Redis 就会从旧 AOF 文件切换到新 AOF 文件，并开始对新 AOF 文件进行追加操作。
- AOF 文件有序地保存了对数据库执行的所有写入操作， 这些写入操作以 Redis 协议的格式保存， 因此 AOF  文件的内容非常容易被人读懂， 对文件进行分析（parse）也很轻松。 导出（export） AOF 文件也非常简单： 举个例子，  如果你不小心执行了 FLUSHALL 命令， 但只要 AOF 文件未被重写， 那么只要停止服务器， 移除 AOF 文件末尾的 FLUSHALL  命令， 并重启 Redis ， 就可以将数据集恢复到 FLUSHALL 执行之前的状态。

**AOF 缺点**

- 对于相同的数据集来说，AOF 文件的体积通常要大于 RDB 文件的体积。
- 根据所使用的 fsync 策略，AOF 的速度可能会慢于 RDB 。 在一般情况下， 每秒 fsync 的性能依然非常高， 而关闭  fsync 可以让 AOF 的速度和 RDB 一样快， 即使在高负荷之下也是如此。 不过在处理巨大的写入载入时，RDB  可以提供更有保证的最大延迟时间（latency）。



### Redis发布订阅

Redis 发布订阅 (pub/sub) 是一种消息通信模式：发送者 (pub) 发送消息，订阅者 (sub) 接收消息。

Redis 客户端可以订阅任意数量的频道。

下图展示了频道 channel1 ， 以及订阅这个频道的三个客户端 —— client2 、 client5 和 client1 之间的关系：

![img](https://www.runoob.com/wp-content/uploads/2014/11/pubsub1.png)

当有新消息通过 PUBLISH 命令发送给频道 channel1 时， 这个消息就会被发送给订阅它的三个客户端：

![img](https://www.runoob.com/wp-content/uploads/2014/11/pubsub2.png)

------



以下实例演示了发布订阅是如何工作的，需要开启两个 redis-cli 客户端。

在我们实例中我们创建了订阅频道名为 **xiaozhangshuo**:

**第一个 redis-cli 客户端**

```bash
redis 127.0.0.1:6379> subscribe xiaozhangshuo

Reading messages... (press Ctrl-C to quit)
1) "subscribe"
2) "redisChat"
3) (integer) 1
```

现在，我们先重新开启个 redis 客户端，然后在同一个频道 runoobChat 发布两次消息，订阅者就能接收到消息。

**第二个 redis-cli 客户端**

```bash
redis 127.0.0.1:6379> publish xiaozhangshuo "Redis PUBLISH test"
(integer) 1
redis 127.0.0.1:6379> publish xiaozhangshuo "Learn redis by runoob.com"
(integer) 1

# 订阅者的客户端会显示如下消息
1) "message"			#消息
2) "xiaozhangshuo"			#哪个频道
3) "Redis PUBLISH test"			#消息的具体内容
1) "message"
2) "xiaozhangshuo"
3) "Learn redis by runoob.com"
```

![image-20210521164717302](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521164717302.png)

**使用场景：**

1、实时消息系统！

2、实时聊天！（频道当作聊天室，将信息回显给所有人即可）

3、订阅、关注系统！

复杂场景使用MQ（消息中间件）



### Redis主从复制

![image-20210521170357339](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521170357339.png)



![image-20210521170935576](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521170935576.png)

主从复制，读写分离！80%的情况下都是读的操作！减缓服务器的压力。架构中经常使用。

```bash
127.0.0.1:6379> info replication		#查看复制信息
# Replication
role:master
connected_slaves:0			#连接的从机
master_replid:7ea24aa9388ad35fe5fc649984d4e92bb5869b05
master_replid2:0000000000000000000000000000000000000000
master_repl_offset:0
second_repl_offset:-1
repl_backlog_active:0
repl_backlog_size:1048576
repl_backlog_first_byte_offset:0
repl_backlog_histlen:0
```



一主从二：

**默认情况下，每台Redis服务器都是主节点！一般情况下我们只配置从机**

通过命令配置（暂时的）：

```bash
slaveof 127.0.0.1 6379		#设置为谁的从机
```

真实的配置是在配置文件中（永久的配置）。

**细节：**

1、主机负责写，从机负责读。

2、主机中的数据都会被从机保存。

3、主机断开后，从机依旧连接主机，但是没有写操作，这个时候主机开机后写入数据，从机依旧可以获得消息。

4、如果使用命令行来配置主从，从机重启了就会变成主机！



![image-20210521180703759](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521180703759.png)

> 从机改为主机

主机断开后，我们可以使用`slaveof no one`是自己变成主机。

![image-20210521181526283](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521181526283.png)



### 哨兵模式（重点）

![image-20210521182447799](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521182447799.png)

Redis 的 **Sentinel**（哨兵） 系统用于管理多个 Redis 服务器（instance）， 该系统执行以下三个任务：

- **监控（Monitoring**）： Sentinel 会不断地检查你的主服务器和从服务器是否运作正常。
- **提醒（Notification）**： 当被监控的某个 Redis 服务器出现问题时， Sentinel 可以通过 API 向管理员或者其他应用程序发送通知。
- **自动故障迁移（Automatic failover）**： 当一个主服务器不能正常工作时，  Sentinel 会开始一次自动故障迁移操作， 它会将失效主服务器的其中一个从服务器升级为新的主服务器，  并让失效主服务器的其他从服务器改为复制新的主服务器； 当客户端试图连接失效的主服务器时， 集群也会向客户端返回新主服务器的地址，  使得集群可以使用新主服务器代替失效服务器。



![image-20210521182623243](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521182623243.png)

![image-20210521182832116](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521182832116.png)

![image-20210521183039267](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521183039267.png)

> 哨兵配置文件

```bash
sentinel monitor mymaster 127.0.0.1 6379 2	
sentinel down-after-milliseconds mymaster 60000
sentinel failover-timeout mymaster 180000
sentinel parallel-syncs mymaster 1
```

- 第一行配置指示 Sentinel 去监视一个名为 mymaster 的主服务器， 这个主服务器的 IP 地址为 127.0.0.1 ， 端口号为 6379 ， 而将这个主服务器判断为失效至少需要 2 个 Sentinel 同意 （只要同意 Sentinel 的数量不达标，自动故障迁移就不会执行）。

- **down-after-milliseconds** 选项指定了 Sentinel 认为服务器已经断线所需的毫秒数。如果服务器在给定的毫秒数之内， 没有返回 Sentinel 发送的 PING 命令的回复， 或者返回一个错误， 那么 Sentinel 将这个服务器标记为主观下线

- **parallel-syncs** 选项指定了在执行故障转移时， 最多可以有多少个从服务器同时对新的主服务器进行同步， 这个数字越小， 完成故障转移所需的时间就越长。

启动哨兵：

```bash
redis-sentinel zhangConfig/sentinel.conf
```

![image-20210521211503970](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521211503970.png)



优点：

1、哨兵集群，是基于主从复制模式，所有的主从配置的优点哨兵都有

2、主从可以切换，故障可以转移。系统的可用性就会更好。

3、就是主从复制模式的升级。

缺点：

1、redis不好在线扩容，集群容量一旦达到上限，在线扩容就十分麻烦。

2、实现哨兵模式的配置其实很麻烦。



> 哨兵的配置！

```bash
# Example sentinel.conf
 
# 哨兵sentinel实例运行的端口 默认26379
port 26379
 
# 哨兵sentinel的工作目录
dir /tmp
 
# 哨兵sentinel监控的redis主节点的 ip port 
# master-name  可以自己命名的主节点名字 只能由字母A-z、数字0-9 、这三个字符".-_"组成。
# quorum 当这些quorum个数sentinel哨兵认为master主节点失联 那么这时 客观上认为主节点失联了
# sentinel monitor <master-name> <ip> <redis-port> <quorum>
  sentinel monitor mymaster 127.0.0.1 6379 2
 
# 当在Redis实例中开启了requirepass foobared 授权密码 这样所有连接Redis实例的客户端都要提供密码
# 设置哨兵sentinel 连接主从的密码 注意必须为主从设置一样的验证密码
# sentinel auth-pass <master-name> <password>
sentinel auth-pass mymaster MySUPER--secret-0123passw0rd
 
 
# 指定多少毫秒之后 主节点没有应答哨兵sentinel 此时 哨兵主观上认为主节点下线 默认30秒
# sentinel down-after-milliseconds <master-name> <milliseconds>
sentinel down-after-milliseconds mymaster 30000
 
# 这个配置项指定了在发生failover主备切换时最多可以有多少个slave同时对新的master进行 同步，
这个数字越小，完成failover所需的时间就越长，
但是如果这个数字越大，就意味着越 多的slave因为replication而不可用。
可以通过将这个值设为 1 来保证每次只有一个slave 处于不能处理命令请求的状态。
# sentinel parallel-syncs <master-name> <numslaves>
sentinel parallel-syncs mymaster 1 
 
 
# 故障转移的超时时间 failover-timeout 可以用在以下这些方面： 
#1. 同一个sentinel对同一个master两次failover之间的间隔时间。
#2. 当一个slave从一个错误的master那里同步数据开始计算时间。直到slave被纠正为向正确的master那里同步数据时。
#3.当想要取消一个正在进行的failover所需要的时间。  
#4.当进行failover时，配置所有slaves指向新的master所需的最大时间。不过，即使过了这个超时，slaves依然会被正确配置为指向master，但是就不按parallel-syncs所配置的规则来了
# 默认三分钟
# sentinel failover-timeout <master-name> <milliseconds>
sentinel failover-timeout mymaster 180000
 
# SCRIPTS EXECUTION
 
#配置当某一事件发生时所需要执行的脚本，可以通过脚本来通知管理员，例如当系统运行不正常时发邮件通知相关人员。
#对于脚本的运行结果有以下规则：
#若脚本执行后返回1，那么该脚本稍后将会被再次执行，重复次数目前默认为10
#若脚本执行后返回2，或者比2更高的一个返回值，脚本将不会重复执行。
#如果脚本在执行过程中由于收到系统中断信号被终止了，则同返回值为1时的行为相同。
#一个脚本的最大执行时间为60s，如果超过这个时间，脚本将会被一个SIGKILL信号终止，之后重新执行。
 
#通知型脚本:当sentinel有任何警告级别的事件发生时（比如说redis实例的主观失效和客观失效等等），将会去调用这个脚本，
这时这个脚本应该通过邮件，SMS等方式去通知系统管理员关于系统不正常运行的信息。调用该脚本时，将传给脚本两个参数，
一个是事件的类型，
一个是事件的描述。
如果sentinel.conf配置文件中配置了这个脚本路径，那么必须保证这个脚本存在于这个路径，并且是可执行的，否则sentinel无法正常启动成功。
#通知脚本
# sentinel notification-script <master-name> <script-path>
  sentinel notification-script mymaster /var/redis/notify.sh
 
# 客户端重新配置主节点参数脚本
# 当一个master由于failover而发生改变时，这个脚本将会被调用，通知相关的客户端关于master地址已经发生改变的信息。
# 以下参数将会在调用脚本时传给脚本:
# <master-name> <role> <state> <from-ip> <from-port> <to-ip> <to-port>
# 目前<state>总是“failover”,
# <role>是“leader”或者“observer”中的一个。 
# 参数 from-ip, from-port, to-ip, to-port是用来和旧的master和新的master(即旧的slave)通信的
# 这个脚本应该是通用的，能被多次调用，不是针对性的。
# sentinel client-reconfig-script <master-name> <script-path>
 sentinel client-reconfig-script mymaster /var/redis/reconfig.sh
```



### Redis缓存雪崩和穿透(面试高频，工作常用！)

#### 缓存穿透（查不到导致的）

> 概念

用户想要查询一个数据，发现redis中没有，也就是缓存没有命中，于是向持久层数据库查询。发现也没有，于是本次查询失败。当用户很多时，缓存都没有命中，于是都去请求数据库。这回给持久层数据库造成很大的压力，这时候就出现了缓存穿透。

> 解决方案1

**布隆过滤器**

布隆过滤器是一种数据结构，对所有可能查询的参数以hash形式存储，在控制层先进行校验，不符合则丢弃。从而避免了对底层存储系统的查询压力。

![image-20210521215037117](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521215037117.png)

> 解决方案2

**缓存空对象**

当存储层不命中后，即使返回的空对象也将其缓存起来，同时设置一个过期时间，之后在访问这个数据将会从缓存中取，保护了后端的数据源。

![image-20210521215346798](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521215346798.png)

空对象缺点：

1、如果空值能被缓存起来，这就意味着缓存需要更多的空间存储更多的键，因为着当中可能有很多的空值的键。

2、即使对空值设置了过期时间，还是会存在缓存层和数据层的数据会有一段时间窗口的不一致，这对于需要保持一致性的业务会有影响。



#### 缓存击穿（量太大，缓存过期！）

![image-20210521220325387](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521220325387.png)



#### 缓存雪崩

![image-20210521220504533](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521220504533.png)

![image-20210521220612573](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521220612573.png)

![image-20210521220644439](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521220644439.png)



![image-20210521220913954](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210521220913954.png)

