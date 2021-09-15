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
> <span style="color: red;">protected关键字</span>(<span style="color: #329BDC;">保护</span>)：
>
> - 是一个权限修饰符
> - 可以修饰成员(成员变量和成员方法)
>
> <span style="color: red;">public关键字</span>(<span style="color: #329BDC;">公共</span>)：
>
> - 是一个权限修饰符
> - 可以修饰成员(成员变量和成员方法)
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
> - 1
>
> <span style="color: red;">static关键字</span>：
>
> - 1
>
> *注意：静态方法不得访问非静态内容，非静态可以访问静态内容*

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
>  private String name;
> 
>  public String getName() {
>      return name;
>  }
>  public void setName(String name) {
>      this.name = name; // this.name 指代的是 private String name
>  }
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
> 构造方法是一种特殊的方法
>
> - 作用：创建对象
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

##### 类的多态

> 

##### 类的抽象

> 

##### 复制对象和复制引用的区别

> 

##### 重载和重写的区别

> 方法重载（overload）实现的是编译时的多态性（也称为前绑定），而方法重写（override）实现的是运行时的多态性（也称为后绑定）。运行时的多态是面向对象最精髓的东西，要实现多态需要做两件事：1. 方法重写（子类继承父类并重写父类中已有的或抽象的方法）

##### 深拷贝和浅拷贝

> 

##### final、finally、finalize 有什么区别

> 

##### spring mvc 和 struts 的区别是什么

> 

##### 如何避免 SQL 注入

> 

