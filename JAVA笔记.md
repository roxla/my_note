##### 什么是程序

> ==程序可以看成是指令(代码)的集合，就是程序==

##### JDK、JRE、JVM之间的关系

> <span style="color: green;">JDK：</span>
>   java开发工具包，包含jre和开发人员使用的工具(date，类型...，Scanner)
> <span style="color: green;">JRE：</span>
> java运行环境，包含jvm和运行所需的核心类
> <span style="color: green;">JVM：</span>
>  java运行虚拟机

##### 类和对象之间的关系

> **对象是类的实例，类是对象的模板**

##### Java面向对象编程的特性

> - **封装**
>   - *通常认为封装是把数据和操作数据的方法绑定起来，对数据的访问只能通过已定义的接口。面向对象的本质就是将现实世界描绘成一系列完全自治、封闭的对象。我们在类中编写的方法就是对实现细节的一种封装；我们编写一个类就是对数据和数据操作的封装。可以说，封装就是隐藏一切可隐藏的东西，只向外界提供最简单的编程接口。*
> - **继承**
>   - *继承是从已有类得到继承信息创建新类的过程。提供继承信息的类被称为父类（超类、基类）；得到继承信息的类被称为子类（派生类）。继承让变化中的软件系统有了一定的延续性，同时继承也是封装程序中可变因素的重要手段。*
> - **多态**
>   - *多态性是指允许不同子类型的对象对同一消息作出不同的响应。简单的说就是用同样的对象引用调用同样的方法但是做了不同的事情。多态性分为编译时的多态性和运行时的多态性。如果将对象的方法视为对象向外界提供的服务，那么运行时的多态性可以解释为：当A 系统访问B 系统提供的服务时，B系统有多种提供服务的方式， 但一切对A 系统来说都是透明的。方法重载（overload）实现的是编译时的多态性（也称为前绑定），而方法重写（override）实现的是运行时的多态性（也称为后绑定）。运行时的多态是面向对象最精髓的东西，要实现多态需要做两件事：1. 方法重写（子类继承父类并重写父类中已有的或抽象的方法）；2. 对象造型（用父类型引用引用子类型对象，这样同样的引用调用同样的方法就会根据子类对象的不同而表现出不同的行为）。*
> - **抽象**
>   - *抽象是将一类对象的共同特征总结出来构造类的过程，包括数据抽象和行为抽象两方面。抽象只关注对象有哪些属性和行为，并不关注这些行为的细节是什么。*

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
> **数组元素访问**
>
> - 数组变量访问方式
>   - 格式：数组名
> - 数组内部保存的数据的访问方式
>   - 格式：数组名[<span style="color: red;">索引</span>]
>
> **数组初始化常见错误**
>
> ```java
> public static void main(String[] args) {
> 	int[] num = new int[]{2,3,4,5};
> 	// 常见的错误1,创建静态数组初始化时,给长度
> 	// int[] nums = new int[3]{1,2,3};
> 
> 	// 常见错误2,静态数组先声明,后简版赋值
> 	int[] nums = null;
> 	// nums = {1,2,3,4,5};数组没有这种赋值方式   //静态数组初始化简版赋值,必须一步到位
> 	// nums = new int[]{1,3,4,56}; 
> 
> 	// int[] nums = new int[3];
> 	// nums = {1,2,3};  //数组没有这种赋值方式
> 
> 	//常见错误3,通过长度取值,数组下标越界
> 	//System.out.println(num[4]);
> 	System.out.println(nums[1]);
> }
> ```
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
>
> **java.util.Arrays**	java数组工具类 

##### Java中的数组排序

