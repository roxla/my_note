##### 什么是程序

> 程序可以看成是指令(代码)的集合，就是程序

##### JDK、JRE、JVM之间的关系

> <span style="color: green;">JDK：</span>
>      java开发工具包，包含jre和开发人员使用的工具(date，类型...，Scanner)
> <span style="color: green;">JRE：</span>
>    java运行环境，包含jvm和运行所需的核心类
> <span style="color: green;">JVM：</span>
>     java运行虚拟机

##### Java代码注意事项

> 一个java文件中有且只有一个public类，且类的名词要与文件名相同
>
> 数字默认赋值为int，如果想要使用long类型，数字的后面必须加上L或小写的l(不建议使用)
>
> 小数默认赋值为double，如果想要使用float类型，数字的后面必须加上f

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

