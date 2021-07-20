



## maven可以做什么？

1. **maven可以管理jar文件**
2. **自动下载jar文件和他的文档，源代码。**
3. **管库jar之间的依赖，a.jar需要b.jar，maven会自动下载b.jar。**
4. **管理需要jar的版本。**
5. **帮你编译程序，把Java编译成class**
6. **帮你测试你的代码是否正确**
7. **帮你打包文件，生成 jar 文件或者 war 文件**
8. **帮你部署项目。**



## 构建（功能）

构建就是项目的构建。

**构建是面向过程的，就是一些步骤，完成项目代码的编译、测试运行、打包、部署等等。**

maven支持的构建包括有：

1. **清理，** 把之前项目编译的的东西删除掉，为新的代码编译做准备。

2. **编译，** 把程序源代码编译成执行代码，Java-class文件。

   ​			编译时批量的，maven可以把成千上百的文件编译为class

   ​			javac 不一样，javac一次只能编译一个文件。

3. **测试，** maven可以执行测试程序代码，验证你的功能是否正确。

   ​			批量的，maven同时执行多个测试代码，同时测试很多功能。

4. **报告，** 生成测试结果的文件，测试通过是否通过。

5. **打包，** 把你的项目中所有的class文件，配置文件等所有的资源放到一个压缩文件中，这个压缩文件就是项目的结果文件。

   ​			 通常Java程序，压缩问价是jar扩展名的

   ​			 对于web应用，压缩文件的扩展名是.war。

6. **安装，** 把打包生成的jar、war文件安装到本地仓库。

7. **部署，** 把我们的程序安装好可以执行。（此步骤一般不用，maven比较复杂）



## maven的核心概念

- **POM：**一个文件，名称pom.xml，pom翻译是**项目对象模型**。

  ​		maven把一个项目当成一个模型使用。控制maven构建项目的过程管理jar依赖。

- **约定的目录结构：**maven项目的目录和文件的位置都是规定的。

- **坐标：**是一个唯一的字符串，用来表示资源的。

- **依赖管理：**管理项目的jar文件。

- **仓库管理（了解）：**资源存放的位置

- **生命周期（了解）：**maven工具构建项目的过程，就是生命周期。

- **插件和目标（了解）：**执行maven构建的时候用的工具是插件。

- **继承：**

- **聚合：**



## maven的安装和配置

1. 官网下载maven安装包：https://maven.apache.org/  `apache-maven -3.3.9-bin.zip`使用比较广泛，结合jdk 1.8

   ![image-20210317163854096](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317163854096.png)

2. 解压安装包，解压一个非中文目录。

3. 配置环境变量，指定一个**M2_HOME**的名称，指定它的值是maven工具的安装目录，不包括bin目录。

   再把M2_HOME加入到**path**之中，在最前边加入**%M2_HOME%\bin;**

4. 验证，新的命令行中执行**mvn -v；**命令

   ![image-20210317165345473](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210317165345473.png)



## maven的目录结构

![image-20210318152113599](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210318152113599.png)

## 仓库

> 修改本地仓库的位置。

![image-20210318155025612](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210318155025612.png)

仓库的使用，maven仓库的使用不需要人为参与。

​	**开发人员需要使用MySQL驱动---> maven首先检查本地仓库---> 私服（一般公司）--->镜像(中央仓库的备份)--->中央仓库。**

## pom:项目对象模型，是一个pom.xml文件

1. 坐标：唯一值，在互联网中唯一标识一个项目的

   ```xml
   <groupID>com.xiaozhang</groupID>  #公司的名称，要倒着写
   <artifactId>hello</artifactId>		#项目的名称
   <version>1.0-SNAPSHOT</version>		#版本号 SNAPSHOT是快照
   ```

2. packaging：打包后压缩文件的扩展名，默认是jar，web应用是war。

   packaging 可以不写，默认是jar。

3. 依赖

   dependencies和dependency，相当于Java代码中import

   你的项目中要使用的各种资源说明，比我的项目要使用MySQL驱动

4. properties：设置属性

5. build：maven在进行项目的构建时，配置信息，例如指定编译Java代码使用的额版本。

## maven生命周期，maven的命令，maven的插件

- **maven的生命周期：**就是maven的构建项目的过程，清理、编译、测试、报告、打包、安装、部署。

- **maven的命令：**maven独立使用，通过命令，完成maven的生命周期

  ​							maven可以使用命令，完成项目的清理，编译等。

  - **mvn clean：**清楚class文件，target目录。
  - **mvn compile：**编译main/java/下的Java为class文件，同时把class文件拷贝到target/classes目录下。把main/resources目录下的所有文件，都拷贝到target/classes目录下。
  - mvn test-compile：编译test目录下的Java文件.
  - mvn test：测试。
  - **mvn package：**打包主程序（编译、测试、按照pom.xml文件把主程序打包成jar/war文件。）
  - **mvn install：**安装主程序（会把本地工程打包，并且按照工程的坐标保存到本地仓库中）。
  - **mvn deploy：**部署主程序（会把工程打包，按照工程的坐标保存到本地仓库，还会保存到私服仓库中，会自动把项目部署到web容器中）。

- **maven的插件：**maven命令执行时，真正完成功能的时插件，就是jar，一些类。

  ![image-20210318165300705](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210318165300705.png)

## 在IDEA中配置maven

![image-20210318170758262](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210318170758262.png)

​		**注意：改为-DarchetypeCatalog=internal**

28