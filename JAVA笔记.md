##### 什么是程序

> 程序可以看成是指令(代码)的集合，就是程序

##### JDK、JRE、JVM之间的关系

> <span style="color: green;">JDK：</span>
>   java开发工具包，包含jre和开发人员使用的工具(date，类型...，Scanner)
> <span style="color: green;">JRE：</span>
> java运行环境，包含jvm和运行所需的核心类
> <span style="color: green;">JVM：</span>
>  java运行虚拟机

##### 类和对象之间的关系

> <span style="color: red;">**对象是类的实例，类是对象的模板**</span>

##### Java面向对象编程的特性

> 封装，继承，多态，抽象

##### Java中的八大基本数据类型

> - byte（位）	1字节	-128 ~ 127
> - short（短整数）	2字节	-32768 ~ 32767
> - int（整数）	4字节	-2147483648 ~ 2147483647	java默认的整数数据类型
> - long（长整数）	8字节	-2^63^ ~ 2^63^-1
> - float（单精度）	4字节	---
> - double（双精度）	8字节	---	java默认的小数数据类型
> - char（字符）	2字节	0 ~ 65535(ASCII表对比)
> - boolean（布尔值）	1字节	true，false

##### Java中&和&&，|和||的区别

> &：无论左边真假，右边都要执行
>
> &&：如果左边为真，右边执行；如果左边为假，右边不执行
>
> |：无论左边真假，右边都要执行
>
> ||：如果左边为假，右边执行；如果左边为真，右边不执行

##### Java 中 String 使用 equals() 和 == 的区别

> String 中 == 比较引用地址是否相同，equals() 比较字符串的内容是否相同
>
> ```java
> String s1 = "Hello";              // String 直接创建
> String s2 = "Hello";              // String 直接创建
> String s3 = s1;                   // 相同引用
> String s4 = new String("Hello");  // String 对象创建
> String s5 = new String("Hello");  // String 对象创建
> 
> s1 == s1;         // true, 相同引用
> s1 == s2;         // true, s1 和 s2 都在公共池中，引用相同
> s1 == s3;         // true, s3 与 s1 引用相同
> s1 == s4;         // false, 不同引用地址
> s4 == s5;         // false, 堆中不同引用地址
> 
> s1.equals(s3);    // true, 相同内容
> s1.equals(s4);    // true, 相同内容
> s4.equals(s5);    // true, 相同内容
> ```

##### if与switch结构之间的区别

> if常用于区间型判断，进行大量数据的判断，减少代码的编写
>
> switch常用于精确型判断，进行少量数据的精确判断，性能略高

##### Java代码注意事项

> 一个java文件中有且只有一个public类，且类的名词要与文件名相同
>
> 数字默认赋值为int，如果想要使用long类型，数字的后面必须加上L或小写的l(不建议使用)
>
> 小数默认赋值为double，如果想要使用float类型，数字的后面必须加上f

##### Java中的数组

> **数组的定义格式**
>
> - 格式一：<span style="color: red;">数据类型</span>[] <span style="color: #329BDC;">变量名</span>
>   - 范例：<span style="color: red;">int</span>[] <span style="color: #329BDC;">arr</span>	<span style="color: green;">定义了一个int类型的数组，数组名是arr</span>
> - 格式二：<span style="color: red;">数据类型</span> <span style="color: #329BDC;">变量名</span>[]
>   - 范例：<span style="color: red;">int</span> <span style="color: #329BDC;">arr</span>[]	<span style="color: green;">定义了一个int类型的变量，变量名是arr数组</span>
>
> <span style="color: red;">推荐使用格式一来定义数组</span>
>
> 
>
> **数组的初始化的方式**
>
> - 动态初始化：初始化时只指定数组长度，由系统为数组分配初始值
>   - 格式：<span style="color: red;">数据类型</span>[] <span style="color: #329BDC;">变量名</span> = <span style="color: red;">new</span> 数组类型[<span style="color: #329BDC;">数组长度</span>];
>   - 范例：<span style="color: red;">int</span>[] <span style="color: #329BDC;">arr</span> = <span style="color: red;">new</span> int[<span style="color: #329BDC;">3</span>];
> - 静态初始化：
>   - 格式：<span style="color: red;">数据类型</span>[] <span style="color: #329BDC;">变量名</span> = <span style="color: red;">new</span> 数组类型[]<span style="color: #329BDC;">{数据1, 数据2, 数据3}</span>;
>   - 范例：<span style="color: red;">int</span>[] <span style="color: #329BDC;">arr</span> = <span style="color: red;">new</span> int[]{<span style="color: #329BDC;">1, 2, 3</span>};
>   - 简化版：<span style="color: red;">int</span>[] <span style="color: #329BDC;">arr</span> = {<span style="color: #329BDC;">1, 2, 3</span>};
>
> 
>
> **数组在初始化时，会为存储空间添加默认值**
>
> - 整数：默认值是0
>
> - 浮点数：默认值是0.0
>
> - 布尔值：默认值是false
>
> - 字符：默认值是空字符
>
> - 引用数据类型：默认值是<span style="color: red;">null</span>
>
>   
>
> **多个数组指向相同内存**
>
> ```java
> int[] arr = new int[3];
> arr[0] = 100;
> System.out.println(arr[0]); // 100
> 
> int[] arr2 = arr;	// 这两个数组指向相同的内存
> arr2[0] = 111; // 修改arr2的值就等于修改arr的值
> System.out.println(arr[0]); // 111
> ```
>
> 
>
> **数组元素访问**
>
> - 数组变量访问方式
>   - 格式：数组名
> - 数组内部保存的数据的访问方式
>   - 格式：数组名[<span style="color: red;">索引</span>]
>
> 
>
> **数组初始化常见错误**
>
> ```java
> 
> ```
>
> 
>
> **for...each循环**
>
> ```java
> String[] names = {"A", "B", "C"}
> // forEach循环，将数组names中的元素，每次循环后交给String name变量
> // 这种循环，数据源(names)中的数据，类型要保持一致
> for(String name : names){
> 	System.out.print(name+" ,");
> }
> // 输出A, B, C
> ```
>
> <span style="color: red;">for...Each循环的缺点：丢掉了索引信息</span>
>
> *当遍历集合或数组时，如果需要访问集合或数组的下标，那么最好使用旧式的方式来实现循环或遍历，而不要使用增强的for循环，因为它丢失了下标信息*

##### Java中的break用法

> break 名称		结束指定名称的循环
>
> ```java
> public class ForDemo3 {
> 
> 	public static void main(String[] args) {
> 		stop:for(int j=1;j<=5;j++){  //5个学生
> 			for(int i=1;i<=10;i++){		//每个学生打印10
> 				if(i==5)
> 					break stop;  //表示结束指定循环,stop相当于一个定位,执行对应名称的循环
> 				System.out.println("第"+j+"个学生,打印第"+i+"次,好好学习,天天向上");
> 			}
> 		}
> 	}
> }
> ```

##### Java生成指定范围的随机数

```java
public static void main(String[] args) {
	// 打印 30到50之间的随机数
	int min = 30;
	int max = 50;
	for (int i = 0; i < 10; i++) {
		System.out.println(new Random().nextInt(max - min) + min);
	}
}
```

