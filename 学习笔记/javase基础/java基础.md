# java基础

## Java API

API(Application Programming Interface),应用程序编程接口。Java API是一本程序员的`字典`，JDK自带一些类和方法，这些类称为API。



## 面下对象的三大特征：

### 封装

封装性就是Java当中的体现：

1. 方法就是一种封装

2. 关键字private也是一种封装

   封装就是对外界一些信息隐藏起来，都外界不可见。

### 继承



### 多态



## 2、基础代码练习

### 计算数组最大值

```java
public class Demo02Method {
	public static void main(String[] args) {
		int[] array = {1,2,3,5};
		int max = getMax(array);
		System.out.println("最大值："+max);
	}

	public static  int getMax(int[] array){
		int max = array[0];

		for (int i = 1; i < array.length ;i++) {
			if (array[i] > max){
				max = array[i];
			}
		}
		return max;
	}
}
```

### 求1~100的偶数和

```java
/*求1~100的偶数和*/
public class Demo03 {
	public static void main(String[] args) {
		int sum = 0;

		for(int i = 1;i <= 100; i++){
			if (i % 2 == 0){
				sum = sum + i;
			}
		}
		System.out.println("结果为：" + sum);
	}
}
```

### 定义一个方法判断是否相等

```java
/*定义一个方法，判断两个数字是否相等。
*
* */
public class Demo05 {
	public static void main(String[] args) {

	}

	public static boolean isSame(int a,int b){
		boolean same;
		same = a == b ? true : false;  //第一种

		//boolean same  = a == b;   第二种

		//return a == b;
		return same;
	}
}
```

### 计算数组的长度

```java
/*
* 求数组的长度
* 程序运行之间，数组一旦创建就不会发生改变。
* */
public class Demo06 {
	public static void main(String[] args) {
		int[] arrayA = new int[3];

		int[] arrayB = {1,2,3,4,5,6,7,8,9,10,12,45,74,100};
		int len = arrayB.length;
		System.out.println("arrayB的长度为：" + len);
		System.out.println("=====================");

		int[] arrayC = new int[3];
		System.out.println(arrayC.length);	//3
		arrayC = new int[5];
		System.out.println(arrayC.length);	//5

	}
}
```

### 数组反转

```java
/*
* 求数组元素反转的练习。
* 本来的样子：[1,2,3,4]
* 后来的样子：[4,3,2,1]
* */
public class Demo07 {
	public static void main(String[] args) {
		int[] array = {10, 20, 30, 40, 50};
		//遍历打印数组原来的样子
		for (int i = 0; i < array.length; i++) {
			System.out.println(array[i]);
		}
		System.out.println("==============");

		/*
		* 初始化语句：int min = 0,max = array.length - 1
		* 条件判断：min < max
		* 步进表达式：min ++, max --
		* 循环体：用第三变量倒手
		* */
		for (int min = 0,max = array.length - 1; min < max; min ++,max --) {
			int temp = array[min];
			array[min] = array[max];
			array[max] = temp;
		}
		//再次打印反转后的数组
		for (int i = 0; i < array.length; i++) {
			System.out.println(array[i]);
		}

	}
}
```

### 随机数字小游戏

```java
/*
* 猜数字小游戏。
* 思路：
* 1.产生一个随机数字，并且不在变化。用Random的nextInt方法。
* 2.需要键盘输入，所以用到了Scanner
* 3.获取输入的数字，用Scanner当中的nextInt方法。
* 4.将两个数字对比，if判断
* 		如果大了，提示太大了，并且重试。
* 		如果小了，提示太小了，并且重试。
* 		如果猜中了，游戏结束。
* */
public class Demo01 {
	public static void main(String[] args) {
		Random r = new Random();
		int randomNum = r.nextInt(100) + 1;	//1~100

		Scanner sc = new Scanner(System.in);
		System.out.println("请输入你猜测的数字：");

		while (true){
			int guessNum = sc.nextInt();	//键盘输入的数字
			if (randomNum > guessNum){
				System.out.println("太小了，请重新输入：");
			}else if (randomNum < guessNum){
				System.out.println("太大了，请重新输入：");
			}else{
				System.out.println("恭喜你猜中了！！！");
				break;	//如果猜中了，不再重试
			}
		}
		System.out.println("游戏结束！！！");
	}
}
```

## 标准的学生类

```java
/*
标准的类也叫Java bean
* 一个标准的学生类：
* 1.所有的成员变量都要使用private关键字修饰
* 2.为每一个成员变量编写一对Getter和Setter方法
* 3.编写一个无参的构造方法
* 4.编写一个全参的构造方法
* */
public class Student {
	private String name;
	private int age;

	public Student(){}

	public Student(String name,int age){
		this.name = name;
		this.age = age;
	}

	public void setName(String name){
		this.name = name;
	}
	public void setAge(int age){
		this.age = age;
	}

	public String getName(){
		return name;
	}
	public int getAge(){
		return age;
	}
}
```















## 反射

就是将类的各个组成部分封装成为其他的对象，这就是反射机制。

![image-20210307210318253](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210307210318253.png)



> 获取class的三种方式

1. **Class.forName(“全类名”)：将字节码文件加载进内存，返回Class对象**
   - 多用于配置为文件，将类名定义在配置文件中。读取文件，加载类。
2. **类名.class：通过类名的属性class获取**
   - 多用于参数的传递
3. **对象.getClass()：getClass()方法在object类中定义。**
   - 多用于对象获取字节码的方式

结论：

**同一个字节码文件（*.class）在一次程序运行的过程中，只会被加载一次，不论通过哪一种方式获取的class对象都是同一个。**



### 1、Class对象功能



## 集合



> 单列集合的体系结构：

![image-20210318102054858](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210318102054858.png)







ArrayList





## io流

![image-20210324085108498](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210324085108498.png)

![image-20210324091936447](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210324091936447.png)

![image-20210324095009199](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210324095009199.png)

**注意：读取文件的时候，读到文件的末尾会返回“-1”。**

例子：复制一张图片

```java
package com.heima.Stream;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

public class Demo_3 {
    //复制一个图片
    public static void main(String[] args) throws IOException {
        FileInputStream fis = new FileInputStream("1.jpg");				//创建输入流
        FileOutputStream fos = new FileOutputStream("2.jpg");		//创建一个输出流
        int b;
        while((b = fis.read()) != -1) {
            fos.write(b);
        }
        fis.close();
        fos.close();
    }
}
```



**字符输入/输出**

![image-20210324125757800](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210324125757800.png)

注意：字符输出流是先把字符写到缓冲区中，在把缓冲区的字符转换成字节刷新到文件中。



**关闭和刷新区别：**

- flush()：刷新缓冲区，流对象可以继续使用。
- close()：先刷新缓冲区，然后通知系统释放资源。流对象不可以在使用。



**Properties集合**

唯一一个和 io 流结合使用的集合。

![image-20210324133334827](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210324133334827.png)

![image-20210324133933623](C:\Users\87766\AppData\Roaming\Typora\typora-user-images\image-20210324133933623.png)



**缓冲流**

391