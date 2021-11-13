## 什么是程序

> ==程序可以看成是指令(代码)的集合，就是程序==

## JDK、JRE、JVM之间的关系

> <span style="color: green;">JDK：</span>
>   java开发工具包，包含jre和开发人员使用的工具(date，类型...，Scanner)
> <span style="color: green;">JRE：</span>
> java运行环境，包含jvm和运行所需的核心类
> <span style="color: green;">JVM：</span>
>  java运行虚拟机

## Java中的八大基本数据类型

> - byte（位）	1字节	-128 ~ 127
> - short（短整数）	2字节	-32768 ~ 32767
> - int（整数）	4字节	-2147483648 ~ 2147483647	java默认的整数数据类型
> - long（长整数）	8字节	-2^63^ ~ 2^63^-1
> - float（单精度）	4字节
> - double（双精度）	8字节	---	java默认的小数数据类型
> - char（字符）	2字节	0 ~ 65535(ASCII表对比)
> - boolean（布尔值）	1字节	true，false

## Java中的四大基本引用类型

> - 数组
> - String
> - 类
> - 接口

## Java中&和&&，|和||的区别

> &：无论左边真假，右边都要执行
>
> &&：如果左边为真，右边执行；如果左边为假，右边不执行
>
> |：无论左边真假，右边都要执行
>
> ||：如果左边为假，右边执行；如果左边为真，右边不执行

## Java 中 String 使用 equals() 和 == 的区别

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

## if与switch结构之间的区别

> if常用于区间型判断，进行大量数据的判断，减少代码的编写
>
> switch常用于精确型判断，进行少量数据的精确判断，性能略高

## Java代码注意事项

> 一个java文件中有且只有一个public类，且类的名词要与文件名相同
>
> 数字默认赋值为int，如果想要使用long类型，数字的后面必须加上L或小写的l(不建议使用)
>
> 小数默认赋值为double，如果想要使用float类型，数字的后面必须加上f

## Java中的数组

### 数组的定义格式

> - 格式一：<span style="color: red;">数据类型</span>[] <span style="color: #329BDC;">变量名</span>
>   - 范例：<span style="color: red;">int</span>[] <span style="color: #329BDC;">arr</span>	<span style="color: green;">定义了一个int类型的数组，数组名是arr</span>
> - 格式二：<span style="color: red;">数据类型</span> <span style="color: #329BDC;">变量名</span>[]
>   - 范例：<span style="color: red;">int</span> <span style="color: #329BDC;">arr</span>[]	<span style="color: green;">定义了一个int类型的变量，变量名是arr数组</span>
>
> <span style="color: red;">推荐使用格式一来定义数组</span>
>

### 数组的初始化的方式

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

### 多个数组指向相同内存

```java
int[] arr = new int[3];
arr[0] = 100;
System.out.println(arr[0]); // 100

int[] arr2 = arr;	// 这两个数组指向相同的内存
arr2[0] = 111; // 修改arr2的值就等于修改arr的值
System.out.println(arr[0]); // 111
```

### 数组元素访问

> - 数组变量访问方式
>   - 格式：数组名
> - 数组内部保存的数据的访问方式
>   - 格式：数组名[<span style="color: red;">索引</span>]
>

### 数组初始化常见错误

```java
public static void main(String[] args) {
	int[] num = new int[]{2,3,4,5};
	// 常见的错误1,创建静态数组初始化时,给长度
	// int[] nums = new int[3]{1,2,3};

	// 常见错误2,静态数组先声明,后简版赋值
	int[] nums = null;
	// nums = {1,2,3,4,5};数组没有这种赋值方式   //静态数组初始化简版赋值,必须一步到位
	// nums = new int[]{1,3,4,56}; 

	// int[] nums = new int[3];
	// nums = {1,2,3};  //数组没有这种赋值方式

	//常见错误3,通过长度取值,数组下标越界
	//System.out.println(num[4]);
	System.out.println(nums[1]);
}
```

### for...each循环

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

### 对象数组

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

### Java中的数组排序

#### 冒泡排序

```java
public static void sort(int[] array) {
    for (int i = 0; i < array.length - 1; i++) {
        for (int j = 0; j < array.length - i - 1; j++) {
            // array[j] < array[j+1]：从大到小排序；array[j] > array[j+1]：从小到大排序
            if (array[j] < array[j + 1]) {
                int temp = array[j];
                array[j] = array[j + 1];
                array[j + 1] = temp;
            }
        }
    }
}
```

#### 选择排序

 ```java
public static void choiceSort(int[] array) {
	for(int i = 0; i < array.length - 1; i++){
		int max = 0;
		for(int j = 0; j < array.length - i; j++){
			if(array[max] < array[j])
				max = j;
		}
		int temp = array[array.length - 1 - i];
		array[array.length - 1 - i] = array[max];
		array[max] = temp;
	}
}
 ```

#### 插入排序

```java
public static void insertionSort(int[] array) {
	/**
	 * 默认，第一个数为已排序的数
	 * 直接插入排序法：从第一个开始遍历数组，每个数字都在前面已经被遍历的数字中插入
	 * 从小到大排序的话，碰到比它大的数，往后移，直到比它小就停下
	 */
	for(int i = 1; i < array.length; i++){
		int temp = array[i];
		int j;
		// 在前面已经遍历过的数中比较
		for(j = i - 1; j >= 0; j--){
			if(temp < array[j]){
				array[j+1] = array[j];
			}else{
				break;
			}
		}
		// 遇到比比较值小的，就放在比较值的后面
		array[j+1] = temp;
	}
}
```

#### 快速排序

```java
/**
 * 快速排序
 * 
 * @param array
 */
public static void quickSort(int[] array) {
    int len;
    if (array == null || (len = array.length) == 0 || len == 1) {
        return;
    }
    quickSortCore(array, 0, len - 1);
}

/**
 * 快排核心算法，递归实现
 * 
 * @param array
 * @param left
 * @param right
 */
public static void quickSortCore(int[] array, int left, int right) {
    if (left > right) {
        return;
    }
    // base中存放基准数
    int base = array[left];
    int i = left, j = right;
    while (i != j) {
        // 顺序很重要，先从右边开始往左找，直到找到比base值小的数
        while (array[j] >= base && i < j) {
            j--;
        }

        // 再从左往右边找，直到找到比base值大的数
        while (array[i] <= base && i < j) {
            i++;
        }

        // 上面的循环结束表示找到了位置或者(i>=j)了，交换两个数在数组中的位置
        if (i < j) {
            int tmp = array[i];
            array[i] = array[j];
            array[j] = tmp;
        }
    }
    // 这时候，跳出上面大的while循环之后，i和j肯定是相等的，因为上面循环的条件是i&lt;j，所以，跳出循环时，i和j是相等的
    /**
     * 假如最好的情况是一个有序序列 1 3 5 7 9 temp = 1 i = 0 arr[i] = 1 j = 4 arr[j] = 9
	 * 而且在这里，如果先从左边开始寻找的话，一直往右寻找大于1的数，直到i变成4还没有找到就停止了；但是下面的语句就会把9赋值在1上了
	 * 如果先从右边开始寻找的话，一直往左寻找小于1的数，直到j变成0还没有找到然后停止，此时i和j都是0，所以就是把自身交换一下并不影响顺序。
	 * 这也是为什么强调如果选择数组左边第一个数作为基准值的时候，得先从右边开始查找数。
	 */
    // 将基准数放到中间的位置（基准数归位）
    // 下面的i和j其实相等的，所以用哪一个都一样。
    array[left] = array[i];
    array[i] = base;

    // 递归，继续向基准的左右两边执行和上面同样的操作
    // i的索引处为上面已确定好的基准值的位置，无需再处理
    quickSortCore(array, left, i - 1);
    quickSortCore(array, i + 1, right);
}
```

## Java中的break用法

> <span style="color: red;">break 名称</span>		*结束指定名称的循环*
>
> ```java
> public class ForDemo3 {
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

## Java中的方法

### 方法定义

> - <span style='color: purple; text-decoration:underline;'>无参数</span>：
>
>   格式：
>
>   ```java
>   public static void 方法名(){
>    	// 方法体
>   }
>   ```
>
>   范例：
>
>   ```java
>    public static void isEvenNumber(){
>   	// 方法体
>   }
>   ```
>
> - <span style='color: purple; text-decoration:underline;'>有参数</span>：
>
>   - 格式：
>
>      ```java
>      public static void 方法名(数据类型 变量名1, 数据类型 变量名2, ...){
>       	// 方法体
>      }
>      ```
>
>   - 范例：
>
>      ```java
>      public static void isEvenNumber(int num1, int num2, ...){
>       	// 方法体
>      }
>      ```
>
>   - 注意：
>
>     - 方法定义时，参数中的数据类型与变量名都不能缺少，缺少任意一个程序将报错
>     
>    - 方法定义时，多个参数之间使用逗号(，)分隔
>
> - <span style='color: purple; text-decoration:underline;'>有返回值</span>：
>
>   - 格式：
>
>      ```java
>      public static 数据类型 方法名(参数){
>         return 数据;
>      }
>      ```
>
>   - 范例：
>
>      ```java
>      public static boolean isEvenNumber(int number){
>         return true;
>      }
>      ```
>
>   - 注意：
>
>     - 方法定义时return后面的返回值与方法定义上的数据类型要匹配，否则程序将报错
>

### 方法调用

> - <span style='color: purple; text-decoration:underline;'>无参数</span>：
>  - 格式：<span style="color: red;">方法名</span>();
>     - 范例：<span style="color: red;">isEvenNumber</span>();
>- <span style='color: purple; text-decoration:underline;'>有参数</span>：
>   - 格式：<span style="color: red;">方法名</span>(<span style="color: #329BDC;">变量名1/常量值1, 变量名2/常量值2</span>);
>    - 范例：<span style="color: red;">getMax</span>(<span style="color: #329BDC;">5, 6</span>);
>   - 方法调用时，参数的数量与类型必须与方法定义中的设置相匹配，否则程序将报错
> - <span style='color: purple; text-decoration:underline;'>有返回值</span>：
>   - 格式1：方法名(参数);
>     - 范例：isEvenNumber(5);
>   - 格式2：<span style="color: red;">数据类型 变量名</span> = 方法名(参数);
>    - 范例：<span style="color: blue;">boolean</span> flag = isEvenNumber(5);
>   - 方法的返回值通常会使用变量接收，否则该返回值将无意义 (<span style="color: #42B983;">一般使用格式2来进行调用</span>)
>

### 方法的注意事项

> - 方法不能嵌套定义
>
>   ```java
>   // 错误的定义方式
>   public static void methodOne() {
>      // 代码片段1
>       public static void methodTwo() {
>           // 代码片段2
>       }
>   }
>   ```
>
> - void 表示无返回值，可以省略 return，也可以单独的书写 return，后面不加数据
>
>   ```java
>   // 错误的返回值书写
>   public static void methodOne() {
>       // 代码片段
>       return 100;
>   }
>   ```
>

### 方法的通用格式

> 格式：
>
> ```java
>public static 返回值类型 方法名(参数) {
>    	方法体
>    	return 数据;
> }
> ```
> 
> | <span style="color: #DB2D20;">public static</span> | 修饰符，用于控制用户对于修饰的成员的访问权限                 |
> | :------------------------------------------------: | :----------------------------------------------------------- |
>|  <span style="color: #42B983;">返回值类型</span>   | 方法操作完毕之后返回的数据的数据类型。如果方法操作完毕，没有数据返回，这里写 void，而且方法体重一般不写 return |
> |    <span style="color: #E2287F;">方法名</span>     | 调用方法时候使用的标识                                       |
>|     <span style="color: #329BDC;">参数</span>      | 由数据类型和变量名组成，多个参数之间用逗号隔开               |
> |      <span style="color: blue;">方法体</span>      | 完成功能的代码块                                             |
> |    <span style="color: #E04D42;">return</span>     | 如果方法操作完毕，有数据返回，用于把数据返回给调用者         |
> 
> 定义方法时，要做到<span style="color: red;">两个明确</span>
> 
>- <span style="color: #DB2D20;">明确返回值类型：</span>主要是明确方法操作完毕之后是否有数据返回，如果没有，写 void；如果有，写对应的数据类型
> - <span style="color: #DB2D20;">明确参数：</span>主要是明确参数的类型和数量
>
> 调用方法时：*void 类型的方法，直接调用即可；非 void 类型的方法，推荐用变量接收调用*
>

### 方法的重载

> - 概述：
>
>   - 方法重载指同一类中定义的多个方法之间的关系，满足下列条件的多个方法相互构成重载
>
>     - 多个方法在同一个类中
>    - 多个方法具有相同的方法名
>     - 多个方法的参数不相同，类型不同或者数量不同
> 
>   - ```java
>     public class methodDemo {
>         public static int main(String[] args) {
>            // 调用方法
>             int result = sum( a: 10, b: 20);
>            System.out.println(result);		// 30
>                                                                     
>             int result2 = sum( a: 10.0, b: 20.0);
>             System.out.println(result2);	// 30.0
>                                                                     
>             int result3 = sum( a: 10, b: 20, c: 30);
>            System.out.println(result3);	// 60
>         }
>                                                                    
>         // 需求1：求两个 int 类型数据和的方法
>        public static int sum(int a, int b) {
>             return a + b;
>         }
>                                                                     
>         // 需求2：求两个 double 类型数据和的方法
>         public static double sum(double a, double b) {
>            return a + b;
>         }
>                                                                    
>         // 需求3：求三个 int 类型数据和的方法
>         public static int sum(int a, int b, int c) {
>             return a + b + c;
>         }
>     }
>   
> - 特点：
>
>   - 重载仅对应方法的定义，与方法的调用无关，调用方式参照标准格式
> 
>  - 重载仅针对同一类中方法的名称与参数进行识别，与返回值无关，换句话说不能通过返回值来判定两个方法是否相互构成重载
> 
>  - ```java
>    // 不属于方法重载
>     public class methodDemo {
>         public static void fn(int a) {
>             // 方法体
>         }
>         public static int fn(int a) {
>            // 方法体
>         }
>      }
>                             
>                                                                                                     // 属于方法重载
>     public class methodDemo {
>         public static void fn(int a) {
>             // 方法体
>        }
>         public static int fn(int a, int b) {
>            // 方法体
>         }
>      }
>    ```
> 

### 方法的参数传递

> - 基本类型
>
>   - ==对于基本数据类型的参数，形式参数的改变，不影响实际参数的值==
>
>   - ```java
>    public class argsDemo01 {
>         public static void main(String[] args) {
>             int number = 100;
>             syso("调用change方法前：" + number);	// number = 100
>             change(number);
>             syso("调用change方法后：" + number);	// number = 100
>        }
>         public static void change(int number) {
>            number = 200;
>         }
>     }
>     ```
> 
> - 引用类型
>
>   - ==对于引用类型的参数，形式参数的改变，影响实际参数的值==
>
>   - ```java
>    public class argsDemo02 {
>         public static void main(String[] args) {
>             int[] arr = {10, 20, 30};
>             syso("调用change方法前：" + arr[1]);	// arr[1] = 20
>             change(arr);
>             syso("调用change方法后：" + arr[1]);	// arr[1] = 200
>        }
>         public static void change(int[] arr) {
>            arr[1] = 200;
>         }
>     }
>     ```
> 
>     *基本数据类型传递的是栈空间中的值，引用数据类型传递的是堆空间的地址值*

## Java生成指定范围的随机数

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

## Java面向对象编程的特性

### 封装

> **通常认为封装是把数据和操作数据的方法绑定起来，对数据的访问只能通过已定义的接口。面向对象的本质就是将现实世界描绘成一系列完全自治、封闭的对象。我们在类中编写的方法就是对实现细节的一种封装；我们编写一个类就是对数据和数据操作的封装。可以说，封装就是隐藏一切可隐藏的东西，只向外界提供最简单的编程接口。**

### 继承

> **继承是从已有类得到继承信息创建新类的过程。提供继承信息的类被称为父类（超类、基类）；得到继承信息的类被称为子类（派生类）。继承让变化中的软件系统有了一定的延续性，同时继承也是封装程序中可变因素的重要手段。**

### 多态

> **多态性是指允许不同子类型的对象对同一消息作出不同的响应。简单的说就是用同样的对象引用调用同样的方法但是做了不同的事情。多态性分为编译时的多态性和运行时的多态性。如果将对象的方法视为对象向外界提供的服务，那么运行时的多态性可以解释为：当A 系统访问B 系统提供的服务时，B系统有多种提供服务的方式， 但一切对A 系统来说都是透明的。方法重载（overload）实现的是编译时的多态性（也称为前绑定），而方法重写（override）实现的是运行时的多态性（也称为后绑定）。运行时的多态是面向对象最精髓的东西，要实现多态需要做两件事：1. 方法重写（子类继承父类并重写父类中已有的或抽象的方法）；2. 对象造型（用父类型引用引用子类型对象，这样同样的引用调用同样的方法就会根据子类对象的不同而表现出不同的行为）。**

### 抽象

> **抽象是将一类对象的共同特征总结出来构造类的过程，包括数据抽象和行为抽象两方面。抽象只关注对象有哪些属性和行为，并不关注这些行为的细节是什么。**

## Java中的类与对象

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

### 类的定义