> **冒泡排序：**
>
> ```java
> public static void sort(int[] array) {
> 	for(int i = 0; i < array.length - 1; i++){
>         for(int j = 0; j < array.length - i - 1; j++){
>             // array[j] < array[j+1]：从大到小排序；array[j] > array[j+1]：从小到大排序
>             if(array[j] < array[j+1])
>             {
>                 int temp = array[j];
>                 array[j] = array[j+1];
>                 array[j+1] = temp;
>             }
>         }  
>     }   
> }
> ```
>
> **快速排序：**
>
> ```java
> /**
>  * 快速排序
>  * 
>  * @param array
>  */
> public static void quickSort(int[] array) {
> 	int len;
> 	if (array == null || (len = array.length) == 0 || len == 1) {
> 		return;
> 	}
> 	quickSortCore(array, 0, len - 1);
> }
> 
> /**
>  * 快排核心算法，递归实现
>  * 
>  * @param array
>  * @param left
>  * @param right
>  */
> public static void quickSortCore(int[] array, int left, int right) {
> 	if (left > right) {
> 		return;
> 	}
> 	// base中存放基准数
> 	int base = array[left];
> 	int i = left, j = right;
> 	while (i != j) {
> 		// 顺序很重要，先从右边开始往左找，直到找到比base值小的数
> 		while (array[j] >= base && i < j) {
> 			j--;
> 		}
> 
> 		// 再从左往右边找，直到找到比base值大的数
> 		while (array[i] <= base && i < j) {
> 			i++;
> 		}
> 
> 		// 上面的循环结束表示找到了位置或者(i>=j)了，交换两个数在数组中的位置
> 		if (i < j) {
> 			int tmp = array[i];
> 			array[i] = array[j];
> 			array[j] = tmp;
> 		}
> 	}
> 	// 这时候，跳出上面大的while循环之后，i和j肯定是相等的，因为上面循环的条件是i&lt;j，所以，跳出循环时，i和j是相等的
> 	/**
> 	 * 假如最好的情况是一个有序序列 1 3 5 7 9 temp = 1 i = 0 arr[i] = 1 j = 4 arr[j] = 9
> 	 * 而且在这里，如果先从左边开始寻找的话，一直往右寻找大于1的数，直到i变成4还没有找到就停止了；但是下面的语句就会把9赋值在1上了
> 	 * 如果先从右边开始寻找的话，一直往左寻找小于1的数，直到j变成0还没有找到然后停止，此时i和j都是0，所以就是把自身交换一下并不影响顺序。
> 	 * 这也是为什么强调如果选择数组左边第一个数作为基准值的时候，得先从右边开始查找数。
> 	 */
> 	// 将基准数放到中间的位置（基准数归位）
> 	// 下面的i和j其实相等的，所以用哪一个都一样。
> 	array[left] = array[i];
> 	array[i] = base;
> 
> 	// 递归，继续向基准的左右两边执行和上面同样的操作
> 	// i的索引处为上面已确定好的基准值的位置，无需再处理
> 	quickSortCore(array, left, i - 1);
> 	quickSortCore(array, i + 1, right);
> }
> ```
>
> 

##### Java中的break用法

> <span style="color: red;">break 名称</span>		*结束指定名称的循环*
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

##### Java中的方法

