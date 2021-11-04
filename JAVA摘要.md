### JDK、JRE、JVM之间的关系

> <span style="color: green;">JDK：</span>
> java开发工具包，包含jre和开发环境，开发人员使用的工具(date，类型...，Scanner)
> <span style="color: green;">JRE：</span>
> java运行环境，包含jvm和运行所需的核心类
> <span style="color: green;">JVM：</span>
> java运行虚拟机

### Java 中 String 使用 equals() 和 == 的区别

> 在 String 中 == 比较引用地址是否相同，equals() 比较字符串的内容是否相同
>
> 在 int 中 == 和 equals() 相同
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

### 类和对象之间的关系

> <span style="color: red;">**对象是类的实例，类是对象的模板**</span>

### Java面向对象编程的特性

> - **封装**
>   - *通常认为封装是把数据和操作数据的方法绑定起来，对数据的访问只能通过已定义的接口。面向对象的本质就是将现实世界描绘成一系列完全自治、封闭的对象。我们在类中编写的方法就是对实现细节的一种封装；我们编写一个类就是对数据和数据操作的封装。可以说，封装就是隐藏一切可隐藏的东西，只向外界提供最简单的编程接口。*
> - **继承**
>   - *继承是从已有类得到继承信息创建新类的过程。提供继承信息的类被称为父类（超类、基类）；得到继承信息的类被称为子类（派生类）。继承让变化中的软件系统有了一定的延续性，同时继承也是封装程序中可变因素的重要手段。*
> - **多态**
>   - *多态性是指允许不同子类型的对象对同一消息作出不同的响应。简单的说就是用同样的对象引用调用同样的方法但是做了不同的事情。多态性分为编译时的多态性和运行时的多态性。如果将对象的方法视为对象向外界提供的服务，那么运行时的多态性可以解释为：当A 系统访问B 系统提供的服务时，B系统有多种提供服务的方式， 但一切对A 系统来说都是透明的。方法重载（overload）实现的是编译时的多态性（也称为前绑定），而方法重写（override）实现的是运行时的多态性（也称为后绑定）。运行时的多态是面向对象最精髓的东西，要实现多态需要做两件事：1. 方法重写（子类继承父类并重写父类中已有的或抽象的方法）；2. 对象造型（用父类型引用引用子类型对象，这样同样的引用调用同样的方法就会根据子类对象的不同而表现出不同的行为）。*
> - **抽象**
>   - *抽象是将一类对象的共同特征总结出来构造类的过程，包括数据抽象和行为抽象两方面。抽象只关注对象有哪些属性和行为，并不关注这些行为的细节是什么。*

### if与switch结构之间的区别

> if常用于区间型判断，进行大量数据的判断，减少代码的编写
>
> switch常用于精确型判断，进行少量数据的精确判断，性能略高

### Java中的数组排序

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
> 

### 复制对象和复制引用的区别

> 

### 深拷贝和浅拷贝

> 

### 重载和重写的区别

> ~~方法重载（overload）实现的是编译时的多态性（也称为前绑定），而方法重写（override）实现的是运行时的多态性（也称为后绑定）。运行时的多态是面向对象最精髓的东西，要实现多态需要做两件事：1. 方法重写（子类继承父类并重写父类中已有的或抽象的方法）~~
>
> *重载发生在一个类中，同名的方法如果有不同的参数列表则视为重载；重写发生在子类与父类之间，重写要求子类被重写方法与父类被重写方法有相同的参数列表，有兼容的返回类型。*
>
> <span style="color: #329BDC;">在同一个类中，方法名相同，参数列表不同，重载；在子类和父类之间，方法名相同，参数列表相同，返回值相同，子类权限修饰符不严于父类，重写</span>

### final 在 Java 中有什么作用

> - 修饰方法：表明该方法是最终方法，<span style="color: red;">不能被重写</span>
>
> - 修饰变量：表明该变量是常量，<span style="color: red;">不能再次被赋值</span>
> - 修饰类：表明该类是最终类，<span style="color: red;">不能被继承</span>

### final、finally、finalize 有什么区别

> - **final**：是修饰符，如果修饰类，此类不能被继承；如果修饰方法和变量，则表示此方法和此变量不能在被改变，只能使用。
> - **finally**：是 try{} catch{} finally{} 最后一部分，表示不论发生任何情况都会执行，finally 部分可以省略，但如果 finally 部分存在，则一定会执行 finally 里面的代码。
> - **finalize**： 是 Object 类的一个方法，在垃圾收集器执行的时候会调用被回收对象的此方法。

### Integer的值范围-128~127

> java中数据类型可以分为两类，一种的基本数据类型，一种是引用数据类型。
>
> 基本数据类型的数据不是对象，所以对于要将数据类型作为对象来使用的情况，java提供了相对应的包装类。
>
> int是基本数据类型，integer是引用数据类型，是int的包装类。
>
> 自动装箱的过程：引用了valueOf()的方法
>
> ```java
> public static Integer valueOf(int i) {
>     assert IntegerCache.high >= 127;
>     if (i >= IntegerCache.low && i <= IntegerCache.high)
>         return IntegerCache.cache[i + (-IntegerCache.low)];
>     return new Integer(i);
> }
> ```
>
> assertion就是在程序中的一条语句，它对一个boolean表达式进行检查，一个正确程序必须保证这个boolean表达式的值为true；如果该值为false，说明程序已经处于不正确的状态下，系统将给出警告并且退出。一般来说，assertion用于保证程序最基本、关键的正确性。
>
> *java内部为了节省内存，IntegerCache类中有一个数组缓存了值从-128到127的Integer对象。当我们调用Integer.valueOf（int i）的时候，如果i的值时结余-128到127之间的，会直接从这个缓存中返回一个对象，否则就new一个新的Integer对象。*
>
> <span style="color: red;">总结：当我们给一个Integer赋予一个int类型的值的时候它会调用Integer的静态方法ValueOf()方法。一旦程序调用valueOf 方法，如果i的值是在-128 到 127 之间就直接在cache缓存数组中去取Integer对象。而不在此范围内的数值则要new到堆中了</span>