> **类是Java程序的基本组成单位**
>
> 类的组成：属性和行为
>
> - 属性：在类中铜卦成员变量来体现(勒种方法外的变量)
>- 行为：在勒种铜卦成员方法来体现(和前面的方法相比去掉static关键字即可)
> 
>==类的定义步骤==
> 
>格式：
> 
>```java
> // 定义类
> public class 类名{
>    // 编写类的成员变量
>     变量1的数据类型 变量1;
>    变量2的数据类型 变量2;
>     ...
>    // 编写类的成员方法
>     方法1;
>    方法2;
>     ...
>}
> ```
>
> 范例：
> 
>```java
> public class Phone{
>    // 成员变量
>     String brand;
>    int price;
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

### 对象的使用

> ==创建对象==
>
> - 格式：<span style="color: red;">类名</span> <span style="color: #329BDC;">对象名</span> = <span style="color: #8163BD;">new</span> <span style="color: red;">类名</span>();
>- 范例：<span style="color: red;">Phone</span> <span style="color: #329BDC;">p</span> = <span style="color: #8163BD;">new</span> <span style="color: red;">Phone</span>();
> 
>==使用对象==
> 
>使用成员变量：
> 
>- 格式：<span style="color: red;">对象名</span>.<span style="color: #329BDC;">变量名</span> 
> - 范例：<span style="color: red;">p</span>.<span style="color: #329BDC;">brand</span> 
>
> 使用成员方法：
> 
>- 格式：<span style="color: red;">对象名</span>.<span style="color: #329BDC;">方法名</span>()
> - 范例：<span style="color: red;">p</span>.<span style="color: #329BDC;">call</span>()
>
> ```java
>public class PhoneDemo{
> 	publie static main(String[] args){
>        // 创建对象
>         Phone p = new Phone();
>        // 使用成员变量
>         System.out.println(p.brand); // null
>        System.out.println(p.price); // 0
>         // 给成员变量赋值
>         p.brand = "小米";
>        p.price = 2999;
>         System.out.println(p.brand); // 小米
>        System.out.println(p.price); // 2999
>         // 使用成员方法
>        p.call(); // 打电话
>         p.sendMessage(); // 发短信
>     }
> }
> ```
> 
> *Java堆内存中的成员变量有默认值*
> 

#### 匿名对象

> 匿名对象：没有名字的对象
>
> **匿名对象其实就是定义对象的简写格式**
>
> 不使用匿名对象
>
> ```java
> Car c = new Car();
> c.run();
> ```
>
> 使用匿名对象
>
> ```java
> new Car().run();
> ```

### 成员变量和局部变量

> - 成员变量(全局变量)：类中方法外的变量
>- 局部变量：方法中的变量
> 
>==成员变量和局部变量的区别==
> 
>|      区别      |                  成员变量                  |                    局部变量                    |
> | :------------: | :----------------------------------------: | :--------------------------------------------: |
>|  类中位置不同  |                 类中方法外                 |              方法内或者方法声明上              |
> | 内存中位置不同 |                   堆内存                   |                     栈内存                     |
>|  生命周期不同  | 随着对象的存在而存在，随着对象的消失而消失 | 随着方法的调用而存在，随着方法的调用完毕而消失 |
> |  初始化值不同  |              有默认的初始化值              | 没有默认的初始化值，必须先定义，复制，才能使用 |
>

### 类的关键字

#### private

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

#### default

> <span style="color: red;">default关键字</span>(<span style="color: #329BDC;">默认</span>)：
>
> - 是一个权限修饰符，如果成员和类不写权限修饰符，默认使用此关键字
> - 可以修饰成员(成员变量和成员方法)
> - default修饰的属性和方法，只能在本包下使用，其他包的子类继承本包的父类也不能在其他包中使用
>

#### protected

> <span style="color: red;">protected关键字</span>(<span style="color: #329BDC;">保护</span>)：
>
> - 是一个权限修饰符
> - 可以修饰成员(成员变量和成员方法)
> - protected修饰的属性和方法，在不同包的子类中可以被使用，但在无继承关系的两个类中不能使用
>

#### public

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

#### this

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

#### <span name="Super">super</span>

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

#### static

> <span style="color: red;">static关键字</span>：
>
> - <span style="color: red;">static</span> 关键字是静态的意思，可以修饰成员方法，成员变量
> - <span style="color: red;">static</span> 修饰的内容不需要依赖于对象进行访问，只要类加载，就可以通过类直接访问
>
> <span style="color: red;">static</span> 修饰的特点
>
> - 被类的所有对象共享	<- *判断是否使用静态关键字的条件*
> - 可以通过类名直接调用	<- *也可以通过对象名调用，但推荐使用类名调用*
>
> **静态块**
>
> - static关键字还有一个比较关键的作用，用来形成静态代码块（static{}(即static块)）以优化程序性能
>
>   ```java
>   static {}
>   ```
>
> - *static块可以置于类中的任何地方，类中可以有多个static块*
>
> - <span style="color: red;">在类初次被加载的时候执行且仅会被执行一次</span>（这是优化性能的原因！！！），<span style="color: #329BDC;">会按照static块的顺序来执行每个static块，一般用来初始化静态变量和调用静态方法</span>
>
> *static块是会按照顺序执行，与main入口函数无关*
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

#### final

> <span style="color: red;">final关键字</span>(<span style="color: #329BDC;">最终态</span>)：
>
> <span style="color: red;">final</span> 关键字是最终的意思，可以修饰成员方法，成员变量，类
>
> <span style="color: red;">final</span> 修饰的特点
>
> - 修饰方法：表明该方法是最终方法，<span style="color: red;">不能被重写</span>
> - 修饰变量：表明该变量是常量，<span style="color: red;">不能再次被赋值</span>
> - 修饰类：表明该类是最终类，<span style="color: red;">不能被继承</span>

### 类的封装

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

#### 构造方法

> 在类的实例过程中，需要构造对象，这时就需要使用到构造方法
>
> 构造方法是一种特殊的方法
>
> - 作用：用于对象的创建，类的实例化与对象的初始化
>
> - 格式：
>
>   ```java
>  public class 类名 {
>       修饰符 类名(参数) {
>       }
>   }
>   ```
> 
>   - 范例：
> 
>   ```java
>     public class Student {
>       public Student() {
>           // 构造方法内书写的内容
>       }
>  }
>   ```
>
> - 功能：主要是完成对象数据的初始化
> 
>```java
> public class Student {
>    private String name;
>     private int age;
>    // 构造方法
>     public Student() {
>        System.out.println("无参构造方法");
>     }
>    public void show() {
>         System.out.println(name + "，" + age);
>    }
> }
> ```
> 

#### 构造方法的注意事项

> 1. 构造方法的创建
>   1. 如果没有定义构造方法，系统将给出一个<span style="color: red;">默认</span>的<span style="color: red;">无参数构造方法</span>
>    2. 如果定义了构造方法，系统将不再提供默认的构造方法
>2. 构造方法的重载
>    1. 如果自定义了带参构造方法，还要使用无参构造方法，就必须再写一个无参数构造方法
>3. 推荐的使用方式
>    1. <span style="color: red;">无论是否使用，都手工书写无参数构造方法</span>
>

#### 标准类的制作

> 1. 成员变量
>   1. 使用<span style="color: red;">private</span>修饰
> 2. 构造方法
>   1. 提供一个无参构造方法
>    2. 提供一个带多个参数的构造方法
>3. 成员方法
>    1. 提供每一个成员变量对应的<span style="color: red;">setXxx()/getXxx()</span>
>   2. 提供一个现实对象信息的<span style="color: red;">show()</span>
> 4. 创建对象并为其成员变量赋值的两种方式
>   1. 无参构造方法创建对象后使用<span style="color: red;">setXxx()</span>赋值
>    2. 使用带参构造方法直接创建带有属性值的对象

### 类的继承

> **继承的概述**
>
> 继承是面相对象三大特征之一。可以使得子类具有父类的属性和方法，还可以在子类中重新定义，追加属性和方法
>
> Java只支持单继承，不允许多重继承
>
> - 一个子类只能有一个父类
> - 一个父类可以派生出多个子类
>

#### 继承的格式

> <span style="color: #E25B51;">public class</span> <span style="color: #329BDC;">子类名</span> <span style="color: red;">extends</span> <span style="color: #329BDC;">父类名</span>{}
>
> ```java
>public class Zi extends Fu{}
> ```
>
> - Fu：是父类，也被称为基类、超类
> - Zi：是子类，也被称为派生类
>

#### 继承的好处和弊端

> ==好处==
>
> - 提高了代码的<span style="color: red; font-weight: bold;">复用性</span>(多个类相同的成员可以放到同一个类中)
>- 提高了代码的<span style="color: red; font-weight: bold;">维护性</span>(如果方法的代码需要修改，修改一处即可)
> 
>==弊端==
> 
> - 继承让类与类之间产生了关系，类的耦合性增强了，当父类发生变化时子类实现也不得不跟着变化，削弱了子类的独立性
>

#### 什么时候使用继承

> - 继承体现的关系：<span style="color: red;">is a</span>
>- 假设法：我有两个类A和B，如果他们满足A是B的一种，或者B是A的一种，就说明他们存在继承关系，这个时候就可以考虑使用继承来体现，否则就不能滥用继承
> - 举例：苹果和水果(可以使用继承，水果为父类)，猫和动物(可以使用继承，动物为父类)，猫和狗(不可以使用继承)
>

#### 继承中构造方法的访问特点

> ==子类中所有的构造方法默认都会访问父类中无参的构造方法==
>
> ```java
>public class Fu {
>     public Fu() {
>        System.out.printLn("Fu中的无参构造方法被调用");
>     }
> 
>    public Fu(int age) {
>         System.out.printLn("Fu中的带参构造方法被调用");
>    }
> }
>
> public class Zi extends Fu {
>     public Zi() {
>         System.out.printLn("Zi中的无参构造方法被调用");
>    }
> 
>     public Zi(int age) {
>        System.out.printLn("Zi中的带参构造方法被调用");
>     }
>}
> 
>public class Demo {
>     public static void main(String[] args) {
>         Zi z = new Zi();	// Fu中的无参构造方法被调用
>         					// Zi中的无参构造方法被调用
> 
>        Zi z2 = new Zi(20);	// Fu中的无参构造方法被调用
>         					// Zi中的带参构造方法被调用
>    }
> }
> ```
> 
>- 因为子类会继承父类中的数据，可能还会使用父类的数据，所有，子类初始化之前，一定要先完成父类数据的初始化
> - 每一个子类构造方法的第一条语句默认都是：[super()](#Super)
>
> ==如果父类中没有无参构造方法，只有带参构造方法==
>
> - 通过使用 super 关键字去显示的调用父类的带参构造方法
>- 在父类中自己提供一个无参构造方法
> 
><span style="color: red;">推荐：自己给出无参构造方法</span>
> 
> ```java
>public class Fu {
>     public Fu() {
>        System.out.printLn("Fu中的无参构造方法被调用");
>     }
>
>     public Fu(int age) {
>        System.out.printLn("Fu中的带参构造方法被调用");
>     }
> }
> 
>public class Zi extends Fu {
>     public Zi() {
>        System.out.printLn("Zi中的无参构造方法被调用");
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

#### 方法重写

> ==方法重写的概念==
>
> 子类出现了和父类中一模一样的方法声明(方法名相同，参数列表相同)，返回值相同，访问权限不得严于父类
>
> ==方法重写的注意事项==
>
> *需要重写的父类的方法访问权限不能是 private*
> 
>子类方法访问权限不能更低(public > 默认 >private)
> 
>- 父类方法的访问权限为 default 时，子类重写方法的权限不能低于 default
> - [权限修饰符层级表](#Ptable)
>
> ==方法重写的使用==
> 
> 当子类需要父类功能，而功能主体有子类特有的内容时，可以重写父类方法，这样就沿袭了父类的功能，又定义了子类特有的内容
>
> ```java
> // 手机类
>public class Phone {
> 	public void call(String name) {
>		System.out.println("给" + name + "打电话");
> 	}
>}
> 
> // 新手机类
> public class NewPhone extends Phone {
> 	public void call(String name) {
>		System.out.println("开启视频功能");
> //		System.out.println("给" + name + "打电话");
>		super.call(name);
> 	}
> }
> 
>// 测试类
> public class PhomeDemo {
>	public static void main(String[] args) {
> 		// 创建对象，调用方法
>		Phone p = new Phone();
> 		p.call("李狗蛋");		// 给李狗蛋打电话
>		System.out.println("-------");
> 
>		NewPhone np = new NewPhone();
> 		np.call("李狗蛋");		// 开启视频功能
> 							  // 给李狗蛋打电话
>	}
> }
>```
> 
>==@Override 注解==
> 
>用来检测当前的方法，是否为重写方法，如果不是就报出异常
> 
> ```java
> // 手机类
>public class Phone {
> 	public void call(String name) {
>		System.out.println("给" + name + "打电话");
> 	}
>}
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

#### 继承的注意事项

> **在子类方法中访问一个变量**
>
> 1. 先从子类局部范围找
> 2. 再从子类成员范围找
> 3. 最后从父类成员范围找
> 4. 如果都没有就报错(不考虑父类的父类)
>
> **在子类方法中访问一个方法**
>
> 1. 先从子类成员范围找
> 2. 再从父类成员范围找
> 3. 如果都没有就报错(不考虑父类的父类)
>
> **子类继承父类：只能继承父类中非私有的属性和方法，构造方法不能被继承**
>
> **Java中类只支持单继承，不支持多继承**
>
> ```java
> public class Father {
>     public void smoke() {
>         System.out.println("爸爸爱抽烟");
>     }
> }
> public class Mother {
>     public void dance() {
>         System.out.println("妈妈爱跳舞");
>     }
> }
> public class Son extends Father, Mother {
>     // 报错，Java中类只支持单继承，不支持多继承
> }
> ```
>
> **Java中类支持多层继承**
>
> ```java
> public class Grandad {
>     public void drink() {
>         System.out.println("爷爷爱喝酒");
>     }
> }
> public class Father extends Grandad {
>     public void smoke() {
>         System.out.println("爸爸爱抽烟");
>     }
> }
> public class Son extends Father {
>     // 可以使用 drink()，Java中类支持多层继承
> }
> ```

### 类的抽象

> **抽象的概念**
>
> 在Java中，一个没有方法体的方法应该定义为抽象方法，而类中如果有抽象方法，该类必须定义为抽象类
>

#### 抽象类和抽象方法的格式

> - 格式：使用 <span style="color: red;">abstract</span> 修饰的类和方法就是抽象类和抽象方法
>
> - 范例：
>
> ```java
>// 用abstract修饰的类，叫作抽象类
> public abstract class MotoVehicle() {
>    // 用abstract修饰的方法，叫作抽象方法
>     public abstract void calcRent(int day);
>}
> ```
> 
> <span style="color: red;">抽象类中可以没有抽象方法，但是有抽象方法的类必须是一个抽象类</span>
> 

#### 抽象的注意事项

> - 抽象类不能被初始化，只能被继承
>
> - 抽象方法在子类中必须重写，除非子类是一个抽象类
>  - 在抽象子类中，可以不实现父类的抽象方法
>   - 但是最终的子类也必须去实现所有父类的抽象方法
>
> ```java
>//用abstract修饰的类,叫做抽象类
> public abstract class MotoVehicle {
>
> 	private String no;
> 
> 	public MotoVehicle() {
> 		// TODO Auto-generated constructor stub
> 	}
> 	public MotoVehicle(String no){
> 		this.no = no;
>	}
> 	public String getNo() {
>		return no;
> 	}
>	public void setNo(String no) {
> 		this.no = no;
>	}
> 	//在父类中的方法,因为概念模糊化,没有具体操作,需要将方法设置为抽象方法,使子类中必须重写
> 	//用abstract修饰的方法为抽象方法,抽象方法没有方法体
> 	public abstract int calcRent(int day);
>}
> 
> public abstract class HuoChe extends MotoVehicle {
> 		//在抽象子类中,可以不实现父类的抽象方法
> 
> 		public abstract void lahuo();
> 	}
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

### 类的多态

> **多态的概念**
>
> 同一个对象，在不同时刻表现出来的不同状态，最终得到不同的结果
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

#### 多态的前提和体现

> - 有继承/实现关系
>- 有方法重现
> - 有父类引用指向子类对象
>  - 动物 animal = new 猫();
>     - 动物 animal：父类引用
>    - new 猫()：子类对象
> 
> 范例：
>
> ```java
>public class Animal {
>     public void eat() {
>        System.out.println("动物吃东西");
>     }
>}
> public class Cat extends Animal {
>    @Override
>     public void eat() {
>         System.out.println("猫吃鱼");
>     }
> }
> public class AnimalDemo {
>     public static void main(String[] args) {
>        //  有父类引用指向子类对象
>         Animal a = new Cat();
>    }
> }
> ```
> 

#### 多态的使用

> 使用父类作为形参时，根据实参来决定执行哪个子类中的方法(*根据传入的参数不同，同一个父类的方法表现出不同的状态*)
>
> ```java
>public abstract class Pet {
> 	public abstract void eat(String food);
>}
> 
> public class Penguin extends Pet {
>	@Override
> 	public void eat(String food) {
>		System.out.println("企鹅吃" + food);
> 	}
>}
> 
>public class Dog extends Pet {
> 	@Override
>	public void eat(String food) {
> 		System.out.println("狗吃" + food);
> 	}
> }
> 
> public class Master {
>     public void feed(Pet pet, String food){
>		pet.eat(food);
> 	}
>}
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

#### 多态中成员访问特点

> - 成员变量：**编译看左边，执行看左边**
>- 成员方法：**编译看左边，执行看右边**
> 
>```java
> public class Animal {
>	public int age = 40;
> 
> 	public void eat() {
>		System.out.println("动物吃东西");
> 	}
>}
> 
>public class Cat extends Animal {
> 	public int age = 20;
>	public int weight = 10;
> 
>	@Override
> 	public void eat() {
> 		System.out.println("猫吃鱼");
> 	}
> 
> 	public void playGame() {
> 		System.out.println("猫捉迷藏");
>	}
> }
>
> public class AnimalDemo {
> 	public static void main(String[] args) {
> 	//  有父类引用指向子类对象
>         Animal a = new Cat();
> 
>         System.out.println(a.age);	// 40 (执行看 Animal)
>         System.out.println(a.weight);	// 编译不通过 (编译看 Animal)
> 
>         a.eat();	// 猫吃鱼 (执行看 Cat)
>         a.playGame();	// 编译不通过 (编译看 Animal)
> 	}
> }
> ```
> 
> *为什么成员变量和成员方法的访问不一样*
> 
> - **因为成员方法有重写，而成员变量没有**
> 

#### 多态的好处和弊端

> - 好处：**提高了程序的扩展性**
>  - 具体体现：**定义方法的时候，使用父类型作为参数，将来在使用的时候，使用具体的子类型参与操作**
> - 弊端：**不能使用子类的特有功能**
>

#### 多态中的转型

> - 向上转型
>    - *从子到父*
>     - **父类引用指向子类对象**
>- 向下转型
>   - *从父到子*
>    - **父类引用转为子类对象**
>   - 当需要使用到子类对象中特有的方法及属性时,将父类类型重新还原为子类类型,才可以调用子类中特有的方法和属性
> 
>```java
> public class Animal {
>	public void eat() {
> 		System.out.println("动物吃东西");
>	}
> }
>
> public class Cat extends Animal {
>	@Override
> 	public void eat() {
> 		System.out.println("猫吃鱼");
> 	}
> 
> 	public void playGame() {
> 		System.out.println("猫捉迷藏");
>	}
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

### Java接口

> **接口的概述**
>
> 接口就是一种公共的规范标准，只要符合规范标准，大家都可以通用
>
> Java中的接口更多的体现在对行为的抽象，提出标准(功能)
>

#### 接口的特点

> - 接口用关键字<span style="color: red;">interface</span>修饰
>
>   - public <span style="color: red;">interface</span> 接口名 {}
>
>     ```java
>      public interface USBInterfase {
>         // USB的标准是提供服务
>        // 在接口中因为默认都是抽象方法，所以 abstract 可以省略，
>         public void service();
>      }
>     ```
>
> - 类实现接口用<span style="color: red;">implements</span>表示
>
>   - public class 类名 <span style="color: red;">implements</span> 接口名 {}
>
>     ```java
>     public class UDisk implements USBInterfase {
>         @Override
>         public void service() {
>     		System.out.println("USB插入，交换数据");
>         }
>     }
>                                                     
>     public class USBSan implements USBInterfase {
>     	@Override
>     	public void service() {
>     		System.out.println("USB插入，风扇转起来了");
>     	}
>     }
>                                                     
>     public class USBDemo{
>     	public static void main(String[] args) {
>     		USBInterfase usb = new USBSan();
>     		usb.service(); // USB插入，交换数据
>     		USBInterfase usb = new UDisk();
>     		usb.service(); // USB插入，风扇转起来了
>     	}
>     }
>
> - **接口不能实例化**
>
>   - 接口如何实例化
>     - 参照多态的方式，通过实现类对象实例化，这叫接口多态
>     - 多态的形式：具有类多态，抽象类多态，接口多态
>     - 多态的前提：有继承或者实现关系；有方法重写；有父(类/接口)引用指向(子/实现)类对象
>
> - 接口的实现类
>
>    - 要么重写接口中的所有抽象方法
>     - 要么是抽象类
>

#### 接口的成员特点

> - 成员变量
>    - 只能是常量
>     - 默认修饰符：<span style="color: red;">public static final</span>
>- 构造方法
>   - 接口没有构造方法，因为接口主要是对行为进行抽象的，是没有具体存在
>    - 一个类如果没有父类，默认继承自Object类
> - 成员方法
>    - 只能是抽象方法
>     - 默认修饰符：<span style="color: red;">public abstract</span>
>
> **JDK1.8之后提供的实体方法**
>
> - 默认方法
>   - 使用default修饰，不可省略，供子类调用或重写
> - 静态方法
>   - 使用static修饰，供接口直接调用
> 
> ```java
> public interface USBInterfase {
>    // 默认方法
>     public default void show() {
>		System.out.println("这是接口的默认方法");
> 	}
>    // 静态方法
>     public static void print() {
> 		System.out.println("这是可以被接口直接调用的方法");
> 	}
> }
> ```
> 

#### 类和接口的关系

> - 类和类的关系
>    - **继承关系，只能单继承，但是可以多层继承**
> - 类和接口的关系
>    - **实现关系，可以单实现，也可以多实现，还可以在继承一个类的同时实现多个接口**
> - 接口和接口的关系
>    - **继承关系，可以单继承，也可以多继承**
> 
>被实现的接口可以视为类内自带的方法，当使用该类的数组时，所有数组内的成员均持有该方法，并且方法内的属性使用的是对应数组成员的属性
> 
>```java
> public interface ShowNum {
>    // 默认方法
>     public void show();
> }
> 
> public class Num implements ShowNum {
>    private int n;
> 
>    public Num() {
>   }
> 
>   public Num(int n) {
>        this.n = n;
>   }
> 
>    public int getNum() {
> 		return id;
>    }
> 
>    public int setNum(int n) {
> 		this.n = n;
>    }
> 
>    @Override
> 	public void show() {
> 		System.out.println(n);
> 	}
>                           }
> 
> public class NumDemo {
>     public static void main(String[] args) {
>         Num[] nums = new Num[3];
>                                   for(int i = 0; i < 3; i++)
>             nums[i] = new Num(i);
> 
>         nums[0].show();	// 0
>         nums[1].show();	// 1
>         nums[2].show();	// 2
>    }
> }
>```
> 

#### 抽象类和接口的区别

> - **成员区别**
>    - 抽象类：变量，常量；有构造方法；有抽象方法，也有非抽象方法
>     - 接口：常量；抽象方法
>- **关系区别**
>   - 类与类：继承，单继承
>    - 类与接口：实现，可以单实现，也可以多实现
>     - 接口与接口：继承，单继承，多继承
>- **设计理念区别**
>   - 抽象类：对类抽象，包括属性、行为
>    - 接口：对行为抽象，主要是行为

## 重载和重写的区别

> ~~方法重载（overload）实现的是编译时的多态性（也称为前绑定），而方法重写（override）实现的是运行时的多态性（也称为后绑定）。运行时的多态是面向对象最精髓的东西，要实现多态需要做两件事：1. 方法重写（子类继承父类并重写父类中已有的或抽象的方法）~~
>
> *重载发生在一个类中，同名的方法如果有不同的参数列表则视为重载；重写发生在子类与父类之间，重写要求子类被重写方法与父类被重写方法有相同的参数列表，有兼容的返回类型。*
>
> <span style="color: #329BDC;">在同一个类中，方法名相同，参数列表不同，重载；在子类和父类之间，方法名相同，参数列表相同，返回值相同，子类权限修饰符不严于父类，重写</span>

## 设计模式

> **设计模式的概述**
>
> - 是一套可以反复使用，多数人知晓，经过分类编目的代码设计经验总结
> - 代码可以重复利用，让代码更容易让人理解，保证代码的可靠性，提高工作的效率，优化代码结构
> - 设计模式初步确定23种设计模式：单例设计模式，工厂方法模式，抽象工厂模式，模板设计模式，代理设计模式
>
> *设计模式主要掌握：单例设计模式，简单工厂设计模式，抽象工厂模式，工厂方法模式，模板设计模式，代理设计模式*
>

### 单例设计模式

> 确保只有一个实例，且该实例向整个系统提供，这种设计的类叫做单例类，该类创建的实例也就叫做单例。单例模式是一种对象的创建模式
>

#### 懒汉式单例设计模式

> 该模式只在你需要对象时才会生成单例对象
>
> **懒汉式单例设计模式的格式**
> 
> - 将构造方法设置为私有的
>
>   ```java
> private LazySingle() {}
>   ```
>
> - 声明本类类型，并设置为static
>
>   ```java
> private static LazySingle ls = null;
>   ```
>
> - 设置一个可被外部访问获取实例的静态方法
>
>   ```java
>   public static LazySingle getExample() {
>       if(ls == null)
>           ls = new LazySingle();
>       return ls;
>   }
>   ```
>
> ```java
> public class LazySingle {
>     private String name;
>
>     public void setName(String name) {
>        this.name = name;
>     }
>     public String getName() {
>         return name;
>     }
> 
>     private LazySingle() {}
>     private static LazySingle ls = null;
>     public static LazySingle getExample() {
>         if(ls == null)
>             ls = new LazySingle();
>         return ls;
>     }
> 
>     public void print() {
>         System.out.println(name + "说：今天天气不错");
>     }
> }
> 
> public class LazySingleDemo {
>     public static void main(String[] args) {
>         LazySingle lazy = LazySingle.getExample();
>         lazy.setName("张三");
>         lazy.print();	//  张三说：今天天气不错
> 
>         // 再次创建一个对象，判断两个对象是否相等
>         LazySingle lisi = LazySingle.getExample();
>             lisi.setName("李四");
>         lisi.print();	//  李四说：今天天气不错
> 
>         System.out.println(lazy == lisi);	// true
>     }
> }
> ```
> 

#### 饿汉式单例设计模式

> 该模式在类被加载时就会实例化一个对象
>
> **饿汉式单例设计模式的格式**
> 
> - 将构造方法设置为私有的
>
>   ```java
> private HungrySingle() {}
>   ```
>
> - 创建对象，需要将对象设置为私有的，并将对象设置为最终的对象
>
>   ```java
> private static final HungrySingle hs = new HungrySingle();
>   ```
>
> - 设置获取实例的静态方法
>
>   ```java
>   public static HungrySingle getExample() {
>       return hs;
>   }
>   ```
>
> ```java
>/**
> * 饿汉式单例模式：在声明时就需要创建的一种方式
> */
> public class HungrySingle {
>     private String name;
> 
>     public void setName(String name) {
>         this.name = name;
>     }
>     public String getName() {
>         return name;
>     }
> 
>     private HungrySingle() {}
>     private static final HungrySingle hs = new HungrySingle();
>     public static HungrySingle getExample() {
>         return hs;
>     }
>     
>     public void print() {
>         System.out.println(name + "说：今天天气不错");
>     }
> }
> 
> public class HungrySingleDemo {
>     public static void main(String[] args) {
>         HungrySingle hungry = HungrySingle.getExample();
>         hungry.setName("张三");
>         hungry.print();	//  张三说：今天天气不错
> 
>         // 再次创建一个对象，判断两个对象是否相等
>         HungrySingle lisi = HungrySingle.getExample();
>         lisi.setName("李四");
>         lisi.print();	//  李四说：今天天气不错
> 
>         System.out.println(hungry == lisi);	// true
>     }
> }
> ```
> 

#### 饿汉式与懒汉式的区别

> 饿汉式
>
> - 类一旦加载，就把单例初始化完成，保证获取的时候单例是已经存在的
> - 天生就是线程安全的，可以直接用于多线程而不出现问题
> - 在类的创建的同时就实例化一个静态对象，不管用不用，都会占据内存，但相应的，在第一次调用对象时，速度也会更快，因为资源早就初始完成
>
> 懒汉式
>
> - 只有当调用的时候，才会去初始化单例对象
>- 本身线程是不安全的，为了实现线程安全，需要控制线程的进入
> - 懒汉式会延迟加载对象，在第一次调用单例对象时，在调用的时候才初始化对象，第一次调用对象时会慢，后续跟饿汉式一样
>

### 工厂设计模式

> 工厂模式是我们最常用的实例化对象模式了，是用工厂方法代替new操作的一种模式
>
> *工厂模式就相当于创建实例对象的new*
> 
> 工厂模式让对象的使用者无需了解具体实现，只需要通过对象工厂直接拿过来用就行了

#### 简单工厂设计模式

> 简单工厂模式是指由一个工厂对象决定创建出哪一种产品类的实例
>
> 负责实现创建所有实例的内部逻辑，并提供外部所调用的方法，创建所需要的对象
> 
> ```java
>// 设计生产线模型
> public interface Product {
>        public void intro();
> }
>public class ColaProduct implements Product {
>     @Override
>    public void intro() {
>         System.out.println("机器轰隆隆响,可乐慢慢生产出来....");
>    }
> }
>public class SpriteProduct implements Product {
>     @Override
>    public void intro() {
>         System.out.println("机器轰隆隆响,雪碧慢慢生产出来....");
>    }
> }
> // 负责实现创建所有实例的内部逻辑，并提供外部所调用的方法，创建所需要的对象
> public class SimpleFactory {
>        // 通过不同的参数，获取到不同的结果
>        public static Product getProduct(String type) {
>            switch(type) {
>                case "c":
>                    return new ColaProduct();
>                case "s":
>                    return new SpriteProduct();
>            }
>            return null;
>        }
> }
> 
> public class FactoryDemo {
>        public static void main(String[] args) {
>            System.out.println("Cola raw materials");
>         Product cola = SimpleFactory.getProduct("c");
>        cola.intro();	// 机器轰隆隆响,可乐慢慢生产出来....
>         System.out.println("Sprite raw materials");
>         Product sprite = SimpleFactory.getProduct("s");
>         sprite.intro();	// 机器轰隆隆响,雪碧慢慢生产出来....
>        }
> }
>    ```
> 
> - 特点：
>       - 它是一个具体的类,非接口,抽象类,有一个重要的方法create()的方法,利用if或者switch创建不同对象返回
>   - Create()一般是静态方法,所以也称之为静态工厂
> - 缺点：
>   - 扩展性差(我想要增加一种芬达,除了新增芬达类,还要修改工厂方法)
>   - 不同产品需要不同的额外参数进行创建,不支持自动化
> 

#### 抽象工厂模式

> 提供一个创建一系列相关或相互依赖对象的接口，而无需指定它们具体的类
>
> ==何时使用==
>
> 系统的产品有多于一个的产品族，而系统只消费其中某一族的产品
>
> ==格式==
>
> ```java
> public interface Product {
>      // 生产流水线标准
>     public void intro();
> }
> 
> public class ColaProduct implements Product {
>     @Override
>     public void intro() {
>         System.out.println("机器轰隆隆响,可乐慢慢生产出来....");
>     }
> }
> 
> public abstract class Packing {
>     // 包装流水线标准
>     public abstract void doPack();
> }
> 
> public class NormalPack extends Packing {
>     @Override
>     public void doPack() {
>         System.out.println("对商品进行简易包装...");
>     }
> }
> 
> public class HigherPack extends Packing {
>     @Override
>     public void doPack() {
>         System.out.println("对商品进行豪华礼盒包装...");
>     }
> }
> /**
>  * 工厂设计,既有商品,还要包装
>  */
> public interface ProductFactory {
>     public Product getProduct();
>     public Packing getPack();
> }
> 
> public class NormalFactory implements ProductFactory {
>     @Override
>     public Product getProduct() {
>         //普通工厂主动创建生产线对象
>         return new ColaProduct(); 
>     }
>     @Override
>     public Packing getPack() {
>         //创建包装线对象
>         return new NormalPack();
>     }
> }
> 
> public class HigherFactory implements ProductFactory {
>     @Override
>     public Product getProduct() {
>         return new ColaProduct();
>     }
>     @Override
>     public Packing getPack() {
>         return new HigherPack();
>     }
> }
> 
> public class FactoryDemo {
>     public static void main(String[] args) {
>         //普通工厂进行商品的生产与简单包装
>         ProductFactory pf = new NormalFactory();
>         pf.getProduct().intro();	// 机器轰隆隆响,可乐慢慢生产出来....
>         pf.getPack().doPack();		// 对商品进行简易包装...
>         //高级工厂生产商品,并豪华包装
>         ProductFactory hf = new HigherFactory();
>         hf.getProduct().intro();	// 机器轰隆隆响,可乐慢慢生产出来....
>         hf.getPack().doPack();		// 对商品进行豪华礼盒包装...
>     }
> }
> ```
> 

### 工厂方法模式

> 

### 模板设计模式

> 

### 代理设计模式

> 
>

### 设计模式的七大原则

> 1. 单一职责原则
> 2. 接口隔离原则
> 3. 依赖倒转（倒置）原则
> 4. 里氏替换原则
> 5. 开闭原则
> 6. 迪米特法则
> 7. 合成复用原则

#### 单一职责原则

> **基本介绍**
>
> 对类来说的，即一个类应该只负责一项职责。如类 A 负责两个不同职责：职责 1，职责 2。当职责 1 需求变更而改变 A 时，可能造成职责 2 执行错误，所以需要将类 A 的粒度分解为 A1，A2
>
> **应用实例**
>
> 以交通工具案例讲解
>
> 方案一
>
> ```java
> public class SingleResponsibility1 {
>     public static void main(String[] args) {
>         Vehicle vehicle = new Vehicle();
>         vehicle.run("摩托车");
>         vehicle.run("汽车");
>         vehicle.run("飞机");
>     }
> }
> /**
>  * 交通工具类
>  * 方式一
>  * 1. 在方式一的 run 方法中，违反了单一职责原则
>  * 2. 解决的方案非常的简单，根据交通工具运行方法不同，分解成不同类即可
>  */
> class Vehicle{
>     public void run(String vehicle){
>         System.out.println(vehicle + "在公路上运行...");
>     }
> }
> ```
>
> 方案二
>
> ```java
> public class SingleResponsibility2 {
>     public static void main(String[] args) {
>         RoadVehicle roadVehicle = new RoadVehicle();
>         roadVehicle.run("摩托车");
>         roadVehicle.run("汽车");
> 
>         AirVehicle airVehicle = new AirVehicle();
>         airVehicle.run("飞机");
>     }
> }
> /**
>  * 方案二的分析
>  * 1. 遵守单一职责原则
>  * 2. 这样做的改动很大，即 将类分解，同时修改客户端
>  * 3. 改进：直接修改 Vehicle 类，改动的代码会比较少 => 方案三
>  */
> class RoadVehicle{
>     public void run(String vehicle){
>         System.out.println(vehicle + "在公路运行");
>     }
> }
> class AirVehicle{
>     public void run(String vehicle){
>         System.out.println(vehicle + "在天空运行");
>     }
> }
> class WaterVehicle{
>     public void run(String vehicle){
>         System.out.println(vehicle + "在水中运行");
>     }
> }
> ```
>
> 方案三
>
> ```java
> public class SingleResponsibility3 {
>     public static void main(String[] args) {
>         Vehicle2 vehicle2 = new Vehicle2();
>         vehicle2.run("摩托车");
>         vehicle2.runAir("飞机");
>         vehicle2.runWater("轮船");
>     }
> }
> /**
>  * 方式三的分析
>  * 1. 这种修改方法没有对原来的类做大的修改，只是增加方法
>  * 2. 这里虽然没有在类这个级别上遵守单一职责原则，但是在方法级别上，仍然是遵守单一职责
>  */
> class Vehicle2{
>     public void run(String vehicle){
>         System.out.println(vehicle + "在公路运行...");
>     }
>     public void runAir(String vehicle){
>         System.out.println(vehicle + "在天空运行...");
>     }
>     public void runWater(String vehicle){
>         System.out.println(vehicle + "在水中运行...");
>     }
> }
> ```
>
> **单一职责原则注意事项和细节**
>
> - 降低类的复杂度，一个类只负责一项职责
> - 提高类的可读性，可维护性
> - 降低变更引起的风险
> - 通常情况下，**我们应当遵守单一职责原则**，只有逻辑足够简单，才可以在代码级违反单一职责原则; 只有类中方法数量足够少，可以在方法级别保持单一职责原则

#### 接口隔离原则

> **基本介绍**
>
> 客户端不应该依赖它不需要的接口，即==一个类对另一个类的依赖应该建立在最小的接口==上
>
> **案例**
>
> 类A通过接口 Interface1 依赖类B，类C通过接口 Interface1 依赖类D，如果接口 Interface1 对于类A和类C来说不是最小接口，那么类 B 和类 D 必须去实现他们不需要的方法
>
> 按隔离原则应当这样处理
>
> 将**接口 Interface1**拆分为**独立的几个接口(这里我们拆分成 3 个接口)**，类 A 和类 C 分别与他们需要的接口建立依赖关系。也就是采用接口隔离原则
>
> **应用实例**
>
> - 类A通过接口Interface1依赖类B，类C通过接口Interface1依赖类D。
>
>
> - 没有实现接口隔离原则的代码实现
>
> - Segregation1
>
>   ```java
>   /**
>    * 接口隔离原则
>    */
>   public class Segregation1 {
>   }
>   // 接口
>   interface Interface1{
>       void operation1();
>       void operation2();
>       void operation3();
>       void operation4();
>       void operation5();
>   }
>   class B implements Interface1{
>       @Override
>       public void operation1() {
>           System.out.println("B 实现了 operation1");
>       }
>       @Override
>       public void operation2() {
>           System.out.println("B 实现了 operation2");
>       }
>       @Override
>       public void operation3() {
>           System.out.println("B 实现了 operation3");
>       }
>       @Override
>       public void operation4() {
>           System.out.println("B 实现了 operation4");
>       }
>       @Override
>       public void operation5() {
>           System.out.println("B 实现了 operation5");
>       }
>   }
>   class D implements Interface1{
>       
>       @Override
>       public void operation1() {
>           System.out.println("D 实现了 operation1");
>       }
>       @Override
>       public void operation2() {
>           System.out.println("D 实现了 operation2");
>       }
>       @Override
>       public void operation3() {
>           System.out.println("D 实现了 operation3");
>       }
>       @Override
>       public void operation4() {
>           System.out.println("D 实现了 operation4");
>       }
>       @Override
>       public void operation5() {
>           System.out.println("D 实现了 operation5");
>       }
>   }
>   class A{    // A类通过接口 Interface1依赖（使用）B类，但是只会用到1，2，3方法
>       public void depend1(Interface1 i){
>           i.operation1();
>       }
>       public void depend2(Interface1 i){
>           i.operation2();
>       }
>       public void depend3(Interface1 i){
>           i.operation3();
>       }
>   }
>   class C{    // C类通过接口 Interface1依赖（使用）D类，但是只会用到1，4，5方法
>       public void depend1(Interface1 i){
>           i.operation1();
>       }
>       public void depend4(Interface1 i){
>           i.operation4();
>       }
>       public void depend5(Interface1 i){
>           i.operation5();
>       }
>   }
>   ```
>
> **应传统方法的问题和使用接口隔离原则改进**
>
> 类A通过接口 Interface1 依赖类 B，类 C 通过接口 Interface1 依赖类 D，如果接口 Interface1 对于类 A 和类 C 来说不是最小接口，那么类 B 和类 D 必须去实现他们不需要的方法
>
> 将接口 Interface1 拆分为独立的几个接口，类A和类C分别与他们需要的接口建立依赖关系。也就是采用接口隔离原则
>
> 接口 Interface1 中出现的方法，根据实现情况拆分为三个接口
>
> *代码实现*
>
> ```java
> /**
>  * 接口隔离原则 改造后
>  */
> public class Segregation1 {
> 
>     public static void main(String[] args) {
>         A a = new A();
>         a.depend1(new B()); // A类通过接口去依赖B类
>         a.depend2(new B());
>         a.depend3(new B());
> 
>         C c = new C();
>         c.depend1(new D()); // C类通过接口去依赖D类
>         c.depend4(new D());
>         c.depend5(new D());
>     }
> }
> // 接口1
> interface Interface1{
>     void operation1();
> }
> // 接口2
> interface Interface2{
>     void operation2();
>     void operation3();
> }
> // 接口3
> interface Interface3{
>     void operation4();
>     void operation5();
> }
> class B implements Interface1,Interface2{
>     @Override
>     public void operation1() {
>         System.out.println("B 实现了 operation1");
>     }
>     @Override
>     public void operation2() {
>         System.out.println("B 实现了 operation2");
>     }
>     @Override
>     public void operation3() {
>         System.out.println("B 实现了 operation3");
>     }
> }
> class D implements Interface1,Interface3{
>     @Override
>     public void operation1() {
>         System.out.println("D 实现了 operation1");
>     }
>     @Override
>     public void operation4() {
>         System.out.println("D 实现了 operation4");
>     }
>     @Override
>     public void operation5() {
>         System.out.println("D 实现了 operation5");
>     }
> }
> class A{    // A类通过接口 Interface1,Interface2 依赖（使用）B类，但是只会用到1，2，3方法
>     public void depend1(Interface1 i){
>         i.operation1();
>     }
>     public void depend2(Interface2 i){
>         i.operation2();
>     }
>     public void depend3(Interface2 i){
>         i.operation3();
>     }
> }
> class C{    // C类通过接口 Interface1,Interface3 依赖（使用）D类，但是只会用到1，4，5方法
>     public void depend1(Interface1 i){
>         i.operation1();
>     }
>     public void depend4(Interface3 i){
>         i.operation4();
>     }
>     public void depend5(Interface3 i){
>         i.operation5();
>     }
> }
> ```

#### 依赖倒转（倒置）原则

> **基本介绍**
>
> 依赖倒转原则（Dependence Inversion Principle）是指：
>
> - 高层模块不应该依赖低层模块，二者都应该依赖其抽象
>
>
> - ==抽象不应该依赖细节，细节应该依赖抽象==
>
> - 依赖倒转（倒置）的中心思想是面向接口编程
>
>
> - 依赖倒转原则是基于这样的设计理念：相对于细节的多变性，抽象的东西要稳定的多。以抽象为基础搭建的架构比以细节为基础的架构要稳定的多。在java中，抽象指的是接口或抽象类，细节就是具体的实现类。
>
>
> - 使用==接口或抽象类==的目的是**制定好规范**，而不涉及任何具体的操作，把==展现细节的任务交给他们的实现类==去完成
>
> **应用实例**
>
> 编程完成Person 接收消息的功能
>
> *依赖倒转原则 改造前*
>
> ```java
> /**
>  * 依赖倒转原则
>  */
> public class DependencyInversion {
> 
>     public static void main(String[] args) {
>         Person person = new Person();
>         person.receive(new Email());
>     }
> }
> // 邮件类
> class Email{
>     public String getInfo(){
>         return "电子邮件信息：Hello，world！";
>     }
> }
> // 完成 Person 接收消息的功能
> // 方式1 分析
> // 1. 简单，比较容易想到
> // 2. 如果我们获取的对象是微信，短信等，则要新增类，同时Person也要增加相应的接收方法
> // 3. 解决思路：引入一个抽象的接口 IReceiver，表示接收者，这样Person类与接口发生依赖
> // 因为Email还有微信等都属于接收的范围，它们各自实现 IReceiver 接口就ok，这样我们就符合依赖倒转原则
> class Person{
>     public void receive(Email email){
>         System.out.println(email.getInfo());
>     }
> }
> ```
>
> *依赖倒转原则 改造后*
>
> ```java
> /**
>  * 依赖倒转原则 改造后
>  */
> public class DependencyInversion {
>     public static void main(String[] args) {
>         // 客户端无需改变
>         Person person = new Person();
>         person.receive(new Email());
> 
>         person.receive(new WeChat());
>     }
> }
> // 定义接口
> interface IReceiver{
>     String getInfo();
> }
> // 邮件类
> class Email implements IReceiver{
>     @Override
>     public String getInfo(){
>         return "电子邮件信息：Hello，world！";
>     }
> }
> // 增加微信
> class WeChat implements IReceiver{
>     @Override
>     public String getInfo() {
>         return "微信消息：hello，ok！";
>     }
> }
> // 完成 Person 接收消息的功能
> // 方式2
> class Person{
>     public void receive(IReceiver receiver){
>         // 这里我们是对接口的依赖
>         System.out.println(receiver.getInfo());
>     }
> }
> ```
>
> **依赖关系传递的三种方式和应用案例**
>
> - 接口传递
>
>
> - 构造方法传递
>
>
> - setter 方法传递
>
> *依赖关系传递的三种方式*
>
> 方式一
>
> ```java
> public class DependencyPass {
>     public static void main(String[] args) {
> 		// 方式一
> 		ChangHong changHong = new ChangHong();
> 		OpenAndClose openAndClose = new OpenAndClose();
> 		openAndClose.open(changHong);
>     }
> }
> // 方式1：通过接口传递实现依赖
> // 开关的接口
> interface IOpenAndClose{
>     void open(ITV tv);  // 抽象方法，接收接口
> }
> 
> interface ITV{  // ITV 接口
>     void play();
> }
> class ChangHong implements ITV{
> 
>     @Override
>     public void play() {
>         System.out.println("长虹电视机,打开");
>     }
> }
> 
> // 接口实现
> class OpenAndClose implements IOpenAndClose{
> 
>     @Override
>     public void open(ITV tv) {
>         tv.play();
>     }
> }
> ```
>
> 方式二
>
> ```java
> public class DependencyPass {
>     public static void main(String[] args) {
>         // 方式二 通过构造器进行依赖传递
>         ChangHong changHong = new ChangHong();
>         OpenAndClose openAndClose = new OpenAndClose(changHong);
>         openAndClose.open();
>     }
> }
> // 方式2：通过构造方法依赖传递
> interface IOpenAndClose{
>     void open();    // 抽象方法
> }
> interface ITV{  // ITV接口
>     void play();
> }
> class ChangHong implements ITV{
> 
>     @Override
>     public void play() {
>         System.out.println("长虹电视机,打开");
>     }
> }
> class OpenAndClose implements IOpenAndClose{
>     public ITV tv;  // 成员属性
> 
>     public OpenAndClose(ITV tv) {   // 构造器
>         this.tv = tv;
>     }
> 
>     @Override
>     public void open() {
>         tv.play();
>     }
> }
> ```
>
> 方式三
>
> ```java
> public class DependencyPass {
>     public static void main(String[] args) {
>         // 方式三 通过 setter 方法传递
>         ChangHong changHong = new ChangHong();
>         OpenAndClose openAndClose = new OpenAndClose();
>         openAndClose.setTv(changHong);
>         openAndClose.open();
>     }
> }
> // 方式3：通过 setter 方法传递
> interface IOpenAndClose{
>     void open();    // 抽象方法
> 
>     void setTv(ITV tv);
> }
> interface ITV{  // ITV接口
>     void play();
> }
> class OpenAndClose implements IOpenAndClose{
>     private ITV tv;
> 
>     @Override
>     public void setTv(ITV tv) {
>         this.tv = tv;
>     }
>     @Override
>     public void open() {
>         tv.play();
>     }
> }
> class ChangHong implements ITV{
> 
>     @Override
>     public void play() {
>         System.out.println("长虹电视机,打开");
>     }
> }
> ```
>
> **依赖倒转原则的注意事项和细节**
>
> - 低层模块尽量都要有抽象类或接口，或者两者都有，程序稳定性更好
>
> - 变量的声明类型尽量是抽象类或接口，这样我们的变量引用和实际对象间，就存在一个**缓冲层**，利于程序扩展和优化。
>
> - 继承时遵循里氏替换原则

#### 里氏替换原则

> **OO中的继承性的思考和说明**
>
> 继承包含这样一层含义：父类中凡是已经实现好的方法，实际上是在设定规范和契约，虽然它不强制要求所有的子类必须遵循这些契约，但是如果子类对这些已经实现的方法任意修改，就会对整个继承体系造成破坏。
>
> 继承在给程序设计带来便利的同时，也带来了弊端。比如使用继承会给程序带来侵入性，程序的可移植性降低，增加对象间的耦合性，如果一个类被其他的类所继承，则当这个类需要修改时，必须考虑到所有的子类，并且父类修改后，所有涉及到子类的功能都有可能产生故障。
>
> 问题提出：在编程中，如何正确的使用继承？ =>里氏替换原则
>
> **基本介绍**
>
> 里氏替换原则（Liskov Substitution Principle）在1988年，由麻省理工学院的一位姓里的女士提出的。
>
> 如果对每个类型为 T1 的对象 o1，都有类型为 T2 的对象 o2，使得以 T1 定义的所有程序 P 在所有的对象 o1 都代换成 o2 时，程序 P 的行为没有发生变化，那么类型 T2 是类型 T1 的子类型。换句话说，所有引用基类的地方必须能透明地使用其子类的对象。
>
> 在使用继承时，遵循里氏替换原则，在子类中尽量不要重写父类的方法。
>
> 里氏替换原则告诉我们，继承实际上让两个类耦合性增强了，在适当的情况下，可以通过聚合，组合，依赖来解决问题。
>
> **应用实例**
>
> *里氏替换原则示例*
>
> ```java
> /**
>  * 里氏替换原则
>  */
> public class LisKov {
>     public static void main(String[] args) {
>         A a = new A();
>         System.out.println("11 - 3 = " + a.func1(11,3));
>         System.out.println("1 - 8 = " + a.func1(1,8));
> 
>         System.out.println("---------------------------");
> 
>         B b = new B();
>         System.out.println("11 - 3 = " + b.func1(11,3));
>         System.out.println("1 - 8 = " + b.func1(1,8));
>         System.out.println("11 + 3 + 9 = " + b.func2(11,3));
>     }
> }
> // A类
> class A{
>     // 返回两个数的差
>     public int func1(int num1,int num2){
>         return num1 - num2;
>     }
> }
> // B继承了A
> // 增加了一个新功能：完成两个数相加，然后和9求和
> class B extends A{
>     // 这里重写了A类的方法，可能是无意识的
>     @Override
>     public int func1(int a, int b){
>         return a + b;
>     }
> 
>     public int func2(int a,int b){
>         return func1(a,b) + 9;
>     }
> }
> ```
>
> **解决方法**
>
> 我们发现原来运行正常的相减功能发生了错误。原因就是类 B 无意中重写了父类的方法，造成原有功能出现错误。在实际编程中，我们常常会通过重写父类的方法完成新的功能，这样写起来虽然简单，但整个继承体系的复用性会比较差。特别是运行多态比较频繁的时候。
>
> 通用的做法是：原来的父类和子类都继承一个更通俗的基类，原有的继承关系去掉，采用依赖，聚合，组合等关系代替
>
> **改进方案**
>
> ```java
> /**
>  * 里氏替换原则 改造后
>  */
> public class LisKov {
>     public static void main(String[] args) {
>         A a = new A();
>         System.out.println("11 - 3 = " + a.func1(11,3));
>         System.out.println("1 - 8 = " + a.func1(1,8));
> 
>         System.out.println("---------------------------");
> 
>         B b = new B();
>         // 因为 B 类不再继承 A类，因此调用者，不会再认为 func1 是求减法
>         // 调用完成的功能就会很明确
>         System.out.println("11 + 3 = " + b.func1(11,3));
>         System.out.println("1 + 8 = " + b.func1(1,8));
>         System.out.println("11 + 3 + 9 = " + b.func2(11,3));
> 
>         // 使用组合仍然可以使用 A 类的相关方法
>         System.out.println("11 -3 = " + b.func3(11,3));
>     }
> }
> // 创建一个更加基础的基类
> class Base{
>     // 把更加基础的方法和成员写到Base类
> }
> // A类
> class A extends Base{
>     // 返回两个数的差
>     public int func1(int num1,int num2){
>         return num1 - num2;
>     }
> }
> // B继承了A
> // 增加了一个新功能：完成两个数相加，然后和9求和
> class B extends Base {
>     // 如果B需要使用 A 类的方法，使用组合关系
>     private A a = new A();
>     // 这里重写了A类的方法，可能是无意识的
>     public int func1(int a, int b){
>         return a + b;
>     }
>     public int func2(int a,int b){
>         return func1(a,b) + 9;
>     }
>     // 我们仍然想使用 A 的方法
>     public int func3(int a,int b){
>         return this.a.func1(a,b);
>     }
> }
> ```

#### 开闭原则

> **基本介绍**
>
> 开闭原则（Open Closed Principle）是编程中最基础、最重要的设计原则
>
> 一个软件实体如类，模块和函数应该对扩展开放（对提供方），对修改关闭（对使用方）。用抽象构建框架，用实现扩展细节。
>
> 当软件需要变化时，尽量通过扩展软件实体的行为来实现变化，而不是通过修改已有的代码来实现变化。
>
> 编程中遵循其它原则，以及使用设计模式的目的就是遵循开闭原则。
>
> **应用实例**
>
> 看一个画图形的功能
>
> *方式一*
>
> ```java
> public class Ocp {
>     public static void main(String[] args) {
>         // 使用，看看存在的问题
>         GraphicEditor graphicEditor = new GraphicEditor();
>         graphicEditor.drawShape(new Rectangle());
>         graphicEditor.drawShape(new Circle());
>     }
> }
> // 这是一个用于绘图的类
> class GraphicEditor {
>     // 接收 Shape 对象，然后根据 type,来绘制不同的图形
>     public void drawShape(Shape s) {
>         if (s.m_type == 1) {
>             drawRectangle(s);
>         } else if (s.m_type == 2) {
>             drawCircle(s);
>         }
>     }
>     public void drawRectangle(Shape r) {
>         System.out.println("绘制矩形");
>     }
>     public void drawCircle(Shape r) {
>         System.out.println("绘制圆形");
>     }
> }
> // Shape 类，基类
> class Shape {
>     int m_type;
> }
> class Rectangle extends Shape {
>     Rectangle() {
>         super.m_type = 1;
>     }
> }
> class Circle extends Shape {
>     Circle() {
>         super.m_type = 2;
>     }
> }
> ```
>
> ==方式一的优缺点==
>
> - 优点是比较好理解，简单易操作
>
> - 缺点是违反了设计模式的ocp原则，即**对扩展开放（提供方），对修改关闭（使用方）**。即当我们给类增加新功能的时候，尽量不修改代码，或者尽可能少修改代码。
>
> **比如我们这时要新增加一个图形种类三角形，我们需要做如下修改，修改的地方较多**
>
> *代码演示*
>
> ```java
> public class Ocp {
>     public static void main(String[] args) {
>         // 使用，看看存在的问题
>         GraphicEditor graphicEditor = new GraphicEditor();
>         graphicEditor.drawShape(new Rectangle());
>         graphicEditor.drawShape(new Circle());
>         graphicEditor.drawShape(new Triangle());
>     }
> }
> // 这是一个用于绘图的类 [使用方法]
> class GraphicEditor {
>     // 接收 Shape 对象，然后根据 type,来绘制不同的图形
>     public void drawShape(Shape s) {
>         if (s.m_type == 1) {
>             drawRectangle(s);
>         } else if (s.m_type == 2) {
>             drawCircle(s);
>         }else if (s.m_type == 3) {
>             drawTriangle(s);
>         }
>     }
>     // 绘制矩形
>     public void drawRectangle(Shape r) {
>         System.out.println("绘制矩形");
>     }
>     // 绘制圆形
>     public void drawCircle(Shape r) {
>         System.out.println("绘制圆形");
>     }
>     // 绘制三角形
>     public void drawTriangle(Shape r) {
>         System.out.println("绘制三角形");
>     }
> }
> // Shape 类，基类
> class Shape {
>     int m_type;
> }
> class Rectangle extends Shape {
>     Rectangle() {
>         super.m_type = 1;
>     }
> }
> class Circle extends Shape {
>     Circle() {
>         super.m_type = 2;
>     }
> }
> // 新增画三角形
> class Triangle extends Shape{
>     Triangle() {
>         super.m_type = 3;
>     }
> }
> ```
>
> **方式一的改进思路分析**
>
> **思路**：把创建 **Shape 类做成抽象类**，并提供一个**抽象的 draw 方法**，让**子类去实现**即可，这样我们有新的图形种类时，只需要让新的图形类继承 Shape，并实现 draw 方法即可，使用方的代码不需要修改，满足了开闭原则
>
> *开闭原则 改造后*
>
> ```java
> public class Ocp {
>     public static void main(String[] args) {
>         // 使用，看看存在的问题
>         GraphicEditor graphicEditor = new GraphicEditor();
>         graphicEditor.drawShape(new Rectangle());
>         graphicEditor.drawShape(new Circle());
>         graphicEditor.drawShape(new Triangle());
>         graphicEditor.drawShape(new OtherGraphic());
>     }
> }
> // 这是一个用于绘图的类 [使用方]
> class GraphicEditor {
>     // 接收 Shape 对象，调用draw方法
>     public void drawShape(Shape s) {
>         s.draw();
>     }
> }
> // Shape 类，基类
> abstract class Shape {
>     int m_type;
>     public abstract void draw();
> }
> class Rectangle extends Shape {
>     Rectangle() {
>         super.m_type = 1;
>     }
>     @Override
>     public void draw() {
>         System.out.println("绘制矩形");
>     }
> }
> class Circle extends Shape {
>     Circle() {
>         super.m_type = 2;
>     }
>     @Override
>     public void draw() {
>         System.out.println("绘制圆形");
>     }
> }
> class Triangle extends Shape {
>     Triangle() {
>         super.m_type = 3;
>     }
>     @Override
>     public void draw() {
>         System.out.println("绘制三角形");
>     }
> }
> // 新增一个图形
> class OtherGraphic extends Shape {
>     OtherGraphic() {
>         super.m_type = 4;
>     }
>     @Override
>     public void draw() {
>         System.out.println("绘制其它图形");
>     }
> }
> ```

#### 迪米特法则

> **基本介绍**
>
> 
>
> 

#### 合成复用原则

> **基本介绍**
>
> 

## 代码块

> <span style="color: #329BDC;">代码块分为</span>：
>
> - **局部代码块**
>
>   ```java
>   public class DataInit {
>       private int id;
>       public int getId() {
>           {
>               id = 10;
>           }
>           return id;
>       }
>   }
>   ```
>
>   - 局部代码块定义在方法或语句中的代码块
>   - 特点：
>     - 注意代码块的作用域
>
> - **构造代码块**
>
>   ```java
>   public class DataInit {
>       private int id;
>       {
>           id = 5;
>       }
>   }
>   ```
>
>   - 构造代码块是定义在类的成员位置
>
>   - 特点：
>     - 优先于构造方法执行，构造代码块用于执行所有对象所需的初始化动作
>     - 每次创建对象的时候，都会执行一次构造代码块
>
> - **静态代码块**
>
>   ```java
>   public class DataInit {
>       private static int id;
>       static {
>           id = 5;
>       }
>   }
>   ```
>
>   - 静态代码块是定义在成员位置，使用static修饰的代码块
>   - 特点：
>     - 优先于主方法执行，优先于构造代码块执行，当以任意形式第一次使用到该类时执行
>     - 该类不管创建多少个对象，静态代码块只会执行一次
>     - 静态代码块，只能为静态属性赋值

## 内部类

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
>  	修饰符 class 类名 {
>  	}
> }
> ```
>
> 范例：
>
> ```java
> public class Outer {
>  	public class Inner {
>  	}
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

### 成员内部类

> 按照内部类在类中定义的位置不同，可以分为如下两种形式
>
> - 在类的成员位置：成员内部类
>- 在类的局部位置：局部内部类
> 
>成员内部类，外界创建对象使用的格式
> 
>- 格式：<span style="color: red;">外部类名</span>.<span style="color: #329BDC;">内部类名</span> 对象名 = <span style="color: red;">外部类对象</span>.<span style="color: #329BDC;">内部类对象</span>;
> - 范例：<span style="color: red;">Outer</span>.<span style="color: #329BDC;">Inner</span> oi = <span style="color: red;">new Outer()</span>.<span style="color: #329BDC;">new Inner()</span>;
> 
>  ```java
>  public class Outer {
>     private int num = 10;
> 
>    public class Inner {
>         public void show() {
>            System.out.println(num);	// 10
>         }
>     }
>  }
>  public class InneerDemo {
>     public static void main(String[] args) {
>         // 创建内部类对象，并调用方法
>      	Outer.Inner oi = new Outer().new Inner();
>         oi.show();	// 10
>    }
> }
>  ```
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
>    }
> }
>
> public class InneerDemo {
>    public static void main(String[] args) {
>       	Outer.o = new Outer();
>         o.method;	// 10
>    }
> }
>```
> 

### 局部内部类

> 局部内部类是在方法中定义的类，所以外界是无法直接使用，需要在方法内部创建对象并使用
>
> 该类可以直接访问外部类的成员，也可以访问方法内的局部变量
>
> ```java
>public class Outer {
>     private int num = 10;
>
>     public void method() {
>         int num2 = 20;
>          class Inner {
>          	public void show() {
>                 // 访问外部类的成员
>             	System.out.println(num);	// 10
>                // 访问方法内的局部变量
>                 System.out.println(num2);	
>        	}
>         }
>         // 在方法内部创建对象并使用
>          Inner i = new Inner();
>          i.show();
>     }
> }
>
> public class OuterDemo {
>    public static void main(String[] args) {
>       	Outer.o = new Outer();
>         o.method;	// 10
>        			// 20
>     }
> }
> ```
> 

### 匿名内部类

> 匿名内部类属于一种特殊的局部内部类
>
> *前提：存在一个类或者接口，这里的类可以是具体类也可以是抽象类*
>
> - 格式：
>
>   ```java
>  new 类名或者接口名(){
>       重写方法;
>   }
>   ```
>
> - 范例：
>
>  ```java
>   new Inter() {
>      public void show(){
>       }
>   }
>  ```
>
> <span style="color: red;">匿名内部类的本质：是一个继承了该类或者实现了该接口的子类匿名对象</span>
>
> **单次调用**
>
> ```java
> public class Outer {
>     public void method() {
>       new Inter() {
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
> **多次调用**
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
>           @Override
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
> **匿名内部类不可以定义构造器(没有类名)**
>
> - 匿名内部类中的构造代码块充当了构造器的作用
>
> - 如果需要定义有参数构造器，只需要在小括号中传参就可以了
>
>   ```java
>    new Inter(int id) {
>       public void show(){
>        }
>    }
>   ```
>
> **在使用匿名内部类的过程中，我们需要注意如下几点**
>
> - 匿名内部类中不能存在任何的静态成员变量和静态方法
> - 匿名内部类不能是抽象的，它必须要实现继承的类或者实现的接口的所有抽象方法
> - 使用匿名内部类时，我们必须是继承一个类或者实现一个接口，但是两者不可兼得，同时也只能继承一个类或者实现一个接口
> - 匿名内部类中是不能定义构造函数的
> - 匿名内部类为局部内部类，所以局部内部类的所有限制同样对匿名内部类生效

### 静态内部类

> 创建内部类对象，静态内部类不需要依靠外部类的实例，跟普通类是一样的
>
> ```java
>// 外部类
> public class Outer {
>    // 静态内部类
>     public static class Inner {
>    	System.out.println("这是一个静态内部类");
>     }
> }
>  
>  public class OuterDemo {
>     public static void main(String[] args) {
>       	Inner in = new Inner();
>        in.show();
>     }
>}
> ```
> 
>  

## 常用类

### String类

> 字符串类属于四大基本引用类型之一，该类用于创建和操作字符串
>
> 常用的方法：
>
> | 方法名                | 说明                                                         |
>| --------------------- | ------------------------------------------------------------ |
> | charAt()              | 通过指定位置，返回对应字符                                   |
> | indexOf()             | 通过查找字符，返回第一次出现字符的位置                       |
> | lastIndexOf()         | 通过末尾开始查找，返回第一次出现字符的位置                   |
> | subString(start, end) | 截取子字符串，形成新字符串(如果有结束下标位置，不包含结束下标) |
> | length()              | 获取到字符串的长度                                           |
> | indexOf(str, start)   | 从指定位置开始查找，对应字符，并返回第一次匹配到的字符位置   |
> | split()               | 通过指定字符拆分字符串为字符串数组，数组中不包含指定字符     |
> | String.join(str, arr) | 通过指定字符，将数组元素拼接为字符串                         |
> | trim()                | 去掉字符串前后空格                                           |
> | replace(str, str)     | 通过查找字符，将该字符替换为指定的字符                       |
> | toCharArray()         | 将内容转换为字符数组                                         |
> 
> <span style="color: red;">String对象的特点</span>
>
> 1. 通过new创建的字符串对象，每一次new都会申请一个内存空间，虽然内容相同，但是地址值不同
>
>    ```java
>     String a = new String("helloworld");
>    String b = new String("helloworld");
>    Systen.out.println(a == b); // false
>    ```
> 
> 2. 以“”方式给出的字符串，只要字符序列相同(顺序和大小写)，无论在程序代码中出现几次，JVM都只会建立一个String对象，并在字符串池中维护
>
>    ```java
>     String a = "helloworld";
>    String b = "hello"+"world";
>    Systen.out.println(a == b); // true
>    ```
> 

### StringBuffer类

> 概述：线程安全的一个可变长度字符序列。 字符串缓冲区就像一个String，但可以修改。初始容量为16个字符
>
> |       方法名        | 说明                                   |
>| :-----------------: | -------------------------------------- |
> | new StringBuffer()  | 构造方法                               |
>|    append(元素);    | 添加元素到末尾                         |
> |     indexOf();      | 通过查找字符，返回第一次出现字符的位置 |
> | insert(下标, 元素); | 在指定位置插入元素                     |
> |     reverse();      | 倒转字符串                             |
> 

### StringBuilder类

> 概述：StringBuilder是一个可变字符串类，我们可以把它看成是一个容器(这里的可变指的是StringBuilder对象中的内容是可变的)
>
> 此类的方法与StringBuffer相同，但不保证线程安全。 此类设计用作简易替换为StringBuffer在正在使用由单个线程字符串缓冲区的地方（如通常是这种情况）
>
> <span style="color: red;">String和StringBuilder的区别</span>
>
> - String：内容是不可变的
> - StringBuilder：内容是可变的
> 
> **String、StringBuffer、StringBuilder之间的区别**
> 
> - String
>   - 效率最低
>   - 在操作字符串过程中,会舍弃原有空间开辟新的空间
>   - 没有做线程安全
> - StringBuffer
>   - 效率略高
>   - 这是一个字符串缓冲区,所有字符操作在同一空间,所有效率略高
>   - 有做线程安全
>- StringBuilder
>   - 效率最高
>  - 和StringBuffer是在同一空间
>   - 没有做线程安全
>

### Java 中操作字符串都有哪些类？它们之间有什么区别？

> 操作字符串的类有：<span style="color: red;">String、StringBuffer、StringBuilder</span>。
>
> **String**：
>
> String 是只读字符串，也就意味着String 引用的字符串内容是不能被改变的。str 仅仅是一个引用对象，它指向一个字符串对象“abc”。第
> 二行代码的含义是让str 重新指向了一个新的字符串“bcd”对象，而“abc”对象并没有任何改变，只不过该对象已
> 经成为一个不可及对象罢了。
>
> **StringBuffer**：
>
> StringBuffer/StringBuilder 表示的字符串对象可以直接进行修改
>
> **StringBuilder**：
>
> StringBuilder 是Java5 中引入的，它和StringBuffer 的方法完全相同，区别在于它是在单线程环境下使用的，因为它的所有方法都没有被synchronized 修饰，因此它的效率理论上也比StringBuffer 要高

### System类

> System包含几个有用的类字段和方法，它不能被实例化，这个类为我们提供了一些与工具或系统交互的方法
>
> **exit**	终止当前运行java虚拟机，非零表示异常终止
>
> ```java
>public static void main(String[] args) {
>     for(int i=0;i<100000;i++){
>         System.out.println("第"+(i+1)+"次");	// 第50001次
> 		if(i==50000){
> 			//系统退出,停掉了虚拟机
> 			System.exit(0);
> 		}
>     }
> }
> ```
> 
> **currentTimeMillis**	获取当前时间毫秒数
> 
> ```java
>public static void main(String[] args) {
>     //获取开始时间
>    long start = System.currentTimeMillis();
>     for(int i=0;i<100000;i++)
>		System.out.println("第"+(i+1)+"次");	// 进行100000次循环总共用时692毫秒
>     //获取结束时间
> 	long end = System.currentTimeMillis();
> 	System.out.println("总共耗时:"+(end-start));	// 总共耗时:692
> }
> ```
>

### Date类

> Date代表了一个特定的时间，精确到毫秒
>
> 构造方法：
>
> |        构造方法        | 说明                                                         |
>| :--------------------: | ------------------------------------------------------------ |
> |     public Date()      | 分配一个 `Date`对象，并初始化它，以便它代表它被分配的时间，测量到最近的毫秒 |
> | public Date(long date) | 分配一个 `Date`对象，并将其初始化为表示从标准基准时间起指定的毫秒数 |
> 
> 常用的方法：
> 
> |             方法名             | 说明                                                 |
> | :----------------------------: | ---------------------------------------------------- |
> |     public long getTime()      | 获取的是日期对象从1970年1月1日00:00:00到现在的毫秒数 |
> | public void setTime(long time) | 设置时间，给的是毫秒值                               |
> 

### DateFormat类

> DateFormat类是日期/时间格式化子类的抽象类，它以语言无关的方式格式化和分析日期或时间。可以通过指定格式将日期转换为字符串,字符串转换为日期
>
> DateFormat有一个子类实现类叫做SimpleDateFormat,这个子类实现类中提供了转换的方法
>
> 日期和时间格式由日期和时间模式字符串指定，在日期和时间模式字符串中，从‘A’到‘Z’以及从‘a’到‘z’引号的字母被解释为表示日期或时间字符串的组件的模式字母
>
> ![][4]
>
> 常用的模式字母及对应关系：
>
> | 字母 | 模式 |
> | :--: | :--: |
> |  y   |  年  |
> |  M   |  月  |
> |  d   |  日  |
> |  H   |  时  |
> |  m   |  分  |
> |  s   |  秒  |
>
> SimpleDateFormat的构造方法
>
> |                 方法名                  | 说明                                                     |
> | :-------------------------------------: | -------------------------------------------------------- |
> |        public SimpleDateFormat()        | 构造一个SimpleDateFormat，使用默认模式和日期格式         |
> | public SimpleDateFormat(String pattern) | 构造一个SimpleDateFormat，使用给定的模式和默认的日期格式 |
>
> SimpleDateFormat格式化和解析日期
>
> 1. 格式化(从 Date 到 String)：
>
>    1. public final String <span style="color: red;">fomat(Date date)</span>：将日期格式化成日期/时间字符串
>
>       ```java
>       public class DateFormatDemo {
>       	public static void main(String[] args) {
>               Date date = new Date();
>       		// 创建一个格式化对象,并设定格式
>               DateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss SS");
>       		String time = df.format(date);
>       		System.out.println(time);	// 2021-09-26 10:42:19 587
>       	}
>       }
>
> 2. 解析(从 String 到 Date)：
>
>    1. public Date <span style="color: red;">parse(String source)</span>：从给定字符串的开始解析文本以生成日期
>
>       ```java
>       public class DateFormatDemo {
>       	public static void main(String[] args) {
>       		// 设定日期字符串
>       		String str = "2008年10月01日 20时18分52秒";
>       		df = new SimpleDateFormat("yyyy年MM月dd日 HH时mm分ss秒");
>       		//将字符串转换为日期
>       		Date d = df.parse(str);
>       		System.out.println(d);	// Wed Oct 01 20:18:52 CST 2008
>       	}
>       }
>    
>

### Calendar日历类

> Calendar为特定瞬间与一组日历字段之间的转换提供一系列操作方法
>
> Calendar提供一个类方法getInstance用于获取当前日期的日历对象
>
> 使用方法获取到日历或操作日历
>
> 常用方法:
> 
> - get(日历字段);
> - set(year,month,date);
> - add();
> 

### Integer 包装类

> 包装类是基本数据类型封装成对象，为该数据类型提供丰富的操作方法
>
> 常用方法：基本数据类型与字符串之间的转换
>
> 基本类型对应的包装类：
>
> | 基本类型 | 包装类型  |
> | -------- | --------- |
> | byte     | Byte      |
> | short    | Short     |
> | int      | Integer   |
> | long     | Long      |
> | float    | Float     |
> | double   | Double    |
> | char     | Character |
> | boolean  | Boolean   |
> 
> Integer类(常用)：包装一个对象中的原始类型int值
> 
>可以使用方法: Integer(int value) Integer(String 数字) parseInt(String 数字) ValueOf(String 数字)
> 
>```java
> public class IntegerDemo {
>	public static void main(String[] args) {
> 		//通过包装类,将原始数据类型转换为包装类
> 		int num = 34;
> 		//将原始数据包装
> 		Integer i = new Integer(num);
> 		//通过构造方法将字符串转换为数字
>		Integer s = new Integer("15");
> 		//通过parseInt将字符串转换为数字
>		Integer s1 = Integer.parseInt("23");
> 		//通过valueOf()将字符串转换为数字
> 		Integer s2 = Integer.valueOf("28");
> 
> 		Integer num1 = 35;   //直接将数字赋值给包装类,这种方式叫做包装类的自动装箱
> 		int num2 = num1;		//直接将包装类数据变为原始数据,这种叫做包装类的自动拆箱
>
> 		Double d = new Double("32.5"); //字符串转换小数
>		System.out.println(i+s);		// 49
> 		System.out.println(i+s+s1);		// 72
>		System.out.println(i+s+s1+s2);	// 100
> 	}
> }
> ```
> 
> *int和String的相互转换*
> 
> ```java
>// int ---> String
> int number = 100;
>String s = "" + number;
> 
>// String ---> int
> String s = "100";
>Integer i = Integer.valueof(s);
> int x = i.intValue();
>System.out.println
> ```
> 

### Object类

> Object类是所有类的基类，所有类都直接或间接的继承自Object类
>
> - toString方法是属于Object类的方法，其他类使用的toString是重写Object的方法
>- equals方法是属于Object类的方法，其他类使用时，也是重写的Object类的方法
> 

### Math类

> 数学类
>
> 包含执行基本数字运算方法，方法为静态方法
>
> 包含的方法：
>
> | 方法名                                                 | 说明                               |
> | ------------------------------------------------------ | ---------------------------------- |
> | abs                                                    | 返回参数的绝对值                   |
> | ceil                                                   | 向上取整，取到一个最大值整数       |
> | floor                                                  | 向下取整，取到一个最小值整数       |
> | <span style="color: #329BDC;">round</span>             | 四舍五入                           |
> | <span style="color: #329BDC;">max(int a, int b)</span> | 获取两个值中的最大值               |
> | <span style="color: #329BDC;">min(int a, int b)</span> | 获取两个值中的最小值               |
> | <span style="color: #329BDC;">random</span>            | 获取一个0到1之间的小数(不包含0和1) |

## 异常处理

> **编译时异常和运行时异常的区别**
>
> Java 中的异常被分为两大类：<span style="color: red;">编译时异常</span>和<span style="color: red;">运行时异常</span>，也被称为<span style="color: red;">受检异常</span>和<span style="color: red;">非受检异常</span>
>
> 所有的RuntimeException类及其子类被称为运行时异常，其他的异常都是编译时异常
>
> - 编译时异常：必须显示处理，否则程序就会发生错误，无法通过编译
> - 运行时异常：无需显示处理，也可以和编译时异常一样处理
>
> ```java
> public class ExceptionDemo {
> 	public static void main(String[] args) {
> 		method();
> 		method2();
> 	}
> 
> 	// 运行时异常
> 	public static void method() {
> 		try {
> 			int[] arr = { 1, 2, 3 };
> 			System.out.println(arr[3]); // java.lang.ArrayIndexOutOfBoundsException
> 		} catch (ArrayIndexOutOfBoundsException e) {
> 			e.printStackTrace();
> 		}
> 	}
> 
> 	// 编译时异常
> 	public static void method2() {
> 		String s = "2048-08-09";
> 		SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
> 		Date d;
> 		try {
> 			d = sdf.parse(s);	// 可能会出问题，需要处理
> 			System.out.println(d);
> 		} catch (ParseException e) {
> 			e.printStackTrace();
> 		}
> 	}
> }
> ```
>
> 如果程序出现了问题，我们需要自己来处理，有两种方案：**try--catch**和**throws**
>

### try--catch

> - 格式
>
>   ```java
>    try {
>       可能出现异常的代码;
>    } catch(异常类名 变量名) {
>       异常的处理代码;
>   }
>
> - 范例
>
>   ```java
>   try {
>         System.out.println("pls input num1:");
>         int num1 = in.nextInt();
>         System.out.println("pls input num2:");
>         int num2 = in.nextInt();
>         System.out.println(num1 / num2);
>     } catch (Exception e) {
>         System.out.println(e.getMessage());
>     }
>   ```
>
> - 执行流程：
>
>   - 程序从try里面的代码开始执行
>   - 出现异常，会自动生成一个异常类对象，该异常对象将被提交给Java运行时系统
>   - 当Java运行时系统接收到异常对象时，会到catch中去找匹配的异常类，找到后进行异常的处理
>   - 执行完毕之后，程序还可以继续往下执行
>

### throws

> - 格式
>
>   ```java
>  throws 异常类名;
>   ```
>
>   <span style="color: red;">注意：</span>这个格式是跟在方法的括号后面的
> 
>- 范例
> 
>   ```java
>   public static void method() throws ArrayIndexOutOfBoundsException {
>       int[] arr = {1, 2, 3};
>       System.out.println(arr[3]);
>   }
>   ```
> 
>   - <span style="color: red;">编译时异常必须要进行处理</span>，两种处理方案：**try--catch**和**throws**，如果采用**throws**这种方案，将来谁调用谁处理
>   - <span style="color: red;">运行时异常可以不处理</span>，出现问题后，需要我们回来修改代码
> 
> - 使用
> 
>   ```java
>   public static void main(String[] args) {
>       Scanner in = new Scanner(System.in);
>       System.out.println("请输入当前日期:");
>       String str = in.next();
>       // 调用转换方法,但是转换方法中可能出现异常,在这里必须处理异常,否则也抛出异常,最终抛向JVM,处理后结束
>       Date date = null;
>       try {
>           // 这里处理抛出的异常
>           date = format(str);
>       } catch (ParseException e) {
>           System.out.println("格式转换异常");
>       }
>       System.out.println(date);
>   }
>                                                       
>   private static Date format(String str) throws ParseException {	// 仅抛出异常
>       DateFormat df = new SimpleDateFormat("yyyy-MM-dd");
>      // 因为异常已经抛出,所以当前不需要处理异常
>       return df.parse(str);
>    }
>   ```
>
> ![][1]
>

### Throwable

> **Throwable的成员方法**
>
> |            方法名             |               说明                |
>| :---------------------------: | :-------------------------------: |
> |  public String getMessage()   | 返回此 throwable 的详细消息字符串 |
>|   public String toString()    |      返回此可抛出的简短描述       |
> | public void printStackTrace() |   把异常的错误信息输出在控制台    |
> 
>- <span style="color: red;">异常的体系结构</span>
> 
>   - **Throwable  所有异常和错误的父类**
>   - **Error错误 这种错误,程序本身无法解决**
>   - **Exception 所有异常的父类 包含运行时异常(RuntimeException)和非运行时异常。可以由程序捕捉、处理**
> 
>   ![][2]
> 
> *异常可以分为三大类：**运行时异常**、**非运行时异常(编译异常)**、**Error（错误）*** 

### 自定义异常

> **用于开发者手动抛出自定义异常**
>
> - 格式：
>
>   ```java
>  public class 异常类名 extends Exception {
>      无参构造
>      带参构造
>   }
>   ```
>
> - 范例：
>
>   ```java
>   public class ScoreException extends Exception {
>       public ScoreException() {}
>       public ScoreException(String message) {
>           super(message);
>       }
>   }
>   ```
>
> - 使用：
>
>   ```java
>   public static void main(String[] args) {
>       Scanner in = new Scanner(System.in);
>       System.out.println("请输入学生性别:");
>       String sex = in.next();
>       try {
>           checkSex(sex);
>       } catch (Exception e) {
>           // 此处处理的异常为自定义异常
>           System.out.println(e.getMessage());	// 性别必须是'男'或者'女'！
>       }
>       System.out.println("验明正身");
>   }
>             
>   //想要抛出一个实例,方法后还得抛出一个对应的类型
>   public static void checkSex(String sex) throws Exception {
>       if ("男".equals(sex) || "女".equals(sex))
>           System.out.println("性别为:"+sex);
>      else {
>           //throw 抛出一个异常的实例,构造方法填写异常的信息
>          throw new Exception("性别必须是'男'或者'女'！");
>       }
>    }
>   ```
>
> *throw抛出的是异常的实例*
>
> ![][3]
>
> - throws和throw的区别
>
>   |                      throws                      |               throw                |
>    | :----------------------------------------------: | :--------------------------------: |
>   |         用在方法声明后面，跟的是异常类名         |   用在方法体内，跟的是异常对象名   |
>    |       表示抛出异常，由该方法的调用者来处理       | 表示抛出异常，由方法体内的语句处理 |
>   | 表示出现异常的一种可能性，并不一定会发生这些异常 |    执行throw一定抛出了某种异常     |
>

### throw 和 throws 的区别

> **throw**：
>
> 1. throw 语句用在方法体内，表示抛出异常，由方法体内的语句处理。
> 2. throw 是具体向外抛出异常的动作，所以它抛出的是一个异常实例，执行throw 一定是抛出了某种异常。
>
> **throws**：
>
> 1. throws 语句是用在方法声明后面，表示如果抛出异常，由该方法的调用者来进行异常的处理。
> 2. throws 主要是声明这个方法会抛出某种类型的异常，让它的使用者要知道需要捕获的异常的类型。
> 3. throws 表示出现异常的一种可能性，并不一定会发生这种异常

### finally

> <span style="color: red;">finally语句块总是会被执行</span>。它主要用于回收在try块里打开的物理资源(如数据库连接、网络连接和磁盘文件)。只有finally块执行完成之后，才会回来执行try或者catch块中的return或者throw语句，如果finally中使用了return或者throw等终止方法的语句，则就不会跳回执行，直接停止
>
> ```java
> public static void main(String[] args) {
>  	Scanner in = new Scanner(System.in);
> 	System.out.println("请输入学生性别:");
>  	String sex = in.next();
>  	try {
>    		checkSex(sex);
>  	} catch (Exception e) {
>    		// 此处处理的异常为自定义异常
>    		System.out.println(e.getMessage());	// 性别必须是'男'或者'女'！
>  	} finally {
>    		System.out.println("验明正身");
>  	}
> }
> ```
>
> **至少有两种情况下finally语句是不会被执行**
>
> - *try语句没有被执行到，如在try语句之前就返回了，这样finally语句就不会执行，这也说明了finally语句被执行的必要而非充分条件是：相应的try语句一定被执行到*
> - *在try块中有System.exit(0);这样的语句，System.exit(0);是终止Java虚拟机JVM的，连JVM都停止了，所有都结束了，当然finally语句也不会被执行到*
>
> **finally语句是在try的return语句执行之后，return返回之前执行**

## final、finally、finalize 有什么区别

> - **final**：是修饰符，如果修饰类，此类不能被继承；如果修饰方法和变量，则表示此方法和此变量不能在被改变，只能使用。
> - **finally**：是 try{} catch{} finally{} 最后一部分，表示不论发生任何情况都会执行，finally 部分可以省略，但如果 finally 部分存在，则一定会执行 finally 里面的代码。
> - **finalize**： 是 Object 类的一个方法，在垃圾收集器执行的时候会调用被回收对象的此方法。

## 集合

> 集合的特点：提供一种存储空间可变的存储模型，存储的数据容量可以随时发生改变
>
> 集合体系结构
>

### Collection

> 概述：
>
> - 是单例集合的顶层接口，它表示一组对象，这些对象称之为<span style="color: red;">Collection元素</span>，统一存储Object对象
> - **JDK不提供此接口的任何直接实现，它提供更具体的子接口(List和Set)实现**
>

#### List

> - 概述：*有序集合，用户可以精确控制列表中每个元素的插入位置，也可以通过索引访问具体元素，并搜索列表中的元素*
>
> - 特点：
>
>   - 有索引
>   - 可以存储重复元素
>   - 元素取值有序
>
> - List集合下有两个子类实现类：
>
>   - ArrayList(动态数组集合)
>   - LinkedList(链式集合)

##### ArrayList(动态数组集合)

>   变相的数组，和数组一样可以存储多个元素，但集合没有固定长度，集合中的每一个元素类型为Object类型
>
>   - 格式：
>
>     ```java
>     List 集合名 = new ArrayList();
>     ```
>
>   - 常用方法：
>
>     |                  方法名                  | 说明                         |
>     | :--------------------------------------: | ---------------------------- |
>     | add(元素)，add(下标, 元素)，addAll(集合) | 添加元素                     |
>     |            set(下标, 元素)，             | 修改对应下标元素             |
>     |        remove(下标)，remove(元素)        | 删除对应元素(整数默认为下标) |
>     |                get(下标)                 | 获取对应下标元素             |
>     |                  size()                  | 获取元素的个数               |

##### LinkedList(链式集合)

>   是List集合的子类实现类，是一种链式的动态数组，与ArrayList集合相似，但是
>
>   - 格式
>
>     ```java
>     LinkedList 集合名 = new LinkedList();
>     ```
>
>   - 常用方法：
>
>     |                  方法名                  | 说明             |
>     | :--------------------------------------: | ---------------- |
>     | add(元素)，add(下标, 元素)，addAll(集合) | 添加元素         |
>     |              addFirst(元素)              | 添加元素到开头   |
>     |                get(下标)                 | 获取对应下标元素 |
>     |                getFirst()                | 获取第一个元素   |
>     |                getLast()                 | 获取最后一个元素 |
>     |              removeFirst()               | 删除第一个元素   |
>     |               removeLast()               | 删除最后一个元素 |
>
>   - 遍历集合
>
>     ```java
>     LinkedList ll = new LinkedList();
>     ll.add("1");
>     ll.add("2");
>     ...
>     ll.add("100");
>     for(Object object : ll)
>         System.out.println(object);
>     ```
>
>   - 使用List集合存储学生对象
>
>   ```java
>   public class StudentDemo {
>   	public static void main(String[] args) {
>   		List studentList = new ArrayList();
>   
>   		studentList.add(new Student(1, "123", "男", 25));
>   		studentList.add(new Student(2, "456", "男", 23));
>   		studentList.add(new Student(3, "789", "男", 22));
>   
>   		for (Object object : studentList) {
>   			Student stu = (Student) object;
>   			System.out.println(
>   					"学生编号：" + stu.getId() + " 学生姓名：" + stu.getName() + " 学生性别：" + stu.getSex() + " 学生年龄：" + stu.getAge());
>   		}
>   	}
>   }
>   ```

#### Set

>概述：Set集合继承于Collection，是一种无序且唯一的集合

##### HashSet 

>**HashSet 是 Set 集合接口的子类实现类**
>
>- HashSet 的特点：
>- 不能保证数据的顺序
>- 集合元素可以是 null，但是只能有一个
>- HashSet 不是线程安全的
>
>**格式**
>
>```java
>Set 集合名 = new HashSet;
>```
>
>**常用方法**
>
>|    方法名    | 说明                 |
>| :----------: | -------------------- |
>|  add(元素)   | 添加元素             |
>|    size()    | 获取元素的个数       |
>| remove(元素) | 删除对应元素         |
>|  iterator()  | 迭代器，用于遍历集合 |
>
>- *Iterator 迭代器*
>
>- *Iterator 迭代器*，承载集合中元素,用于遍历集合,迭代器本身不能存储数据,但是能通过迭代器删除集合底层元素
>
>- 循环遍历迭代器：
>
>  ```java
> Set set = new HashSet();
>
> set.add("1");
>  ll.add("2");
>  ...
>        ll.add("100");
>  // 遍历集合，因为Set集合没有下标，故此不能使用for循环遍历，这时候需要使用迭代器
>  Iterator it = set.iterator();
>  // 循环遍历迭代器
>  // 判断迭代器中是否还有下一个元素，如果没有就返回false
>  while(it.hasNext()) {
>      // 有就取出
>      Object obj = it.next();
>      System.out.println(obj);
>  }
>  // forEach循环遍历集合，也不需要下标
>  for(Object object : set)
>      System.out.println(object);
>
>  ```

### Map

>概述：map集合是一种键对应值的集合,键采用set集合方式存储,value采用collection集合方式存储
>
>- Interface Map<K,V>
>  - K：键的类型，使用Set存储，无序且唯一
>  - V：值的类型，使用Collection存储，可重复
>- 将键映射到值的对象；不能包含重复的键；每个键可以映射到最多一个值
>- 举例：学生的学号和姓名
>  - itheima001	李狗蛋
>  - itheima002	王铁蛋
>  - itheima003	张钢蛋
>

#### 创建Map集合的对象

>- 多态的方式
>
>- 具体的实现类HashMap
>
>  ```java
>  Map map = new HashMap();
>  ```
>

#### 特点

>- 键值对映射关系
>- 一个键对应一个值
>- 键不能重复,值可以重复
>- 元素存取无序
>
>常用方法：
>
>|      方法名      | 说明            |
>| :--------------: | --------------- |
>| put(key, value); | 添加元素        |
>|  putAll(Map m);  | 添加Map集合     |
>|     keySet()     | 返回所有的key值 |
>|     get(key)     | 根据key来获取值 |
>|      size()      | 获取元素个数    |
>|     clear()      | 移除所有键值对  |
>|   remove(key)    | 通过key删除元素 |
>| containsKey(key) | 判断键是否存在  |
>

#### 遍历Map集合

>```java
>Map<String, Object> map = new HashMap<>();
>map.put(key1, value1);
>map.put(key2, value2);
>...
>map.put(key10, value10);
>
>// 获取到所有的键
>Set set = map.keySet();
>for(Object key : set){
>	// map.get(键)得到对应的value值
>	System.out.println(key+"对应的值有:"+map.get(key));
>}
>```
>
>**JDK8新增的迭代方式**
>
>```java
>Map<String, Object> map = new HashMap<>();
>map.put(key1, value1);
>map.put(key2, value2);
>...
>map.put(key10, value10);
>
>// 获取到所有的键
>map.forEach((k, v) -> {
>    System.out.println("key:" + k + ",value:" + v);
>});
>```

### 泛型

>概述：本质是参数化类型，就是将类型由原来的具体的类型参数化，然后在使用/调用时传入具体的类型
>
>- 解决元素存储的安全性问题
>- 解决获取元素时，需要类型强制转换的问题
>

#### 泛型使用

>**\<T> **：
>
>- 泛型使用<>来表示泛型，在<>中规定泛型的对应类型
>
>- 声明式泛型，采用T，E来表示一个占位,等待具体赋予指定类型
>
>- <span style="color: red;">注意：T或E只能是类，不能使用基本数据类型；若要使用基本数据类型，需要转换成 Integer 类 </span>
>
>- 范例：
>
> ```java
> // 在JDK1.7之前对象中的<>内也必须填写泛型，JDK1.7之后默认为前方类型
> List<Student> list = new ArrayList<>();
> // list.add("zhangsan");	// 报错，泛型规定list中只能放Student类型对象
> list.add(new Student(1, "123", "男", 25));
> // 遍历集合不需要任何强转
> for(Student stu : list){
>      // 默认规定只能存储类型，所以不需要任何强转
>      System.out.println(stu.toString());
>  }
> ```
> 

##### 泛型中占位符 T 和 ? 的区别

> **T**：指的是某一类具体的对象，*使用 T 占位符后，List集合里只能存放同一类型数据，如果插入不同类型数据则会报错*
>
> **?**：可以表示成占位符，它自己也不知道list集合中会存放多少种类型的数据，所以*使用 ? 作为占位符后，在List中可以存放不同数据类型的数据*

#### Map集合使用泛型

>*值对应的类型是一个集合，就需要放置集合类型，集合中也需要泛型*
>
>- 格式：
>
>  ```java
>  Map<String, List<String>> map = new HashMap<>();
>  ```
>
>- 范例：
>
>  ```java
>  public class MapCityDemo {
>  
>  	public static void main(String[] args) {
>  		//创建map集合,一般key使用String类型,值可以是任意类型
>  		//值对应的类型是一个集合,就需要放置集合类型,集合中也需要泛型
>  		Map<String, List<String>> map = new HashMap<>();
>  		//广东省
>  		List<String> list = new ArrayList<>();
>  		list.add("广州市");
>  		list.add("深圳市");
>  		list.add("佛山市");
>  		//广西省
>  		List<String> list1 = new ArrayList<>();
>  		list1.add("南宁市");
>  		list1.add("桂林市");
>  		list1.add("玉林市");
>  		list1.add("柳州市");
>  
>  		map.put("广东省", list);
>  		map.put("广西省", list1);
>  
>  		//获取到所有的键
>  		Set<String> set = map.keySet();
>  		for (String key : set) {
>  			//map.get(键)得到对应的value值
>  			System.out.println(key+"对应的值有:");
>  			for (String city : map.get(key)) {
>  				System.out.println(city);
>  			}
>  		}
>  		System.out.println("集合中是否有广东这个key:"+map.containsKey("广东省"));
>  	}
>  }
>  ```
>

####　静态方法使用泛型

> **static <T> 表示将该方法声明为泛型方法**
>
> 以下写法不能通过编译
>
> ```java
> public static List<T> getList() {}
> ```
>
> 需要改成如下写法
>
> ```java
> public static <T> List<T> getList() {}
> ```
>
> 对于静态泛型方法的调用
>
> ```java
> 
> ```
>
> 

### 枚举

> https://www.cnblogs.com/singlecodeworld/p/9887926.html

### Collections 集合工具类

>集合工具类，针对集合封装了很多集合工具方法
>
>常用方法：
>
>|     方法      | 描述                     |
>| :-----------: | ------------------------ |
>|  sort(list)   | 集合升序排序             |
>| reverse(list) | 反转指定列表中的元素顺序 |
>| shuffle(list) | 使用默认的随机源随机排列 |
>
>**Java中线程安全的集合**
>
>线程不安全的集合普遍比线程安全的集合效率高的多
>
>- Vector：就比Arraylist多了个同步化机制（线程安全）。
>
>
>- Hashtable：就比Hashmap多了个线程安全。
>
>
>- ConcurrentHashMap:是一种高效但是线程安全的集合。
>
>
>- Stack：栈，也是线程安全的，继承于Vector
>- List item
>- java.util.concurrent 包下所有的集合类
>  - ArrayBlockingQueue
>  - ConcurrentHashMap
>  - ConcurrentLinkedQueue
>  - ConcurrentLinkedDeque

## IO流

### 文件流

> 文件：是存储或记录在一起的一个数据集合，叫作文件

### File类访问文件属性

> **格式**：
>
> ```java
> File file = new File(文件路径);
> ```
>
> **常用方法**：
>
> | 方法名称                 | 说明                                                 |
> | ------------------------ | ---------------------------------------------------- |
> | boolean exists()         | 判断文件或目录是否存在                               |
> | boolean isFile()         | 判断是否是文件                                       |
> | boolean isDirectory()    | 判断是否是目录                                       |
> | String getPath()         | 返回此对象表示的文件的相对路径名                     |
> | String getAbsolutePath() | 返回此对象表示的文件的绝对路径名                     |
> | String getName()         | 返回此对象表示的文件或目录的名称                     |
> | boolean delete()         | 删除此对象指定的文件或目录                           |
> | boolean createNewFile()  | 创建名称的空文件，不创建文件夹                       |
> | long length()            | 返回文件的长度，单位为字节，如果文件不存在，则返回OL |
> | boolean mkdirs()         | 创建文件夹，包含其父目录                             |
> | boolean delete()         | 删除文件或目录                                       |
>
> **寻找文件的方法**：
>
> ```java
> public long showFile(File file) {
> 	long num = 0
>         // 1.通过目录获取到目录中所有内容
>         File[] files = file.listFiles();
>         // 2.判断该文件目录下是否为null，不为null才可以操作
>         if(files != null){
>             // 3.循环遍历当前文件夹下的所有内容
>             for(File fi : files) {
>                 // 4.判断每个内容是否为目录
>                 if(fi.isDirectory()) {
>                     // 如果是文件夹，就调用自己这个方法，将当前文件夹作为根，继续向下遍历
>                     num += showFile(fi);
>                 }else {
>                     // 如果是文件，数量加1，并输出
>                     num++;
>                     System.out.println(fi.getPath());
>                 }
>             }
>        }
>     	return num;
> }
> ```
>

### IO流的分类

> - 按照数据的流向
>   - 输入流：读数据
>   - 输出流：写数据
> - 按照数据类型来分
>   - 字节流
>     - 字节输入流；字节输出流
>   - 字符流
>     - 字符输入流；字符输出流
>   - 一般来说，我们说IO流的分类是按照<span style="color: red;">数据类型</span>来分的
>   - 如果数据通过Window自带的记事本软件打开，我们还可以读懂里面的内容，就是用字符流；否则是用字节流。如果你不知道该使用哪种类型的流，就是用字节流
> - 按对象分：
>   - 高端流：字符流
>   - 低端流：字节流
>   - 一般来说后缀带reader或writer的为高端流,但是有个例外**printStream**是一个高端流(*所有的低端流都是字节流，所有的高端流是字符流*)

### 字节流

> **概述**：
>
> - IO：输入/输出(Input/Output)
>- 流：是一种抽象概念，是对数据传输的总称。也就是说数据在设备间的传输称为流，流的本质是数据传输
> - IO流就是用来处理设备间数据传输问题的
>   - 常见的应用：文件复制；文件上传；文件下载
> - IO流是一组有顺序，有起点和终点的字节集合，是对于数据传输的一种总称。即数据在设备与设备之间的传输都称之为流
> 

#### 字节流写数据

> 字节流抽象基类
>
> - **InputStream**：这个抽象类是表示字节输入流的所有类的超类
> - **OutputStream**：这个抽象类是表示字节输出流的所有类的超类
> - **子类名特点**：子类名称都是其父类名作为子类名的后缀
>

##### FileOutputStream

> <span style="color: red;">FileOutputStream</span>：文件输出流用于将数据写入File
>
> - FileOutputStream(String name)：创建文件输出流以指定的名称写入文件
>
>   ```java
>   FileOutputStream fos = new FileOutputStream("myByteStream\\fos.txt");
>   ```
>
>   - FileOutputStream 做了三件事
>     - 调用系统功能创建了文件
>     - 创建了字节输出流对象
>     - 让字节输出流对象指向创建好的文件
>
> - void write(int b)：将指定的字节写入此文件输出流
>
>   ```java
>   fos.write(97); // fos.txt ---> a
>   fos.write(57); // fos.txt ---> 9
>   ```
>
> - 所有和IO相关的操作，最后都要释放资源
>
>   - void close()：关闭此文件输出流并释放与此流相关联的任何系统资源
>
>   ```java
>   fos.close();
>   ```
>
> - 使用字节输出流写数据的步骤
>
>   - 创建字节流对象(调用系统功能创建了文件，创建字节输出流对象，让字节输出流对象指向文件)
>   - 调用字节输出流对象的写数据方法
>   - 释放资源(关闭此文件输出流并释放与此流相关联的任何系统资源)
>

##### 字节流写数据的3种方式

> |                 方法名                 | 说明                                                         |
> | :------------------------------------: | ------------------------------------------------------------ |
> |           void write(int b)            | 将指定的字节写入此文件输出流；一次写一个字节数据             |
> |          void write(byte[] b)          | 将b.length字节从指定的字节数组写入此文件输出流；一次写一个字节数组数据 |
> | void write(byte[] b, int off, int len) | 将len字节从指定的字节数组开始，从偏移量off开始写入此文件输出流；一次写一个字节数组的部分数据 |
>
> ```java
> FileOutputStream fos = new FileOutputStream("myByteStream\\fos.txt");
> // void write(byte[] b)
> byte[] bys = {97, 98, 99, 100, 101};
> fos.write(bys);	// abcde
> // byte[] getBytes()：返回字符串对应的字节数组
> byte[] = "abcde".getBytes();
> fos.write(bys);	// abcde
> // void write(byte[] b, int off, int len)
> fos.write(bys, 1, 3); // bcd
> ```
> 
>字节流写数据的两个小问题
> 
>- 字节流写数据如何实现换行
> 
>  - 写完数据后，加换行符
> 
>    - windows: \r\n
> 
>    - linux: \n
> 
>    - mac: \r
> 
>      ```java
>       fos.write("hello\n".getBytes());	// hello<br/>
>      ```
> 
>- 字节流写数据如何实现追加写入
> 
>  - public FileOutputStream(String name, boolean append)
>   - 创建文件输出流以指定的名称写入文件。如果第二个参数为true，则字节将写入文件的末尾而不是开头
> 

##### 字节流写数据加异常处理

> <span style="color: red;">finally</span>：在异常处理时提供<span style="color: red;">finally</span>块来执行所有清除操作。比如说IO流中的释放资源
>
> 特点：被<span style="color: red;">finally</span>控制的语句一定会执行，除非JVM退出
>
> ```java
> public class FileInputStreamDemo {
> 	public static void main(String[] args) {
>         FileOutputStream fos = null;
> 		try {
> 			fos = new FileOutputStream("myByteStream\\fos.txt");
>             fos.write("hello".getBytes());
> 		} catch (IOException e) {
> 			e.printStackTrace();
> 		} finally {
>             // 只有文件有被打开才进行资源的释放
>             if(fos != null) {
>                 try {
>                     fos.close();
>                 } catch (IOException e) {
>    					e.printStackTrace();
>    				}
> 			}
>    		}
> 	}
> }
> ```
>

#### 字节流读数据

##### FileInputStream

> <span style="color: red;">FileInputStream</span>：从文件系统中的文件获取输入字节
>
> - FileInputStream(String name)：通过打开与实际文件的连接来创建一个FileInputStream，该文件由文件系统中的路径名name命名
>
> 使用字节输入流读数据的步骤：
>
> 1. 创建字节输入流对象
> 2. 调用字节输入流对象的读数据方法
> 3. 释放资源
>
> 范例：
>
> ```java
> public class FileInputStreamDemo {
>     public static void main(String[] args) throws IOException {
>         // 创建字节输入流对象
>         // fos.txt文件内容 ab
>         FileInputStream fis = new FileInputStream("myByteStream\\fos.txt");
>         // 调用字节输入流对象的读数据方法
>         // int read()：从该输入流读取一个字节的数据
> 
>         // 第一次读取数据
>         int by = fis.read();
>         System.out.println(by); // 97
>         System.out.println((char)by); // a
> 
>         // 多次读取数据
>         int by;
>         while((by = fis.read()) != -1) 
>             System.out.print((char)by); // ab
> 
>         // 释放资源
>         fis.close();
>     }
> }
> ```
>

##### 字节流读数据的3种方式

> |              方法名              | 说明                                                         |
> | :------------------------------: | ------------------------------------------------------------ |
> |              read()              | 从指定的文件中读取输入流；一次读一个字节数据                 |
> |          read(byte[] b)          | 从指定的文件中读取b.length字节数组长度的输入流；一次读一个字节数组数据 |
> | read(byte[] b, int off, int len) | 从指定文件的输入流读取len字节，从偏移量off开始将读取到的第一个字节存入到指定的字节数组中 |
>
> ```java
> FileInputStream fis = new FileInputStream("myByteStream\\fos.txt");
> // fos.txt文件内容 abcde
> // int read(byte[] b)
> byte[] bys = new byte[2];
> fis.read(bys);	// abcde
> System.out.println((char)bys[0]); // a
> System.out.println((char)bys[1]); // b
> 
> // int read(byte[] b, int off, int len)
> fis.read(bys, 1, 1); // bys[0]被偏移，读取到的a被存入到bys[1]中
> System.out.println((char)bys[0]); // null
> System.out.println((char)bys[1]); // a
> ```
>

#### 字节流复制图片

> 案例
>
> ```java
> public class StreamCopy {
> 	/*
> 	 * 采用数组的方式读取和输出内容
> 	 */
> 	public static void main(String[] args) {
> 		//准备文件
> 		File file = new File("d:/java/java.jpg");
> 		File of = new File("D:/java/test",file.getName());
> 		//记录开始时间
> 		long start = System.currentTimeMillis();
> 		//准备输入输出流
> 		InputStream in = null;
> 		OutputStream out = null;
> 		try {
> 			in = new FileInputStream(file);
> 			out = new FileOutputStream(of);
> 			//准备一个自定义的存储数组,为读取时设置一个自定义缓冲区
> 			byte[] bs = new byte[10];
> 			//每次读取的长度
> 			int len = 0;
> 			//读取数据,每次读取数据到数组,后面的每次读取都是在替换数组内容
> 			while((len=in.read(bs))!=-1){
> 				//将读取的数据输出
> 				//len保证最后一个读取的内容是对应长度内容,而非整个数组
> 				//0表示读取数组便宜量
> 				out.write(bs,0,len);
> 			}
> 			System.out.println("文件复制成功!");
> 			out.flush();  //清空缓存
> 		} catch (Exception e) {
> 			// TODO Auto-generated catch block
> 			e.printStackTrace();
> 		}finally {
> 			//关闭资源
> 			try {
> 				if(in!=null)
> 					in.close();
> 				if(out!=null)
> 					out.close();
> 			} catch (IOException e) {
> 				e.printStackTrace();
> 			}
> 		}
> 		long end = System.currentTimeMillis();
> 		System.out.println("总共耗时:"+(end-start));
> 	}
> }
> ```
>

#### 字节缓冲流

> - BufferedOutputStream：
>   - 该类实现缓冲输出流。通过设置这样的输出流，应用程序可以向底层输出流写入字节，而不必为写入的每个字节导致底层系统的调用
> - BufferedInputStream：
>   - 创建BufferedInputStream将创建一个内部缓冲区数组。当从流中读取或跳过字节时，内部缓冲区将根据需要从所包含的输入流中重新填充，一次很多字节
>

##### 构造方法

> - 字节缓冲输出流：<span style="color: red;">BufferedOutputStream</span>(<span style="color: #329BDC;">OutputStream out</span>)
>
>   ```java
>   BufferedOutputStream(new FileOutputStream("myByteStream\\fos.txt"));
>   ```
>
> - 字节缓冲输入流：<span style="color: red;">BufferedInputStream</span>(<span style="color: #329BDC;">InputStream in</span>)
>
>   ```java
>   BufferedInputStream(new FileInputStream("myByteStream\\fos.txt"));
>   ```
>
> - 字节缓冲流<span style="color: red;">仅仅提供缓冲区</span>，而真正的读写数据还得依靠基本的字节流对象进行操作
>

##### 字节缓冲输出流写数据

```java
BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("myByteStream\\bos.txt"));
// 写数据
bos.write("hello\r\n".getBytes());
bos.write("world\r\n".getBytes());
// 释放资源
bos.close();
```

##### 字节缓冲输入流读数据

```java
BufferedInputStream bis = new BufferedInputStream(new FileInputStream("myByteStream\\bos.txt"));
// 一次读取一个字节数据
int by;
while((by = bis.read()) != -1) {
    System.out.print((char)by);
}
// 一次读取一个字节数组的数据
byte[] bys = new byte[1024];
int len;
while((len = bis.read(bys)) != -1) {
    System.out.print(new String(bys, 0, len));
}
// 释放资源
bos.close();
```

##### 字节缓冲流复制视频

```java
public static void method() {
    BufferedInputStream bis = null;
    BufferedOutputStream bos = null;
    try {
        // 准备文件
        bis = new BufferedInputStream(new FileInputStream("E:/copy/source/字节输出流.mp4"));
        bos = new BufferedOutputStream(new FileOutputStream("E:/copy/target/字节输出流.mp4"));
		//准备一个自定义的存储数组,为读取时设置一个自定义缓冲区
        byte[] bys = new byte[1024];
        //每次读取的长度
        int len;
		// 开始拷贝
        while ((len = bis.read(bys)) != -1) {
            bos.write(bys, 0, len);
        }
        System.out.println("文件复制成功!");
        // 清空缓存
		bos.flush();
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        try {
            if (bos != null)
                bos.close();
            if (bis != null)
                bis.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

### 字符流

> 概述：由于字节流操作中文不是特别的方便，所以Java就提供字符流
>
> - <span style="color: red;">字符流</span> = <span style="color: red;">字节流</span> + <span style="color: red;">编码表</span>
>
> 用字节流复制文本文件时，文本文件也会有中文，但是没有问题，原因是最终底层操作会自动进行字节拼接成中文，如何识别是中文的呢？
> 
> - 汉字在存储的时候，无论选择哪种编码存储，第一个字节都是负数
> 

#### 字符串中的编码解码

> 编码：
>
> - <span style="color: #329BDC;">byte[] getBytes()</span>：使用平台的默认字符集将该String编码为一系列字节，将结果存储到新的字节数组中
>- <span style="color: #329BDC;">byte[] getBytes(String charsetName)</span>：使用指定的字符集将该String编码为一系列字节，将结果存储到新的字节数组中
> 
> 解码：
> 
> - <span style="color: #329BDC;">String(byte[] bytes)</span>：通过使用平台的默认字符集解码指定的字节数组来构造新的String
> - <span style="color: #329BDC;">String(byte[] bytes, String charsetName)</span>：通过指定的字符集解码指定的字节数组来构造新的String
>
> <span style="color: red;">注意：编码和解码所使用的编码表必须相同</span>
>

#### 字符流中的编码解码问题

> 字符流抽象基类
>
> 字符输入流与字节输入流类似，但运行的单元更大，且只能用于读取文本
>
> - Reader：字符输入流的抽象类
> - Writer：字符输出流的抽象类
>
> 字符流中和编码解码问题相关的两个类：
>
> - InputStreamReader
> - OutputStreamWriter

##### InputStreamReader

> ```java
> // 使用默认的字符编码
> FileInputStream fis= new FileInputStream("myCharStream/osw.txt");
> InputStreamReader isr = new InputStreamReader(fis);
> int ch;
> while((ch = isr.read()) != -1){
>     System.out.print((char)ch);
> }
> isr.close();
> 
> // 使用自定义的字符编码
> FileInputStream fis= new FileInputStream("myCharStream/osw.txt");
> InputStreamReader isr = new InputStreamReader(fis, "GBK");
> int ch;
> while((ch = isr.read()) != -1){
>     System.out.print((char)ch);
> }
> isr.close();
> ```

##### OutputStreamWriter

> ```java
> // 使用默认的字符编码
> FileOutputStream fos = new FileOutputStream("myCharStream/osw.txt");
> OutputStreamWriter osw = new OutputStreamWriter(fos);
> osw.write("中国");
> osw.close();
> 
> // 使用自定义的字符编码
> FileOutputStream fos = new FileOutputStream("myCharStream/osw.txt");
> OutputStreamWriter osw = new OutputStreamWriter(fos, "GBK");
> osw.write("中国");
> osw.close();
> ```

#### 字符流写数据的5中方式

> |                  方法名                   | 说明                 |
> | :---------------------------------------: | -------------------- |
> |             void write(int c)             | 写一个字符           |
> |          void write(char[] cbuf)          | 写入一个字符数组     |
> | void write(char[] cbuf, int off, int len) | 写入字符数组的一部分 |
> |          void write(String str)           | 写一个字符串         |
> | void write(String str, int off, int len)  | 写一个字符串的一部分 |
>
> **字符流写数据范例**
>
> ```java
> OutputStreamWriter osw = new OutputStreamWriter(new FileOutputStream("myCharStream/osw.txt"));
> osw.write(97);	// 字符流写数据不能直接写入文件，需要通过字节流来写数据
> // 刷新流，清空缓存
> osw.flush();	// 将缓冲区中的字符通过字节流写入到文件中
> char[] chs = {'a','b','c'};
> osw.write(chs);	// abc
> osw.write(chs, 0, 2); // ab
> osw.write("abcde");	// abcde
> osw.write("abcde", 1, 3);	// bcd
> osw.close();	// 关闭文件前先进行刷新
> ```
>

#### 字符流读数据的2种方式

> |        方法名         | 说明                   |
> | :-------------------: | ---------------------- |
> |      int read()       | 一次读一个字符数据     |
> | int read(char[] cbuf) | 一次读一个字符数组数据 |
>
> 字符流写数据范例
>
> ```java
> InputStreamReader isr = new InputStreamReader(new FileInputStream("myCharStream/osw.txt"));
> // 一次读一个字符数据
> int ch;
> while((ch = isr.read()) != -1){
>         System.out.print((char)ch);
> }
> // 一次读一个字符数组数据
> char[] chs = new char[1024];
> int len;
> while((len = isr.read(chs)) != -1){
>    	System.out.print(new String(chs, 0, len));
> }
> // 释放资源
> isr.close();
> ```
>

#### 字符流复制文件

> 案例：
>
> ```java
> public class StreamCopy {
> 
> 	public static void main(String[] args) {
> 		// 准备文件
> 		File file = new File("E:/copy/source/StreamCopy.java");
> 		File of = new File("E:/copy/target/", file.getName());
> 		// 记录开始时间
> 		long start = System.currentTimeMillis();
> 		// 准备输入输出流
> 		InputStreamReader in = null;
> 		OutputStreamWriter out = null;
> 		try {
> 			in = new InputStreamReader(new FileInputStream(file));
> 			out = new OutputStreamWriter(new FileOutputStream(of));
> 			// 准备一个自定义的存储数组,为读取时设置一个自定义缓冲区
> 			char[] bs = new char[10];
> 			// 每次读取的长度
> 			int len = 0;
> 			// 读取数据,每次读取数据到数组,后面的每次读取都是在替换数组内容
> 			while ((len = in.read(bs)) != -1) {
> 				// 将读取的数据输出
> 				// len保证最后一个读取的内容是对应长度内容,而非整个数组
> 				// 0表示读取数组便宜量
> 				out.write(bs, 0, len);
> 			}
> 			System.out.println("文件复制成功!");
> 			out.flush(); // 清空缓存
> 		} catch (IOException e) {
> 			// TODO Auto-generated catch block
> 			e.printStackTrace();
> 		} finally {
> 			// 关闭文件
> 			try {
> 				if (in != null)
> 					in.close();
> 				if (out != null)
> 					out.close();
> 			} catch (IOException e) {
> 				e.printStackTrace();
> 			}
> 		}
> 		// 计算结束时间
> 		long end = System.currentTimeMillis();
> 		System.out.println("总共耗时:" + (end - start));
> 	}
> }
> ```
>
> 为了简化书写，转换流提供了对应的子类
>
> |           方法名            | 说明                     |
> | :-------------------------: | ------------------------ |
> | FileReader(String fileName) | 用于读取字符文件的便捷类 |
> | FileWriter(String fileName) | 用于写入字符文件的便捷类 |
>
> ```java
> // 简化字符流复制文件
> public class StreamCopy {
> 	public static void main(String[] args) throws IOException {
>            // 根据数据源创建字符输入流对象
>            FileReader fr = new FileReader("E:/copy/source/StreamCopy.java");
>            // 根据目的地创建字符输出流对象
>            FileWriter fw new FileWriter("E:/copy/target/StreamCopy.java");
>            // 读写数据，复制文件
>            char[] chs = new char[10];
>            int len;
>            while((len = fr.read(chs)) != -1){
>                fw.write(chs, 0, len);
>            }
>            // 释放资源
>            fw.close();
>            fr.close();
>    	}
> }
> ```
>

#### 字符缓冲流

> - **BufferedWriter**：将文本写入字符输出流，缓冲字符，以提供单个字符，数组和字符串的高效写入，可以指定缓冲区大小，或者可以使用默认大小。默认值足够大，可用于大多数用途
> - **BufferedReader**：从字符输入流读取文本，缓冲字符，以提供字符，数组和行的高效读取，可以指定缓冲区大小，或者可以使用默认大小。默认值足够大，可用于大多数用途
>

##### 构造方法

> - BufferedWriter(Writer out)
>
>   ```java
>   FileWriter fw = new FileWriter("myCharStream/bw.txt");
>   BufferedWriter bw = new BufferedWriter(fw);
>   bw.write("hello\r\n");
>   bw.write("world\r\n");
>   bw.close();
>   ```
>
> - BufferedReader(Reader in)
>
>   ```java
>   FileReader fr = new FileReader("myCharStream/bw.txt");
>   BufferedReader br = new BufferedReader(fr);
>   char[] chs = new char[10];
>   int len;
>   while((len = br.read(chs)) != -1) {
>       System.out.print(new String(chs, 0, len));
>   }
>   ```
>
> <span style="color: #329BDC;">缓冲流的默认值大小均为8192</span>
>

##### 字符缓冲流特有功能

> BufferedWriter：
>
> - void newLine()：写一个行分隔符，行分隔符字符串由系统属性定义
>
>   ```java
>   bw.write("hello");
>   bw.newLine();
>   ```
>
> BufferedReader：
>
> - public String readLine()：读一行文字。结果包含行的内容的字符串，不包括任何行终止字符，如果流的结尾已经到达，则为null
>
>   ```java
>   String line = br.readLine();
>   System.out.println(line);
>   ```
>
> *字符流只能赋值文本数据，有5种方式，一般采用字符缓冲流的特有功能*
>

### 特殊操作流

#### 标准输入输出流

> System类中有两个静态的成员变量：
>
> - public static final InputStream in：标准输入流。通常该流对应于键盘输入或由主机环境或用户指定的另一个输入源
>
>   ```java
>   InputStream is = System.in;
>    int by;
>   while((by = is.read()) != -1) {
>       System.out.print((char)by);
>   }
>   // 把字节流转换为字符流
>   InputStreamReader isr = new InputStreamReader(is);	// 读取汉字
>   // 使用字符缓冲输入流实现一次读取一行数据
>   BufferedReader br = new BufferedReader(isr);
>   // 读取输入的数据
>   String line = br.readLine();
>   System.out.print(line);
>   ```
>   
>  简化
>   
>  ```java
>   BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
>   String line = br.readLine();
>   System.out.print(line);
>   // 字符串转换为整数
>   int i = Integer.parseInt(br.readLine());
>   System.out.print(i);
>  ```
>   
>  Java提供的类Scanner就进行了以上的过程来实现键盘录入
>   
>- public static final PrintStream out：标准输出流。通常该流对应于显示输出或由主机环境或用户指定的另一个输出目标
> 
>  ```java
>   PrintStream ps = System.out;
>   ps.println("hello");	// ---> System.out.println
>   ps.println("100");	// ---> System.out.println
>  ```
> 

#### 打印流

> 打印流分类：
>
> - 字节打印流：PrintSteam
> - 字符打印流：PrintWriter
>
> 打印流的特点：
>
> - 只负责输出数据，不负责读取数据
> - 有自己的特有方法
>
> 字节打印流：
>
> - PrintSteam(String fileName)：使用指定的文件名创建新的打印流
>
>   ```java
>   PrintSteam ps = new PrintSteam("myOtherStream/ps.txt");
>   ps.write(97);	// a
>   ps.print(97);	// 97
>   ps.println(98);	// 98\r\n
>   ps.close();
>   ```
>
> - 使用继承父类的方法写数据，查看的时候会转码；使用自己的特有方法写数据，查看的数据原样输出
>
> 字符打印流：
>
> - 字符打印流PrintWriter的构造方法：
>
>   |                   方法名                   | 说明                                                         |
>   | :----------------------------------------: | ------------------------------------------------------------ |
>   |        PrintWriter(String fileName)        | 使用指定的文件名创建一个新的PrintWriter，而不需要自动执行刷新 |
>   | PrintWriter(Writer out, boolean autoFlush) | 创建一个新的PrintWriter：out：字符输出流；autoFlush：一个布尔值，如果为真，则println，printf，或format方法将刷新输出缓冲区 |
>
>   ```java
>   // 无自动刷新
>   PrintWriter pw = new PrintWriter("myOtherStream/ps.txt");
>   pw.println("hello");
>   pw.flush();
>   pw.println("world");
>   pw.flush();
>   // 自动刷新
>   PrintWriter pw = new PrintWriter(new FileWriter("myOtherStream/ps.txt"), true);
>   pw.println("hello");
>   pw.println("world");
>   ```
>
> 字符打印流改进复制Java文件代码
>
> ```java
> // 根据数据源创建字符输入流对象
> BufferedReader br = new BufferedReader(new FileReader("E:/copy/source/StreamCopy.java"));
> // 根据目的地创建字符输出流对象
> PrintWriter pw = new PrintWriter(new FileWriter("E:/copy/target/StreamCopy.java"), true);
> // 读写数据，复制文件
> String line;
> while ((line = br.readLine()) != null) 
>     pw.println(line);
> // 释放资源
> pw.close();
> br.close();
> ```
>

#### 对象序列化流与对象反序列化流

> 对象序列化：就是将对象保存到磁盘中,或者在网络中传输对象
>
> 这种机制就是使用一个字节序列表示一个对象,该字节序列包含：对象类型，对象数据和对象存储的属性等信息
>
> 字节序列写到文件之后，相当于文件中持久保存了一个对象信息
>
> 反之，该字节序列还可以从文件中读取回来,重构对象，这种叫做反序列化
>
> 要实现序列化和反序列化就要使用对象序列化流和对象反序列化流

##### 对象序列化流

> **对象序列化流**：<span style="color: red;">ObjectOutputStream</span>
>
> - 将Java对象的原始数据类型和图形写入OutputStream。可以使用ObjectInputStream读取(重构)对象。可以通过使用流的文件来实现对象的持久存储。如果流是网络套接字流，则可以在另一个主机上或另一个进程中重构对象
>
> - 构造方法：<span style="color: red;">ObjectOutputStream</span>(<span style="color: #329BDC;">OutputStream out</span>)：创建一个写入指定的OutputStream的ObjectOutputStream
>
> - 序列化对象的方法：<span style="color: red;">void writeObject</span>(<span style="color: #329BDC;">Object obj</span>)：将指定的对象写入ObjectOutputStream
>
>   ```java
>   public class Student implements Serializable{
>   	private String name;
>   	private int age;
>
>   	public Student() {
>   	}
>
>   	public Student(String name, int age) {
>   		super();
>   		this.name = name;
>   		this.age = age;
>   	}
>
>   	public String getName() {
>   		return name;
>   	}
>
>   	public void setName(String name) {
>   		this.name = name;
>   	}
>
>   	public int getAge() {
>   		return age;
>   	}
>
>   	public void setAge(int age) {
>   		this.age = age;
>   	}
>   }
>
>   public class StudentDemo {
>   	public static void main(String[] args) throws IOException {
>   		// 创建一个写入指定的OutputStream的ObjectOutputStream
>   		ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("myOtherStream/oos.txt"));
>   		// 创建对象
>   		Student s = new Student("林青霞", 30);
>   		// 将指定的对象写入ObjectOutputStream
>   		oos.writeObject(s);
>   		// 释放资源
>   		oos.close();
>   	}
>   }
>   ```
>
> - <span style="color: red;">注意</span>：
>
>   - 一个对象要想被序列化，该对象所属的类必须必须实现<span style="color: red;">Serializable</span>接口
>   - <span style="color: red;">Serializable</span>是一个<span style="color: red;">标记接口</span>，实现该接口，不需要重写任何方法(*实现该接口表示该类可以被序列化和反序列化*)

##### 对象反序列化流

> **对象反序列化流**：<span style="color: red;">ObjectInputStream</span>
>
> - **使用ObjectInputStream反序列化，需使用先前ObjectOutputStream编写的原始数据和对象**
>
> - 构造方法：<span style="color: red;">ObjectInputStream</span>(<span style="color: #329BDC;">InputStream in</span>)：创建从指定的InputStream读取的ObjectInputStream
>
> - 反序列化对象的方法：<span style="color: red;">Object readObject</span>()：从ObjectInputStream读取一个对象
>
>   ```java
>   // 创建从指定的InputStream读取的ObjectInputStream
>   ObjectInputStream ois = new ObjectInputStream(new FileInputStream("myOtherStream/oos.txt"));
>   Object obj = ois.readObject();
>   // 输出对象
>   Student s = (Student) obj;
>   System.out.println(s.getName() + "," + s.getAge());
>   // 释放资源
>   ois.close();
>   ```
>
> - 给一个成员变量加上<span style="color: red;">transient</span>关键字修饰，该关键字标记的成员变量不参与序列化过程
>
>   ```java
>   public class Student implements Serializable{
>   	private String name;
>   	private transient int age;
>       ...
>   }
>
>   Student s = new Student("林青霞", 30);
>   序列化。。。
>   反序列化。。。
>   System.out.println(s.getName() + "," + s.getAge()); // 林青霞,0
>   ```
>
> - **serialVersionUID**：<span style="color: red;">private static final long serialVersionUID = 1L</span>;
>
>   - **serialVersionUID**用于给序列化的对象一个固定的UID，以防止用对象序列化流序列化对象后，修改对象所属的类文件，读取数据出现<span style="color: red;">InvalidClassException</span>异常
>   - 显式声明**serialVersionUID**后，序列化运行时将使用此值，而不是根据序列化规范计算该类各个方面以生成的默认的**serialVersionUID**值
>

##### 序列化存储集合

```java
public class StudentStreamDemo {
	/*
	 * 创建集合,添加3到5个学生
	 * 将集合序列化到文件
	 * 再次放文件反序列化处理,并添加2个学生
	 * 最后再序列化到文件
	 */
	public static void main(String[] args) {
		List<Student> stus = new ArrayList<>();
		stus.add(new Student(1,"zhangsan",20,"男"));
		stus.add(new Student(2,"lisi",18,"女"));
		stus.add(new Student(3,"wangwu",20,"男"));
		//调用序列方法,序列化
		try {
			//序列初始化
			outStream(stus,"d:/java/Student.txt");
			//反序列化得到集合
			stus = inStream("d:/java/Student.txt");
			//添加数据
			stus.add(new Student(4, "wanghong", 18, "女"));
			stus.add(new Student(5, "tiantian", 18, "女"));
			//再次序列化,参数1为序列化内容,参数2为序列化地址
			outStream(stus,"d:/java/Student.txt");
			stus = inStream("d:/java/Student.txt");
			for (Student stu : stus) {
				System.out.println(stu.toString());
			}
		} catch (Exception e) {
			e.printStackTrace();
		}

	}
	//序列化方法
	public static void outStream(Object obj,String path) throws Exception{
		 ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(path));
		 oos.writeObject(obj);
		 oos.close();
	}
	//反序列化方法
	public static List<Student> inStream(String path) throws Exception{
		List<Student> list = null;
		ObjectInputStream ois = new ObjectInputStream(new FileInputStream(path));
		list = (List<Student>) ois.readObject();
		return list;
	}
}
```

#### Properties

> 概述：
>
> - 是一个Map体系的集合类
> - Properties可以保存到流中或从流中加载
>
> ```java
> // 创建Properties对象
> Properties prop = new Properties();
> // 添加数据
> prop.put("item01", "123");
> prop.put("item02", "456");
> prop.put("item03", "789");
> // 遍历prop
> Set<Object> keySet = prop.keySet();
> for (Object key : keySet) {
>     Object value = prop.get(key);
>     System.out.println(key + "," + value);
> }
> ```
>

##### Properties作为集合的特有方法

> |                    方法名                    | 说明                                                         |
> | :------------------------------------------: | ------------------------------------------------------------ |
> | Object setProperty(String key, String value) | 设置集合的键和值，都是String类型，底层调用Hashtable方法put   |
> |        String getProperty(String key)        | 使用此属性列表中指定的键搜索属性                             |
> |    Set**<String>** stringPropertyNames()     | 从该属性列表中返回一个不可修改的键集，其中键及其对应的值是字符串 |
>
> ```java
> Properties prop = new Properties();
> // 设置集合的键和值
> prop.setProperty("item01", "123");
> prop.setProperty("item02", "456");
> prop.setProperty("item03", "789");
> // 使用指定的键搜索属性
> System.out.println(prop.getProperty("item01"));		// 123
> System.out.println(prop.getProperty("item011"));	// null
> // 从该属性列表中返回一个不可修改的键集，其中键及其对应的值是字符串
> Set<String> names = prop.stringPropertyNames();
> for (String key : names) {
>     String value = prop.getProperty(key);
> 	System.out.println(key + "," + value);	// item03,789\r\n item02,456\r\n item01,123\r\n
> }
> ```
>

##### properties和IO流相结合使用

> |                    方法名                     | 说明                                                         |
> | :-------------------------------------------: | ------------------------------------------------------------ |
> |        void load(InputStream inStream)        | 从输入字节流读取属性列表(键和元素对)                         |
> |           void load(Reader reader)            | 从输入字符流读取到属性列表(键和元素对)                       |
> | void store(OutputStream out, String comments) | 将此属性列表(键和元素对)写入此Properties表中，以适合于使用load(InputStream)方法的格式写入输出字节流 |
> |  void store(Writer writer, String comments)   | 将此属性列表(键和元素对)写入此Properties表中，以适合使用load(Reader)方法的格式写入输出字节流 |
>
> ```java
> public class PropertiesDemo {
> 	public static void main(String[] args) {
> 		try {
> 			// 把集合中的数据保存到文件
> 			myStore();
> 			//将文件中的键值对读取为java中
> 			myLoad();
> 		} catch (Exception e) {
> 			e.printStackTrace();
> 		}
> 	}
> 	//读取属性文件
> 	private static void myLoad() throws Exception {
> 		Properties prop = new Properties();
> 		//通过输入流找到并获取文件
> 		InputStream in = new FileInputStream("jdbc.properties");
> 		//properties中的load方法,将流加载为属性列表
> 		prop.load(in);
> 		in.close();
> 		//获取各个属性
> 		System.out.println("驱动类名:"+prop.getProperty("className"));
> 		System.out.println("用户名:"+prop.getProperty("name"));
> 	}
> 	//写出属性文件
> 	private static void myStore() throws Exception {
> 		// 创建properties集合
> 		Properties prop = new Properties();
> 
> 		prop.setProperty("className", "com.mysql.jdbc.Driver");
> 		// 通过properties设置属性,键值对应,设置后可以被键搜索
> 		prop.setProperty("username", "root");
> 		prop.setProperty("password", "123456");
> 
> 		//降属性保存到jdbc.properties的文件中
> 		Writer out = new FileWriter("jdbc.properties");
> 		//属性集合properties集合将流写出
> 		prop.store(out, null);
> 		out.close();
> 	}
> }
> ```

## 多线程

> **什么是进程**
>
> 当程序开始运行时，它就是一个进程，进程包括运行中的程序和程序所使用到的内存和资源。而**一个进程至少有一个线程**
> 进程就是当程序被CPU加载时，根据程序每一行代码做出相应动作，形成一个动态的过程，那么这个过程就是进程
> 进程运行时，所申请的空间，都是在运行内存上，关机之后，进程消失了
>
> **什么是线程**
>
> 程序中执行的一个流，每个线程都有自己专属寄存器(栈指针，程序计数器等)，但是代码区是共享，即不同的线程可以执行同样的函数(方法)
>
> **多线程**
>
> 一个进程中有多个执行路径，共同执行同一个代码源.
>
> **Java中的守护线程**
>
> 非人力特意执行的线程，由JVM执行的线程就是守护线程

### 线程的创建

> **实现多线程的三种方式**
>
> 1. 通过<span style="color: red;">继承Thread类</span>，并<span style="color: red;">重写run方法</span>的方式来实现多线程
> 2. 通过<span style="color: red;">实现Runnable接口</span>，将<span style="color: red;">接口实例放入Thread</span>中的形式来实现多线程
> 3. 通过<span style="color: red;">实现Callable接口</span>的方式来实现多线程

#### Thread类

> **实现多线程的方式**
>
> - 定义一个类MyThread继承Thread类
>
>   ```java
>   public class MyThread extends Thread {}
>   ```
>
> - 在MyThread类中重写run()方法
>
>   ```java
>   public class MyThread extends Thread {
>   	//线程的运行体
>   	@Override
>   	public void run() {
>   		for (int i = 0; i < 100; i++) {
>   			System.out.println("第"+(i+1)+"次,好好学习,天天向上!");
>   		}
>       }
>   }
>   ```
>
> - 创建MyThread类的对象
>
>   ```java
>   public class MyThreadDemo {
>   
>   	public static void main(String[] args) {
>   		//创建线程对象
>   		Thread t = new MyThread();
>   		Thread t1 = new MyThread();
>   		Thread t2 = new MyThread();
>   	}
>   }
>   ```
>
> - 启动线程
>
>   - void start()：使此线程开始执行；Java虚拟机调用此线程的 run 方法
>
>   ```java
>   public class MyThreadDemo {
>                                             
>   	public static void main(String[] args) {
>   		//创建线程对象
>   		Thread t = new MyThread();
>   		Thread t1 = new MyThread();
>   		Thread t2 = new MyThread();
>           //调用start方法,启动线程
>   		t.start();
>   		t1.start();
>   		t2.start();
>   	}
>   }
>   ```
>
> *两个小问题*
>
> - 为什么要重写 run() 方法
>   - 因为 run() 是用来封装被线程执行的代码
> - run() 方法和 start() 方法的区别
>   - run()：封装线程执行的代码，直接调用，相当于普通方法的调用
>   - start()：启动线程；然后由JVM调用此线程的 run() 方法
>
> **设置和获取线程名称**
>
> Thread类中设置和获取线程名称的方法
>
> - void setName(String name)：将此线程的名称更改为等于参数 name
>
>   ```java
>   public class MyThreadDemo {
>   
>   	public static void main(String[] args) {
>   		//创建线程对象
>   		Thread t = new MyThread();
>   		Thread t1 = new MyThread();
>   		Thread t2 = new MyThread();
>   		//设置线程名称
>   		t.setName("小明线程-----");
>   		t1.setName("小文线程----");
>   		t2.setName("小林线程----");
>   		//调用start方法,启动线程
>   		t.start();
>   		t1.start();
>   		t2.start();
>   	}
>   }
>   ```
>
> - String getName()：返回此线程的名称
>
>   ```java
>   public class MyThread extends Thread {
>   	//线程的运行体
>   	@Override
>   	public void run() {
>   		for (int i = 0; i < 100; i++) {
>   			System.out.println(this.getName()+"第"+(i+1)+"次,好好学习,天天向上!");
>   		}
>   	}
>   }
>   ```

#### Runnable接口

> **实现多线程的方式**
>
> - 创建 MyRunnable 类实现 Runnable 接口
>
>   ```java
>   public class MyRunnable implements Runnable {}
>   ```
>
> - 重写run方法
>
>   - Runnable 只是接口，无法通过 this.getName() 来获取当前线程名称
>   - 在 MyRunnable 类中使用 Thread.currentThread().getName() 来获取当前线程名称
>     - Thread.currentThread()：线程类中的一个静态方法,用于获取当前线程
>
>   ```java
>   public class MyRunnable implements Runnable {
>   	@Override
>   	public void run() {
>   		for (int i = 0; i <100; i++) {
>   			//获取线程名称currentThread线程类中的一个静态方法,用于获取当前线程
>   			System.out.println(Thread.currentThread().getName()+":"+i);
>   		}
>   	}
>   }
>   ```
>
> - 创建 MyRunnable 类的对象
>
>   ```java
>   public class RunnableDemo {
>   	public static void main(String[] args) {
>   		//创建子类实现类对象
>   		Runnable r = new MyRunnable();
>   	}
>   }
>   ```
>
> - 创建 Thread 类对象,将 MyRunnable 类的对象放入到线程对象中执行
>
>   ```java
>   public class RunnableDemo {
>   	public static void main(String[] args) {
>   		//创建子类实现类对象
>   		Runnable r = new MyRunnable();
>   		//创建线程对象
>   		Thread t = new Thread(r, "小林线程");
>   		Thread t1 = new Thread(r, "张三线程");
>   		Thread t2 = new Thread(r, "文杰线程");
>   	}
>   }
>   ```
>
> - 调用start方法启动线程
>
>   ```java
>   public class RunnableDemo {
>   	public static void main(String[] args) {
>   		//创建子类实现类对象
>   		Runnable r = new MyRunnable();
>   		//创建线程对象
>   		Thread t = new Thread(r, "小林线程");
>   		Thread t1 = new Thread(r, "张三线程");
>   		Thread t2 = new Thread(r, "文杰线程");
>   		//启动线程
>   		t.start();
>   		t1.start();
>   		t2.start();
>   	}
>   }
>   ```

#### Runnable和Thread的对比

> **相比继承Thread类,实现Runnable接口的好处**
>
> - 避免了Java中单继承的问题
> - 适合于多个相同程序的代码去处理同一个资源的情况,把线程和程序的代码、数据有效分离,较好的体现了面向对象的设计思想

### 线程的优先级

> **线程调度**
>
> Java中线程的调度有两种
>
> - *分时调度*
>   - 平均分配CPU资源
> - *抢占式调度*
>   - 优先级高的线程优先抢占CPU,如果优先级相同则随机分配,优先级高的线程可能获取CPU时间片段相对多一些
>
> **获取线程优先级**
>
> ```java
> // 返回一个int类型(线程优先级数字 范围1~10)
> 线程对象.getPriority();
> ```
>
> **抢占调度中设置线程优先级的方法**
>
> ```java
> // 设置线程优先级 数字越大，优先级越高 范围1~10 默认5 
> 线程对象.setPriority(int[常量]);
> ```
>
> 三个常量关键字：
>
> - Thread.MAX_PRIORITY	 10
> - Thread.MIN_PRIORITY     1
> - Thread.NORM_PRIORITY  5

### 线程控制

> |             方法名             | 说明                                                         |
> | :----------------------------: | ------------------------------------------------------------ |
> | static void sleep(long millis) | 使当前正在执行的线程停留(暂停执行)指定的毫秒数               |
> |          void join()           | 等待这个线程死亡                                             |
> |   void setDaemon(boolean on)   | 将此线程编辑为守护线程，当运行的线程都是守护线程时，Java虚拟机将退出 |
> |        void interrupt()        | 中断此线程                                                   |
> |      static void yield()       | 让出cpu，让其他线程执行，但礼让的时间不确定，所以也不一定礼让成功 |
>

#### sleep

> **使当前正在执行的线程停留(暂停执行)指定的毫秒数**
>
> ```java
> public class ThreadDemo extends Thread {
> 	@Override
> 	public void run() {
> 		for (int i = 0; i < 100; i++) {
> 			System.out.println(this.getName() + " 第" + i + "次");
> 			try {
> 				this.sleep(100);
> 			} catch (InterruptedException e) {
> 				e.printStackTrace();
> 			}
> 		}
> 	}
> }
> 
> public class ThreadTest {
> 	public static void main(String[] args) {
> 		Thread t1 = new ThreadDemo();
> 		Thread t2 = new ThreadDemo();
> 		Thread t3 = new ThreadDemo();
> 		
> 		t1.start();
> 		t2.start();
> 		t3.start();
> 	}
> }
> ```

#### join

> **等待这个线程死亡**
>
> ```java
> public class ThreadDemo extends Thread {
> 	@Override
> 	public void run() {
> 		for (int i = 0; i < 100; i++) {
> 			System.out.println(this.getName() + " 第" + i + "次");
> 		}
> 	}
> }
> 
> public class ThreadTest {
> 	public static void main(String[] args) {
> 		Thread t1 = new ThreadDemo();
> 		Thread t2 = new ThreadDemo();
> 		Thread t3 = new ThreadDemo();
> 		
> 		t1.start();
>         	t1.join(); // t1执行完毕后再执行t2和t3
> 		t2.start();
> 		t3.start();
> 	}
> }
> ```

#### setDaemon

> **将此线程编辑为守护线程**
>
> ```java
> public class ThreadDemo extends Thread {
> 	@Override
> 	public void run() {
> 		for (int i = 0; i < 100; i++) {
> 			System.out.println(this.getName() + " 第" + i + "次");
> 		}
> 	}
> }
> 
> public class ThreadTest {
> 	public static void main(String[] args) {
> 		Thread t1 = new ThreadDemo();
> 		Thread t2 = new ThreadDemo();
>         
>         // 设置守护线程
>         t1.setDaemon(true);
>         
> 		t1.start();
> 		t2.start(); // t2运行完毕后，java虚拟机退出
> 	}
> }
> ```

#### interrupt

> **中断线程**(中断的线程为*调用该方法的Thread实例所代表的线程*)
>
> 线程的thread.interrupt()方法是中断线程，将会设置该线程的中断状态位，即设置为true，中断的结果线程是死亡、还是等待新的任务或是继续运行至下一步，就取决于这个程序本身。线程会不时地检测这个中断标示位，以判断线程是否应该被中断（中断标示值是否为true）。它并不像stop方法那样会中断一个正在运行的线程
>
> **示例：interrupt中断线程的休眠**
>
> ```java
> public class ThreadDemo extends Thread {
> 	@Override
> 	public void run() {
> 		for (int i = 0; i < 100; i++) {
> 			System.out.println(this.getName() + " 第" + i + "次");
> 			try {
> 				this.sleep(10000);
> 			} catch (InterruptedException e) {
> 				e.printStackTrace();
> 			}
> 		}
> 	}
> }
> 
> public class ThreadTest {
> 	public static void main(String[] args) {
> 		Thread t1 = new ThreadDemo();
> 
> 		t1.start();
>         for(int i = 0; i < 5; i++){
>             Thread.sleep(100);	// 主线程(main)休眠
>             System.out.println("hi " + i);
>         }
>         t1.interrupt(); // 中断t1线程的休眠
> 	}
> }
> ```

### 线程的生命周期

> **生命周期**：
>
> 1. *新建*
>    - 创建线程对象
> 2. *启动线程*
>    - start()
> 3. *就绪*
>    - 有执行资格，没有执行权
> 4. *抢到CPU的执行权*
> 5. *运行*
>    - 有执行资格，有执行权
>    - *run()结束/stop()*
>      - *死亡*
>        - 线程死亡，变成垃圾
>    - *其他线程抢走CPU的执行权*
>      - 回到就绪态
>    - *sleep()/其他阻塞式方法*
>      - *阻塞*
>        - 没有执行资格，没有执行权
>      - *sleep()方法时间到/阻塞方式结束*
>        - 回到就绪态
>
> ![][5]

### 线程计数器

> 

#### CountDownLatch

> 

#### CyclicBarrier

> 

### 线程同步

> **为什么要线程同步**
>
> 当我们有多个线程要同时访问一个变量或对象时，如果这些线程中既有读又有写操作时，就会导致变量值或对象的状态出现混乱，从而导致程序异常。举个例子，如果一个银行账户同时被两个线程操作，一个取100块，一个存钱100块。假设账户原本有0块，如果取钱线程和存钱线程同时发生，会出现什么结果呢？取钱不成功，账户余额是100。取钱成功了，账户余额是0。那到底是哪个呢？很难说清楚。因此多线程同步就是要解决这个问题
>
> 注：**同步是一种高开销的操作，因此应该尽量减少同步的内容。通常没有必要同步整个方法，使用 synchronized 代码块同步关键代码即可**

#### 同步锁(互斥锁)

> **关键字**：<span style="color: red;">synchronized</span> 是一种同步锁。它修饰的对象有以下几种
>
> - 修饰一个代码块，被修饰的代码块称为同步语句块，其作用的范围是大括号{}括起来的代码，作用的对象是调用这个代码块的对象
> - 修饰一个方法，被修饰的方法称为同步方法，其作用的范围是整个方法，作用的对象是调用这个方法的对象
> - 修改一个静态的方法，其作用的范围是整个静态方法，作用的对象是这个类的所有对象
> - 修改一个类，其作用的范围是 <span style="color: red;">synchronized</span> 后面括号括起来的部分，作用主的对象是这个类的所有对象

##### 同步代码块

> 被<span style="color: red;">synchronized</span>修饰的语句块会自动被加上内置锁，从而实现同步
>
> 锁多条语句操作共享数据，可以使用同步代码块实现
>
> **格式**
>
> ```java
> synchronized(任意对象) {
>         多条语句操作共享数据的代码
> }
> ```
>
> **同步代码块的锁对象**
>
> - synchronized块：直接锁定指定的对象，该对象在多个地方的同步锁定块，只能多线程同时执行其中一个
>
> **同步的好处和弊端**
>
> - 好处：解决了多线程的数据安全问题
> - 弊端：当线程很多时，因为每个线程都会去判断同步上的锁，这是很耗费资源的，无形中会降低程序的运行效率
>
> **关于 synchronized 中传入的对象**
>
> - 传入的对象其实就是**synchronized**的“锁”(用于监视)，*该“锁”作为锁定代码块的对象，在代码块执行完毕之前都会被占用，不能被其他的线程访问*
>
> - 对于使用相同“锁”的**synchronized**，**synchronized**中的**代码块**不能同时运行
>
>   ```java
>   synchronized (obj) {
>       ...
>   }
>   ```
>
> - 如果把锁改成**Thread.currentThread().getName()**，因为每一个线程的名字不一样，所以“锁”就不一样，就会导致同步锁失效
>
>   ```java
>   synchronized (Thread.currentThread().getName()) {
>       ...
>   }
>   ```
>
> - 如果要同步就要保证“锁”是一样的，或者说地址一样
>
> - *传入参数为this时，表示的是该代码块所在的类的实例；如果该类有多个实例，则访问不同实例的资源也不会同步*

##### 同步方法

> 就是把<span style="color: red;">synchronized</span>关键字加到方法上
>
> java的每个对象都有一个内置锁，当用<span style="color: red;">synchronized</span>关键字修饰方法时，内置锁会保护整个方法。在调用该方法前，需要获得内置锁，否则就处于阻塞状态
>
> **格式**
>
> ```java
> 修饰符 synchronized 返回值类型 方法名(方法参数) {
>      方法体
> }
> ```
>
> **同步方法的锁对象**
>
> - <span style="color: red;">this</span>(当前对象)
>   - 一次只能有一个线程进入这个方法
> - synchronized 修饰非静态方法：锁定的是该类的实例 同一实例在多线程中调用才会触发同步锁定 所以，多个被synchronized修饰的非静态方法在同一实例下，只能多线程同时调用一个
>
> **同步静态方法**
>
> 就是把 synchronized 关键字加到静态方法上
>
> **格式**
>
> ```java
> 修饰符 static synchronized 返回值类型 方法名(方法参数) {
>     方法体
> }
> ```
>
> **同步方法的锁对象**
>
> - <span style="color: red;">类名.class</span>
> - synchronized 修饰静态方法：锁定的是类本身，而不是实例,  同一个类中的所有被 synchronized 修饰的静态方法，多线程只能同时调用一个

#### Lock锁

> 虽然我们可以理解同步代码块和同步方法的锁对象问题，但是我们没有直接看到代码加锁，在哪里释放锁，为了清晰展示锁，这采用对象锁Lock
>
> **Lock是接口，不能实例化，这里采用它的实现类ReentrantLock来实例化**
>
> *格式*
>
> ```java
> Lock lock = new ReentrantLock();
> ```
>
> **主要方法**：
>
> - lock()：
> - unlock()：
>
> ```java
> public class Ticket implements Runnable {
> 	// 准备100张票
> 	private int ticket = 100;
> 	// Lock锁,它是一个接口,只能实例化子类实现类
> 	Lock lo = new ReentrantLock();
> 
> 	@Override
> 	public void run() {
> 		/*
> 		 * ticket = 100 张票 有 3个窗口 假设窗口1抢到CPU资源后,其他线程等待
> 		 */
> 		while (true) {
> 			// 让多线程安全化,只有一个线程进入票源,lock对lock与unlock之间的代码进行锁定
> 			lo.lock(); 
> 			// 窗口1进入,就会把这段代码锁起来
> 			if (ticket > 0) {
> 				try {
> 					Thread.sleep(200);
> 				} catch (InterruptedException e) {
> 					e.printStackTrace();
> 				}
> 				System.out.println(Thread.currentThread().getName() + "正在售出第" + (ticket--) + "张票");
> 			} else {
> 				break;
> 			}
> 			// 当窗口1执行完后,重新释放锁,使用unlock 
> 			lo.unlock();
> 		}
> 	}
> }
> ```

#### 死锁

> 不同的线程分别占用对方需要的同步资源不放弃，都在等待对方放弃自己需要的同步资源，就形成了线程的死锁
>
> ```java
> public class DeadLock extends Thread {
> 	//创建出两个静态对象,使运行中对象统一
> 	private static Object boge = new Object();
> 	private static Object wenjie = new Object();
> 	private boolean flag;
> 	public DeadLock(boolean flag) {
> 		this.flag = flag;
> 	}
> 	@Override
> 	public void run() {
> 		if(flag){
> 			while (true) {
> 				//线程1执行boge对象后需要获取到wenjie对象,但是wenjie对象还未执行完成,未释放锁
> 				synchronized (boge) {
> 					System.out.println("对文杰说:嘿,小子赶紧还我500万,我就请你吃黄焖鸡...");
> 					synchronized (wenjie) {
> 						System.out.println("对波哥说:哥,你先请我吃黄焖鸡,我就把500万还给你...");
> 					}
> 				}
> 			}
> 		}else{
> 			while (true) {
> 				//线程2执行wenjie对象后,需要获取到boge对象,但是boge对象还未执行完成,未释放锁
> 				synchronized (wenjie) {
> 					System.out.println("对波哥说:哥,你先请我吃黄焖鸡,我就把500万还给你...");
> 					synchronized (boge) {
> 						System.out.println("对文杰说:嘿,小子赶紧还我500万,我就请你吃黄焖鸡...");
> 					}
> 				}
> 			}
> 		}
> 	}
> }
> 
> public class DeadLockDemo {
> 
> 	public static void main(String[] args) {
> 		//该线程执行上半部分
> 		DeadLock d1 = new DeadLock(true);
> 		//该线程执行下半部分
> 		DeadLock d2 = new DeadLock(false);
> 		d1.start();
> 		d2.start();
> 	}
> }
> ```
>
> 传入的对象其实就是**synchronized**的“锁”，*该“锁”作为锁定代码块的对象，在代码块执行完毕之前都会被占用，不能被其他的线程访问*

### 线程通信(生产者与消费者)

> **概述**
>
> 为了体现生产和消费过程中的等待和唤醒，Java就提供了几个方法供我们使用，这几个方法在Object类中
>
> **Object类的等待和唤醒方法**
>
> |      方法名      | 说明                                                         |
> | :--------------: | ------------------------------------------------------------ |
> |   void wait()    | 导致当前线程等待，直到另一个线程调用该对象的notify()方法或notifyAll()方法 |
> |  void notify()   | 唤醒正在等待对象监视器的单个线程                             |
> | void notifyAll() | 唤醒正在等待对象监视器的所有线程                             |
>

#### 生产者消费者案例

> 所谓的生产者和消费者,实际主要包含两类线程:
>
> *一类是生产者线程用于生产数据*
>
> *一类是消费者线程用于消费数据*
>
> **两个线程共同操作一个数据区域**
> 
> ```java
> public class ThreadModelDemo {
> 	public static void main(String[] args) {
>		//创建集合,表现为同一共享数据区域
> 		List<String> list = new ArrayList<>();
>
> 		//开始时间
>		long start = System.currentTimeMillis();
> 		//生产商   生产者,匿名对象的方式创建线程类
>		Thread t = new Thread(new Runnable() {
> 			@Override
>			public void run() {
> 				//定义包子初始量为0
>				int num = 0;
> 				boolean flag = true;
> 				while(flag){
> 					//规定时间内造包子
> 					if(System.currentTimeMillis()-start<=2000){
> 						synchronized (list) {
>         							if(list.size()>=30){
> 								//如果数量大于等于30,这时候需要等待
> 								try {
> 									list.wait();  //需要其他线程唤醒
> 								} catch (InterruptedException e) {
> 									e.printStackTrace();
> 								}
> 							}else{
> 								//没有库存包子,就造
> 								list.add("湾仔码头小笼包"+(++num));
> 								//查看生产的包子
> 								System.out.println(Thread.currentThread().getName()+"生产包子的数量:"+num);
> 							}
> 						}
> 					}else{
> 						flag = false;
> 					}
> 				}
> 			}
> 		},"湾仔码头");
> 
> 		//消费者
> 		Thread t1 = new Thread(new Runnable() {
> 			@Override
> 			public void run() {
> 				//卖出包子初始数量
> 				int num = 0;
> 				boolean flag = true;
> 				while(flag){
> 					//规定时间内卖包子
> 					if(System.currentTimeMillis()-start<=2000){
> 						synchronized (list) {
> 							if(list.size()<=0){
> 								//如果数量小于等于0表示包子卖没了
>         								list.notify();  //唤醒其他线程
> 							}else{
> 								//消费者,卖包子
> 								list.remove("湾仔码头小笼包"+(++num));
> 								//查看卖出的包子数量
> 								System.out.println(Thread.currentThread().getName()+"卖出包子的数量:"+num);
> 							}
> 						}
> 					}else{
> 						flag = false;
> 					}
> 				}
> 			}
> 		}, "销冠");
> 
> 		//启动线程
> 		t.start();
> 		t1.start();
> 	}
> }
> ```
> 

#### sleep与wait的异同

> **相同**
>
> - 都是用于线程等待
>
> **不同**
>
> - sleep来自于线程类；wait来自于Object类
> - sleep睡眠时放弃资源但是没有放弃锁；wait放弃资源和锁
> - sleep在指定时间后自动唤醒；wait等待后需要notify或notifyAll唤醒
> - sleep可以在任意地方使用；wait，notify，notifyAll只能在同步方法或同步代码块使用

### 线程池

> 线程池的思想
>
> 是一种对象池的思想,开辟一块内存空间,里面存众多(未死亡)的线程,池中的线程执行调度由线程池来管理.当有线程任务时,从池子中获取一个线程,执行完成又将线程放入线程池中,这样就可以避免反复获取创建线程和销毁线程,节省系统资源
>
> 线程池类: **ThreadPoolExecutor**
>
> ```java
> public class ThreadPoolDemo {
> 
> 	public static void main(String[] args) throws Exception {
> 		Demo demo = new Demo();
> 		//创建一个线程池,线程池是通过Executors线程工厂类,创建一个新的线程池对象
> 		ExecutorService es = Executors.newCachedThreadPool();
> 		
> 		//线程池是以提交任务的形式执行
> 		Future<Integer> rs1 = es.submit(demo);
> 		Future<Integer> rs2 = es.submit(demo);
> 		//输出结果
> 		System.out.println("得到返回的结果为:"+rs1.get());
> 		System.out.println("得到返回的结果为:"+rs2.get());
> 		
> 	}
> 
> }
> //线程类,必须返回一个Integer类型的结果
> class Demo implements Callable<Integer>{
> 
> 	@Override
> 	public Integer call() throws Exception {
> 		int j=0;
> 		for (int i = 0; i < 5; i++) {
> 			j += i;
> 		}
> 		return j;
> 	}
> }
> ```
>
> 

## 网络编程

> **计算机网络**
>
> 是指将地理位置不同的具有独立功能的多台计算机及设备，通过通信线路连接起来，在网络操作系统，网络管理软件及网络通信协议的管理和协调下，实现资源共享和信息传递的计算机系统
>
> **网络编程**
>
> 在网络通信协议下，实现网络互连的不同计算机裕兴的程序间可以进行数据交互

### 网络编程三要素

> **IP地址**
>
> - 要想让网络中的计算机能够互相通信，必须为每台计算机指定一个标识号，通过这个标识号来指定要接收数据的计算机和识别发送的计算机，而IP地址就是这个标识号。也就是设备的标识
>
>
> **端口号**
>
> - 网络的通信，本质上是两个应用程序的通信。每台计算机都有很多的应用程序，那么在网络通信时，如何区分这些应用程序呢？如果说IP地址可以唯一标识网络中的设备，那么端口号就可以唯一标识设备中的应用程序了。也就是应用程序的标识
>
>
> **协议**
>
> - 通过计算机网络可以使多台计算机实现连接，位于同一个网络中的计算机在进行连接和通信时需要遵守一定的规则，这就好比在道路中行驶的汽车一定要遵守交通规则一样。在计算机网络中，这些连接和通信的规则被称为网络通信协议，它对数据的传输格式、传输速率、传输步骤等做了统一规定，通信双方必须同时遵守才能完成数据交换。常见的协议有UDP协议和TCP协议

### IP地址和InterAddress

#### IP地址

> 是网络计算机的唯一标识
>
> **IP地址分为两大类**
>
> - *IPv4*：**是给每个连接在网络上的主机分配一个32bit地址**。按照TCP/IP规定，IP地址用二进制来表示，每个IP地址长32bit，也就是4个字节。例如一个采用二进制形式的IP地址是“11000000101010000000000101000010”，这么长的地址，处理起来也太费劲了。为了方便使用，IP地址经常被写成十进制的形式，中间使用符号“”分隔不同的字节。于是，上面的IP地址可以表示为“192.168.1.66”。IP地的这种表示法叫做“点分十进制表示法”，这显然比1和0容易记忆得多
>
> - *IPv6*：由于互联网的蓬勃发展，IP地址的需求量愈来愈大，但是网络地址资源有限，使得IP的分配越发紧张。为了扩大地址空间，通过IPv6重新定义地空间，**采用128位地址长度，每16个字节一组，分成8组十六进制数**，这样就解决了网络地址资源数量不够的问题
>
> **常用命令**
>
> - ipconfig：查看本机IP
> - ping IP地址：查看网络是否连通
>
> **特殊IP地址**
>
> - 127.0.0.1：是回送地址，可以代表本机地址，一般用来测试使用

#### InterAddress

> 为了方便我们对IP地址的获取和操作，Java提供了一个类InterAddress供我们使用
>
> InterAddress：此类表示Internet协议(IP)地址
>
> |                  方法名                   | 说明                                                         |
> | :---------------------------------------: | ------------------------------------------------------------ |
> | static InetAddress getByName(string host) | 确定主机名称的ip地址，主机名称可以是机器名称，也可以是ip地址 |
> |           String getHostName()            | 获取此ip地址的主机名                                         |
> |          String getHostAddress()          | 返回文本显示中的ip地址字符串                                 |
>

### 端口和协议

#### 端口

> **端口**：*设备上应用程序的唯一标识*
>
> **端口号**：用两个字节表示的整数，*它的取值范围是0 ~ 65535.其中，0 ~ 1023之间的端口号用于一些知名网络服务和应用，普通的应用程序需要使用1024以上的端口号*。如果端口号被另外一个服务或应用所占用，会导致当前程序启动失败

#### 协议

> 计算机网络中，连接和同学的规则被称为网络通信协议
>
> 常用的协议有：**TCP通信协议**和**UDP通信协议**

##### UDP通信协议

> **概念**
>
> 用户数据报协议(User Datagram Protocol)
>
> **UDP是一种无连接通信协议，就是在数据传输时，数据的发送端和接收不用建立逻辑连接**。简单来说，当一台计算机向另外一台计算机发送数据时，发送端不会确认接收端是否存在，就会发出数据，同样接收端在收到数据时，也不会向发送端反馈是否收到数据。
>
> **由于使用UDP协议消耗资源小，通信效率高，所以通常都会用于音频，视频和普通数据的传输**
>
> 例如视频会议通常采用UDP协议，因为这种情况即使偶尔丢失一两个数据包，也不会对接受结果产生太大影响。但是在使用UDP协议传输数据时，由于UDP的面向无连接性，不能保证数据的完整性，因此在传输重要数据时不建议使用UDP协议
>
> **UDP通信原理**
>
> UDP协议是一种不可靠的网络协议，它在通信的两端各建立一个 Socket 对象，但是这两个  Socket 只是发送，接收数据的对象
>
> 因此对于基于UDP协议的通信双方而言，没有所谓的客户端和服务器的概念
>
> Java提供了 DatagramSocket 类作为基于 UDP 协议的 Socket
>
> **UDP发送数据**
>
> 发送数据的步骤
>
> 1. 创建发送端的Socket对象(DatagramSocket)
>
>    ```java
>    // DatagramSocket() 构造数据报套接字并将其绑定到本地主机上的任何可用端口
>    DatagramSocket ds = new DatagramSocket();
>    ```
>
> 2. 创建数据，并把数据打包
>
>    ```java
>    // DatagramPacket(byte[] buf, int length, InetAddress address, int port)
>    // 构造一个数据包，发送长度为length的数据包到指定主机上的指定端口号
>    byte[] buf = "hello world".getBytes();
>    int length = buf.length;
>    InetAddress address = InetAddress.getByName("127.0.0.1");
>    int port = 10086;
>    DatagramPacket dp = new DatagramPacket(buf, length, address, port);
>    // 优化
>    DatagramPacket dp2 = new DatagramPacket(buf, buf.length, InetAddress.getByName("127.0.0.1"), 10086);
>    ```
>
> 3. 调用DatagramSocket对象的方法发送数据
>
>    ```java
>    // void send(DatagramPacket p)从此套接字发送数据报包
>    ds.send(dp);
>    ```
>
> 4. 关闭发送端
>
>    ```java
>    // void close() 关闭此数据报套接字
>    ds.close();
>    ```
>
> **UDP接收数据**
>
> 接收数据的步骤
>
> 1. 创建接收端的Socket对象(DatagramSocket)
>
>    ```java
>    // DatagramSocket(int port) 构造数据报套接字并将其绑定到本地主机上的指定端口
>    DatagramSocket ds = new DatagramSocket(10086);
>    ```
>
> 2. 创建一个数据包，用于接收数据
>
>    ```java
>    // DatagramPacket(byte[] buf, int length) 构造一个DatagramPacket用于接收长度为length的数据包
>    byte[] buf = new byte[1024];
>    DatagramPacket dp = new DatagramPacket(buf, buf.length);
>    ```
>
> 3. 调用DatagramSocket对象的方法接收数据
>
>    ```java
>    ds.receive(dp);
>    ```
>
> 4. 解析数据包，并把数据在控制台显示
>
>    ```java
>    // byte[] getData() 返回数据缓冲区
>    byte[] datas = dp.getData();
>    // int getLength() 返回要发送的数据的长度或接收到的数据的长度
>    int len = dp.getLength();
>    String dataString = new String(datas, 0, len);
>    System.out.println("数据是：" + dataString);
>    // 优化
>    System.out.println("数据是：" + new String(dp.getData(), 0, dp.getLength()));
>    ```
>
> 5. 关闭接收端
>
>    ```java
>    // void close() 关闭此数据报套接字
>    ds.close();
>    ```
>
> **运行时需要先开启接收端，再开启发送端**

##### TCP通信协议

> **概念**
>
> 传输控制协议(Transmission Control Protocol)
>
> TCP协议是**面向连接**的通信协议，即传输数据之前，在发送端课接收端建立逻辑连接，然后再传输数据，它提供了两台计算机之间**可靠无差错**的数据传输。在TCP连接中必须要明确客户端与服务器端，由客户端向服务端发出连接请求，每次连接的创建都需要经过“三次握手”
>
> **TCP需要经过三次握手建立连接, 四次挥手断开连接**
>
> **三次握手**：
>
> 1. 第一次：**客户端向服务器端发出连接请求**，此时服务器知道了客户端要建立连接了
> 2. 第二次：**服务器端向客户端回送一个响应**，此时客户端知道服务器收到连接请求了
> 3. 第三次：**客户端再次向服务器端发送确认信息**，确认连接
>
> 刚开始, 客户端和服务器都处于 CLOSE 状态。此时, 客户端向服务器主动发出连接请求, 服务器被动接受连接请求。
>
> **四次挥手**：
>
> 1. 客户端 向 服务器 发出 FIN 包，表示自己没有数据要发送了
> 2. 服务器 收到 FIN 包，回复 FIN ACK，表示收到了 客户端 的 FIN 包，不会再接收 客户端 的数据了
> 3. 服务器 在发完 FIN ACK 后，可能还有数据要发给 客户端，这个数据是不能停止发送的，有数据还是需要继续发送
> 4. 服务器 发完了数据，也发出 FIN 包，告诉 客户端 自己的数据发完了，不再发送数据了
> 5. 客户端 收到了 服务器 的 FIN 包，知道 服务器 也没有数据要发送了，回复 FIN ACK。此时，连接可以断开了
>
> **确认应答机制(ACK机制)**
>
> **超时重传机制**
>
> **TCP/IP协议有几层**
>
> 在TCP/IP协议有四层
>
> 1. 应用层：应用层是TCP/IP协议的第一层，是直接为应用进程提供服务的。
> 2. 运输层：作为TCP/IP协议的第二层，运输层在整个TCP/IP协议中起到了中流砥柱的作用。且在运输层中，TCP和UDP也同样起到了中流砥柱的作用。
> 3. 网络层：网络层在TCP/IP协议中的位于第三层。在TCP/IP协议中网络层可以进行网络连接的建立和终止以及IP地址的寻找等功能。 
> 4. 网络接口层：在TCP/IP协议中，网络接口层位于第四层。由于网络接口层兼并了物理层和数据链路层所以，网络接口层既是传输数据的物理媒介，也可以为网络层提供一条准确无误的线路。
>
> **TCP通信原理**
>
> TCP通信协议是一种可靠的网络协议，它在通信的两端各建立一个Socket对象，从而在通信的两端形成网络虚拟链路，一旦建立了虚拟的网络链路，两端的程序就可以通过虚拟链路进行通信
>
> Java对基于TCP协议的网络提供了良好的封装，使用Socket对象来代表两端的通信端口，并通过Socket产生IO流来进行网络通信
>
> Java为客户端提供了Socket类，为服务器端提供了ServerSocket类
>
> **TCP发送数据**
>
> 发送数据的步骤
>
> 1. 创建客户端的Socket对象(Socket)
>
>    ```java
>    // Socket(InetAddress address, int port) 创建流套接字并将其连接到指定IP地址的指定端口号
>    Socket s = new Socket(InetAddress.getByName("127.0.0.1"), 10000);
>    // Socket(String host, int port) 创建流套接字并将其连接到指定IP地址的指定端口号
>    Socket s = new Socket("127.0.0.1", 10000);
>    ```
>
> 2. 获取输出流，写数据
>
>    ```java
>    // OutputStream getOutputStream() 返回此套接字的输出流
>    OutputStream out = s.getOutputStream();
>    out.write("Hello,TCP,我想建立连接...".getBytes());
>    ```
>
> 3. 释放资源
>
>    ```java
>    s.close();
>    ```
>
> **TCP接收数据**
>
> 1. 创建服务器端的Socket对象(ServerSocket)
>
>    ```java
>    // ServerSocket(int port) 创建绑定到指定端口的服务器套接字
>    ServerSocket ss = new ServerSocket(10000);
>    // Socket accept() 监听要连接到此套接字并接受它
>    Socket s = ss.accept();
>    ```
>
> 2. 获取输入流，读数据，并把数据显示在控制台
>
>    ```java
>    InputStream in = s.getInputStream();
>    byte[] buf = new byte[1024];
>    int len = in.read(buf);
>    String data = new String(buf, 0, len);
>    System.out.println("数据是：" + data);
>    ```
>
> 3. 释放资源
>
>    ```java
>    s.close();
>    ss.close();
>    ```
>
> **运行时需要先开启接收端，再开启发送端**

#### URL资源访问

> **概述**
>
> URL(Uniform Resource Locator),这是一个资源访问类,可以通过给定的地址找到指定的资源.这个资源可以是简单的作为一个文件或目录,或是一个搜索引擎等
>
> **最简单理解** 
>
> URL就是一个网址,如：http://www.baidu.com/xxx.html
>
> **URL解析**
>
> - http://：超文本传输协议
> - [www.baidu.com](http://www.baidu.com)：主机名或域名，表示资源主机
> - xxx.html：资源地址。表示一个资源，这个资源是一个网页
>
> **示例**
>
> ```java
> public class HttpURLDemo {
> 
> 	public static void main(String[] args) throws Exception {
> 		//创建一个URL对象,访问网络资源
> 		URL url = new URL("http://39.105.177.58:8888/www_hcq_cn");
> 		System.out.println(url.getHost());
> 		System.out.println(url.getPort());
> 		System.out.println(url.getProtocol());
> 		String result = login(url,"rf3dsxcd","285c57b1");
> 		System.out.println("login result:"+result);
> 	}
> 
> 	private static String login(URL url, String name, String pwd) throws Exception {
> 		//建立http连接
> 		HttpURLConnection connection = (HttpURLConnection) url.openConnection();
> 		//设置连接参数
> 		connection.setDoOutput(true);   //打开输出流(可以发送数据到服务器)
> 		connection.setDoInput(true);  	//打开输入流(可以接收服务器数据)
> 		//web请求方式两种  :  get   和 post请求方式      get快捷,携带量小,数据不安全
> 		connection.setRequestMethod("POST");
> 		
> 		//发送参数
> 		OutputStream out = connection.getOutputStream();
> 		String content = "username="+name+"&password="+pwd;
> 		out.write(content.getBytes());
> 		out.flush();
> 		
> 		String result = null;
> 		InputStream in = null;
> 		//获取访问状态码  200表示成功   404表示路径未找到    500表述数据处理异常
> 		int code = connection.getResponseCode();   //response 响应      request请求
> 		if(code==200){
> 			byte[] bs = new byte[1024];
> 			in = connection.getInputStream();
> 			int len = in.read(bs);
> 			result = new String(bs, 0, len);
> 		}else{
> 			System.out.println("异常编号为:"+code);
> 		}
> 		return result;
> 	}
> }
> ```
>
> 

## 反射

> 在 Java 的开发过程中，
>
> **概念**
>
> 是指在运行的过程中获取到一个类的变量和方法信息。然后通过获取到的信息来创建对象，调用方法的一种机制。由于这种动态性，可以极大地增加程序的灵活性，程序不用在编译时就完成对象的确定，在运行期仍然可以扩展功能

### 用于加载的类User

> ```java
> public class User {
> 	public int id;
> 	private String name;
> 	private String password;
> 	private int money;
> 
> 	public User() {
> 	}
> 
> 	private User(String name, String password) {
> 		this.name = name;
> 		this.password = password;
> 	}
> 
> 	public User(int id, String name, String password, int money) {
> 		this.id = id;
> 		this.name = name;
> 		this.password = password;
> 		this.money = money;
> 	}
> 
> 	public int getId() {
> 		return id;
> 	}
> 
> 	public void setId(int id) {
> 		this.id = id;
> 	}
> 
> 	public String getName() {
> 		return name;
> 	}
> 
> 	private void setName(String name) {
> 		this.name = name;
> 	}
> 
> 	public String getPassword() {
> 		return password;
> 	}
> 
> 	public void setPassword(String password) {
> 		this.password = password;
> 	}
> 
> 	public int getMoney() {
> 		return money;
> 	}
> 
> 	public void setMoney(int money) {
> 		this.money = money;
> 	}
> 
> 	@Override
> 	public String toString() {
> 		return "User [id=" + id + ", name=" + name + ", password=" + password + ", money=" + money + "]";
> 	}
> 
> }
> ```

### 类的加载

> **就是指将class文件读取到内存，并且创建一个 java.lang.Class**
>
> **任何类被使用时，系统都会为之建立一个 java.lang.Class**

#### Class类

> - Class 本身也是一个类
> - Class 对象只能由系统建立对象
> - 一个类在 JVM 中只会有一个Class实例
> - 一个Class对象对应的是一个加载到JVM中的一个.class文件
> - 每个类的实例都会记得自己是由哪个 Class 实例所生成
> - 通过Class可以完整地得到一个类中的完整结构

#### 类连接

> **验证阶段**
>
> - 用于检测被加载的类是否有正确的内部结构，并和其他类协调一致
>
> **准备阶段**
>
> - 负责为类的变量分配内存，并设置默认初始值
>
> **解析阶段**
>
> - 将类的二进制数据的符号引用替换为直接引用

#### 类的初始化

> - 创建类的实例
>
> - 调用类的对象方法
>
> - 访问类或者接口的变量，或者为变量赋值
>
> - 使用反射方式来强制创建某个类或接口对应的 java.lang.Class
> - 初始化某个类的子类
> - 直接使用 java.exe 命令来运行某个主类

### 获取Class类对象的三种方式

#### Class.forName(全类名)

> 通过Class类中的**静态方法forName(String className)**加载找到类
>
> ```java
> Class<?> clazz1 = Class.forName("com.roxla.classs.User");
> System.out.println(clazz1); // class com.roxla.classs.User
> ```
>
> 简单演示类创建对象，反射简单生成实例，无参构造的实例
>
> ```java
> User user = (User) clazz1.newInstance();
> user.setId(100);
> user.SetName("张三");
> System.out.println(user.toString()); // User [id=100, name=张三, password=null, money=0]
> ```

#### 对象.getClass()

> 通过对象调用**getClass()方法**，返回该对应的Class类
>
> - getClass()
>
> ```java
> User u = new User();
> Class<?> clazz2 = u.getClass();
> System.out.println(clazz2); // class com.roxla.classs.User
> ```

#### 类名.class属性

> 通过**类名.class属性**的方式，找到类
>
> ```java
> Class<?> clazz3 = User.Class;
> System.out.println(clazz3); // class com.roxla.classs.User
> ```

#### 以上三种方式所获取到的类的地址相同

> ```java
> System.out.println(clazz1 == clazz3); // true
> ```

### 反射内容

#### 反射获取到构造方法并使用

> |                 方法名                 | 说明                     |
> | :------------------------------------: | ------------------------ |
> |     Constructor[] getConstructor()     | 返回所有公共构造方法     |
> | Constructor[] getDeclaredConstructor() | 返回所有构造方法         |
> |  Constructor getDeclaredConstructor()  | 获取指定构造方法         |
> |      Constructor getConstructor()      | 获取指定公共构造方法     |
> |           int getModifiers()           | 返回指定访问修饰符编号   |
> |            String getName()            | 获取到构造方法名称       |
> |      Parameter[] getParameters()       | 获取到参数               |
> |   Object newInstance([Object.....])    | 根据指定构造方法创建对象 |
> |        void setAccessible(true)        | 忽略访问权限             |

##### 获取到类

> ```java
> Class<?> clazz = User.class;
> ```

##### 通过类反射获取到所有公共的构造方法

> ```java
> Constructor<?>[] cs = clazz.getConstructors();
> ```

##### 通过类反射找到所有的构造方法

> ```java
> Constructor<?>[] cs = clazz.getDeclaredConstructors();
> ```

##### 通过类反射找到指定的构造方法

> **无参构造方法**
>
> ```java
> Constructor<?> c = clazz.getConstructors();
> ```
>
> **带参构造方法**
>
> - 访问带参构造方法时，getConstructors() 中传入的参数要与要访问的带参构造方法相一致
>
>   - 访问全参构造方法
>
>     ```java
>     Constructor<?> c1 = clazz.getDeclaredConstructor(int.class, String.class, String.class, double.class);
>     ```
>
>   - 访问半参构造方法
>
>     ```java
>     Constructor<?> c2 = clazz.getDeclaredConstructor(String.class, String.class);
>     ```

##### 获取到访问修饰符

> ```java
> String m = Modifier.toString(c.getModifiers);
> ```

##### 获取到构造方法名称

> ```java
> String name = c.getName();
> ```

##### 获取到参数

> ```java
> Parameter[] pars = c1.Parameters();
> for(Parameter p : pars) {
>     System.out.println(p+",");
> }
> ```

##### 使用newInstance方法实例化对象

> **实例化无参构造方法的对象**
>
> ```java
> User user = (User) c.newInstance();
> ```
>
> **实例化有参构造方法的对象**
>
> - 如果构造方法的访问权限不为 public 的话，在实例化构造方法之前，需要忽略权限
>
>   ```java
>   // 使用 setAccessible() 方法忽略权限，true表示忽略权限
>   c2.setAccessible(true);
>   User user = (User) c2.newInstance("admin", "123456");
>   ```
>
> - 实例化访问权限为 public 的构造方法的对象
>
>   ```java
>   User user = (User) c1.newInstance("admin", "123456");
>   ```

#### 反射获取到属性并使用

> |               方法名                | 说明                   |
> | :---------------------------------: | ---------------------- |
> |         field[] getFields()         | 获取所有公共的属性     |
> |     field[] getDeclaredFields()     | 获取所有的属性         |
> | Field getDeclaredField(String name) | 通过属性名获取到属性   |
> | void set(Object obj, Object value)  | 对某个对象中的属性赋值 |
> |       Object get(Object obj)        | 获取指定类型的值       |

##### 获取到类，创建对象

> ```java
> // 获取到类
> Class<?> clazz = Class.forName("com.roxla.reflect.User");
> // 创建对象
> Object obj = clazz.newInstance();
> ```

##### 通过类反射获取所有公共属性

> ```java
> field[] fs = clazz.getfields();
> ```

##### 通过类反射获取所有属性

> ```java
> Field[] fs = clazz.getDeclaredFields();
> ```

##### 通过属性名获取到指定属性

> ```java
> Field f = clazz.getDeclaredField("name");
> ```

##### 获取访问权限

> ```java
> for(Field field : fs) {
>     String m = Modifier.toString(field.getModifiers());
> }
> ```

##### 获取类型

> ```java
> Class<?> type = f.getType();
> System.out.println(type.getSimpleName());
> ```

##### 获取简单属性名

> ```java
> String name = f.getName();
> ```

##### 操作属性，通过get和set方法操作对象中的属性

> **set方法，对某个对象中的属性赋值**
>
> - 因为操作的属性 name 的访问权限是 private，所以需要使用 setAccessible() 方法忽略权限
>
> ```java
> // 忽略权限
> f.setAccessible(true);
> f.set(obj, "张三");
> ```
>
> **获取对象中的属性，getXXX() 或 get() 可以获取指定类型的值，也可以直接获取 Object 类型的值**
>
> ```java
> System.out.println("用户名为："+f.get(obj));
> ```

#### 反射获取到方法并使用

> |                          方法名                           | 说明                 |
> | :-------------------------------------------------------: | -------------------- |
> |                   Method[] getMethods()                   | 获取所有公共的方法   |
> |               Method[] getDeclaredMethods()               | 获取所有的方法       |
> | Method getDeclaredMethod(String name, Class parameter...) | 通过方法名获取到方法 |
> |       Object invoke(Object obj, Object...parameter)       | 通过invoke执行方法   |

##### 获取到类，创建对象

> ```java
> // 获取到类
> User u = new User();
> Class<?> clazz = u.getClass();
> // 创建对象
> Object obj = clazz.newInstance();
> ```

##### 通过类获取到所有公共的方法

> ```java
> Method[] ms = clazz.getMethods();
> ```

##### 通过类获取到所有的方法

> ```java
> Method[] ms = clazz.getDeclaredMethods();
> ```

##### 获取指定方法

> ```java
> Method m = clazz.getDeclaredMethod("setName", String.class);
> ```

##### 获取返回值类型

> ```java
> for (Method method : ms) {
> 	//获取返回值类型
> 	Class<?> rtype = method.getReturnType();
> }
> ```

##### 获取方法名

> ```java
> String name = m.getName();
> ```

##### 获取到参数

> ```java
> Parameter[] pars = method.getParameters();
> for (Parameter p : pars) {
> 	System.out.print(p.getType().getSimpleName()+" "+p.getName()+",");
> }
> ```

##### 调用方法中的invoke方法，执行带返回值方法

> ```java
> //获取到指定方法
> Method m1 = clazz.getDeclaredMethod("toString");
> //调用方法中的invoke方法,执行带返回值方法
> Object str = m1.invoke(obj);
> System.out.println(str);
> ```



------

base64:

[1]:data:image/png;base64,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
[2]:data:image/png;base64,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
[3]:data:image/png;base64,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
[4]:data:image/png;base64,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

[5]:data:image/png;base64,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
