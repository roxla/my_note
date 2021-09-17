##### 什么是程序

> ==程序可以看成是指令(代码)的集合，就是程序==

##### JDK、JRE、JVM之间的关系

> <span style="color: green;">JDK：</span>
>   java开发工具包，包含jre和开发人员使用的工具(date，类型...，Scanner)
> <span style="color: green;">JRE：</span>
> java运行环境，包含jvm和运行所需的核心类
> <span style="color: green;">JVM：</span>
>  java运行虚拟机

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
> <span style="color: #329BDC;">java.util.Arrays</span>	java数组工具类
>
> **对象数组**
>
> - 在数组中存储的是对象，表示数组中的每一个元素都是对象
> - 格式：<span style="color: red;">类的类型</span>[] <span style="color: #329BDC;">数组名</span> = <span style="color: #DB2D20;">new</span> <span style="color: red;">类的类型</span>[<span style="color: #329BDC;">长度</span>];
> - 注意：
>   - 新建数组中不存在对象，数组中的默认初始值为null
>   - 这时候的每一个元素相当于：Person[0] = null;
>
> ```java
> Person[] pers = new Person[3];
> // 此时 pers[0] 存储的内容为null
> System.out.println(pers[0]); // null
> 
> Person per1 = new Person();
> pers[0] = per1;
> // 此时 pers[0] 存储的内容为 per1 所指向的堆内存的地址
> System.out.println(pers[0]); // per1的地址
> ```
>
> 

##### Java中的数组排序