### Java 中的 Math. round(-1. 5) 等于多少

> 等于 -1，因为在数轴上取值时，中间值（0.5）向右取整，所以正 0.5 是往上取整，负 0.5 是直接舍弃

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

### Java异常

> java中，异常可以分为三大类: Error，运行时异常，非运行时异常。抛出自定义异常用 throw 语句，在方法中抛出异常采用 throws 语句。

### error和exception的区别

> **error：**
>
> 表示系统级错误，由 java 虚拟机( jvm )抛出的，是 java 运行环境内部错误或者硬件问题，不能指望程序来处理这样的问题，除了退出运行外别无选择
>
> **exception：**
>
> 表示程序需要捕捉、需要处理的异常。是由于程序设计的不完善而出现的问题，程序必须处理的问题

### throw 和throws 的区别

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

### spring mvc 和 struts 的区别是什么

> 

### 如何避免 SQL 注入

> **什么是SQL注入**
>
> SQL注入是在程序运行过程中，通过特殊的手段，为SQL注入特殊的语句，达到任意查询
>
> ```java
> Class.forName("com.mysql.jdbc.Driver");
> String url = "jdbc:mysql://localhost:3306/test?characterEncoding=utf-8";
> Connection conn = DriverManager.getConnection(url, "root", "root");
> // 登录操作，注入密码sql
> String name="admin";
> String pwd = "123456 or 1=1";
> // sql注入 在sql中注入 or 1=1，在拼接时，不是将该语句认为是一个值，而是拼接成了语句。1=1 表示条件恒成立
> // 注入 or 1=1，会将表内所有的数据查询出来(select * from users where 1=1 相当于 select * from users)
> String sql = "select * from users where name='"+ name +"' and password=" + pwd;
> Statement st = conn.createStatement();
> ResultSet rs = st.executeQuery(sql);
> while(rs.next()){
>  System.out.println("登录成功!用户ID:"+rs.getInt(1)+", 用户名为:"+rs.getString("name")+", 密码为:"+rs.getString(3));
> }
> ```
>
> **如何避免**
>
> MySQL 中使用 PreparedStatement 接口
>
> - 是 Statement 接口的子接口，解决在 sql 拼接时造成的 sql 注入问题，这时候设置的值不会呈现结构的方式
> - PreparedStatement 接口以预编译 sql 的方式解决拼接的问题，每一个参数的地方使用 ？作为占位符
> - 再使用setXXX()方法设置对应类型对应位置的值，下标位置从1开始
>
> ```java
> // 加载驱动
> Class.forName("com.mysql.jdbc.Driver");
> // 获取连接字符串对象
> String url = "jdbc:mysql://localhost:3306/test?characterEncoding=utf-8";
> Connection conn = DriverManager.getConnection(url, "root", "root");
> // 准备SQL
> String name = "admin";
> String pwd = "123456 or 1=1";
> String sql = "select * from users where name=? and password=?";
> // 通过conn获取到执行对象，并预编译sql语句
> PreparedStatement pst = conn.prepareStatement(sql);
> // 为占位符赋值，有占位符就赋值，没有就不需要赋值
> pst.setString(1, name);
> pst.setString(2, pwd);
> // 执行sql，并得到结果
> rs = pst.executeQuery();
> // 循环遍历结果集，如果明确知道最多只有一个结果，可以使用判断
> if(rs.next()){
>      System.out.println("登录成功!用户ID:"+rs.getInt(1)+", 用户名为:"+rs.getString("name")+", 密码为:"+rs.getString(3));
> }else{
>     System.out.println("登录失败");
> }
> ```

### 接口声明中有\_\_\_\_\_\_和\_\_\_\_\_\_

> 接口声明中有**变量**和**抽象方法**

### jdbc提供的主要接口有哪几个

> **Statement接口、Connection接口、ResultSet接口、PreparedStatement接口**

### Java_如果去掉main方法的static修饰符会怎样

> ```java
> public class Test {
>     public void main(String[] args) {
>         System.out.println("test");
>     }
> }
> ```
>
> 结果：<span style="color: red;">错误: main 方法不是类 com.roxla.demo1.test.SupermarketDemo 中的static, 请将 main 方法定义为:
>    public static void main(String[] args)</span>
>
> **正常编译，运行报错**

### 什么是对象序列化

> 序列化就是将对象转化为字节序列的过程
>
> 反序列化是将字节序列转化为对象的过程
>
> 用于网络传输或者本地存储

### 抽象类和接口的区别

> - 抽象类可以有默认的方法实现，接口没有
> -  抽象类继承如果子类不是抽象类就是要全部实现父类中的抽象方法，接口一定要全部实现
> -  抽象类可以有构造器，接口不能有
> - 抽象类可以用public，protected，default修饰，接口只能用public

### 编译时多态、运行时多态

> 根据何时确定执行多态方法中的哪一个，多态分为两种情况：编译时多态和运行时多态。
>
> 如果在编译时能够确定执行多态方法中的哪一个，称为编译时多态，否则称为运行时多态
>
> **编译时多态**
>
> 
>
> **运行时多态**
>
> 



