> **方法定义**
>
> - <span style='color: purple; text-decoration:underline;'>无参数</span>：
>
>   格式：
>
>   - ```java
>     public static void 方法名(){
>     	// 方法体
>     }
>     ```
>
>   范例：
>
>   ```java
>   public static void isEvenNumber(){
>   	// 方法体
>   }
>   ```
>
> - <span style='color: purple; text-decoration:underline;'>有参数</span>：
>
>   - 格式：
>
>   - ```java
>     public static void 方法名(数据类型 变量名1, 数据类型 变量名2, ...){
>     	// 方法体
>     }
>     ```
>
>   - 范例：
>
>   - ```java
>     public static void isEvenNumber(int num1, int num2, ...){
>     	// 方法体
>     }
>     ```
>
>   - 注意：
>
>     - 方法定义时，参数中的数据类型与变量名都不能缺少，缺少任意一个程序将报错
>     - 方法定义时，多个参数之间使用逗号(，)分隔
>
> - <span style='color: purple; text-decoration:underline;'>有返回值</span>：
>
>   - 格式：
>
>   - ```java
>     public static 数据类型 方法名(参数){
>         return 数据;
>     }
>     ```
>
>   - 范例：
>
>   - ```java
>     public static boolean isEvenNumber(int number){
>         return true;
>     }
>     ```
>
>   - 注意：
>
>     - 方法定义时return后面的返回值与方法定义上的数据类型要匹配，否则程序将报错
>
> **方法调用**
>
> - <span style='color: purple; text-decoration:underline;'>无参数</span>：
>   - 格式：<span style="color: red;">方法名</span>();
>     - 范例：<span style="color: red;">isEvenNumber</span>();
> - <span style='color: purple; text-decoration:underline;'>有参数</span>：
>   - 格式：<span style="color: red;">方法名</span>(<span style="color: #329BDC;">变量名1/常量值1, 变量名2/常量值2</span>);
>     - 范例：<span style="color: red;">getMax</span>(<span style="color: #329BDC;">5, 6</span>);
>   - 方法调用时，参数的数量与类型必须与方法定义中的设置相匹配，否则程序将报错
> - <span style='color: purple; text-decoration:underline;'>有返回值</span>：
>   - 格式1：方法名(参数);
>     - 范例：isEvenNumber(5);
>   - 格式2：<span style="color: red;">数据类型 变量名</span> = 方法名(参数);
>     - 范例：<span style="color: blue;">boolean</span> flag = isEvenNumber(5);
>   - 方法的返回值通常会使用变量接收，否则该返回值将无意义 (<span style="color: #42B983;">一般使用格式2来进行调用</span>)
>
> **方法的注意事项**
>
> - 方法不能嵌套定义
>
>   - ```java
>     // 错误的定义方式
>     public static void methodOne() {
>         // 代码片段1
>         public static void methodTwo() {
>             // 代码片段2
>         }
>     }
>     ```
>
> - void 表示无返回值，可以省略 return，也可以单独的书写 return，后面不加数据
>
>   - ```java
>     // 错误的返回值书写
>     public static void methodOne() {
>         // 代码片段
>         return 100;
>     }
>     ```
>
> **方法的通用格式**
>
> 格式：
>
> ```java
> public static 返回值类型 方法名(参数) {
>     方法体
>     return 数据;
> }
> ```
>
> | <span style="color: #DB2D20;">public static</span> | 修饰符                                                       |
> | :------------------------------------------------: | :----------------------------------------------------------- |
> |  <span style="color: #42B983;">返回值类型</span>   | 方法操作完毕之后返回的数据的数据类型。如果方法操作完毕，没有数据返回，这里写 void，而且方法体重一般不写 return |
> |    <span style="color: #E2287F;">方法名</span>     | 调用方法时候使用的标识                                       |
> |     <span style="color: #329BDC;">参数</span>      | 由数据类型和变量名组成，多个参数之间用逗号隔开               |
> |      <span style="color: blue;">方法体</span>      | 完成功能的代码块                                             |
> |    <span style="color: #E04D42;">return</span>     | 如果方法操作完毕，有数据返回，用于把数据返回给调用者         |
>
> 定义方法时，要做到<span style="color: red;">两个明确</span>
>
> - <span style="color: #DB2D20;">明确返回值类型：</span>主要是明确方法操作完毕之后是否有数据返回，如果没有，写 void；如果有，写对应的数据类型
> - <span style="color: #DB2D20;">明确参数：</span>主要是明确参数的类型和数量
>
> 调用方法时：*void 类型的方法，直接调用即可；非 void 类型的方法，推荐用变量接收调用*
>
> **方法的重载**
>
> - 概述：
>
>   - 方法重载指同一类中定义的多个方法之间的关系，满足下列条件的多个方法相互构成重载
>
>     - 多个方法在同一个类中
>     - 多个方法具有相同的方法名
>     - 多个方法的参数不相同，类型不同或者数量不同
>
>   - ```java
>     public class methodDemo {
>         public static int main(String[] args) {
>             // 调用方法
>             int result = sum( a: 10, b: 20);
>             System.out.println(result);		// 30
>               
>             int result2 = sum( a: 10.0, b: 20.0);
>             System.out.println(result2);	// 30.0
>               
>             int result3 = sum( a: 10, b: 20, c: 30);
>             System.out.println(result3);	// 60
>         }
>           
>         // 需求1：求两个 int 类型数据和的方法
>         public static int sum(int a, int b) {
>             return a + b;
>         }
>           
>         // 需求2：求两个 double 类型数据和的方法
>         public static double sum(double a, double b) {
>             return a + b;
>         }
>           
>         // 需求3：求三个 int 类型数据和的方法
>         public static int sum(int a, int b, int c) {
>             return a + b + c;
>         }
>     }
>     ```
>
> - 特点：
>
>   - 重载仅对应方法的定义，与方法的调用无关，调用方式参照标准格式
>
>   - 重载仅针对同一类中方法的名称与参数进行识别，与返回值无关，换句话说不能通过返回值来判定两个方法是否相互构成重载
>
>   - ```java
>     // 不属于方法重载
>     public class methodDemo {
>         public static void fn(int a) {
>             // 方法体
>         }
>         public static int fn(int a) {
>             // 方法体
>         }
>     }
>         
>     // 属于方法重载
>     public class methodDemo {
>         public static void fn(int a) {
>             // 方法体
>         }
>         public static int fn(int a, int b) {
>             // 方法体
>         }
>     }
>     ```
>
> **方法的参数传递**
>
> - 基本类型
>
>   - ==对于基本数据类型的参数，形式参数的改变，不影响实际参数的值==
>
>   - ```java
>     public class argsDemo01 {
>         public static void main(String[] args) {
>             int number = 100;
>             syso("调用change方法前：" + number);	// number = 100
>             change(number);
>             syso("调用change方法后：" + number);	// number = 100
>         }
>         public static void change(int number) {
>             number = 200;
>         }
>     }
>     ```
>
> - 引用类型
>
>   - ==对于引用类型的参数，形式参数的改变，英雄实际参数的值==
>
>   - ```java
>     public class argsDemo02 {
>         public static void main(String[] args) {
>             int[] arr = {10, 20, 30};
>             syso("调用change方法前：" + arr[1]);	// arr[1] = 20
>             change(arr);
>             syso("调用change方法后：" + arr[1]);	// arr[1] = 200
>         }
>         public static void change(int[] arr) {
>             arr[1] = 200;
>         }
>     }
>     ```
>
>     

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

##### 复制对象和复制引用的区别

> 

##### 深拷贝和浅拷贝

> 