> **冒泡排序：**
>
> ```java
> public static void sort(int[] array) {
> 	for(int i = 0; i < array.length - 1; i++) {
> 		for(int j = 0; j < array.length - i - 1; j++) {
>              // array[j] < array[j+1]：从大到小排序；array[j] > array[j+1]：从小到大排序
>              if(array[j] < array[j+1]) {
>              	int temp = array[j];
>              	array[j] = array[j+1];
>              	array[j+1] = temp;
>          	}
>      	}
>  	}
> }
> ```
>
> **选择排序：**
>
> ```java
> public static void choiceSort(int[] array) {
>     for(int i = 0; i < array.length - 1; i++){
>         int max = 0;
>         for(int j = 0; j < array.length - i; j++){
>             if(array[max] < array[j])
>                 max = j;
>         }
>         int temp = array[array.length - 1 - i];
>         array[array.length - 1 - i] = array[max];
>         array[max] = temp;
>     }
> }
> ```
>
> **插入排序：**
>
> ```java
> public static void insertionSort(int[] array) {
>    /*
> 	* 默认，第一个数为已排序的数
> 	* 直接插入排序法：从第一个开始遍历数组，每个数字都在前面已经被遍历的数字中插入
> 	* 从小到大排序的话，碰到比它大的数，往后移，直到比它小就停下
> 	*/
>     for(int i = 1; i < array.length; i++){
>         int temp = array[i];
>         int j;
>         // 在前面已经遍历过的数中比较
>         for(j = i - 1; j >= 0; j--){
>             if(temp < array[j]){
>                 array[j+1] = array[j];
>             }else{
>                 break;
>             }
>         }
>         // 遇到比比较值小的，就放在比较值的后面
>         array[j+1] = temp;
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
> | <span style="color: #DB2D20;">public static</span> | 修饰符，用于控制用户对于修饰的成员的访问权限                 |
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

##### Java中的类与对象

> **对象的概念：**
>
> 对象是实际存在的该类事物的每个个体，因而也称为实例
>
> Java中一切皆对象
>
> **类的概念：**
>
> 类是对现实生活中一类具有<span style="color: red;">共同属性</span>和<span style="color:red;">行为</span>的事物的抽象
>
> **类的特点：**
>
> - 类是对象的数据类型
> - 类是具有相同属性和行为的一组对象的集合
>
> **类与对象之间的关系：**
>
> <span style="color: red;text-decoration:underline;">对象是类的实例，类是对象的模板</span>
>
> **类的定义：**
>
> 类是Java程序的基本组成单位
>
> 类的组成：属性和行为
>
> - 属性：在类中铜卦成员变量来体现(勒种方法外的变量)
> - 行为：在勒种铜卦成员方法来体现(和前面的方法相比去掉static关键字即可)
>
> ==类的定义步骤==
>
> 格式：
>
> ```java
> // 定义类
> public class 类名{
>     // 编写类的成员变量
>     变量1的数据类型 变量1;
>     变量2的数据类型 变量2;
>     ...
>     // 编写类的成员方法
>     方法1;
>     方法2;
>     ...
> }
> ```
>
> 范例：
>
> ```java
> public class Phone{
>     // 成员变量
>     String brand;
>     int price;
>     // 成员方法
>     public void call() {
>         System.out.println("打电话");
>     }
>     public void sendMessage() {
>         System.out.println("发短信");
>     }
> }
> ```
>
> **对象的使用**
>
> ==创建对象==
>
> - 格式：<span style="color: red;">类名</span> <span style="color: #329BDC;">对象名</span> = <span style="color: #8163BD;">new</span> <span style="color: red;">类名</span>();
> - 范例：<span style="color: red;">Phone</span> <span style="color: #329BDC;">p</span> = <span style="color: #8163BD;">new</span> <span style="color: red;">Phone</span>();
>
> ==使用对象==
>
> 使用成员变量：
>
> - 格式：<span style="color: red;">对象名</span>.<span style="color: #329BDC;">变量名</span> 
> - 范例：<span style="color: red;">p</span>.<span style="color: #329BDC;">brand</span> 
>
> 使用成员方法：
>
> - 格式：<span style="color: red;">对象名</span>.<span style="color: #329BDC;">方法名</span>()
> - 范例：<span style="color: red;">p</span>.<span style="color: #329BDC;">call</span>()
>
> ```java
> public class PhoneDemo{
> 	publie static main(String[] args){
>         // 创建对象
>         Phone p = new Phone();
>         // 使用成员变量
>         System.out.println(p.brand); // null
>         System.out.println(p.price); // 0
>         // 给成员变量赋值
>         p.brand = "小米";
>         p.price = 2999;
>         System.out.println(p.brand); // 小米
>         System.out.println(p.price); // 2999
>         // 使用成员方法
>         p.call(); // 打电话
>         p.sendMessage(); // 发短信
>     }
> }
> ```
>
> *Java堆内存中的成员变量有默认值*
>
> **成员变量和局部变量**
>
> - 成员变量(全局变量)：类中方法外的变量
> - 局部变量：方法中的变量
>
> ==成员变量和局部变量的区别==
>
> |      区别      |                  成员变量                  |                    局部变量                    |
> | :------------: | :----------------------------------------: | :--------------------------------------------: |
> |  类中位置不同  |                 类中方法外                 |              方法内或者方法声明上              |
> | 内存中位置不同 |                   堆内存                   |                     栈内存                     |
> |  生命周期不同  | 随着对象的存在而存在，随着对象的消失而消失 | 随着方法的调用而存在，随着方法的调用完毕而消失 |
> |  初始化值不同  |              有默认的初始化值              | 没有默认的初始化值，必须先定义，复制，才能使用 |
>

##### 类的关键字

> <span style="color: red;">private关键字</span>(<span style="color: #329BDC;">私有</span>)：
>
> - 是一个权限修饰符
> - 可以修饰成员(成员变量和成员方法)
> - 作用是保护成员不被别的类使用，被<span style="color: red;">private</span>修饰的成员只在本类中才能访问
>
> 针对<span style="color: red;">private</span>修饰的成员变量，如果需要被其他类使用，提供相应的操作
>
> - 提供"<span style="color: red;">get变量名()</span>"方法，用于获取成员变量的值，方法用<span style="color: red;">public</span>修饰
> - 提供"<span style="color: red;">set变量名(参数)</span>"方法，用于设置成员变量的值，方法用<span style="color: red;">public</span>修饰
>
> ```java
> // 学生类
> public class Student {
>     // 成员变量
>     private String name;
>     private int age;
> 
>     // get/set方法
>     public void setName(String n) {
>         name = n;
>     }
>     public String getName() {
>         return name;
>     }
> 
>     public void setAge(int a) {
>         age = a;
>     }
>     public int getAge() {
>         return age;
>     }
> 
>     public void show() {
>         System.out.println(name + "，" + age);
>     }
> }
> ```
>
> <span style="color: red;">default关键字</span>(<span style="color: #329BDC;">默认</span>)：
>
> - 是一个权限修饰符
> - 可以修饰成员(成员变量和成员方法)
> - default修饰的属性和方法，只能在本包下使用，其他包的子类继承本包的父类也不能在其他包中使用
>
> <span style="color: red;">protected关键字</span>(<span style="color: #329BDC;">保护</span>)：
>
> - 是一个权限修饰符
> - 可以修饰成员(成员变量和成员方法)
> - protected修饰的属性和方法，在不同包的子类中可以被使用，但在无继承关系的两个类中不能使用
>
> <span style="color: red;">public关键字</span>(<span style="color: #329BDC;">公共</span>)：
>
> - 是一个权限修饰符
> - 可以修饰成员(成员变量和成员方法)
> - public修饰的属性和方法，在任何地方都能使用
>
> <span name="Ptable" style="color: green;">权限修饰符层级表(由低到高)</span>
>
> |                   修饰符                   | 类内部 | 同一个包 | 子类 | 任何地方 |
> | :----------------------------------------: | :----: | :------: | :--: | :------: |
> |  <span style="color: red;">private</span>  |  Yes   |          |      |          |
> |  <span style="color: red;">default</span>  |  Yes   |   Yes    |      |          |
> | <span style="color: red;">protected</span> |  Yes   |   Yes    | Yes  |          |
> |  <span style="color: red;">public</span>   |  Yes   |   Yes    | Yes  |   Yes    |
>
> *对于class的权限修饰只可以用 public 和 default*
>
> - public 类可以在任意地方被访问
> - default 类只可以被同一个包内部的类访问
>
> <span style="color: red;">this关键字</span>：
>
> ```java
> // 标准类
> public class Student {
>     private String name;
> 
>     public String getName() {
>         return name;
>     }
>     public void setName(String name) {
>         this.name = name; // this.name 指代的是 private String name
>     }
> }
> ```
>
> - this修饰的变量用于指代成员变量
>
>   - 方法的形参如果与成员变量同名，不带this修饰的变量指的是形参，而不是成员变量
>   - 方法的形参没有与成员变量同名，不带this修饰的变量指的是成员变量
>
> - <span style="color: red;">解决局部变量隐藏成员变量</span>的时候使用<span style="color: red;">this</span>关键字
>
> - <span style="color: red;">this</span>：代表所在类的对象引用
>
>   - 记住：方法被哪个对象调用，this就代表哪个对象
>
>   - ```java
>     // 测试类
>     public class StudentDemo {
>         public static void main(String[] args) {
>             Student s1 = new Student();
>             s1.setName("王狗蛋"); // setName 方法中的 this 代表 s1 这个对象
>     
>             Student s2 = new Student();
>             s2.setName("李铁蛋"); // setName 方法中的 this 代表 s2 这个对象
>         }
>     }
>     ```
>
>
> <span id="Super" style="color: red;">super关键字</span>：
>
> <span style="color: red;">super</span>关键字的用法和<span style="color: red;">this</span>关键字的用法相似
>
> - <span style="color: red;">this</span>：代表本类对象的引用
> - <span style="color: red;">super</span>：代表父类存储空间的标识(可以理解为父类对象引用)
>
> | 关键字 |              访问成员变量              |             访问构造方法             |              访问成员方法              |
> | :----: | :------------------------------------: | :----------------------------------: | :------------------------------------: |
> |  this  | this.成员变量        访问本类成员变量  | this(. . .)        访问本类构造方法  | this.成员方法        访问本类成员方法  |
> | super  | super.成员变量        访问父类成员变量 | super(. . .)        访问父类构造方法 | super.成员方法        访问父类成员方法 |
>
> ```java
> public class Fu {
>     public Fu(int age) {
>         System.out.printLn("Fu中的带参构造方法被调用");
>     }
> }
> 
> public class Zi extends Fu {
>     public Zi(int age) {
>         super(20);
>         System.out.printLn("Zi中的带参构造方法被调用");
>     }
> }
> 
> public class Demo {
>     public static void main(String[] args) {
>         Zi z2 = new Zi(20);	// Fu中的带参构造方法被调用
>         					// Zi中的带参构造方法被调用
>     }
> }
> ```
>
> <span style="color: red;">static关键字</span>：
>
> - <span style="color: red;">static</span> 关键字是静态的意思，可以修饰成员方法，成员变量
>
> <span style="color: red;">static</span> 修饰的特点
>
> - 被类的所有对象共享	<- *判断是否使用静态关键字的条件*
> - 可以通过类名调用	<- *也可以通过对象名调用，但推荐使用类名调用*
>
> ==static 访问特点==
>
> 非静态的成员方法
>
> - 能访问静态的成员变量
> - 能访问非静态的成员变量
> - 能访问静态的成员方法
> - 能访问非京台的成员方法
>
> 静态的成员方法
>
> - 能访问静态的成员变量
> - 能访问静态的成员方法
>
> *静态成员方法只能访问静态成员，非静态成员可以访问静态内容*
>
> <span style="color: red;">final关键字</span>(<span style="color: #329BDC;">最终态</span>)：
>
> <span style="color: red;">final</span> 关键字是最终的意思，可以修饰成员方法，成员变量，类
>
> <span style="color: red;">final</span> 修饰的特点
>
> - 修饰方法：表明该方法是最终方法，<span style="color: red;">不能被重写</span>
> - 修饰变量：表明该变量是常量，<span style="color: red;">不能再次被赋值</span>
> - 修饰类：表明该类是最终类，<span style="color: red;">不能被继承</span>

##### 类的封装

> **封装概述**
>
> 封装是面相对象三大特征之一
>
> 封装是面相对象编程语言对客观世界的模拟，客观世界里成员变量都是隐藏在对象内部的，外界是无法直接操作的
>
> **封装的原则**
>
> 将类的某些信息隐藏在类内部，不允许外部程序直接访问，而是通过该类提供的方法来实现对隐藏信息的操作和访问成员变量<span style="color: red;">private</span>，提供对应的<span style="color: red;">getXxx()/setXxx()</span>方法
>
> ```java
> public class Student {
> private String name;
> 
> public String getName() {
>   return name;
> }
> public void setName(String name) {
>   this.name = name; // this.name 指代的是 private String name
> }
> }
> ```
>
> **封装的好处**
>
> - 通过方法来控制成员变量的操作，提高了代码的安全性
> - 把代码用方法进行封装，提高了代码的复用性
>
> **构造方法**
>
> 在类的实例过程中，需要构造对象，这时就需要使用到构造方法
>
> 构造方法是一种特殊的方法
>
> - 作用：用于对象的创建，类的实例化与对象的初始化
>
> - 格式：
>
>   ```java
>   public class 类名 {
>       修饰符 类名(参数) {
>       }
>   }
>   ```
>
> - 范例：
>
>   ```java
>   public class Student {
>       public Student() {
>           // 构造方法内书写的内容
>       }
>   }
>   ```
>
> - 功能：主要是完成对象数据的初始化
>
> ```java
> public class Student {
>     private String name;
>     private int age;
>     // 构造方法
>     public Student() {
>         System.out.println("无参构造方法");
>     }
>     public void show() {
>         System.out.println(name + "，" + age);
>     }
> }
> ```
>
> **构造方法的注意事项**
>
> 1. 构造方法的创建
>    1. 如果没有定义构造方法，系统将给出一个<span style="color: red;">默认</span>的<span style="color: red;">无参数构造方法</span>
>    2. 如果定义了构造方法，系统将不再提供默认的构造方法
> 2. 构造方法的重载
>    1. 如果自定义了带参构造方法，还要使用无参构造方法，就必须再写一个无参数构造方法
> 3. 推荐的使用方式
>    1. <span style="color: red;">无论是否使用，都手工书写无参数构造方法</span>
>
> **标准类的制作**
>
> 1. 成员变量
>    1. 使用<span style="color: red;">private</span>修饰
> 2. 构造方法
>    1. 提供一个无参构造方法
>    2. 提供一个带多个参数的构造方法
> 3. 成员方法
>    1. 提供每一个成员变量对应的<span style="color: red;">setXxx()/getXxx()</span>
>    2. 提供一个现实对象信息的<span style="color: red;">show()</span>
> 4. 创建对象并为其成员变量赋值的两种方式
>    1. 无参构造方法创建对象后使用<span style="color: red;">setXxx()</span>赋值
>    2. 使用带参构造方法直接创建带有属性值的对象

##### 类的继承

> **继承的概述**
>
> 继承是面相对象三大特征之一。可以使得子类具有父类的属性和方法，还可以在子类中重新定义，追加属性和方法
>
> Java只支持单继承，不允许多重继承
>
> - 一个子类只能有一个父类
> - 一个父类可以派生出多个子类
>
> **继承的格式**
>
> <span style="color: #E25B51;">public class</span> <span style="color: #329BDC;">子类名</span> <span style="color: red;">extends</span> <span style="color: #329BDC;">父类名</span>{}
>
> ```java
> public class Zi extends Fu{}
> ```
>
> - Fu：是父类，也被称为基类、超类
> - Zi：是子类，也被称为派生类
>
> **继承的注意事项**
>
> 在子类方法中访问一个变量
>
> 1. 先从子类局部范围找
> 2. 再从子类成员范围找
> 3. 最后从父类成员范围找
> 4. 如果都没有就报错(不考虑父类的父类)
>
> 在子类方法中访问一个方法
>
> 1. 先从子类成员范围找
> 2. 再从父类成员范围找
> 3. 如果都没有就报错(不考虑父类的父类)
>
> 子类继承父类：只能继承父类中非私有的属性和方法
>
> 构造方法不能被继承
>
> **继承的好处和弊端**
>
> ==好处==
>
> - 提高了代码的<span style="color: red; font-weight: bold;">复用性</span>(多个类相同的成员可以放到同一个类中)
> - 提高了代码的<span style="color: red; font-weight: bold;">维护性</span>(如果方法的代码需要修改，修改一处即可)
>
> ==弊端==
>
> - 继承让类与类之间产生了关系，类的耦合性增强了，当父类发生变化时子类实现也不得不跟着变化，削弱了子类的独立性
>
> **什么时候使用继承**
>
> - 继承体现的关系：<span style="color: red;">is a</span>
> - 假设法：我有两个类A和B，如果他们满足A是B的一种，或者B是A的一种，就说明他们存在继承关系，这个时候就可以考虑使用继承来体现，否则就不能滥用继承
> - 举例：苹果和水果(可以使用继承，水果为父类)，猫和动物(可以使用继承，动物为父类)，猫和狗(不可以使用继承)
>
> **继承中构造方法的访问特点**
>
> ==子类中所有的构造方法默认都会访问父类中无参的构造方法==
>
> ```java
> public class Fu {
>     public Fu() {
>         System.out.printLn("Fu中的无参构造方法被调用");
>     }
> 
>     public Fu(int age) {
>         System.out.printLn("Fu中的带参构造方法被调用");
>     }
> }
> 
> public class Zi extends Fu {
>     public Zi() {
>         System.out.printLn("Zi中的无参构造方法被调用");
>     }
> 
>     public Zi(int age) {
>         System.out.printLn("Zi中的带参构造方法被调用");
>     }
> }
> 
> public class Demo {
>     public static void main(String[] args) {
>         Zi z = new Zi();	// Fu中的无参构造方法被调用
>         					// Zi中的无参构造方法被调用
> 
>         Zi z2 = new Zi(20);	// Fu中的无参构造方法被调用
>         					// Zi中的带参构造方法被调用
>     }
> }
> ```
>
> - 因为子类会继承父类中的数据，可能还会使用父类的数据，所有，子类初始化之前，一定要先完成父类数据的初始化
> - 每一个子类构造方法的第一条语句默认都是：[super()](#Super)
>
> ==如果父类中没有无参构造方法，只有带参构造方法==
>
> - 通过使用 super 关键字去显示的调用父类的带参构造方法
> - 在父类中自己提供一个无参构造方法
>
> <span style="color: red;">推荐：自己给出无参构造方法</span>
>
> ```java
> public class Fu {
>     public Fu() {
>         System.out.printLn("Fu中的无参构造方法被调用");
>     }
> 
>     public Fu(int age) {
>         System.out.printLn("Fu中的带参构造方法被调用");
>     }
> }
> 
> public class Zi extends Fu {
>     public Zi() {
>         System.out.printLn("Zi中的无参构造方法被调用");
>     }
> 
>     public Zi(int age) {
>         super(20);
>         System.out.printLn("Zi中的带参构造方法被调用");
>     }
> }
> 
> public class Demo {
>     public static void main(String[] args) {
>         Zi z = new Zi();	// Fu中的无参构造方法被调用
>         					// Zi中的无参构造方法被调用
> 
>         Zi z2 = new Zi(20);	// Fu中的带参构造方法被调用
>         					// Zi中的带参构造方法被调用
>     }
> }
> ```
>
> *注意：如果使用父类带参构造方法，调用父类构造方法必须放在第一行*
>
> **方法重写**
>
> ==方法重写的概念==
>
> 子类出现了和父类中一模一样的方法声明(方法名相同，参数列表相同)，返回值相同，访问权限不得严于父类
>
> ==方法重写的注意事项==
>
> *需要重写的父类的方法访问权限不能是 private*
>
> 子类方法访问权限不能更低(public > 默认 >private)
>
> - 父类方法的访问权限为 default 时，子类重写方法的权限不能低于 default
> - [权限修饰符层级表](#Ptable)
>
> ==方法重写的使用==
>
> 当子类需要父类功能，而功能主体有子类特有的内容时，可以重写父类方法，这样就沿袭了父类的功能，又定义了子类特有的内容
>
> ```java
> // 手机类
> public class Phone {
> 	public void call(String name) {
> 		System.out.println("给" + name + "打电话");
> 	}
> }
> 
> // 新手机类
> public class NewPhone extends Phone {
> 	public void call(String name) {
> 		System.out.println("开启视频功能");
> //		System.out.println("给" + name + "打电话");
> 		super.call(name);
> 	}
> }
> 
> // 测试类
> public class PhomeDemo {
> 	public static void main(String[] args) {
> 		// 创建对象，调用方法
> 		Phone p = new Phone();
> 		p.call("李狗蛋");		// 给李狗蛋打电话
> 		System.out.println("-------");
> 
> 		NewPhone np = new NewPhone();
> 		np.call("李狗蛋");		// 开启视频功能
> 							  // 给李狗蛋打电话
> 	}
> }
> ```
>
> ==@Override 注解==
>
> 用来检测当前的方法，是否为重写方法，如果不是就报出异常
>
> ```java
> // 手机类
> public class Phone {
> 	public void call(String name) {
> 		System.out.println("给" + name + "打电话");
> 	}
> }
> 
> // 新手机类
> public class NewPhone extends Phone {
>     @Override // 不是重写 报错
> 	public void calll(String name) {
> 		System.out.println("开启视频功能");
> //		System.out.println("给" + name + "打电话");
> 		super.call(name);
> 	}
> }
> ```
>
> ```java
> // 手机类
> public class Phone {
> 	public void call(String name) {
> 		System.out.println("给" + name + "打电话");
> 	}
> }
> 
> // 新手机类
> public class NewPhone extends Phone {
>     @Override // 是重写 不报错
> 	public void call(String name) {
> 		System.out.println("开启视频功能");
> //		System.out.println("给" + name + "打电话");
> 		super.call(name);
> 	}
> }
> ```
>
> **继承的注意事项**
>
> - Java中类只支持单继承，不支持多继承
>
>   ```java
>   public class Father {
>       public void smoke() {
>           System.out.println("爸爸爱抽烟");
>       }
>   }
>   public class Mother {
>       public void dance() {
>           System.out.println("妈妈爱跳舞");
>       }
>   }
>   public class Son extends Father, Mother {
>       // 报错，Java中类只支持单继承，不支持多继承
>   }
>   ```
>
> - Java中类支持多层继承
>
>   ```java
>   public class Grandad {
>       public void drink() {
>           System.out.println("爷爷爱喝酒");
>       }
>   }
>   public class Father extends Grandad {
>       public void smoke() {
>           System.out.println("爸爸爱抽烟");
>       }
>   }
>   public class Son extends Father {
>       // 可以使用 drink()，Java中类支持多层继承
>   }
>   ```

##### 类的抽象

> **抽象的概念**
>
> 在Java中，一个没有方法体的方法应该定义为抽象方法，而类中如果有抽象方法，该类必须定义为抽象类
>
> **抽象类和抽象方法的格式**
>
> - 格式：使用 <span style="color: red;">abstract</span> 修饰的类和方法就是抽象类和抽象方法
>
> - 范例：
>
> ```java
> // 用abstract修饰的类，叫作抽象类
> public abstract class MotoVehicle() {
>     // 用abstract修饰的方法，叫作抽象方法
>     public abstract void calcRent(int day);
> }
> ```
>
> <span style="color: red;">抽象类中可以没有抽象方法，但是有抽象方法的类必须是一个抽象类</span>
>
> **抽象的注意事项**
>
> - 抽象类不能被初始化，只能被继承
>
> - 抽象方法在子类中必须重写，除非子类是一个抽象类
>   - 在抽象子类中，可以不实现父类的抽象方法
>   - 但是最终的子类也必须去实现所有父类的抽象方法
>
> ```java
> //用abstract修饰的类,叫做抽象类
> public abstract class MotoVehicle {
> 
> 	private String no;
> 	
> 	public MotoVehicle() {
> 		// TODO Auto-generated constructor stub
> 	}
> 	public MotoVehicle(String no){
> 		this.no = no;
> 	}
> 	public String getNo() {
> 		return no;
> 	}
> 	public void setNo(String no) {
> 		this.no = no;
> 	}
> 	//在父类中的方法,因为概念模糊化,没有具体操作,需要将方法设置为抽象方法,使子类中必须重写
> 	//用abstract修饰的方法为抽象方法,抽象方法没有方法体
> 	public abstract int calcRent(int day);
> }
> 
> public abstract class HuoChe extends MotoVehicle {
> 		//在抽象子类中,可以不实现父类的抽象方法
> 	
> 		public abstract void lahuo();
> }
> 
> public class HuoCheZi extends HuoChe {
> 	//但是最终的子类也必须去实现,所有父类的抽象方法
> 	@Override
> 	public int calcRent(int day) {
> 		// TODO Auto-generated method stub
> 		return 0;
> 	}
> 	@Override
> 	public void lahuo() {
> 		// TODO Auto-generated method stub
> 		
> 	}
> }
> ```

##### 类的多态

> **多态的概念**
>
> 同一个对象，在不同时刻表现出来的不同状态
>
> 举例：猫
>
> - 我们可以说猫是猫：<span style="color: red;">猫 cat = new 猫();</span>
> - 我们也可以说猫是动物：<span style="color: red;">动物 animal = new 猫();</span>
>
> 这里猫在不同的时刻表现出来了不同的形态，这就是多态
>
> **多态的作用**
>
> *提高代码的复用率，增加代码的灵活性*
>
> **多态的前提和体现**
>
> - 有继承/实现关系
> - 有方法重现
> - 有父类引用指向子类对象
>   - 动物 animal = new 猫();
>     - 动物 animal：父类引用
>     - new 猫()：子类对象
>
> 范例：
>
> ```java
> public class Animal {
>     public void eat() {
>         System.out.println("动物吃东西");
>     }
> }
> public class Cat extends Animal {
>     @Override
>     public void eat() {
>         System.out.println("猫吃鱼");
>     }
> }
> public class AnimalDemo {
>     public static void main(String[] args) {
>         //  有父类引用指向子类对象
>         Animal a = new Cat();
>     }
> }
> ```
>
> **多态的使用**
>
> 使用父类作为形参时，根据实参来决定执行哪个子类中的方法(*根据传入的参数不同，同一个父类的方法表现出不同的状态*)
>
> ```java
> public abstract class Pet {
> 	public abstract void eat(String food);
> }
> 
> public class Penguin extends Pet {
> 	@Override
> 	public void eat(String food) {
> 		System.out.println("企鹅吃" + food);
> 	}
> }
> 
> public class Dog extends Pet {
> 	@Override
> 	public void eat(String food) {
> 		System.out.println("狗吃" + food);
> 	}
> }
> 
> public class Master {
>     public void feed(Pet pet, String food){
> 		pet.eat(food);
> 	}
> }
> 
> public class PetDemo {
> 	public static void main(String[] args) {
>        	Master m = new Master();
> 		Dog dog = new Dog();
>         Penguin pen = new Penguin();
>         
>         m.feed(dog, "骨头");	// 狗吃骨头
>         m.feed(pen, "鱼");	// 企鹅吃鱼
>     }
> }
> ```
>
> **多态中成员访问特点**
>
> - 成员变量：编译看左边，执行看左边
> - 成员方法：编译看左边，执行看右边
>
> ```java
> public class Animal {
> 	public int age = 40;
> 	
> 	public void eat() {
> 		System.out.println("动物吃东西");
> 	}
> }
> 
> public class Cat extends Animal {
> 	public int age = 20;
> 	public int weight = 10;
> 
> 	@Override
> 	public void eat() {
> 		System.out.println("猫吃鱼");
> 	}
> 
> 	public void playGame() {
> 		System.out.println("猫捉迷藏");
> 	}
> }
> 
> public class AnimalDemo {
> 	public static void main(String[] args) {
> 	//  有父类引用指向子类对象
>         Animal a = new Cat();
>         
>         System.out.println(a.age);	// 40
>         System.out.println(a.weight);	// 编译不通过
>         
>         a.eat();	// 猫吃鱼
>         a.playGame();	// 编译不通过
> 	}
> }
> ```
>
> 为什么成员变量和成员方法的访问不一样
>
> - 因为成员方法有重写，而成员变量没有
>
> **多态的好处和弊端**
>
> - 好处：提高了程序的扩展性
>   - 具体体现：定义方法的时候，使用父类型作为参数，将来在使用的时候，使用具体的子类型参与操作
> - 弊端：不能使用子类的特有功能
>
> **多态中的转型**
>
> - 向上转型
>   - 从子到父
>   - 父类引用指向子类对象
> - 向下转型
>   - 从父到子
>   - 父类引用转为子类对象
>
> ```java
> public class Animal {
> 	public void eat() {
> 		System.out.println("动物吃东西");
> 	}
> }
> 
> public class Cat extends Animal {
> 	@Override
> 	public void eat() {
> 		System.out.println("猫吃鱼");
> 	}
> 
> 	public void playGame() {
> 		System.out.println("猫捉迷藏");
> 	}
> }
> 
> public class AnimalDemo {
> 	public static void main(String[] args) {
> 	// 父类引用指向子类对象
>     Animal a = new Cat();	// 向上转型
>     a.eat();	// 猫吃鱼
> //  a.playGame();	// 编译报错，因为 Animal 类中没有 playGame() 方法
>         
>     // 父类引用转为子类对象
>     Cat c = (Cat)a; // 向下转型
>     c.eat();	// 猫吃鱼
> 	c.playGame();	// 猫捉迷藏
> }
> ```
>
> 

##### 重载和重写的区别

> ~~方法重载（overload）实现的是编译时的多态性（也称为前绑定），而方法重写（override）实现的是运行时的多态性（也称为后绑定）。运行时的多态是面向对象最精髓的东西，要实现多态需要做两件事：1. 方法重写（子类继承父类并重写父类中已有的或抽象的方法）~~
>
> *重载发生在一个类中，同名的方法如果有不同的参数列表则视为重载；重写发生在子类与父类之间，重写要求子类被重写方法与父类被重写方法有相同的参数列表，有兼容的返回类型。*
>
> <span style="color: #329BDC;">在同一个类中，方法名相同，参数列表不同，重载；在子类和父类之间，方法名相同，参数列表相同，返回值相同，子类权限修饰符不严于父类，重写</span>

##### 内部类

> **内部类概述**
>
> 就是在一个类中定义一个类。距离：在一个类A的内部定义一个类B，类B就被称为内部类
>
> **内部类的定义格式**
>
> 格式：
>
> ```java
> public class 类名 {
>     修饰符 class 类名 {
>     }
> }
> ```
>
> 范例：
>
> ```java
> public class Outer {
>     public class Inner {
>     }
> }
> ```
>
> **内部类的访问特点**
>
> - 内部类可以直接访问外部类的成员，包括私有
> - 外部类要访问内部类的成员，必须创建对象
>
> ```java
> public class Outer {
>     private int num = 10;
>     public class Inner {
>         public void show() {
>             System.out.println(num);	// 10
>         }
>     }
>     public void method() {
> //		show();        // 报错
>         Inner i = new Inner();
>         i.show();
>     }
> }
> ```
>
> **成员内部类**
>
> 按照内部类在类中定义的位置不同，可以分为如下两种形式
>
> - 在类的成员位置：成员内部类
> - 在类的局部位置：局部内部类
>
> 成员内部类，外界创建对象使用的格式
>
> - 格式：<span style="color: red;">外部类名</span>.<span style="color: #329BDC;">内部类名</span> 对象名 = <span style="color: red;">外部类对象</span>.<span style="color: #329BDC;">内部类对象</span>;
> - 范例：<span style="color: red;">Outer</span>.<span style="color: #329BDC;">Inner</span> oi = <span style="color: red;">new Outer()</span>.<span style="color: #329BDC;">new Inner()</span>;
>
> ```java
> public class Outer {
>     private int num = 10;
>     
>     public class Inner {
>         public void show() {
>             System.out.println(num);	// 10
>         }
>     }
> }
> public class InneerDemo {
>     public static void main(String[] args) {
>         // 创建内部类对象，并调用方法
>       	Outer.Inner oi = new Outer().new Inner();
>         oi.show();	// 10
>     }
> }
> ```
>
> ==常用的内部类的定义格式和使用==
>
> ```java
> public class Outer {
>     private int num = 10;
>     
>     private class Inner {
>         public void show() {
>             System.out.println(num);	// 10
>         }
>     }
>     
>     public void method() {
>         Inner i = new Inner();
>         i.show();
>     }
> }
> 
> public class InneerDemo {
>     public static void main(String[] args) {
>       	Outer.o = new Outer();
>         o.method;	// 10
>     }
> }
> ```
>
> **局部内部类**
>
> 局部内部类是在方法中定义的类，所以外界是无法直接使用，需要在方法内部创建对象并使用
>
> 该类可以直接访问外部类的成员，也可以访问方法内的局部变量
>
> ```java
> public class Outer {
>     private int num = 10;
>     
>     public void method() {
>         int num2 = 20;
>         class Inner {
>         	public void show() {
>                 // 访问外部类的成员
>             	System.out.println(num);	// 10
>                 // 访问方法内的局部变量
>                 System.out.println(num2);	
>         	}
>         }
>         // 在方法内部创建对象并使用
>         Inner i = new Inner();
>         i.show();
>     }
> }
> 
> public class OuterDemo {
>     public static void main(String[] args) {
>       	Outer.o = new Outer();
>         o.method;	// 10
>         			// 20
>     }
> }
> ```
>
> **匿名内部类**
>
> 匿名内部类属于一种特殊的局部内部类
>
> *前提：存在一个类或者接口，这里的类可以是具体类也可以是抽象类*
>
> - 格式：
>
>   ```java
>   new 类名或者接口名(){
>       重写方法;
>   }
>   ```
>
> - 范例：
>
>   ```java
>   new Inter() {
>       public void show(){
>       }
>   }
>   ```
>
> <span style="color: red;">本质：是一个继承了该类或者实现了该接口的子类匿名对象</span>
>
> 单次调用：
>
> ```java
> public class Outer {
>     
>     public void method() {
>        new Inter() {
>            @Override
>            public void show() {
>                System.out.println("匿名内部类");
>            }
>        }.show(); 
>     }
> }
> 
> public class OuterDemo {
>     public static void main(String[] args) {
>       	Outer.o = new Outer();
>         o.method;	// 匿名内部类
>     }
> }
> ```
>
> 多次调用：
>
> ```java
> public interface Inter {
>     void show();
> }
> 
> public class Outer {
>     
>     public void method() {
>        Inter i = new Inter() {
>            @Override
>            public void show() {
>                System.out.println("匿名内部类");
>            }
>        };
>        i.show();	// 1次调用
>        i.show();	// 2次调用
>     }
> }
> 
> public class OuterDemo {
>     public static void main(String[] args) {
>       	Outer.o = new Outer();
>         o.method;	// 匿名内部类
>         			// 匿名内部类
>     }
> }
> ```
>
> 

##### 常用类

> 

##### 复制对象和复制引用的区别

> 

##### 深拷贝和浅拷贝

> 

##### final、finally、finalize 有什么区别

> 

##### spring mvc 和 struts 的区别是什么

> 

##### 如何避免 SQL 注入

> 

