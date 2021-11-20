## 访问网站的过程

> 浏览器发出请求(http) -----> 域名服务器将域名解析为IP地址 -----> 网站服务器响应 -----> 浏览器显示页面
>
> **http**
>
> - 超文本传输协议（Hypertext Transfer Prtcl）
> - 是一个无状态的协议，不需要长时间保持(web浏览器-服务器)连接
> - 遵循请求--响应模型

## WEB原理

### java编写的客户端和服务端

> **客户端发请求**
>
> ```java
> socket s = new Socket("192.168.1.1/jd/index.html", 8080);
> InputStream is = s.getInputStream
> ```
>
> **服务端**
>
> ```java
> ServerSocket s = new ServerSocket(8080);
> Socket ss = s.getSocket();
> ....
> //查询商品列表
> os.write(...);
> ```

### 前后端交互的请求和响应方式

> **请求报文**(客户端)
>
> - 请求行
>   - s?ie=utf-8 HTTP/1.1
>
> - 请求头
>   - Host: gec.org
>   - Cookie: xx
>   - Content-Type
>
> - 空行
>
> - 请求体
>   - wd = 粤嵌
>
> **响应报文**(服务端)
>
> - 响应行
>
>   - HTTP/1.1 200 ok
>
> - 响应头
>
>   - Content-Type: text/html; charset=utf-8
>   - Content-length: 2048
>
> - 空行
>
> - 响应体
>
>   - ```html
>     <html>
>         <body>
>         	粤嵌...
>         </body>
>     </html>
>     ```
>

### <span id="State">状态码</span>

> **200**：成功响应
>
> **302**：重定向
>
> **403**：没有权限访问
>
> **404**：找不到资源
>
> **500**：服务器内部错误

### Web开发流程

> ![][3]
>
> 1. 前端页面发送请求
> 2. servlet 接收页面请求参数
> 3. 调用 dao 操作数据库
>    1. 接收 servlet 调用方法传参
>    2. 执行 sql 操作表
>    3. 如果有数据返回，返回给 servlet 
> 4. 响应前端请求

## Tomcat服务器

> **概述**
>
> Tomcat是Apache 软件基金会（Apache Software Foundation）的Jakarta 项目中的一个核心项目，由Apache、Sun 和其他一些公司及个人共同开发而成
>
> Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用服务器，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选
>
> *Tomcat就是一个 web 的服务器，用来发布 web 项目*

### Tomcat的安装

> **下载Tomcat**
>
> - 官网：https://tomcat.apache.org/
> - 下载地址：https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.54/bin/apache-tomcat-9.0.54-windows-x64.zip (Tomcat9)
>
> **解压Tomcat**
>
> 解压到一个非中文无空格的路径
>
> **启动Tomcat**
>
> - 进入 tomcat/bin
> - 双击 bin 目录里面的 startup.bat
> - 正常启动后会弹出一个 dos 窗口(*若关闭dos窗口则会关闭服务器*)
>
> **测试Tomcat**
>
> 打开浏览器输入以下地址
>
> - http://localhost:端口号
>
> 出现猫的欢迎界面则服务器启动成功

### Tomcat安装的注意事项

#### Java环境变量的配置

> Tomcat 运行需要依赖 Java环境，也就是说需要在电脑上安装了 JDK 之后才可以安装和启动 Tomcat。因为 Tomcat 启动的时候需要使用 JRE 的环境。必须要配置 JAVA_HOME 环境变量，如果没有配置 JAVA_HOME 环境变量，那么服务器在启动的时候就会一闪然后关闭。
>
> **配置 JAVA_HOME 环境变量**
>
> 1. `文件资源管理器` --> `此电脑鼠标右键` --> 选择`属性`
> 2. 选择 `高级系统设置` --> 选择 `环境变量`
> 3. 点击下方系统变量的 `新建`，创建新的环境变量，变量名输入 `JAVA_HOME` ，变量值输入`JDK的安装目录`
> 4. 选中 `Path` 环境变量， `双击` 或者 `点击编辑`
> 5. 点击 `新建` ，键入 `%JAVA_HOME%\bin`(必须是英文格式)，点击确定

#### Tomcat端口号冲突的问题

> 如果电脑上安装了一个应用之后，有可能会占用 Tomcat 的端口，如果将 Tomcat 端口占用了，同样这个 Tomcat 启动不了的
>
> **Tomcat 默认的端口号是 8080。一般 80 端口容易被其他程序占用。因为80端口是 HTTP 协议的默认端口(可以省略)**
>
> **解决办法**
>
> - 将占用端口的程序结束掉
>
>   - 输入命令查看端口号
>     - cmd --> netstat -ano
>     - 找到占用端口进程的`PID`
>   - 在任务管理器中结束占用端口的进程
>     - 任务管理器 --> 详细信息 --> 找到`PID对应的进程` --> 右键`结束任务`
>
> - 改变自身程序的端口
>
>   - 修改 Tomcat 的端口号
>
>     - 进入 tomcat/conf
>
>     - 编辑`conf`目录里面的`server.xml` 
>
>     - 修改 <Connector> 标签的`port`属性
>
>       ```xml
>       <Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" />
>       ```

### Tomcat的目录结构

> - **bin** <span style="color: red;">可执行脚本</span> 
> - **lib** <span style="color: red;">第三方jar包</span> 
> - **temp **<span style="color: red;">临时文件夹</span> 
> - **webapps** <span style="color: red;">要部署的web项目所在目录</span> 
> - **conf** <span style="color: red;">配置文件夹</span> 
> - **logs** <span style="color: red;">日志文件夹</span> 
> - **work** <span style="color: red;">jsp编译后文件夹</span> 

### web资源目录结构

> **动态web资源目录结构**
>
> website(web项目文件夹)
>
> - 静态页面(html、css、js、图片)
> - JSP页面
> - WEB-INF
>   - web.xml(必须的)
>   - classes(可选的，用于存放java类，一些servlet)
>   - lib(可选的，用于存放第三方jar包)
>
> **静态web资源目录结构**
>
> website(web项目文件夹)
>
> - 静态页面(html、css、js、图片)

### Tomcat的项目发布方式

> **第一种**
>
> 直接将项目复制到`tomcat/webapps`下
>
> **第二种**
>
> 在`tomcat/conf/server.xml`配置`tomcat`的虚拟路径
>
> **第三种**
>
> 在`tomcat/conf/Catalina/localhost`下配置`tomcat`的虚拟路径

#### 方式一

> 1. 在`tomcat`的`webapss`下创建`hello`的文件夹
>
> 2. 在`hello`文件夹下创建`WEB-INF`的文件夹
>
> 3. 在`hello`的文件夹下创建`index.html` 
>
> 4. 复制`tomcat/conf/web.xml`到`hello/WEB-INF`文件夹里面，编辑
>
>    ```xml
>    <?xml version="1.0" encoding="UTF-8"?>
>       
>    <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
>             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>             xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
>                                 http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
>             version="4.0">
>           <welcome-file-list>
>            <welcome-file>index.html</welcome-file>
>            <welcome-file>index.htm</welcome-file>
>            <welcome-file>index.jsp</welcome-file>
>        </welcome-file-list>
>    </web-app>
>    ```
>    
> 5. 点击`tomcat/bin/startup.bat` 
>
> 6. 在浏览器输入http://localhost:8080/hello 访问

#### 方式二

> <span id="path">**虚拟路径**</span> 
>
> 配置一个名词与一个真实的路径进行绑定，然后访问这个名称，从而找到真实路径
>
> **配置虚拟路径**
>
> 在`conf/server.xml`中进行配置(可在`tomcat`的文档中找到)
>
> 1. 创建一个项目
>
>    1. 在`D:\`下创建`hello`文件夹
>    2. 在`hello`文件夹下创建`index.html` 
>
> 2. 编辑`tomcat/conf`目录下的`server.xml` 
>
>    1. 在<Host>标签内添加
>
>       ```xml
>       <Context docBase="D:\hello" path="/index"></Context>
>       ```
>
>       - docBase：真实路径
>       - path：虚拟路径
>
> 3. 在浏览器输入http://localhost:8080/index 访问

#### 方式三

> 第三种方式也需要配置[虚拟路径](#path)，第二种需要修改`server.xml`。`server.xml`是`tomcat`的核心配置文件，一旦修改错了，那么`tomcat`服务器就会出现问题
>
> **配置虚拟路径**
>
> 在`tomcat/conf/Catalina/localhost`下进行配置(可在`tomcat`的文档中找到)
>
> 1. 创建一个项目
>
>    1. 在`D:\`下创建`ccc`文件夹
>    2. 在`ccc`文件夹下创建`index.html` 
>
> 2. 在`tomcat/conf/Catalina/localhost`下创建一个`itcast.xml`
>
> 3. 编辑`itcast.xml`内容
>
>    ```xml
>    <?xml version="1.0" encoding="UTF-8"?>
>    <Context docBase="D:\ccc"></Context>
>    ```
>
>    - xml文件名称(`itcast`)就是虚拟路径，只需要访问`itcast`就可以访问`D:\ccc`这个路径
>
> 4. 在浏览器输入http://localhost:8080/itcast 访问

### 配置Tomcat虚拟主机

> **虚拟主机的概述**
>
> 在电脑上设置一个目录，使用一个名称与该目录进行绑定。这个路径称为是虚拟主机。主机是可以发布web项目的
>
> **虚拟主机的配置**
>
> 1. 创建一个路径(虚拟主机)
>
>    1. 在`D:\`下创建`web/website`目录(`web`是虚拟主机的目录，`website`是项目名称)
>    2. 在`website`目录下创建`index.html` 
>    
> 2. 编辑`tomcat/conf`目录下的`server.xml` 
>
>    - 在`server.xml`中添加
>
>      ```xml
>      <Host name="www.baidu.com" appBase="D:\web" unpackWARs="true" autoDeploy="true">
>          <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs" prefix="localhost_access_log" suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b" />
>      </Host>
>      ```
>
>      - 访问`www.baidu.com`时，会跳转到`D:\web`
>
> 3. 修改本地的host文件
>
>    1. `hosts`文件在`C:\Windows\System32\drivers\etc`目录下
>
>    2. 添加内容
>
>       ```tex
>       192.168.0.2(本机ip) www.baidu.com
>       ```
>
> 4. 在浏览器输入http://www.baidu.com:8080 访问；输入http://www.baidu.com:8080/website 访问项目
>
> 5. 可以进行如下配置
>
>    ```xml
>    <Host name="www.baidu.com" appBase="D:\web" unpackWARs="true" autoDeploy="true">
>        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs" prefix="localhost_access_log" suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b" />
>        <Context path="/" docBase="website "></Context>
>    </Host>
>    ```
>
>    - 配置后在浏览器输入http://www.baidu.com:8080 可以直接访问项目
>

## IDEA

> **概述**
>
> IDEA 全称 IntelliJ IDEA，是java编程语言开发的集成环境。IntelliJ在业界被公认为最好的java开发工具，尤其在智能代码助手、代码自动提示、重构、JavaEE支持、各类版本工具(git、svn等)、JUnit、CVS整合、代码分析、 创新的GUI设计等方面的功能可以说是超常的

### IDEA设置

> **设置界面字体**
>
> 1. 打开`idea`，点击`File`-->`Settings` 
> 2. 点击进去`Settings`界面之后，点击`Appearance & Behavior`-->`Appearance` 
> 3. 勾选`Override default fonts by (not recommended)`，设置字体和大小
>
> **设置程序字体**
>
> 1. 打开`idea`，点击`File`-->`Settings` 
> 2. 点击进去`Settings`界面之后，点击`Editor`-->-`Font`，设置字体、大小和间距
>
> **设置当前项目编码格式**
>
> 1. 打开`idea`，点击`File`-->`Settings` 
> 2. 点击进去`Settings`界面之后，点击`Editor`-->`File Encodings` 
> 3. 将`Project Encoding`还有下方的`Default encoding for properties files`设置为`utf-8`格式
> 4. 把当前项目添加上，点击OK，就把当前项目设置为`utf-8`格式
>
> **设置默认文件编码格式**
>
> 1. 点击`File`-->`Other`，`Settings`-->`Default Settings` 
> 2. 进去`Default Settings`界面之后，点击`Editor`-->`File Encodings` ，同样将`Project Encoding`还有下方的`Default encoding for properties files`设置为`utf-8`格式，这设置的默认所有文件编码格式
> 3. 把当前项目添加上，点击OK，就把当前项目设置为`utf-8`格式

### IDEA集成Tomcat

> **添加tomcat**
>
> 1. 打开`idea`，点击`Run`-->`Edit Configurations`
> 2. 点击进去`Edit Configurations`界面之后，点击加号
> 3. 找到`TomcatServer`，选择`Local` 
>    - 有的时候`TomcatServer`会被折叠上，找到展开按钮，展开后就看到`TomcatServer`了
> 4. 配置tomcat信息
>    - 在`Tomcat Server`-->`Unnamed`-->`Server`-->`Application server`项目下，点击`Configuration`，找到本地`Tomcat`服务器，再点击`OK`按钮
>    - 在`Tomcat Server`-->`Unnamed`-->`Name`项目下设置`Tomcat Server`的名称
>
> **部署tomcat**
>
> 1. 在`Tomcat Server`-->`Unnamed`-->`Deployment`项目下，点击加号，将需要部署的项目添加
> 2. 修改该项目下的`Application context`为你想要的地址
>    - 当有部署多个项目，启动时默认访问第一个项目，可以通过上下箭头来将想访问的项目上移
> 3. 点击`OK`按钮
>
> **控制台乱码解决**
>
> 打开`Intellij idea`安装目录，在`bin`目录下的`idea.exe.vmoptions`和`idea64.exe.vmoptions`两个文件结尾添加
>
> ```
> -Dfile.encoding=UTF-8
> ```
>
> 在`Tomcat Server`-->`Unnamed`-->`Server`-->`VM options`项目中添加
>
> ```
> -Dfile.encoding=UTF-8
> ```
> 
> *如果还有乱码，则点击 Help --> Edit Custom VM Options，在打开的文件后面添加 -Dfile.encoding=utf-8，然后重启 IDEA*

## XML

> **概述**
>
> xml 是可扩展的标记性语言
>
> xml 的主要作用有：
>
> - 用来保存数据，而且这些数据具有自我描述性
> - 可以作为项目或者模块的配置文件
> - 可以作为网络传输数据的格式（现在以 JSON 为主）

### XML的语法

> - 文档声明
> - 元素标签
> - xml 属性
> - xml 注释
> - 文本区域（CDATA区）
>
> **创建一个 xml 文件**
>
> ```xml
> <!-- xml 的声明 -->
> <?xml version="1.0" encoding="UTF-8"?>
> <!-- xml 的注释 -->
> <books>
> 	<book sn="SN123412123412">
>         <name>时间简史</name>
>         <author>霍金</author>
>         <price>75</price>
>     </book>
>     <book sn="SN123412123412">
>         <name>Java从入门到放弃</name>
>         <author>高斯林</author>
>         <price>105.7</price>
>     </book>
> </books>
> ```
>
> - books：表示多个图书信息
> - book：表示一个图书信息
>   - sn属性表示图书序列号
> - name：表示书名
> - author：表示作者
> - price：表示图书价格

#### XML文件的声明

> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> ```
>
> - version：xml 的版本
> - encoding：xml 文件本身的编码格式

#### XML的注释

> HTML 和 XML 注释一样：<!-- html 的注释 -->

#### XML的元素

> XML 元素指的是从 **<**（且包括）开始标签直到 **>**（且包括)结束标签的部分。元素可包含其他元素、文本或者两者的混合物。元素也可以拥有属性
>
> ```xml
> <bookstore>
>     <book category="CHILDREN">
>         <title>Harry Potter</title>
>         <author>J K.Rowling</author>
>         <year>2005</year>
>         <price>29.99</price>
>     </book>
>     <book category="WEB">
>         <title>Learning XML</title>
>         <author>Erik T.Ray</author>
>         <year>2003</ year>
>         <price>39.95</price>
>     </book>
> </bookstore>
> ```
>
> 在上例中，`<bookstore>`和`<book>`都拥有元素内容，因为它们包含了其他元素。`<author>`只有文本内容，因为它仅包含文本
>
> *元素是指从开始标签到结束标签的内容*
>
> 例如：`<title>Java编程思想</title>`
>
> **元素：我们可以简单的理解为是 标签**
>
> 注意：
>
> **XML 标签对大小写敏感**
>
> **XML 文档必须有根元素（根元素就是顶级元素，没有父标签的元素，而且是唯一一个才行）**

##### XML命名规则

> XML 元素必须遵守以下命名规则
>
> - 名称可以含字母、数字以及其他的字符
>
>   ```xml
>   <title_1>Learning XML</title_1>
>   ```
>
> - 名称不能以数字或者标点符号开头
>
>   ```xml
>   <!-- <1book>Learning XML</1book> -->
>   ```
>
> - 名称不能包含空格
>
>   ```xml
>   <!-- <bo ok>Learning XML</bo ok> -->
>   ```

##### XML中的元素(标签)也分成单标签和双标签

> **单标签**
>
> 格式：
>
> ```xml
> <标签名 属性="值" 属性="值" />
> ```
>
> **双标签**
>
> 格式：
>
> ```xml
> <标签名 属性="值" 属性="值">...文本数据或子标签</标签名>
> ```
>
> **所有 xml 元素都必须有关闭标签（也就是闭合），不闭合就会报错**
>
> **xml 必须正确的嵌套**

#### XML的属性

> xml 的标签属性和 html 的标签属性是非常类似的，**属性可以提供元素的额外信息**
>
> 在标签上可以书写属性的规则和标签的书写规则一致
>
> 一个标签上可以书写多个属性。**每个属性的值必须使用引号引起来**
>
> **属性必须使用引号引起来，不引会报错**

#### XML中的特殊字符

> ```xml
> <author>&lt;班长&gt;</author>
> ```
>
> - &lt; 特殊字符：\&lt;
> - &gt; lt; 特殊字符：\&gt;

#### 文本区域（CDATA区）

> CDATA 语法可以告诉 xml 解析器，我 CDATA 里的文本内容，只是纯文本，不需要 xml 语法解析
>
> **格式**
>
> \<![CDATA[这里可以把你输入的字符原样显示，不会解析 xml]]>
>
> ```xml
> <![CDATA[<<<<<<<<<<<< 123]]>
> ```

## Servlet

> 是Web的规范
>
> 是Web的三大组件（Servlet/filter/listener）之一
>
> **是运行在服务器的一小段程序，用来接收请求，响应请求**

### Servlet的实现方式(重点)

> **Servlet 的实现方式有三种**
>
> - 实现Servlet接口
> - 继承GenericServlet类
> - 继承HttpServlet类

#### 实现Servlet接口

> **class Fxx implements Servlet{ //重写方法}**
>
> **步骤**
>
> - 写一个类实现 Servlet 接口
> - 在`web.xml`配置`servlet`和`servlet-mapping`
> - 在浏览器发起一个 url 请求
>
> **代码**
>
> *Servlet实现类*
>
> ```java
> public class Hello implements Servlet {
>     @Override
>     public void init(ServletConfig servletConfig) throws ServletException {
>     }
> 
>     @Override
>     public ServletConfig getServletConfig() {
>         return null;
>     }
> 
>     @Override
>     public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
>         System.out.println("有请求过来了...");
>     }
> 
>     @Override
>     public String getServletInfo() {
>         return null;
>     }
> 
>     @Override
>     public void destroy() {
>     }
> }
> ```
> 
> *web.xml 配置*
>
> ```xml
><servlet>
>     <!--给servlet起一个别名 -->
>     <servlet-name>Hello</servlet-name>
>     <!--servlet的实现类-->
>     <servlet-class>com.gec.serlvet.Hello</servlet-class>
> </servlet>
> 
> <servlet-mapping>
>     <!--servlet-name的作用是告诉tomcat服务器，当前的Hello给哪个servlet使用的-->
>     <servlet-name>Hello</servlet-name>
>     <!-- web服务器解析web.xml的时候，请求过来就会匹配 /hello -->
>     <url-pattern>/hello</url-pattern>
> </servlet-mapping>
> ```

#### 继承GenericServlet

> **步骤**
>
> - 写一个类继承 GenericServlet
> - 重写 service 方法
> - 配置`web.xml`
>
> **代码**
>
> *GenericServlet子类*
>
> ```java
> public class Gen extends GenericServlet {
>     @Override
>     public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
>         System.out.println("hello....");
>     }
> }
> ```
> 
>*web.xml 配置*
> 
>```xml
> <servlet>
>     <!--给servlet起一个别名 -->
>     <servlet-name>Gen</servlet-name>
>     <!--servlet的实现类-->
>     <servlet-class>com.roxla.serlvet.Gen</servlet-class>
> </servlet>
> 
> <servlet-mapping>
>     <!--servlet-name的作用是告诉tomcat服务器，当前的Hello给哪个servlet使用的-->
>     <servlet-name>Gen</servlet-name>
>     <!-- web服务器解析web.xml的时候，请求过来就会匹配 /hello -->
>     <url-pattern>/gen</url-pattern>
> </servlet-mapping>
> ```

#### 继承HttpServlet方式(重点)

> **步骤**
>
> - 写一个类继承 HttpServlet
> - 重写 init/destroy/service 方法
> - 配置`web.xml`
>
> **代码**
>
> *HttpServlet子类*
>
> ```java
> public class Http extends HttpServlet {
>     @Override
>     protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
>         System.out.println("hello....");
>     }
> }
> ```
>
> *web.xml 配置*
>
> ```xml
> <servlet>
>     <!--给servlet起一个别名 -->
>     <servlet-name>Http</servlet-name>
>     <!--servlet的实现类-->
>     <servlet-class>com.roxla.serlvet.Http</servlet-class>
> </servlet>
> 
> <servlet-mapping>
>     <!--servlet-name的作用是告诉tomcat服务器，当前的Hello给哪个servlet使用的-->
>     <servlet-name>Http</servlet-name>
>     <!-- web服务器解析web.xml的时候，请求过来就会匹配 /hello -->
>     <url-pattern>/http</url-pattern>
> </servlet-mapping>
> ```

#### 常见错误

> servlet-name 在 servlet 和 servlet-mapping 里面不一致
>
> ```xml
> <servlet>
>        <!--给servlet起一个别名 -->
>        <servlet-name>Hello</servlet-name>
>        <servlet-class>com.gec.serlvet.Hello</servlet-class>
> </servlet>
> 
> <servlet-mapping>
>        <!--和servlet中的servlet-name不一致-->
>        <servlet-name>a</servlet-name>
>        <url-pattern>/hello</url-pattern>
> </servlet-mapping>
> ```
>
> url-pattern 没有以斜杠开头 
>
> ```xml
> <url-pattern>hello</url-pattern> <!-- 错误 -->
> <url-pattern>/hello</url-pattern> <!-- 正确 -->
> ```
>

#### 使用注解实现

> ```java
> @WebServlet("/http")
> public class Http extends HttpServlet {
>        @Override
>        protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
>            System.out.println("hello....");
>        }
> }
> ```
>
> @WebServlet("/http") 注解相当于实现了下列代码
>
> ```xml
> <servlet>
>        <!--给servlet起一个别名 -->
>        <servlet-name>Http</servlet-name>
>        <!--servlet的实现类-->
>        <servlet-class>com.roxla.serlvet.Http</servlet-class>
> </servlet>
> <servlet-mapping>
>        <!--servlet-name的作用是告诉tomcat服务器，当前的Hello给哪个servlet使用的-->
>        <servlet-name>Http</servlet-name>
>        <!-- web服务器解析web.xml的时候，请求过来就会匹配 /hello -->
>        <url-pattern>/http</url-pattern>
> </servlet-mapping>
> ```

#### @WebServlet注解

> **属性**
>
> |       属性        |      类型      | 是否必须 | 说明                                        |
> | :---------------: | :------------: | :------: | ------------------------------------------- |
> |  asyncSupported   |    boolean     |    否    | 指定 Servlet 是否支持异步操作模式           |
> |    displayName    |     String     |    否    | 指定 Servlet 显示名称                       |
> |    initParams     | WebInitParam[] |    否    | 配置初始化参数                              |
> |   loadOnStartup   |      int       |    否    | 标记容器是否在应用启动时就加载这个 Servlet  |
> |       name        |     String     |    否    | 指定  Servlet 名称                          |
> | urlPatterns/value |    String[]    |    否    | 这两个属性作用相同，指定 Servlet 处理的 url |
>
> **可以通过配置 @WebServlet 来实现不同的功能**
>
> *通过注解配置 Servlet 响应的 url 和 初始化参数*
>
> ```java
> @WebServlet(urlPatterns = {"/demo"}, initParams = {@WebInitParam(name="class",value = "2171")})
> /*
> 	initParams = {@WebInitParam(name="class",value = "2171")}相当于下面的配置
>     <init-param>
>         <param-name>class</param-name>
>         <param-value>2171</param-value>
>     </init-param>
> */
> ```
>
> *通过注解配置 Servlet 响应多个 url 的请求*
>
> ```java
> @WebServlet(urlPatterns = {"/addUser.action","/checkName.action"})
> ```

### servlet执行流程(重点)

> **流程**
>
> 1. 浏览器的地址栏上输入地址 http://localhost:8080/s1/http
>    - http://：http协议
>    - localhost：本地IP
>    - 8080：端口号
>    - /s1：工程路径
>    - /http：资源路径
> 2. 浏览器向服务器发起请求
> 3. 服务器会根据`web.xml`中对 servlet 的配置，找到对应的资源文件
>    1. 服务器先根据浏览器地址栏的`资源路径`找到`web.xml`配置中的`url-pattern` 
>    2. 获取与`url-pattern`在同一个`servlet-mapping`标签下的`servlet-name`标签的值
>    3. 找到在`servlet`标签下的`servlet-name`的值与获取的值相同的标签
>    4. 获取与`servlet-name`在同一个`servlet`标签下的`servlet-class`中所写的实现类的路径
>    5. 访问该路径，执行类中的 service 方法
>
> **图解**
>
> ![][2]

### 请求方式

#### get请求(未完成)

> 超链接 `<a href="http">xx< /a>  `
>
> 浏览器输入的地址

#### post请求(未完成)

> 表单提交 `<form method="post"> xxxx</form> `

#### 什么时候调用哪个方法？(笔试里面的选择题)

> 重写父类( HttpServlet 类的 service )，HttpServlet 子类的 service 方法，doGet，doPost 方法同时存在
>
> 调用父类的 service
>
> HttpServlet 子类的 service 方法，doGet，doPost 三个方法同时存在
>
> 调用 HttpServlet 子类的 service 方法
>
> doGet，doPost 两个方法同时存在
>
> 根据调用时请求的方式调用，如果 getMethod 是 GET，调用 doGet，否则就是 doPost

#### get/post区别(笔试题)

> 在语义上讲，get是客户端发出向服务端请求数据（获取数据），post是客户端向服务端提交数据
>
> **标准回答**
>
> get：
>
> - 提交的数据在浏览器地址栏能看到 如：**localhost:8080/03servlet/login?name=tom**
> - 不安全(*提交的数据可以从 url 中直接看到*)
> - get请求是幂等性的（*请求url发给所有人都能看到同样的结果*）
>
> post：
>
> - 提交的数据在 form-data 里面
> - 提交的数据可以很大
> - 相对于 get 方法来说更加安全
> - post 请求是不幂等性的，其它人获取到这个链接无效的
>
> **小数据情况下，get请求的效率会更高一些，因为get只发一次数据包，而post要发两次数据包**

### HttpServletRequest请求对象(未完成)

> 

### 使用idea创建servlet

> ![][1]

### MIME类型(未完成)

> **MIME 是 HTTP协议中数据的类型**
>
> MIME的英文全称是"Multipurpose Internet Mal Extensions”多功能Internet邮件扩充服务。MiIME类型的格式是“大类型小类型”,并与某一种文件的扩展名相对应。
>
> 规定的类型在`tomcat/conf/web.xml`
>
> **常见的 MIME 类型**
>
> | 文件               | 扩展名      | MIE类型                      |
> | ------------------ | ----------- | ---------------------------- |
> | 超文本标记语言文本 | .htm，.html | text/html                    |
> | 普通文本           | .txt        | text/plain                   |
> | RTF文本            | .rtf        | application/rtf              |
> | GIF图形            | .gif        | image/gif                    |
> | JPEG图形           | .jpeg，.jpg | image/jpeg                   |
> | au声音文件         | .au         | audio/basic                  |
> | MIDl音乐文件       | .mid，.midi | audio/midi                   |
> | RealAudio音乐文件  | .ra，.ram   | audio/x-pn-realaudio         |
> | MPEG文件           | .mpg，.mpeg | video/mpeg                   |
> | AVI文件            | .avi        | video/x-msvideo              |
> | GZIP文件           | .gz         | application/x-gzip           |
> | TAR文件            | .tar        | application/x-tar            |
> | RAR文件            | .rar        | application/x-rar-compressed |
> | ZIP文件            | .zip        | application/zip              |
>
> 

### HttpServletResponse

> **概述**
>
> 开发的软件是 B/S 结构的软件，可以通过浏览器访问服务器的软件。从浏览器输入一个地址访问服务器（将这个过程称为是请求)。服务器接收到请求，需要进行处理，处理以后需要将处理结果显示回浏览器端（将这个过程称为是响应)。

#### 设置Response响应的状态码

> ```java
> response.setStatus(int sc);
> ```
>
> [状态码](#State)

#### HttpServletResponse关于响应头的方法

> **set开头的方法**
>
> |                方法名                 | 描述                                                         |
> | :-----------------------------------: | ------------------------------------------------------------ |
> | setDateHeader(String name, long date) | 该方法把指定的头名称以及日期设置为响应头信息，其中日期用 long 类型的值表示，其值是从新纪元开始算起的毫秒数 |
> | setHeader(String name, String value)  | 该方法把指定的头名称以及字符串设置为响应头信息               |
> |  setIntHeader(String name, intvalue)  | 该方法把指定的头名称以及数字设置为响应头信息                 |
>
> *set开头的方法：针对一个 key 对应 一个 value 的情况*
>
> - 举例：比如有一个头 content-Type:text/html
>   - setHeader("content-Type", "text/plain")；
>   - 最终得到的头结果：content-Type:text/plain
>
> **add开头的方法**
>
> |                方法名                 | 描述                                                         |
> | :-----------------------------------: | ------------------------------------------------------------ |
> | addDateHeader(String name, long date) | 该方法把指定的头名称以及日期添加为响应头信息，不会影响原有的响应头信息 |
> | addHeader(String name, String value)  | 该方法把指定的头名称以及字符串添加为响应头信息，不会影响原有的响应头信息 |
> |  addIntHeader(String name, intvalue)  | 该方法把指定的头名称以及数字添加为响应头信息，不会影响原有的响应头信息 |
>
> *add开头的方法：针对一个 key 对应 多个 value 的情况*
>
> 举例：比如有一个头 content-Type:text/html
>
> - setHeader("content-Type", "text/plain")；
> - 最终得到的头结果：content-Type:text/html, text/plain

#### HttpServletResponse关于响应体的方法

> |      方法名       | 描述 |
> | :---------------: | ---- |
> | getOutputStream() |      |
> |    getWriter()    |      |
>
> 

#### HttpServletResponse响应对象(未完成)

> 
>
> 
>
> 打印流：getWriter()
>
> 打印的方法：print/println(Object o)
>
> 设置响应类型：setContentType(String type)

#### HttpServletRequest的常用方法(重点)(未完成)

> |      方法名      | 描述                       |
> | :--------------: | -------------------------- |
> | getContextPath() | 获取上下文/context/工程名  |
> |   getMethod()    | 获取提交方式               |
> | getRemoteAddr()  | 获取本地IP                 |
> | getRequestURI()  | 获取端口后面的一个请求路径 |
> | getRequestURL()  | 获取完整的一个请求路径     |
> | getServletPath() | 获取资源路径               |
> |  getProtocol()   | 获取http协议版本           |
> |   getHeaders()   | 获取请求头                 |
>
> 

##### getContextPath()

> 

##### getMethod()

> 

##### getRemoteAddr()

> 

##### getRequestURI()

> 

##### getRequestURL()

> 

##### getServletPath()

> 

##### getProtocol()

> 

##### getHeaders()

> **getHeaders()返回一个枚举数据**
>
> 

### 乱码处理(重点)

> **处理方案**
>
> 1. setCharsetEncoding("utf-8") 
>    - 为什么要设编码？servlet 里面的方法的默认编码是`iso-8859-1`是欧洲信息标准编码
> 2. new String(获取的字符串.getBytes("iso-8859-1"),"utf-8");
>    - tomcat 的 doGet 方法不支持
> 3. `tomcat/conf/server.xml`在`connetor`标签里面添加`URIEncoding="utf-8"`
>
> *idea2019  tomcat7 doGet无法处理乱码(把方法改成service就可以了)*

### ServletConfig(未完成)

> **概述**
>
> ServletConfig 用来获得 Servlet 的相关的配置的对象
>
> **获得ServletConfig对象**
>
> ```java
> // 获取当前类的ServletConfig
> ServletConfig config = this.getServletConfig();
> ```
>
> **ServletConfig对象的API**
>
> |            方法名             | 描述                      |
> | :---------------------------: | ------------------------- |
> | getInitParameter(String name) | 获得 Servlet 的初始化参数 |
> |    getInitParameterNames()    | 获得所有初始化参数的名称  |
> |      getServletContext()      | 获得 ServletContext 对象  |
> |       getServletName()        | 获得 Servlet 的名称       |
>
> *要演示 ServletConfig 的 API，需要先在 web.xml中配置 Servlet 的初始化参数*
>
> ```xml
> <servlet>
> 	<servlet-name>XXXX</servlet-name>
>     <servlet-class>XXXX</servlet-class>
>     <init-param>
>         <param-name>username</param-name>
>         <param-value>root</param-value>
>     </init-param>
>     <init-param>
>         <param-name>password</param-name>
>         <param-value>abc</param-value>
>     </init-param>
> </servlet>
> ```

#### getInitParameter()

> 获得对应名称的初始化参数的值
>
> **格式**
>
> ```java
> ServletConfig config = this.getServletConfig();
> String username = config.getInitParameter("username");
> String password = config.getInitParameter("password");
> System.out.println(username+"    "+password);
> ```
>
> **结果**
>
> *root    abc*

#### getInitParameterNames()

> 获得所有初始化参数的名称
>
> **格式**
>
> ```java
> ServletConfig config = this.getServletConfig();
> Enumeration<String> names = config.getInitParameterNames();
> while(names.hasMoreElements) {
>     String name = names.nextElement();
>     String value = config.getInitParameter(name);
>     System.out.println(name+"    "+value);
> }
> ```
>
> **结果**
>
> *username    root*
>
> *password    abc*

#### getServletContext()

> 

#### getServletName()

> 

### ServletContext(重点)(未完成)

> 每个 Java 虚拟机的每个“Web 应用程序”都有一个上下文。
>
> 每一个web Module 就是对应的context 
>
> 还是域对象，想象成是一个Map,可以存取数据
>
> **常用方法**
>
> |                 方法名                 | 描述              |
> | :------------------------------------: | ----------------- |
> |     getInitParameter(String name)      | 根据名字获取值    |
> |        getRealPath(String path)        | 部署工程路径      |
> | setAttribute(String name,Object value) | 存储名字-值       |
> |       getAttribute(String name)        | 取值              |
> |      removeAttribute(String name)      | 在context移除name |
> |        getServletContextName()         |                   |
> |          getServletContext()           |                   |
>
> **域对象的存储的有效时间为：tomcat提供时一直有效，tomcat停止服务，就没有值了**
>
> **设置的 <cotext-param>**
>
> ```xml
> <context-param>
>     <param-name>boss</param-name>
>     <param-value>张三</param-value>
> </context-param>
> ```

#### getInitParameter()

> 

#### getRealPath()

> 

#### setAttribute()

> 

#### getAttribute()

> 

#### removeAttribute()

> 

#### getServletContextName()

> 

#### getServletContext()

> 

### Servlet生命周期(重点)

> **生命周期**
>
> 一件事物从出现到消失的过程
>
> **生命周期方法**
>
> |                             方法                             | 说明                                                         |
> | :----------------------------------------------------------: | ------------------------------------------------------------ |
> |            public void init(SorvletConfig config)            | 初始化方法                                                   |
> | protected void service(HttpServletRequest req, HttpServletResponse resp) | service() 方法是执行实际任务的主要方法。Servlet 容器（即 Web 服务器）调用 service() 方法来处理来自客户端（浏览器）的请求，并把格式化的响应写回给客户端 |
> |                    public void destroy()                     | destroy() 方法可以让您的 Servlet 关闭数据库连接、停止后台线程、把 Cookie 列表或点击计数器写入到磁盘，并执行其他类似的清理活动。在调用 destroy() 方法之后，servlet 对象被标记为垃圾回收。 |
>
> **生命周期方法执行顺序**
>
> 1. 构造方法
> 2. init 方法
> 3. service 方法
> 4. destroy 方法
>
> **在servlet的整个生命周期中，构造器和init只会执行一次**
>
> **第二次以后访问该serlvet,只会执行 service方法**
>
> **当tomcat服务器停止的时候，会执行destroy方法**

### ServletResponse常用功能(未完成)

#### 显示

> 

#### 下载(重点)

> Content-Disposition 属性是作为对下载文件的一个标识字段
>
> Content-Disposition属性有两种类型：inline 和 attachment 
>
> inline：将文件内容直接显示在页面 
>
> attachment：弹出对话框让用户下载

#### 刷新

> 

#### 重定向

> sendRedirect(String location)
>
> 状态码 302 重定向

#### 响应

> 

### Servlet的跳转(重点)

#### request跳转

> public interface **RequestDispatcher**
>
> 定义接收来自客户端的请求并将它们发送到服务器上的任何资源（比如 servlet、HTML 文件或 JSP 文件）的对象
>
> **两个方法**
>
> 跳转到html/jsp/servlet
>
> ```java
> forward(request, response);
> ```
>
> 跳转到html/jsp/servlet
>
> ```java
> include(request, response);
> ```
>
> - 区别：forward 不包含跳转之前的资源，include 包含，但通常用 forward
>
> ```java
> out.println("这是Login.java的输出文字...");
> //到主页
> RequestDispatcher rd = request.getRequestDispatcher("main");
> //rd.forward(request,response);
> //如果想看到这是Login.java的输出文字...，需要用到include方法
> rd.include(request,response);
> ```
>

#### response跳转

> **格式**
>
> ```java
> response.sendRedirect("路径");
> ```
>
> - 不可以传递 request 的 setAttribute(String name,Object obj) 的设值

#### 两种跳转的使用场景

> 如果**需要接收**`request.setAttribute(String name,Object value)`，使用
>
> - 要包含的调用`rd.include(request,response)` 
>
> - 不需要包含的调用`rd.forward(request,response)` 
>
>
> 如果**不需要接收**`request.setAttribute(String name,Object value)`，使用
>
> - `response.sendRedirect("路径")`
>
> **为了防止重复提交数据(删除、修改、添加）的问题，使用 response 跳转**

### Cookie(重点)

> **概述**
>
> Cookie是客户端技术，程序把每个用户的数据以cookie 的形式保存到各自浏览器中。当用户使用浏览器再次访问服务器中的web资源的时候,就会带着各自的数据过去。这样, web资源处理的就是用户各自的数据了
>
> 一个 cookie 拥有一个名称、一个值和一些可选属性，比如注释、路径和域限定符、最大生存时间和版本号。一些 Web 浏览器在处理可选属性方面存在  bug，因此有节制地使用这些属性可提高 servlet 的互操作性

#### Cookie的实现原理(未完成)

> 

#### Cookie的分类

> **默认级别的Cookie**
>
> 指的是没有设置有效时间的 Cookie，默认的情况下只要关闭了浏览器，Cookie也会被销毁
>
> Cookie存在于浏览器的内存中，当关闭了浏览器，Cookie就销毁了
>
> **持久级别的Cookie**
>
> 指的是设置了有效时间的 Cookie，这种 Cookie 的内容不是保存在浏览器的内存中，而是将 Cookie 的内容保存(持久化)到硬盘上
>
> 这个时候，关闭浏览器，再次打开浏览器会加载硬盘上的文件，从而 Cookie 中的数据就不会丢失，直到设置的 Cookie 的有效时间到期

#### Cookie的使用(未完成)

> **创建对象**
>
> ```java
> Cookie ck = new Cookie(name,value);
> ```
>
> **添加response对象**
>
> ```java
> response.addCookie(ck);
> ```
>
> **发送回浏览器**
>
> 

#### 获取Cookie(未完成)

> 

### Session(未完成)

> **概述**
>
> Session 是服务器端技术，利用这个技术，服务器在运行时为每一个用户的浏览器创建一个**独享的 session 对象。由于 session 为用户浏览器独享，所有用户在访问服务器的时候，可以把各自的数据放在各自的 session 中，当用户再次访问服务器中的 web 资源的时候，其他 web 资源再从用户各自的 session 中取出数据为用户服务**

#### Session

> 

#### Session的运行原理

> 

## Filter(重点)

> filter 是用来过滤请求使用的，可以在请求到达之前或之后作处理，也是 web 三大组件之一
>
> web 开发人员通过 Filter 技术，对 web 服务器所管理的资源(jsp，servlet，静态图片或静态html文件)进行拦截，从而实现一些特殊的功能
>
> filter 就是过滤从客户端向服务器发送的请求

### Filter的原理

> **当在 web.xml 中注册了一个 Filter 来对某个 Servlet 程序进行拦截处理时，这个Filter 就成了 Tomcat 与该 Servlet 程序的通信线路上的一道关卡，该 Filter 可以对Servlet 容器发送给 Servlet 程序的请求和 Servlet 程序回送给 Servlet 容器的响应进行拦截，可以决定是否将请求继续传递给 Servlet 程序，以及对请求和相应信息是否进行修改**
>
> 在一个 web 应用程序中可以注册多个 Filter 程序，每个 Filter 程序都可以对一个或一组 Servlet 程序进行拦截。
>
> 若有多个 Filter 程序对某个 Servlet 程序的访问过程进行拦截，当针对该 Servlet 的访问请求到达时，web 容器将把这多个 Filter 程序组合成一个 Filter 链(过滤器链)。Filter 链中各个 Filter 的拦截顺序与它们在应用程序的 web.xml 中映射的顺序一致

### Filter的实现方式

> - 写一个类实现Filter接口
>
>   - web.xml
>
>   ```xml
>   <filter>
>       <filter-name>TestFilter</filter-name>
>       <filter-class>com.roxla.filter.TestFilter</filter-class>
>   </filter>
>   
>   <filter-mapping>
>       <filter-name>TestFilter</filter-name>
>       <url-pattern>/*</url-pattern>
>   </filter-mapping>
>   ```
>
>   - java
>
>   ```java
>   public class TestFilter implements Filter {
>       public void destroy() {
>       }
>   
>       public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws ServletException, IOException {
>           System.out.println("**************1*************");
>           req.setCharacterEncoding("utf-8");
>           resp.setContentType("text/html;charset=utf-8");
>           chain.doFilter(req, resp);
>           System.out.println("**************3*************");
>       }
>   
>       public void init(FilterConfig config) throws ServletException {
>   
>       }
>   }
>   ```
>
> - 写注解@WebFilter("/*")
>
>   ```java
>   @WebFilter("/*")
>   public class TestFilter implements Filter {
>       public void destroy() {
>       }
>                    
>       public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws ServletException, IOException {
>           System.out.println("Filter执行了...");
>       }
>                       
>       public void init(FilterConfig config) throws ServletException {
>       }
>   }
> 
> *因为没有实现过滤器的放行，所以过滤器会将所有内容拦截。看到的页面会是一片空白*
> 
>**过滤器的放行**
> 
>使用方法中的参数**chain**
> 
>```java
> @WebFilter("/*")
>public class TestFilter implements Filter {
>     public void destroy() {
>     }
> 
>     public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws ServletException, IOException {
>         System.out.println("Filter执行了...");
>         req.setCharacterEncoding("utf-8");
>         resp.setContentType("text/html;charset=utf-8");
>         chain.doFilter(req, resp);
>         System.out.println("Filter执行结束了...");
>     }
> 
>     public void init(FilterConfig config) throws ServletException {
>     }
> }

### Filter的生命周期

> 1. 在服务器启动时，filter 被创建并初始化，执行 init() 方法。
> 2. 请求通过 filter 时执行 doFilter 方法。
> 3. 服务器停止时，调用 destroy 方法。

### FilterChain对象

> **概述**
>
> FilterChain 过滤器链：在一个 web 应用中，可以开发编写多个 Filter，这些 Filter 组合起来称为是一个过滤器链
>
> Web 服务器根据 Filter 在web.xml 文件中的注册顺序(mapping 的配置顺序)觉得先调用哪个 Filter。一次调用后面的过滤器，如果没有下一个过滤器，调用目标资源

#### FilterChain中Filter的执行顺序

> **浏览器向服务器请求某个资源，在发送请求时会经过复数个 Filter 过滤器，此时经过的 Filter 过滤器的顺序为**
>
> 1. Filter1
> 2. Filter2
> 3. Filter3
> 4. ...FilterN
>
> **当服务器响应请求时，也会经过复数个 Filter 过滤器，此时经过的 Filter 过滤器的顺序为**
>
> 1. FilterN...
> 2. Filter3
> 3. Filter2
> 4. Filter1

### @WebFilter注解

> **属性**
>
> |      属性      |      类型      | 描述                                                         |
> | :------------: | :------------: | ------------------------------------------------------------ |
> |   filterName   |     String     | 指定过滤器的 name 属性，等价于<filter-name>                  |
> |     value      |    String[]    | 该属性等价于 urlPatterns 属性。但是两者不应该同时使用        |
> |  urlPatterns   |    String[]    | 指定一组过滤器的 URL 匹配模式。等价于<url-pattern>           |
> |  servletNames  |    String[]    | 指定过滤器将应用于哪些 Servlet。取值是 @WebServlet中的 name属性的取值，或者是 web.xml 中 <servlet-name>的取值 |
> | dispatcherType | DispatcherType | 指定过滤器的转发模式。具体取值包括：ASYNC、ERROR、FORWARD、INCLUDE、REQUEST |
> |   initParams   | WebInitParam[] | 指定一组过滤器初始化参数，等价于<init-param>                 |
> | asyncSupported |    boolean     | 声明过滤器是否支持异步操作模式，等价于<async-supported>      |
> |  description   |     String     | 该过滤器的描述信息，等价于<description>                      |
> |  displayName   |     String     | 该过滤器的显示名，通常配合工具使用，等价于<display-name>     |
>
> 如果想要**控制filer的执行顺序**可以通过**控制filter的文件名**来控制
>
> 比如：
>
> UserLoginFilter.java 和 ApiLog.java 这两个文件里面分别是“用户登录检查过滤器”和“接口日志过滤器”，因为这两个文件的 首字母A排U之前 ，导致每次执行的时候都是先执行“接口日志过滤器”再执行“用户登录检查过滤器”，所以我们现在修改两个文件的名称分别为
>
> - Filter0_UserLogin.java
>
> - Filter1_ApiLog.java
>
> 这样就能先执行“用户登录检查过滤器”再执行“接口日志过滤器”

### FilterConfig对象

> **概述**
>
> 用来获得 Filter 的相关的配置的对象

### FilterConfig对象的API(未完成)

> |         方法名          | 描述 |
> | :---------------------: | ---- |
> |     getFilterName()     |      |
> |   getInitParameter()    |      |
> | getInitParameterNames() |      |
> |   getServletContext()   |      |

#### getFilterName()

> 

#### getInitParameter()

> 

#### getInitParameterNames()

> 

#### getServletContext()

> 

### 过滤器的相关配置

#### url-pattern

> **url-pattern 是配置 filter 过滤哪些请求的。主要有以下几种配置**
>
> web.xml 中配置的/都是以当前项目路径为根路径的
>
> - 精确匹配
>   - /index.jsp /user/login 会在请求/index.jsp、/user/login 的时候执行过滤方法
> - 路径匹配
>   - /user/* /* 凡是路径为/user/下的所有请求都会被拦截，/*表示拦截系统的所有请求，包括静态资源文件
> - 扩展匹配
>   - *.jsp *.action 凡是后缀名为.jsp .action 的请求都会被拦截
> - 多重 url-pattern 配置
>   - 上面的三种形式比较有局限性，但是 url-pattern 可以配置多个，这样这三种组合基本就能解决所有问题了
>
> *注意：*
>
> - /login/\*.jsp 这种写法是错误的，只能是上述三种的任意一种形式。不能组合新形式
> - *jsp 也是错误的，扩展匹配必须是后缀名

#### servlet-name

> 专门以 servlet 的配置的名称拦截 servlet
>
> 可以使用 url-pattern 来替代

#### dispatcher

> 默认的情况下过滤器会拦截请求。如果进行转发(需要拦截这次转发)。
>
> **dispatcher的取值**
>
> - ASYNC(Servlet3.0新增)
>   - 页面异步处理的时候进行拦截
> - ERROR
>   - 页面出现全局错误页面跳转的时候进行拦截
> - FORWARD
>   - 页面转发的时候进行拦截
> - INCLUDE
>   - 页面包含的时候进行拦截
> - REQUEST(默认值)
>   - 默认过滤器拦截的就是请求
>
> ```xml
> <filter>
>     <filter-name>FilterDemo</filter-name>
>     <filter-class>com.roxla.filter.FilterDemo</filter-class>
> </filter>
> 
> <filter-mapping>
>     <filter-name>FilterDemo</filter-name>
>     <url-pattern>/*</url-pattern>
>     <dispatcher>REQUEST</dispatcher>
>     <dispatcher>FORWARD</dispatcher>
> </filter-mapping>
> ```

### 权限验证过滤

> **需求**
>
> 现在一个网站上需妻有登录的功能，在登录成功后,重定向到后台的成功页面《后台的页面有很多)。如果现在没有登录直接在地址栏上输入后台页面地址。
>
> 编写一个过滤器：可以对没有登录的用户进行拦截。(没有登录，回到登录页面。如果已经登录，放行)
>
> **使用过滤器进行访问权限验证**
>
> ```java
> @WebFilter("*.action")
> public class RoleFilter implements Filter {
>        public void destroy() {
>        }
> 
>        public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws ServletException, IOException {
>            //强转
>            HttpServletRequest request = (HttpServletRequest)req;
>            HttpServletResponse response = (HttpServletResponse)resp;
>            //获取请求
>            String servletPath = request.getServletPath();
>            //判断
>            if(servletPath.equals("/login.action")){
>                chain.doFilter(req,resp);//放行
>            }else{
>                //获取session
>                HttpSession session = request.getSession();
>                //从session中取用户信息
>                User user = (User) session.getAttribute("user");
>                //判断用户是否为空
>                if(user != null){
>                    //放行
>                    chain.doFilter(req,resp);
>                }else{
>                    response.setContentType("text/html;charset=utf-8");
>                    //提示
>                    response.getWriter().println("请登录后再操作...");
>                    //刷新
>                    response.setHeader("refresh","3;url=index.jsp");
>                    response.getWriter().println("<a href='index.jsp'>登录</a>");
>                }
>            }
> 
>        }
> 
>        public void init(FilterConfig config) throws ServletException {
>     }
>    }
> ```

## 监听器

> **概述**
>
> 监听器就是一个实现类特定接口的 Java 类，这个 Java 类用于监听另一个 Java类的方法调用或者属性的改变。当被监听对象发生上述事件后，监听器某个方法将会立即被执行
>
> **用途**
>
> 用来监听其他对象的变化的。主要应用于图形化界面开发上。
>
> - Java 中 GUI，Android
>
> **术语**
>
> - 事件源：指的是被监听对象(气车)
> - 监听器：指的是监听的对象(报警器)
> - 事件源和监听器绑定：在汽车上安装报警器
> - 事件：指的是事件源对象的改变(踹了气车一脚)
>   - 主要功能：获得事件源对象
>
> **Servlet中的监听器**
>
> 在 Servlet 中定义了多种类型的监听器，它们用于监听的事件源分别是**ServletContext**、**HttpSession**和**ServletRequest**这三个域对象
>
> **Servlet中的监听器的分类**
>
> - 监听三个域对象的创建和销毁的监听器(三个)
> - 监听桑域对象的属性变更(属性添加、溢出、替换)的监听器(三个)
> - 监听 HttpSession 中 JavaBean 的状态改变(钝化、活化、绑定、解除绑定)的监听(两个)

### 监听器的实现方式

> 1. 写一个类实现监听器的接口
>
>    ```java
>    public class ListenerDemo implements HttpSessionListener{
>    }
>    ```
>
> 2. 配置XML或者注解
>
>    - XML配置
>
>      ```xml
>      <web-app>
>      	...
>          <listener>
>              <listener-class>com.roxla.listener.ListenerDemo</listener-class>
>          </listener>
>      </web-app>
>      ```
>
>    - 注解配置
>
>      ```java
>      @WebListener
>      public class ListenerDemo implements HttpSessionListener{
>      }
>      ```
>
> 3. 重写监听器的方法
>
>    ```java
>    @WebListener
>    public class ListenerDemo implements HttpSessionListener{
>        public void sessionCreated(HttpSessionEvent se) {
>        }
>        public void sessionDestroyed(HttpSessionEvent se) {
>        }
>    }
>    ```
>
> 

#### HttpSessionListener(未完成)

> 
>
> *session监听器*
>
> ```java
>@WebListener
> public class ListenerDemo implements HttpSessionListener{
>        // 当session对象被创建的时候，就会通知此监听器
>        public void sessionCreated(HttpSessionEvent se) {
>            
>        }
>        // 当session对象被销毁的时候，就会通知此监听器
>        public void sessionDestroyed(HttpSessionEvent se) {
>            
>        }
>    }
>    ```
> 
> 

#### HttpSessionAttributeListener(未完成)

> 
>
> ```java
> @WebListener
> public class ListenerDemo implements HttpSessionAttributeListener{
>         // 
>         public void attributeAdded(HttpSessionBindingEvent sbe) {
>           /* This method is called when an attribute 
>              is added to a session.
>           */
>         }
>         // 
>         public void attributeRemoved(HttpSessionBindingEvent sbe) {
>           /* This method is called when an attribute
>              is removed from a session.
>           */
>         }
>         // 
>         public void attributeReplaced(HttpSessionBindingEvent sbe) {
>           /* This method is invoked when an attribute
>              is replaced in a session.
>           */
>         }
> }
> ```
>
> 

#### ServletContextListener

> **用来监听 ServletContext 域对象的创建和销毁**
>
> - 创建：在服务器启动的时候，为每个 web 应用创建单独的 ServletContext 对象
> - 销毁：在服务器关闭的时候，或者项目从 web 服务器中移除的时候
>
> ```java
> @WebListener
> public class ListenerDemo implements ServletContextListener {
>     // 监听 ServletContext 对象的创建
>     public void contextInitialized(ServletContextEvent sce) {
>         System.out.println("ServletContext对象被创建了...");
>     }
> 	// 监听 ServletContext 对象的销毁
>     public void contextDestroyed(ServletContextEvent sce) { 
>         System.out.println("ServletContext对象被销毁了...");
>     }
> }
> ```
>
> **用途**
>
> - 加载框架的配置文件
>   - Spring 框架提供了一个核心监听器 ContextLoaderListener
> - 定时任务调度

## 文件上传下载

### 文件上传

> **概述**
>
> 将本地的文件通过流写入到服务器的过程
>
> **技术**
>
> - JSPSmartUpload：应用在 JSP 上的文件上传和下载的组件
> - FileUpload：应用在 Java 环境上的文件上传的功能
> - Servlet3.0：提供文件上传的功能
> - struts2：提供文件上传的功能
>
> **要素**
>
> - 表单的提交方式需要是 POST
> - 表单中需要有`<input type="file">`元素，需要有 name 属性和值
> - 表达 enctype="multipart/form-data"
>
> *注意：java EE 6 不支持文件的上传，需要使用 java EE 8 来创建项目*

#### 实现代码

> **使用监听器来判断文件夹是否创建**
>
> ```java
> @WebListener
> public class ContextpathListener implements ServletContextListener {
>        public void contextInitialized(ServletContextEvent sce) {
>            ServletContext context = sce.getServletContext();
>            // idea里面的tomcat路径下 E:\work_idea\out\artifacts\upload_war_exploded
>            String realPath = context.getRealPath("/upload");
>            // 文件实例
>            File file = new File(realPath);
>            // 判断是否存在 upload 这个文件夹
>            if (!file.exists()){
>                // 如果不存在则创建
>                file.mkdir();
>            }else {
>                System.out.println("已创建好保存路径...");
>            }
>        }
> 
>        public void contextDestroyed(ServletContextEvent sce) {
>        }
> }
> ```
>
> **文件上传实现代码**
>
> ```java
> @javax.servlet.annotation.WebServlet("/upload")
> @MultipartConfig //这个注解用来支持文件上传
> public class Upload extends javax.servlet.http.HttpServlet {
>        @Override
>        protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
>            // 接收上传的文件
>            Part part = req.getPart("file");
>            // 文件类型
>            System.out.println("name: " + part.getName());
>            // 文件大小
>            System.out.println("size: " + part.getSize());
>            // 提交的文件名
>            System.out.println("提交的文件名: " + part.getSubmittedFileName());
>            // 当前系统的盘符  win：\，linux：/
>            System.out.println("当前系统盘符: " + File.separator);
>            // 文件名
>            String fileName = part.getSubmittedFileName();
>            // 找地方把文件保存一下
>            ServletContext context = req.getServletContext();
>            String realPath = context.getRealPath("/upload");
>         // 打印保存路径
>            System.out.println("保存路径: " + realPath);
>            // 保存 调用write 保存文件的路径 = realpath+盘符+提交的文件名
>            part.write(realPath + File.separator + fileName);
>        }
> }
> ```
>
> **jsp页面代码**
>
> ```jsp
> <%@ page contentType="text/html;charset=UTF-8" language="java" %>
> <html>
>     <head>
>            <title>$Title$</title>
>     </head>
>     <body>
>            <form method="post" action="upload" enctype="multipart/form-data">
>                <input type="file" name="file"><br/>
>                <input type="submit" value="上传">
>            </form>
>     </body>
> </html>
> ```

### 文件下载

> **概述**
>
> 将服务器上的一个文件，通过流写入到客户端上
>
> **方式**
>
> - 使用超链接的方式实现文件的下载
>   - 在`<a href="文件的路径">超链接</a>`
>   - *注意：超链接的方式，如果浏览器不能识别这种格式的文件，提示下载；如果支持该格式的文件，直接打开*
> - 通过手动编写代码的方式实现文件的下载
>   - 设置两个头和一个流
>     - Content-Type：文件的 MIME 的类型
>     - Content-Disposition：乱起支持该格式的文件，提示下载
>     - 设置代表该文件的输入流（输出流是固定 response.getOutputStream()）
>
> *可以在上面文件上传模块的基础上添加文件下载模块，模块的文件结构为*
>
> - com.roxla.listener
>   - ContextpathListener
> - com.roxla.servlet
>   - Upload
>   - ViewFileList
>   - Download
> - web
>   - index.jsp
>
> *注意：java EE 6 不支持文件的下载，需要使用 java EE 8 来创建项目*

#### 实现代码

> **使用监听器来判断文件夹是否创建**
>
> ```java
> @WebListener
> public class ContextpathListener implements ServletContextListener {
>         public void contextInitialized(ServletContextEvent sce) {
>             ServletContext context = sce.getServletContext();
>             // idea里面的tomcat路径下 E:\work_idea\out\artifacts\upload_war_exploded
>             String realPath = context.getRealPath("/upload");
>             // 文件实例
>             File file = new File(realPath);
>             // 判断是否存在 upload 这个文件夹
>             if (!file.exists()){
>                 // 如果不存在则创建
>                 file.mkdir();
>             }else {
>                 System.out.println("已创建好保存路径...");
>             }
>         }
> 
>         public void contextDestroyed(ServletContextEvent sce) {
>         }
> }
> ```
>
> **页面显示所有上传的文件**
>
> ```java
> @WebServlet("/filelist")
> public class ViewFileList extends HttpServlet {
>        @Override
>        protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
>            // 设置响应类型和编码
>            resp.setContentType("text/html;charset=utf-8");
>            // 输出流
>            PrintWriter out = resp.getWriter();
>            // 获取保存路径
>            ServletContext context = req.getServletContext();
>            String realPath = context.getRealPath("/upload");
>            // file实例
>            File file = new File(realPath);
>            // 调用listFiles返回文件数组
>            File[] files = file.listFiles();
>            out.println("***文件列表***<br/>");
>            // 循环
>            for (File f : files) {
>                out.println("<a href='download?filename=" + f.getName() + "'>" + file.getName() + "</a><br>");
>            }
>        }
> }
> ```
>
> **文件下载实现代码**
>
> ```java
> @WebServlet("/download")
> public class Download extends HttpServlet {
>        @Override
>        protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
>            /*
>           1设置响应头
>           2 读取图片资源
>           3 读写（循环） try...with...resources:把IO流对象放入try(小括号）里面，这个流对象是自动关闭，离开"}"括号以后就自动关闭，是实现了AutoCloseAble接口的类才有效
>             好处是不再需要手动写finally关闭（极容易忘记写关闭）
>          */
>            resp.setCharacterEncoding("utf-8");
>            resp.setContentType("text/html;charset=UTF-8");
>            // 获取文件名
>            String filename = req.getParameter("filename");
>            System.out.println("filename: " + filename);
>            try {
>                /*
>               content-disposition:内容保存路径
>               attachment:附件，告诉浏览这个附件
>               filename=w.jpg 下载文件的名字
>              */
>                resp.setHeader("content-disposition", "attachment;filename=" + changeCharset(req, filename));
>            } catch (Exception e) {
>                e.printStackTrace();
>            }
>            // 获取文件真实路径
>            String realPath = req.getServletContext().getRealPath("/upload");
>            // 字节流下载文件
>            try (InputStream is = new FileInputStream(realPath + File.separator + filename);
>                 ServletOutputStream out = resp.getOutputStream()) {
>                int len = 0;
>                byte[] bytes = new byte[1024];
>                while ((len = is.read(bytes)) > 0) {
>                    out.write(bytes, 0, len);
>                }
>                System.out.println("写出文件成功...");
>            } catch (IOException e) {
>                e.printStackTrace();
>            }
>        }
> }
> ```
>
> **编写静态方法处理中文文件名乱码**
>
> ```java
> // 文件名处理
> static String changeCharset(HttpServletRequest request, String filename) throws Exception {
>        // 客户端的浏览器
>        String bwname = null;
>        String client = request.getHeader("User-agent");
>        // 判断
>        if (client != null && client.indexOf("MSIE") > 0) {
>            System.out.println("微软浏览器IE");
>            bwname = URLEncoder.encode(filename, "UTF-8");
>        } else {
>            bwname = new String(filename.getBytes("UTF-8"), "iso-8859-1");
>        }
>        return bwname;
> }
> ```
>
> **jsp页面代码**
>
> ```jsp
> <%@ page contentType="text/html;charset=UTF-8" language="java" %>
> <html>
>     <head>
>            <title>$Title$</title>
>     </head>
>     <body>
>            <form method="post" action="upload" enctype="multipart/form-data">
>                <input type="file" name="file"><br/>
>                <input type="submit" value="上传">
>            </form>
>            <a href="filelist">下载文件列表</a>
>     </body>
> </html>
> ```

## JSP

> **概述**
>
> JSP：Java Server Pages(Java 服务器端页面)
>
> JSP 就是 HTML + Java 代码+ JSP 自身的东西
>
> **由来**
>
> servlet 技术生成动态网页的时候很麻烦，需要通过 response 获得输出流，调用 print 方法进行打印的。这种编程方式很麻烦，而且美工也不容易处理。SUN 公司为了简化动态网页开发，推出 JSP。
>
> **运行原理**
>
> JSP 在执行时，会被服务器翻译为 Servlet 编译执行，JSP就是一个 Servlet

### JSP脚本元素

> **<%! %>** 
>
> - jsp声明 翻译成 Servlet 成员部分的内容
> - 声明方法，成员变量，内部类
>
> ```jsp
> <%!
>     String name = "jack";
>     public String sayHello(){
>         return "hello," + name;
>     }
>     class Inner{
>     }
> %>
> ```
>
> **<% %>**
>
> - 嵌入 Java 代码，翻译成 servlet 方法内部的代码块
> - 声明局部变量，局部内部类
>
> ```jsp
> <%
> 	String color = "yellow";
> %>
> ```
>
> **<%=%>**
>
> - 翻译 out.println()，在 Servlet 方法内部
>
>
> - 用于生成 HTML页面源码
>
> ```jsp
> name:<%=name%><br/>
> 调用方法:<%=sayHello()%>
> ```

### JSP里面的循环

> 将 servlet 中的循环输出的操作反向实现
>
> **servlet循环实现99乘法表**
>
> ```java
> @WebServlet("/for")
> public class For extends HttpServlet {
>     @Override
>     protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
>         PrintWriter out = resp.getWriter();
>         out.println("<table border='1'>");
>         for (int i = 0; i < 10; i++) {
>             out.println("<tr>");
>             for (int j = 1; j <= i; j++) {
>                 out.println("<td>" + i + "*" + j + "=" + i * j + "</td>");
>             }
>             out.println("</tr>");
>         }
>     }
> }
> ```
>
> **JSP循环实现99乘法表**
>
> ```jsp
> <%--  99乘法表  --%>
> <table border="1">
> <%
>   for (int i = 0; i < 10; i++) {
> %>
> <tr>
>   <%
>       for (int j = 1; j <= i; j++) {
>   %>
>   <td><%=i%>*<%=j%>=<%=i * j%>
>   </td>
>   <%
>       }%>
> </tr>
> <%
>   }%>
> </table>
> ```
>

### JSP的注释

> **HTML注释**
>
> *写法*
>
> ```html
> <!--HTML的注释-->
> ```
>
> **Java代码注释**
>
> *写法*
>
> ```jsp
> <% 
> 	// 单行注释 
> 	/* 多行注释 */
> 	/** 文档注释 */
> %>
> ```
>
> **JSP注释**
>
> *写法*
>
> ```jsp
> <%-- JSP的注释 --%>
> ```

### JSP指令元素

> **作用**
>
> - 用于指示 JSP 执行的某些步骤
> - 用于指示 JSP 表现的特定行为
>
> **语法**
>
> ```jsp
> <%@ 指令名称 属性名称=属性的值 属性名称=属性的值%>
> ```
>
> **分类(三大指令)**
>
> - page指令
> - include包含指令
> - taglib指令

#### page指令

> page 指令可以定义 JSP 页面设置的属性和行为
>
> **格式**
>
> ```jsp
> <%@ page contentType="text/html;charset=UTF-8" language="java" %>
> ```
>
> - contentType="text/html;charset=UTF-8"   类型为text/html,编码为utf-8
>
> - language="java"   语言为java
>
> - session="true"   当前页面支持Sesssion的创建
>
> - import="java.util.*"   导入 java.util 包下面所有的类
>
>   ```jsp
>   <%-- 导入 User 类和 java.util 包下面所有的类--%>
>   <%@ page import="com.gec.bean.User,java.util.*"%>
>   ```
>
> - isErrorPage="true"   将当前页面设置为错误处理页面（包括显示错误信息等）
>
> - isELIgnored=""   不要设为true,如果true,EL将不能正确获取值，设值等操作
>
> - errorPage=""   如果当前页面出错了，将跳转到指定错误页面

#### include包含指令

> include 指令用于在 JSP页面中静态白喊一个文件，同时由该 JSP 解析包含的文件内容
>
> 这个所包含的jsp不能重复定义的变量，如果重复了会报错。
>
> *原因：被包含的页面会一起到使用包含指令的 _jspservice 方法里面进行编译，导致变量重复定义！java 语法错误*
>
> **格式**
>
> ```jsp
> <%@ include file="top.jsp"%><br/><br/>
> <%@ include file="bottom.jsp"%>
> ```
>
> - file="top.jsp"   导入 top.jsp 页面

#### taglib(导入标签库)指令

> taglib 指令用于在 JSP 页面中引入标签库
>
> **格式**
>
> ```jsp
> <%@ taglib 属性名=属性值%>
> ```
>
> **属性**
>
> - url：引入的标签库的路径
> - prefix：引入标签库的前缀

### 六个常用动作

#### userBean

> 该动作用于创建对象
>
> **代码格式**
>
> ```jsp
> <jsp:userBean id="u" class="com.roxla.bean.User" />
> ```
>
> - id：设置实例对象的别名
> - class：实例对象的类
>
> *上面这行代码相当于 User u = new User();*

#### setProperty

> 该动作用于给对象设值
>
> **代码格式**
>
> ```jsp
> <jsp:setProperty name="u" property="id" value=1 />
> ```
>
> - name：实例对象的别名
> - property：调用 u.setId() 方法
> - value：给 id 赋值为1
>
> **userBean 和 setProperty 的组合相当于实现如下的 Java 代码**
>
> *JSP代码*
>
> ```jsp
> <jsp:userBean id="u" class="com.roxla.bean.User" />
> <jsp:setProperty name="u" property="id" value=1 />
> ```
>
> *Java代码*
>
> ```java
> User u = new User();
> u.setId(1);
> ```
>

#### getProperty

> 该动作用于获取对象的值
>
> **代码格式**
>
> ```jsp
> <jsp:getProperty name="u" property="id" />
> ```
>
> - name：实例对象的别名
> - property：调用 u.getId() 方法
>
> **setProperty 相当于实现如下的 Java 代码**
>
> ```java
> u.getId(1);
> ```
>

#### forward

> 该动作用于请求转发
>
> **代码格式**
>
> ```jsp
> <jsp:forward page="login.jsp"></jsp:forward>
> ```
>
> *forward 动作默认传参当前页面的 request 对象*

#### param

> 该动作用于传递参数
>
> *该动作只能写在`<jsp:forward>`标签内*
>
> **代码格式**
>
> ```jsp
> <jsp:forward page="login.jsp">
> 	<jsp:param name="name" value="jack" />
>  <jsp:param name="password" value="123" />
> </jsp:forward>
> ```
>
> **在 login.jsp 页面获取传递过来的参数**
>
> *login.jsp*
>
> ```jsp
> <%=request.getParameter("name")%>
> <%=request.getParameter("password")%>
> ```
>

#### include

> 该动作用于包含其它页面（动态包含），引入进来
>
> **代码格式**
>
> ```jsp
> <jsp:include page="top.jsp" />
> ```
>
> **jsp:include 和 <%@ include %> 有何区别？**
>
> jsp:include在访问之前，被包含的页面已预先编译，所以同名的变量不会冲突

### 九大内置对象

> - pageContext：当前页面
> - session：session对象
> - request：request对象
> - application：应用上下文
> - config：配置ServletConfig
> - out：printWriter 打印对象
> - page：当前实例
> - response：响应对象
> - exception：异常对象

### 四大作用域(面试题)

> - pageContext：当前页面
> - request：request对象
> - Session：session对象
> - application：应用上下文
>
> **寻值顺序**
>
> 先从pageContext找，找不到再到request找，request还找不到，去Session找，session还找不到，到application
>
> **pageContext-->request-->session-->application**

## JSTL

> **概述**
>
> 在 JSP 页面中，使用标签库代替传统的 Java 片段语言来实现页面的显示逻辑已经不是新技术了，然而，由自定义标签很容易造成重复定义和非标准的实现。鉴于此，出现了 JSTL (JSP Standard Tag Library)。大多数 JSP 页面逻辑提供了实现的 JSTL 技术，该技术本身就是一个标签库。
>
> **要使用 JSTL，需要引入 JSTL 的 jar 包**
>
> - javax.servlet.jsp.jstl-1.2.1.jar
> - javax.servlet.jsp.jstl-api-1.2.1.jar

### EL表达式

> **概述**
>
> JSTL 标签库由标签库和 EL 表达式语言两个部分组成。EL 在 JSTL 1.0 规范中被引入，当时用来作为 Java 表达式来工作，而该表达式必须配合 JSTL 的标签库才能得到需要的结果。
>
> EL 是从 JavaScript 脚本语言得到启发的一种表达式语言，它借鉴了 JavaScript 多类型转换无关性的特点。在使用 EL 从 scope 中得到参数时可以自动转换类型，因此对于类型的限制更加宽松。Web 服务器对于 request 请求参数通常会以 String 类型来发送，在得到时使用的 Java 语言脚本就应该是 request.getParameter("XXX")，这样的话，对于实际应用还必须进行强制类型转换。而 EL 就将用户从这种类型转换的繁琐工作脱离出来，允许用户直接使用 EL 表达式取得的值，而不用关心它是什么类型。
>
> **格式**
>
> EL 表达式必须以 **${XXX}** 来表示，其中 "XXX" 部分就是具体表达式内容，"${}" 将这个表达式内容包含在其中作为 EL 表达式的定义

#### 默认变量

> 一个 EL 表达式包含变量和操作符两个内容。任何存在于 JSP作用范围的 JavaBean 都可以被转化成 EL 表达式来使用，它所包含的默认变量如下：
>
> - pageScope
> - requestScope
> - sessionScope
> - applicationScope
> - param
> - paramValues
> - header
> - headerValues
> - cookie
> - initParam
> - pageContext
>
> 这 11 个默认变量几乎包含了 Web 应用的所有基本操作，**若一个表达式不使用这些变量而直接使用参数名，那么就采用就近原则。该表达式将使用最近取得的参数值**

##### pageScope、requestScope、sessionScope、applicationScope

> 这四个默认变量包含 Scope 作用范围的参数集合，相当于被保存在 java.util.Map 中的某个参数。

###### pageScope

> **格式**
> 
> ```jsp
> <% pageContext.setAttribute("pageContext", new Integer(1)); %>
> ${pageScope.pageContext}
> ```
>
> 取得保存在 pageContext 中参数的 pageScope 变量的 EL 表达式，"." 是 property 访问操作符，在这里表示从 pageContext 中取得 key 为 "pageContext" 的参数，并显示出来。显示结果为 "1"
>
> *${pageScope.pageContext} 的 pageScope 可以省略，jsp 会根据四大作用域的寻值顺序来寻找 key 为 "pageContext" 的参数*

###### requestScope

> **格式**
> 
> ```jsp
> <% request.setAttribute("request", new Integer(10)); %>
> ${requestScope.request}
> ```
>
> 取得保存在 request 中参数的 requestScope 变量的 EL 表达式，"." 是 property 访问操作符，在这里表示从 request 中取得 key 为 "request" 的参数，并显示出来。显示结果为 "10"
>
> *${requestScope.request} 的 requestScope 可以省略，jsp 会根据四大作用域的寻值顺序来寻找 key 为 "request" 的参数*

###### sessionScope

> **格式**
> 
> ```jsp
> <%session.setAttribute("session", new Integer(100));%>
> ${sessionScope.session}
> ```
>
> 取得保存在 session 中参数的 sessionScope 变量的 EL 表达式，"." 是 property 访问操作符，在这里表示从 Session 中取得 key 为 "session" 的参数，并显示出来。显示结果为 "100"
>
> *${sessionScope.session} 的 sessionScope 可以省略，jsp 会根据四大作用域的寻值顺序来寻找 key 为 "session" 的参数*

###### applicationScope

> **格式**
> 
> ```jsp
> <% application.setAttribute("application", "application范围"); %>
> ${applicationScope.application}
> ```
>
> 取得保存在 application 中参数的 applicationScope 变量的 EL 表达式，"." 是 property 访问操作符，在这里表示从 application 中取得 key 为 "application" 的参数，并显示出来。显示结果为 "application范围"
>
> *${applicationScope.application} 的 applicationScope 可以省略，jsp 会根据四大作用域的寻值顺序来寻找 key 为 "application" 的参数*

##### param、paramValues

> 这两个默认变量包含请求参数的集合，**param 表明请求包含的参数为单一控件，paramValues 表明请求包含的参数为控件数组**

###### param

> param 对象用于获取请求参数的某个值，它是 Map 类型，与 request.getParamter() 方法相同，在使用 EL 获取参数时，如果参数不存在，返回的是空字符串，而不是 null
>
> **格式**
>
> ```jsp
> <form action="${pageContext.request.contextPath}/param.jsp">
> 	num: <input type="text" name="num1" /><br />
>     <input type="submit" value="提交" />
>     <hr>
>     num: ${param.num1}
> </form>
> ```

###### paramValues

> 如果一个请求参数有多个值，可以使用paramValues对象来获取请求参数的所有值，该对象用于返回请求参数所有值组成的数组
>
> 如果要获取某个请求参数的第一个值，则用 **${paramValues.num[0]}**
>
> **格式**
>
> ```jsp
> <form action="${pageContext.request.contextPath}/param.jsp">
> 	num1: <input type="text" name="num" /><br />
>     num2: <input type="text" name="num" /><br />
>     <input type="submit" value="提交" />
>     <hr>
>     num1: ${paramValues.num[0]}<br />
>     num2: ${paramValues.num[1]}<br />
> </form>
> ```

##### header、headerValues

> 这两个默认变量包含请求参数头部信息的集合，header 变量表示单一头部信息，headerValues 则表示数组型的头部信息。

##### cookie

> 包含所有请求的 cookie 集合，集合中的每个对象对应 javax.servlet.http.Cookie

##### initParam

> 包含所有应用程序初始化参数的集合

##### pageContext

> 等价于 page 环境类 javax.servlet.jsp.PageContext 的实例，用来提供访问不同的请求参数

#### 操作符

> **EL 表达式中有许多操作符可以帮助完成各种所需的操作**
>
> |   操作符   | 描述                                                         |
> | :--------: | :----------------------------------------------------------- |
> |     .      | 访问一个Bean属性或者一个映射条目                             |
> |     []     | 访问一个数组或者链表的元素                                   |
> |    ( )     | 组织一个子表达式以改变优先级                                 |
> |     +      | 加                                                           |
> |     -      | 减或负                                                       |
> |     *      | 乘                                                           |
> |  / or div  | 除                                                           |
> |  % or mod  | 取模                                                         |
> |  == or eq  | 测试是否相等                                                 |
> |  != or ne  | 测试是否不等                                                 |
> |  < or lt   | 测试是否小于                                                 |
> |  > or gt   | 测试是否大于                                                 |
> |  <= or le  | 测试是否小于等于                                             |
> |  >= or ge  | 测试是否大于等于                                             |
> | && or and  | 测试逻辑与                                                   |
> | \|\| or or | 测试逻辑或                                                   |
> |  ! or not  | 测试取反                                                     |
> |   empty    | 测试是否空值                                                 |
> | func(args) | 调用方法，func是方法名，args是参数，可以没有，或者有一个、多个参数。参数间用逗号隔开 |
>
> **算术表达式示例**
>
> ```jsp
> 1+1:$(1+1)<br/>
> 2-1:$(2-1)<br/>
> 3*3:$(3*3)<br/>
> 10/2:$(10/2)<br/>
> 10%3:$(10%3)<br/>
> ```

### JSTL标签库

> **JSTL 的标签库总共分成五类**
>
> - Core 标签库
>
> - XML processing 标签库
>
> - I18N formatting标签库
>
> - Database access 标签库
>
> - Functions 标签库
>
> **在使用 JSTL 的标签库时，需要使用 taglib 指令进行导入标签库**
>
> ```jsp
> <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
> ```
>
> **标签库的标识符**
>
> | 标签库          | URL                                    | 前缀 |
> | --------------- | -------------------------------------- | ---- |
> | Core            | http://java.sun.com/jsp/jstl/core      | c    |
> | XML processing  | http://java.sun.com/jsp/jstl/xml       | x    |
> | I18N formatting | http://java.sun.com/jsp/jstl/fmt       | fmt  |
> | Database access | http://java.sun.com/jsp/jstl/sql       | sql  |
> | Functions       | http://java.sun.com/jsp/jstl/functions | fn   |

#### Core 标签库

> Core 标签库，又被称为核心标签库，该标签库的工作是对于 JSP 页面一般处理的封装。在该标签库中的标签一共有 14 个，被分为了四类，分别是： 
>
> - 多用途核心标签：`<c:out>`、`<c:set>`、`<c:remove>`、`<c:catch>`
> - 条件控制标签：`<c:if>`、`<c:choose>`、`<c:when>`、`<c:otherwise>`
> - 循环控制标签：`<c:forEach>`、`<c:forToken>`
> - URL相关标签：`<c:import>`、`<c:url>`、`<c:redirect>`、`<c:param>`

##### 多用途标签

###### \<c:out>

> `<c:out>`标签是一个最常用的标签，用于在 JSP 中显示数据
>
> **\<c:out>标签属性和说明**
>
> |   属性    | 描述                                                         |
> | :-------: | ------------------------------------------------------------ |
> |   value   | 输出到页面的数据，可以是 EL 表达式或常量（必须）             |
> |  default  | 当 value 为 null 时显示的数据（可选）                        |
> | escapeXml | 当设置为 true 时会主动更换特殊字符，比如"\&lt;，\&gt;，\&amp;"(可选，默认为true) |
>
> **示例代码**
>
> ```jsp
> <c:out value="123" />
> <c:out value="${value}" default="默认值" />
> ```

###### \<c:set>

> `<c:set>`标签用于为变量或 JavaBean 中的变量属性赋值
>
> *`<c:set>`标签等价于 pageContext.setAttribute(String, Object)*
>
> **\<c:set>标签属性和说明**
>
> |   属性   | 描述                                                         |
> | :------: | ------------------------------------------------------------ |
> |  value   | 值的信息，可以是 EL 表达式或常量                             |
> |  target  | 被赋值的 JavaBean 实例的名称，若存在该属性则必须存在 property 属性（可选） |
> | property | JavaBean 实例的变量属性名称（可选）                          |
> |   var    | 被赋值的变量名（可选）                                       |
> |  scope   | 变量的作用范围，若没有指定，默认为 page（可选）              |
>
> **示例代码**
>
> ```jsp
> <c:set var="value" value="你好，这是c:set设置值"
> ```

###### \<c:remove>

> `<c:remove>`标签用于删除存在于 scope 中的变量
>
> *`<c:remove>`标签等价于 pageContext.removeAttribute(String)*
>
> **\<c:remove>标签属性和说明**
>
> | 属性  | 描述                                               |
> | :---: | -------------------------------------------------- |
> |  var  | 需要被删除的变量名                                 |
> | scope | 变量的作用范围，若没有指定，默认为全部查找（可选） |
>
> **示例代码**
>
> ```jsp
> <c:remove var="value"/>
> ```

###### \<c:catch>(未完成)

> `<c:catch>`标签允许在 JSP 页面中捕捉异常。
>
> 它包含一个 var 属性，是一个描述异常的变量，该变量可选。
>
> 若没有 var 属性的定义，那么仅仅捕捉异常而不做任何事情，若定义了 var 属性，则可以利用 var 所定义的异常变量进行判断转发到其他页面或提示报错信息。
>
> **示例代码**
>
> *index.jsp*
>
> ```jsp
> 
> ```
>
> *error.jsp*
>
> ```jsp
> ```
>
> 

##### 条件控制标签

###### \<c:if>

> `<c:if>`标签用于简单的条件语句
>
> **\<c:if>标签属性和说明**
>
> | 属性  | 描述                                                         |
> | :---: | ------------------------------------------------------------ |
> | test  | 需要判断的条件                                               |
> |  var  | 保存判断结果 true 或 false 的变量名，该变量可供之后的工作使用（可选） |
> | scope | 变量的作用范围，若没有指定，默认为保存于 page 范围中的变量（可选） |
>
> **示例代码**
>
> ```jsp
> <c:set var="age" value="21"/>
> <c:if test="${age == 20}" var="result">
>     年龄20了...
> </c:if>
> 满20没? ${result}
> ```
>

###### \<c:choose>

> `<c:choose>`标签没有属性，可以被认为是父标签

###### \<c:when>

> `<c:when>`标签作为`<c:choose>`标签的子标签使用
>
> `<c:when>`标签等价于 "if" 语句，包含一个 test 属性，该属性表示需要判断的条件
>
> **示例代码**
>
> ```jsp
> <c:choose>
> 	<c:when test="${age <20}">好好上学</c:when>
> </c:choose>
> ```
>

###### \<c:otherwise>

> `<c:otherwise>`标签作为`<c:choose>`标签的子标签使用
>
> `<c:otherwise>`标签没有属性，它等价于 "else" 语句
>
> **示例代码**
>
> ```jsp
> <c:choose>
> 	<c:when test="${age >= 20 && age <=65}">准备好振兴中华没有？有</c:when>
>     <c:otherwise>好好退休！感谢</c:otherwise>
> </c:choose>
> ```
>

##### 循环控制标签

###### \<c:forEach>

> `<c:forEach>`为循环控制标签
>
> **\<c:forEach>标签属性和说明**
>
> |   属性    | 描述                                                         |
> | :-------: | ------------------------------------------------------------ |
> |   items   | 进行循环的集合（可选）                                       |
> |   begin   | 开始条件（可选）                                             |
> |    end    | 结束条件（可选）                                             |
> |   step    | 循环的步长，默认为1（可选）                                  |
> |    var    | 做循环的对象变量名，若存在 items 属性，则表示循环集合中对象的变量名（可选） |
> | varStatus | 显示循环状态的变量（可选）                                   |
>
> **示例代码**
>
> *循环作用域中的集合*
>
> ```jsp
> <%
> 	List<String> list = new ArrayList<>();
> 	list.add("aa");
> 	list.add("阿强");
> 	list.add("阿东");
> 	list.add("阿猫");
> 	// 把集合存储到作用域
> 	request.setAttribute("list", list);
> %>
> <!--循环作用域中的集合-->
> <c:forEach items="${list}" var="string">
>     ${string}<br/>
> </c:forEach>
> ```
>
> *循环数字*
>
> ```jsp
> <!--循环数字 1~10-->
> <c:forEach begin="1" end="10" step="2" var="num">
>     ${num}<br/>
> </c:forEach>
> ```
>
> *循环 map集合*
>
> ```jsp
> <%
> 	Map<String, String> map = new HashMap<>();
> 	map.put("a", "a_val");
> 	map.put("a", "b_val");
> 	map.put("a", "c_val");
> 	// 存储
> 	request.setAttribute("map", map);
> %>
> <c:forEach items="${map}" var="m">
> 	${m.key} -- ${m.value}<br/>
> </c:forEach>
> ```

###### \<c:forToken>

> `<c:forToken>`标签可以根据某个分隔符分割指定字符串，相当于 java.util.StringTokenizer 类
>
> **\<c:forToken>标签属性和说明**
>
> |   属性    | 描述                                                         |
> | :-------: | ------------------------------------------------------------ |
> |   items   | 进行分隔的 EL 表达式或常量                                   |
> |  delims   | 分隔符                                                       |
> |   begin   | 开始条件（可选）                                             |
> |    end    | 结束条件（可选）                                             |
> |   step    | 循环的步长，默认为1（可选）                                  |
> |    var    | 做循环的对象变量名，若存在 items 属性，则表示循环集合中对象的变量名（可选） |
> | varStatus | 显示循环状态的变量（可选）                                   |
>
> **示例代码**
>
> ```jsp
> <c:forTokens items="aa,bb,cc,dd" begin="0" end="2" step="2" delims="," var="avalue">
> 	${avalue}<br/> <!-- aa<br/>cc<br/> -->
> </c:forTokens>
> ```
>

##### URL相关标签

###### \<c:import>

> `<c:import>`标签允许包含另一个 JSP 页面到本页面来
>
> **\<c:import>标签属性和说明**
>
> |     属性     | 描述                                                         |
> | :----------: | ------------------------------------------------------------ |
> |     url      | 需要导入页面的 URL                                           |
> |   context    | Web Context 该属性用于在不同的 Context 下导入页面，当出现 context属性时，必须以“/”开头，此时也需要 url 属性以“/”开头（可选） |
> | charEncoding | 导入页面的字符集（可选）                                     |
> |     var      | 可以定义导入文本的变量名（可选）                             |
> |    scope     | 导入文本的变量名作用范围（可选）                             |
> |  varReader   | 接受文本的 java.io.Reader 类变量名（可选）                   |
>
> **示例代码**
>
> ```jsp
> <c:import url="/MyHtml.html" var="thisPage" />
> <c:import url="/MyHtml.html" context=”/sample2” var="thisPage"/>
> <c:import url="www.sample.com/MyHtml.html" var="thisPage"/>
> ```
>
> 该示例演示了三种不同的导入方法，第一种是在同一 Context 下的导入，第二种是在不同的 Context 下导入，第三种是导入任意一个 URL

###### \<c:url>

> `<c:url>`标签用于得到一个 URL 地址
>
> **\<c:url>标签属性和说明**
>
> |     属性     | 描述                                                         |
> | :----------: | ------------------------------------------------------------ |
> |    value     | 页面的 URL 地址                                              |
> |   context    | Web Context 该属性用于在不同的 Context 下导入页面，当出现 context属性时，必须以“/”开头，此时也需要 url 属性以“/”开头（可选） |
> | charEncoding | URL 的字符集（可选）                                         |
> |     var      | 存储 URL 的变量名（可选）                                    |
> |    scope     | 变量名作用范围（可选）                                       |
>
> **示例代码**
>
> ```jsp
> <c:url value="/MyHtml.html" var="urlPage" />
> <a href="${urlPage}">link</a>
> ```
>
> 得到了一个 URL 后，以 EL 表达式放入`<a>`标签的 href 属性，打到链接的目的

###### \<c:redirect>

> `<c:redirect>`用于页面的重定向，该标签的作用相当于 response.setRedirect 方法的工作。
>
> 它包含 url 和 context 两个属性，属性含义和`<c:url>`标签相同
>
> **示例代码**
>
> ```jsp
> <c:redirect url="/MyHtml.html" />
> ```
>
> 该示例若出现在 JSP 中，则将重定向到当前 Web Context 下的“MyHtml.html”页面，一般会与`<c:if>`等标签一起使用

###### \<c:param>

> `<c:param>`用来为包含或重定向的页面传递参数
>
> **\<c:param>标签属性和说明**
>
> | 属性  | 描述                 |
> | :---: | -------------------- |
> | name  | 传递的参数名         |
> | value | 传递的参数值（可选） |
>
> **示例代码**
>
> ```jsp
> <c:redirect url="/MyHtml.jsp">
> 	<c:param name="userName" value="RW" />
> </c:redirect>
> ```
>
> 该示例将为重定向的 "MyHtml.jsp" 传递指定参数 "userName='RW'"

#### XML processing 标签库

> XML processing标签库为程序设计者提供了基本的对 XML 格式文件的操作。在该标签库中的标签一共有 10 个，被分为了三类，分别是：
>
> - XML 核心标签：`<x:parse>`、`<x:out>`、`<x:set>` 
> - XML 流控制标签：`<x:if>`、`<x:choose>`、`<x:when>`、`<x:otherwise>`、`<x:forEach>` 
> - XML 转换标签：`<x:transform>`、`<x:param>`

#### I18N formatting标签库

> I18N formatting 标签库就是用于在 JSP 页面中做国际化的动作
>
> 在该标签库中的标签一共有 12 个，被分为了两类，分别是：
>
> - 国际化核心标签：`<fmt:setLocale>`、`<fmt:bundle>`、`<fmt:setBundle>`、`<fmt:message>`、`<fmt:param>`、`<fmt:requestEncoding>`
> - 格式化标签：`<fmt:timeZone>`、`<fmt:setTimeZone>`、`<fmt:formatNumber>`、`<fmt:parseNumber>`、`<fmt:formatDate>`、`<fmt:parseDate>`

##### 格式化标签

###### \<fmt:formatDate>

> `<fmt:formatDate>`标签用于格式化日期
>
> **\<fmt:formatDate>标签属性和说明**
>
> |   属性   | 描述                                                       |
> | :------: | ---------------------------------------------------------- |
> |  value   | 格式化的日期，该属性的内容应该是 java.util.Date 类型的实例 |
> |   type   | 格式化的类型                                               |
> | pattern  | 格式化模式                                                 |
> |   var    | 结果保存变量                                               |
> |  scope   | 变量的作用范围                                             |
> | timeZone | 指定格式化日期的时区                                       |
>
> **示例代码**
>
> ```jsp
> <%
> 	java.util.Date d = new Date();
> 	request.setAttribute("d",d);
> %>
> <fmt:formatDate value="${d}" pattern="yyyy/MM/dd HH:mm:ss"/>
> ```
>
> `<fmt:formatDate>`标签与`<fmt:timeZone>`、`<fmt:setTimeZone>`两组标签的关系密切。若没有指定 timeZone 属性，也可以通过`<fmt:timeZone>`、`<fmt:setTimeZone>`两组标签设定的时区来格式化最后的结果。 

###### \<fmt:formatNumber>

> `<fmt:formatNumber>`标签用于格式化数字
>
> **\<fmt:formatNumber>标签属性和说明**
>
> |       属性        | 描述                                                         |
> | :---------------: | ------------------------------------------------------------ |
> |       value       | 格式化的数字，该数值可以是 String 类型或 java.lang.Number 类型的实例 |
> |       type        | 格式化的类型                                                 |
> |      pattern      | 格式化模式                                                   |
> |        var        | 结果保存变量                                                 |
> |       scope       | 变量的作用范围                                               |
> | maxIntegerDigits  | 指定格式化结果的最大值                                       |
> | minIntegerDigits  | 指定格式化结果的最小值                                       |
> | maxFractionDigits | 指定格式化结果的最大值，带小数                               |
> | minFractionDigits | 指定格式化结果的最小值，带小数                               |
>
> **示例代码**
>
> ```jsp
> <% request.setAttribute("num", 3.14159265); %>
> <!--两种写法结果相同-->
> <fmt:formatNumber value="${num}" pattern="#.##"/>
> <fmt:formatNumber value="${num}" pattern="0.00"/>
> ```
>
> `<fmt:formatNumber>`标签实际是对应 java.util.NumberFormat 类，type 属性的可能值包括currency（货币）、number（数字）和 percent（百分比）
>
> 下面看一个示例
>
> ```jsp
> <fmt:formatNumber value="1000.888" type="currency" var="money"/>
> ```
>
> 该结果将被保存在 "money" 变量中，将根据 Locale 环境显示当地的货币格式

#### Database access 标签库

> Database access 标签库中的标签用来提供在 JSP 页面中可以与数据库进行交互的功能，虽然它的存在对于早期纯 JSP 开发的应用以及小型的开发有着意义重大的贡献，但是对于 MVC 模型来说，它却是违反规范的。因为与数据库交互的工作本身就属于业务逻辑层的工作，所以不应该在 JSP 页面中出现，而是应该在模型层中进行
>
> Database access 标签库有以下 6 组标签来进行工作：
>
> - `<sql:setDataSource>`
> - `<sql:query>`
> - `<sql:update>`
> - `<sql:transaction>`
> - `<sql:param>`
> - `<sql:dateParam>`

##### \<sql:setDataSource>

> `<sql:setDataSource>`标签用于设置数据源
>
> **示例代码**
>
> ```jsp
> <sql:setDataSource var="dataSrc" url="jdbc:mysql://localhost:3306/mytest?characterEncoding=utf-8" driver="com.mysql.jdbc.Driver" user="root" password="root" />
> ```
>
> 该示例定义一个数据源并保存在 "dataSrc" 变量内

##### \<sql:query>

> `<sql:query>`标签用于查询数据库，它标签体内可以是一句查询 SQL
>
> **示例代码**
>
> ```jsp
> <sql:query var="queryResults" dataSource="${dataSrc}">
> 	select * from users
> </sql:query>
> ```
>
> 该示例将从数据源 "dataSrc" 中返回查询的结果到变量 "queryResults" 中，保存的结果是 javax.servlet.jsp.jstl.sql.Result 类型的实例
>
> 要取得结果集中的数据可以使用`<c:forEach>`循环来进行
>
> **循环取得数据**
>
> ```jsp
> <c:forEach items="${queryResults.rows}" var="row">
> 	${row}
> </c:forEach>
> ```

##### \<sql:update>

> `<sql:update>`标签用于更新数据库，它的标签体内可以是一句更新的 SQL 语句。
>
> 其使用和`<sql:query>`标签没有什么不同
>
> **示例代码**
>
> ```jsp
> <sql:update dataSource="${dataSrc}" var="row">
>     insert into users values (null, 'name1', 'pwd1', 0)
> </sql:update>
> ```
>
> 该示例将从数据源 "dataSrc" 中返回受影响行数到变量 "row" 中

#### Functions 标签库

> 称呼 Functions 标签库为标签库，倒不如称呼其为函数库来得更容易理解些。因为 Functions 标签库并没有提供传统的标签来为 JSP 页面的工作服务，而是被用于 EL 表达式语句中
>
> 在 JSP2.0 规范下出现的 Functions 标签库为 EL 表达式语句提供了许多更为有用的功能
>
> Functions 标签库分为两大类，共 16 个函数
>
> - 长度函数：fn:length
> - 字符串处理函数：fn:contains、fn:containsIgnoreCase、fn:endsWith、fn:escapeXml、fn:indexOf、fn:join、fn:replace、fn:split、fn:startsWith、fn:substring、fn:substringAfter、fn:substringBefore、fn:toLowerCase、fn:toUpperCase、fn:trim

##### 长度函数

###### fn:length

> 长度函数 fn:length 的出现有重要的意义。在 JSTL1.0 中，有一个功能被忽略了，那就是对集合的长度取值。虽然 java.util.Collection 接口定义了 size 方法，但是该方法不是一个标准的 JavaBean 属性方法（没有 get,set 方法），因此，无法通过 EL 表达式“${collection.size}”来轻松取得。 
> fn:length 函数正是为了解决这个问题而被设计出来的。它的参数为 input，将计算通过该属性传入的对象长度。该对象应该为集合类型或 String 类型。其返回结果是一个 int 类型的值。
>
> **示例代码**
>
> ```JSP
> <%
>     ArrayList arrayList1 = new ArrayList();
>     arrayList1.add("aa");
>     arrayList1.add("bb");
>     arrayList1.add("cc");
> %>
> <%request.getSession().setAttribute("arrayList1", arrayList1);%>
> ${fn:length(sessionScope.arrayList1)}
> ```
>
> 假设一个 ArrayList 类型的实例 "arrayList1" ，并为其添加三个字符串对象，使用 fn:length 函数后就可以取得返回结果为 "3"

##### 字符串处理函数

###### fn:split

> fn:split 函数用于将一组由分隔符分隔的字符串转换成字符串数组
>
> **fn:split 函数**
>
> |    参数    | 描述                                 |
> | :--------: | ------------------------------------ |
> |   string   | 源字符串。其类型必须为 String 类型   |
> | delimiters | 指定分隔符。其类型必须为 String 类型 |
> |  返回结果  | 返回一个 String[]类型的值            |
>
> **示例代码**
>
> ```jsp
> ${fn:split("A,B,C",",")}<br>
> ```
>
> 将“A,B,C”字符串转换为数组{A,B,C}

## AJAX

> **概述**
>
> 
>
> **工作原理**
>
> 

ajax提交的请求的响应数据由ajax的回调函数接收

form表单提交的请求的响应数据直接打印在页面上







****

base64:

[1]:data:image/png;base64,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

[2]:data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAABbwAAALOCAYAAABia9UKAAAgAElEQVR4nOzdXYwj533v+V8ZuvBYDcGacaSxMKPECknFdMs7sG8kliGsDK1gshOgz67RAewsBissSMA+x2QANxB7GwkC9NoHaGOXNHACkDgw0jhnjbgRnPDCzbIVr7WRTY4uomgiUZ2jrsrI9gykkWyNEmWk0d2zF1Uki69NdpPNt+8HaEgs1svDYrH76d/8+1+WMcYIAAAAAAAAAIA596FpDwAAAAAAAAAAgHEg8AYAAAAAAAAALAQCbwAAAAAAAADAQiDwBgAAAAAAAAAsBAJvAAAAAAAAAMBCIPAGAAAAAAAAACwEAm8AAAAAAAAAwEIg8AYAAAAAAAAALAQCbwAAAAAAAADAQiDwBgAAAAAAAAAsBAJvAAAAAAAAAMBCuGvaAwAAANNz62K07fHZ6+6URgIAAAAAwMkReAMAsAQ6g+0GAm4AAAAAwCIh8AYAYIGMGmz3W3/QNgAAAAAAzCrLGGOmPQgAADCa06jYHhSGT/rYAAAAAAAcB4E3AAAzat6qrwnIAQAAAADTRuANAMCULWt/bQJyAAAAAMC4EXgDAHBKljXYHhcCcgAAAADAUQi8AQAYM4Lt2UBADgAAAADLh8AbAIBjItheLATkAAAAADD/CLwBABhg3m4cidNDQA4AAAAAs4fAGwAAUa2NySMgBwAAAIDJI/AGACwVgm3MCwJyAAAAABgdgTcAYCERbGPZEJADAAAAAIE3AGCO0V8bOD4CcgAAAACLiMAbADDzqNYGpo+AHAAAAMA8IPAGAMwMgm1gcRCQAwAAAJgGAm8AwKkj2AbQiYAcAAAAwDgQeAMAJoZgG8CkEJADAAAA6IXAGwBwItw4EsA8ICAHAAAAlgOBNwBgKFRrA1gmBOQAAADAfCLwBgC0IdgGgNERkAMAAACzgcAbAJYUwTYATA8BOQAAADAZBN4AsMDorw0Ai4GAHAAAABgOgTcALACqtXFSjWuIawZYDATkAAAAWFYE3gAwRwi2MU6d1xPXEbC8CMgBAACwKAi8AWAGEWxjUsLXVuf1RAAOYFjLHJDfuhg9+evxCrIvS7vVrCLjGRYAAAACBN4AMCX018ZpGRRyD7vdqNsCQNiiBeTtobejjJVSSZKUVsWNazuaU61ti4TyblXZiCR5KthR5dpXaEpXjIrJXuulVTHrKjeP1VhWVHJ8Lw0AAGDu3TXtAQDAoqNaG9Nw3JA7jApwAOMy6veLWQ/Iz15320PvRF5udU379o7/OF2RKTZiaE8Fe0exoJTbyUS1p4SU3gqtI8nJyNqOa7MtvW4E2v4+WsfKKhJeBgAAgCYCbwAYE4JtTNs4Qu5BCMABnJZ5CMhbofd3+6wRqvxOV2QkORlL5XWjalF+wG0fBkF5VLnViky1s1a7pJTVqOdOqyJJtZyiVq59GQAAAJpoaQIAIyLYxiyZdMg9CgJwAPNiXAF5I/C+dfFrOnfDU7OlyU5M1eLgRiNOxlKqFFrQVhXeS1ApXi1KGUvbcVfVLB3AAQAAOhF4A0AfBNuYVbMUcg8yL+MEgKMcFZB/48F/r82gpUlst18P713pcqsnd6tXd8DJyGok4OmK3Pi2ov0afbftutHiBAAAABKBN4Alx40jMS/mPTym+hvAIgpXeN+67rQC750Drdbj2gz12o5VO28u2W95D15BdnRPG5UN7aX2tNG8ASYAAAA6EXgDWApUa2MezXvIPQgBOIB517pppd+r+9sXIjp34/PNlia78W3txKoqKiP7cDNoPxLq691TQvkgzG5redJWxe2pYLcqxanwBgAAaMdNKwEsFIJtzLtFDrnDuAEmgHnWCrsleYeqpys6W4wqb+8014lktyTLkqW0KqYRRydVNEZFyW9hUl5v69vtZGwdNtYsusrXg2C7llPUOlDFrKvcFpinVSHsBgAAaEPgDWAuEWxjkSxLyD0IATiAedEWdkuSe6CaYt0reoeqS5LqOvSkZCiV9gq2onsbcqvhZiaeDuurirWl12lVTFHJoP2JpFBFd2gZAAAAmgi8Acws+mtjkRFyDzYoAOd8AZiWrrBbklOuK78el22lVEvk5UpSKSWrlFbFmCCstmQpr8rGnlK5mhJ5V6bqJ9ttrUvSFbX3mywpZTWfVEUKqr1z7csAAADQRA9vAFNHtTaWBaHteFD9DWAaeoXdAAAAmD0E3gBODcE2lhEh9+QRgAOYNMJuAACA+UHgDWDsCLax7Ai5p4sAHAAAAACWF4E3gGMj2AZaCLlnFwE4AAAAACwPAm8AA3HjSKA/Qu75RAAOAAAAAIuLwBuAJKq1gWERci8e3lMAAAAAWBwE3sCSIdgGRkcgujyo/gYAAACA+UbgDSwogm3gZAi5IRGAAwAAAMC8IfAG5hj9tYHxIuTGUQjAAQAAAGC2EXgDc4BqbWByCLlxEgTgAAAAADBbCLyBGUKwDUweASUmiX9AAQAAAIDpGmvgbVnWuHYFLLS3L0R6Lj93wzvlkQDLIfyZ43OGTpP6t3/+cQUAAAAATt/YA28KxgEf/bWB6aLSFsM4zbkLATgAAAAATB6BN3BCtCEBZgchN0Y1zbkLATgAAAAAjB+BNzAkgm1gNhFy4yRmae5CAD77aN8HAAAAjMckfw8j8AY6EGwDs4+QG+Myy3MXAvDZM8vXCwAAADAvJj2vJvDG0iLYBuYLITcmYZ7mLnwGpm+erhcAAABgVhF4AyfAjSOB+UbAh0mb17kL1d/TMa/XCwAAADBLCLyBIVCtDSwOQm6cpkWZuxCAn45FuV4AAACAaSLwBkIItoHFRMiNaVnUuQsB+GQs6vUCAAAAnCYCbywlgm1g8RFyYxYsy9yFAHw8luV6AQAAACaJwBsLi/7awPIh5MasWda5C5/F41nW6wUAAAAYJwJvzD2qtYHlRrCGWcbchervUXC9AAAAACdH4I25QbANoIGQG/OCuUs3AvD+uF4AAACAkyPwxswh2AbQCyE35hFzl6MRgLdwvQAAAAAnR+CNqSHYBnAUQm7MO+Yuo1vmAJzrBQAAADg5Am9MFDeOBDAqQm4sEuYuJ7dMATjXCwAAAHByCxp4O8pYZa2bopLjOvixTWos4f1O//XObrX29M8NgKMRcmNREWCO3yJ/v+B6AQAAAE5u0vPqD01sz8fmqWBbyjj9Hh9nlwXZdkHeUcvmwuDzcetitOfX2dLnde6Gp3M3PP3B1x2dve7q7HVXXsGWZVn+V3inTqa53C70OEvDnD8nI8vKqOdQhzr/E7gWAAyt7XtI8D1j0cIrAOMX/n7ROR8BAAAAgEm7a9oDOA3OTk6rW0aRnsvmMz39djqqWz2W/8GNz2vLFJWUp4Id1cGWUTFakB09UMWYoNr8sgprVWVV0OXcqiqm2lw/4wTrp9S9fugE9jqnLf6+ckooodWea8z7+QcW1SJXZgI4fZ3fR5ap/Qk6eAXZl6XdarbP/BEAAAAYj+lWeHdVEQdBaU0qpSxZmULHY0d+C4yMnF4VyF5BtmWrrSDZK2i7ntdm8ohloefsRsWz1VlN7CgTes4/bvsya1D5cb+q6b7H9CuaLcsKVUcl9b/+KuJXa6e+q7PP/nv9wY379F+edXX2+nd7xsve/p5q6fWgZUhS6+ma9vY9KRIbbf2e5681xtbYI8pWjczuRu/z0Ov8j/taADA0KrkBnJbw9xgqwOdZeP6bkdMxl/W/wnNyT4XLOdVqOUW71us9923uu3Ou3e+vBwEAAIDAFAPvklLldRljZNy8lNuRo4iyVVf5hJSuGJlituNxsntbU9FqLupPlCNZVU13JbI21rqquzuXSfKD5+ieNlzTHFc91ZisO8pYKakSPGeMqtmIpKSKxjTHki5tq3fm2uv1HnFMZ0e51YqMMaFfDh39lwe91vloe81JFStSyrJkWVHtbbhqnLJEvPVLZDSeUO3APcb6Pc5faIzGmOb2g3Sf/wlcCwAGIuQGMAsIwIcxCy3deowhkZdr/LmZJCndmg8a4yqfWFUsmOw5maj2lOhYx8hU0lKiswglrUpzH+FjdSwDAAAA+phi4J1WpRFaRmJaVV2HQxfnhrZVUutpqd5zY0flUlpb2cgRywLugWrprVZgHslqK13TgSvJKavUNSFvaFSjpFRSsP6gMYdf76BjRuNKlFKyhu017hVkb8ebvxBs7PUPfxPx6OjrS+o6f6OOsef5P41rAQAhN4BZNygAxzxoVGNHlVv1/1rQyVgqrxtVq1WZ9XIwZwzmzuV1ma4WJ6VmMUauFixqVoaHlgEAAAB9zOBNK8fHK2yrnt9U8ohlJ+JkZFmXpd0JVJ1EsqoaI7N1oGhXe5Vu3v5eqHI6ouxWWqWyv1G4Qts9qB1rfanH+Rt1jOM+/wAGIuTGrCPQxCBUf6tHSzf1b4fnFWRbGRWaNyXvaAnSNlEbtlVfZ5u5YB+1nKJdAXToLx+DgoRksfUXgE651Ge7hqAtXrMKfFOHdlnrxsgvBndlTJF5JAAAAAaa08C7pHJoYr9dSmhjrbNi29FObrWrurt7WUg0rkS4JUmw73hUUnJd6VpOO05rX4WCJ++wLjUqtL197Y1adTLomI7jtz1JFuXmE0dWLkdiq6rt7QeV1p4K2yUl4lFF1jaUKJWDfoeOysH5GnX9nudvpDEecf6PZZhrAVguhNyYZZ2hJdcohrWs7U+6WroNbMEnSSXtaVfGGFXSJaUsPzBub703Squ+zjZzjf53HS1NSqkePbzbe3KX1017S5P1clu47jWD+sZXVLmaX/GdKkm1XNRfPvRfFgIAAGAZ3TXtAXSLaG0joVzKUildkSkmOx5LUloqW7JS/hbpigkC58YvAFWt7W+rlN5SMbRnr9C9rP3QWVUrB7KilnKSpITybqg/tpuXHbVk+UdVxRQV0ZbSVkpWSVIirfSoFd6DjhmRypalVPN4fpDbdj42D5uvOZssqlK2FLX8PSmRl5uNSMpqN28ralnt5ysy2vo9z1+y9xh7OfL8d5+c418LwJIJhz0Eh5glnUHkoOuzsS7XMIbReZ2Mcq3NtaAdXrWtHV5OZVdSVJJareOi8YTUvBF5VPFE0DbP9Vv1uX1b9bUqsNOu1H3jmx7SaaXrcW1Ws4rIU8HeUSwSUbJqlG3b945i1aBKO1mUMeGZYVKmsXJjXl/Z0F4qmOsyxwMAAMAQLGOMGdvOLEtj3F0fjjJWWesD/5zRUcbaVrxtYtxrGYZ30vM3ifM/zLUALC5CbsyicYSOp3ltn87cBdMwiQB8OteLH0AfbAWtQZyM3/s6dKfwRp/sYrQgO3qgrWBu5BVsRQ+2gnVD+1FG1nZcbmf/bCcjK1UPii/Cx+0YQ1AhXpIkpVVx49reiWk3vq2dWFVFZWQfbgZV4+F1e2kVezgZv5LbX5wPja89hG9/DgAAAPNm0vPqGazwHoekiqYzAu21DMM76fnj/APjQMiNWTOJUDG8D6q+cVwLWwHeaIe3mWz+heN2KaGNzRH2kVxXOpXSjpNtBtiFQlRr6m7Vt9pre+9Q9XRFphhVwd5pLo5ktyTLktX2V39+m5Si1Cest3XYWLPoKl8Pgu1aTlHrQBWzrnJbYJ5WhbAbAAAAA0ws8J5kL8VvX5B0MapbEzvC7JnbX8omihAdy4GQG7PktEPDxv75HOCkBgXgs31NdbZ4G9AOb+jG1qO26usYw/qBaop179Y7VF2SVNehJyVDqbRXsBXd25BbbbudvA7rq4q1pdf+WJJB+xP/JTYqur22gB0AAADoZQ5bmgDA4pufIAaLbharYsf5+WDuAmn465zrxedkbB2ub2gvlVMtkZe7K12O5lRrC6ujyimvysaeUrmaEnk3aHHS0bokuE+Lr6N1idK9K7xpZwcAADDXJj2vJvAGgBlByI1ZMIsB9yAnbXnC3AW99PsccL0AAAAAJ0fgDQALjJAb0zZvAXc/x/0sMXfBMBblcwIAAADMAgJvAFgwhNyYpmUI7kb5jDF3wSga18syfI4AAACASSHwBoAFQMiNaVn2YO6ozx5zF4yi3/XC93gAAABgeATeADCnCEAwDcsecA/Sq983cxeMYpjrhc8gAAAAMBiBNwDMEUJunDbCtdGFz9m5Gx5zFwztOHNdPqMAAABAOwJvAJhxhNw4TYRn48XnF6MYx1yXzzAAAACWHYE3AMwgQjKcFsKxyQrPXfhc4yiTmOue9mf81sUo1zcAAACmatIZ8l0T2zMALBjCMJwGAu7pCZ/rXv2+gUnovMb4HgAAAACcDBXeADAAITcmjXBruo6au/A9AGHTmOtO4hqkyhvLxsnYOtysKhsJLfQKsndiqhaTUxsXAADLigpvADhlBFyYJALu+dKr6rtzOTBJ/a7BzucgSY4yVlnrpigizHk2/vcxWdzVoZ2RUy0qWrC1E6uqGPo4tQJxTwU7qlxtwM7SFRlCcgAAZtqHpj0AAJgFty5Gm19nr7vNL+CkwtdW5/XFNTZfwu9b4/0ETlPn94/O7y/H5RVsWZYVfNkqeGMc9Ewf31PBtpRxTut4k8X72GM8GUdOxpJlRZWrlZSyC3IllVKWrGhOtVJKlmUpVQpvmVbFGJleX25eiWAtJ2PJPu2TDAAAhkKFN4ClRbUmJoEKzOXQeF/5PoJpGkv/byej6N6GXFNV5Oi1x2/ax18U0z6P0z5+J6+gy3sbcqtJRWRkiuEnszLZkx8iWXR1aF9WYa2jVQoAAJg6KrwBLBUquTFuVHAvt37VtsA0DFsB3njuSE6mVbFrF+RJft9jK6NMxq/ite2OKlcn01r3yO0zGlhc7RVkNyuGOyt4HWVCz3VX2gbPNzbqGkurdUUpFVqvdXAV7H7HHpWjjJWRExpD1znrOE9OJnxMR5lwxbST6THeQYdfvvfR2clpdSuriPxK74wT/LfQPpb2ryNeR5eIsluryu04ba9zUf5iAACAeUbgDWDhEXJjnAi40Q/hN2ZNvwC84dbFqG6lf6rKak7RzrDRK8jejssNWjm4G3u63Hy+JK0bGVNVdSut2t6+mllsuaT0VlaRobYvKpks9j9+dE8bbquVRD3VCH0dZayUVGm1mqi2341QBTt4vpjs81qkbNVVPiGlG+uFOTvKrVaa++/VstlvldHx1QiEu5SUKq83X4tyO3642uc8JdfTKpUbIW9Z9YS0t+/v2TusKxHv+N4y6Dwu3fvoqFxKaz14zyKxVdUPgzHFsqqG25OkK6GWJcfoGZ5cV7pU9t/LiL9v2nsDADB9BN4AFs6gQBIYFQE3joN+35hF4Wsy/DhZNDLG1cZetFnl6u3vqVbzA0zLshTN1VQ7aHzPa4WJSq4rXdvTvifJK2g7CBqH3l7qeXy5B6qlt1qtIiJZbaVrOnAlOWWVEnlt9gwW69q2o9rbcJvB4+Cx9BGNK1FKDQiwG+Pu+Kpm+7T0SKvSGFBkTRuJug69AWOLxpUIglSnXNfG7pZW9/blydP+nrSx1n0U3seQRFzN77rRuHTgyj2Q4tFQ5X6oh3fv6vJhRBVPHL0WAAA4XQTeABYCgSTGhYAb40bVN2ZF5/e19msxomzVqJIuabsR/LVVv/aogpYkJbWZ96uPvf09Kb/ZqpIdavsBxz+BriB0pLGoWa1rtg4U7dOmYrQK7wF6ja0Zijsq1ze0Fokqrj3tO/va04Z65N2NgfM+dg0pptV6WeX6qmIRyb8pZUXpRF5uo8q7kj7xWAEAwOwg8AYwt6jixjgQcOO00PIE09L5/a2NkwmFuZ4O69JqLKLI2oYSpe1Q3+iC+uWXkbUNaW9HO6HK46G373N8v8I5tL1X0HYpoXhUQTVyTjuhHteF5oqr2qq6ytdTzX7Oo7yW1rgcv0I5WZSbT7RaYoSMVuHdW/+xRbS2Ie1d3lZ9Y02R4PFB+UDaWOs+Bu9ju9qB2q/0uuoKVX2PjauD2th3CgAATuiuaQ8AAEbRedMtYFSdASPXEaYhfN2F20sA43TUtdVYvp6xZKWChemKTFKSstrN7ykatZRrLC9KPcuXI2vaUM7veR1qXTHU9sli3+NXKweyGtsrobxbDVpjJFV087Kjlix/I1VMUWpGnBFlq65kR2XZebnVPmNRRGsbCeVSlkrpSnu1cFIqW5ZSzf2PEmOPoN95UhBA5/a0sdsKn+u5PW24PcYy4Dwu4/u4nk6p7BSVTAbH2T2UHc0pah8oLSk28E0pKWWV+j+drrT+3ymrlF6X/5Y5ylhlrR+nFzgAABgryxhjxrYzy9IYdwcAkgi5cTIE3BhkluYufK+bfbN0vQzCP6Jg6XkF2TsxVYtJORlLqZKkRF5udU379o5i1VAo7WRkpUpKV4yKSU+Fzuf77Nff1NbhZhDgOxlZ5fXh2qwAALDkJj2vJvAGMJMIfnBcBNwYxazOXfgeOJtm9XoB0M0r2IoebE0sgHYylrbjrqrBHTm9gq2dWFXk3QAAHI3AG8DSIODBqHr1P+bawSjmYe7C98bZMQ/XCwAAADDrCLwBLDSCHIyC6m2M27zNXWhVMV3zdr0AAAAAs4jAG8DCIeTGsAi4MWnzOnfh++h0zOv1AgAAAMwSAm8AC4FwBsMg4MZpW4S5C99fT88iXC8AAADAtBF4A5hbhDA4CgE3pm3R5i58352sRbteAAAAgGkg8F42XkGZ/TUVg7t9S5KcjOzDzeYdwIFZRtiCQQi4MWsWee5Cv+/xW+TrBQAAADgtk55Xf2hiex7IUcbKyJnOwQeY3LicjK2C17ZAdtuCQCSr9YPL/rqNdZKb2tjbCcblqWDP4rnDMrt1Mdr8OnvdbX4B4Wuj8/rgGgEmq/E5C38GAQAAAGDRTSnwHsRTwbaUcfo9Ps4uC7Ltgryjlp32uPpIbm5ob8eRonHpwJUUUXY3rnLBk+TqQHHxKyumjZAbvRBwA7Mn/Bkk/AYAAACw6O6a9gBOg7OT0+qWUeSIZaczmIysVCl4UJKVk6SE8m5VzY4lkayqRf9/V+uH8pRUJJJVMSvJ21d9NXb64wZEuxJ0o0UJMF/Cn1FangAAAABYRNOt8HYysixLlmUF7T08FeyocjWplLJkZQodjx012450bSu/atvqaB3iFbRdz2szecSyiY3LrwRPlWrKRW0VokUZY2QqaaUrRsa4yidWFYuoua5lNSrHk1pf3dN+6PV4+3taXe83cGD8qORGGBXcwOKg6hsAAADAIppihXdJqXJFxhT9oDq6IydbVLbqSnZUB1tGxaQkrXU8dtq3laOMFVUmZlRMZlU12bajODs5acPtqu7uXDbRcVWNYhlbh5tVZVWQnYlpN16XYq2jlhvPV43WCrZ2guXRuFT2u5pI8rS/J8V3T3jqgSNQyY0GKriBxder6rtzOQAAAADMiykG3mlVikGlciSmVe3p0JOSQ/XqCG2rpNbT0nbPjR2VS2ltmcgRy05vXH6FdlVueVvxtdaW6+ur2t73lM22HyiS3ZLsgrxkVhFvX3urW6rSzwQTQMgBiYAbWHaE3wAAAADm3UL38PYK26rnd1U8YtnpcbSzt6HNqqf97UYbk0ByXavb+/Ky2Y5tklpfTWnHyWq9nNPqujnNAWPBEWaAgBtAP/T7BgAAADCP5jTwLqnsFJVMyu/HXUpow+2u7t7JrXZVd3cvO81xJVWsJiUno9zquvzo2tVBTYo1npPUaNntFAqKZrNKFisqW5ZSibzc6ST1WCCE3MuNgBvAcTS+V/AzBAAAAMCsm8HAO6K1jYRyKUuldEWmmOx4LElpqWzJSvlbpCtG2YiCntt72nCrWtvfVim91VXd3bnsVMbVxlEmVVc+nFwn4uq8TVQpZUkVo2Jj3JJUO1CznTcwAgKK5UXADWCcaHkCAAAAYNZZxpix9ciwLEtj3F0fjjJWWeumqOTAdbYVd6uhwLnXstMblxPclDK2Y6m8blRMeirYUeVqkoIAvbVuYx3//1MKng8F+pN5DVgkBBHLiYAbGM3pzF0W37K0POF6AQAAAE5u0vPqBQ28p2HM4/IKsqM5rVb84Dv0hB+Ur7aH5IBEyL2MCLiBkyHAHK9F/znE9QIAAACcHIE3gIEWPVxAOwJuYLyYu0zOIv584noBAAAATo7AG0CXRQwR0BsBNzBZzF1Ox6L83OJ6AQAAAE6OwBuApMUJCzAYATdwupi7nL557vfN9QIAAACcHIE3sMQIuRcfATcwXcxdpmcef8ZxvQAAAAAnR+ANLJl5DAAwPAJuYLYwd5kN8/Kzj+sFAAAAODkCb2AJzMsv+hgdATcw25i7zJ5Z/pnI9QIAAACcHIE3sKBm+Rd6HB8BNzBfmLvMtlnr9831AgAAAJwcgTewQAi5Fw8BNzDfmLvMh1n5+cn1AgAAAJwcgTcw52bll3SMBwE3sFiYu8yfaf5c5XoBAAAATm7S8+oPTWzPAznKWBk5E93vpI4xCk8Fe8AYnIzsgtexSUF2xuleZtnqXBWz69bFaPPr7HW3+YX5E34vO99P3lMAOH3h78GN780AAAAA0HDXtAcwHzwV7KgOtoyKyckcwcnYOtysKitJKitjpVRSQnm3qmwkq6rJTubAGBsquRcDFdwAMD8a36P5GQwAAACggcB7jLyCrWiu1v2EVWp/nM4rX8/JX7Uk66CiimrKRS3lJEkJbbhGlR1bhxMfNU6CX7DnW6+qQN5HAJg/4e/d/GwGAAAAltuUWpp08AqyLUtW8NXe0cNRJvSc3wKkfZnV2QKkbfNMx7ZHHdNTwQ4v96u7czWplAqO1afFSCRblTGm+eXmE5KkRN5tW26KWWWrRqaSViLvyo1vK1VKKO8aGTevRHpL2UjnOeho1dLvdWHiaFcyv45qT8L7CADzr1fLE9qeAAAAAMtj+hXeXkF2dE8brlE10nhsq+BWlY04ylgpqWJk2lqJRFQ0RkVJfgC8rcJmsiMklqSSUuWKjCkG+92Rky0qOeiY7o5yqxWZauiASVdqa2mSPLrFiJPRZW0pnyhLuqyMU+3bDiWSrapyMEo1d5vgfuwAACAASURBVOh1yVHGiioTm1y7FVAtNq9oTwIAy61X5Tc/CwAAAIDFNv3A2z1QLb3lB8+SFMlqK51T2ZXkllVK5OX2DHJbldeSlHYldQXeaVUaKXAkplXt6dCTkoOOGY0rUUrJquflVrPduxyGk5FVXpcpRlXYk2LZqmIZSxkNGUrXt2VbKdUSebk9BxB6XUpqPS1tH3pS8lijRR+E3POHgBsA0A/9vgEAAIDlMP3A+zicjKxU3W8BEgluKDmufTduEBm0DElXRqucdjKWUqrIFJOSWq1GkkUjZSxZ5cZzA6xuqVqlXHsa+CV4vhBwAwBGRb9vAAAAYLFNv4d3NK5EabvVD9sraLuUUDwqKbmudC2nnWZ/bUeFgifvsC41+lx7+9rrcZ/IYx/Tcfxe2cmi3HxC9cPh+2M7GUvldSM3vh30144qVyspFfTaLq8bVZRq6zley0Vl2YU+7UwcZeyCukdQUrmxi2DsG2tUdx8XPbnnx1E9uAEAGEWvft8AAAAA5tv0K7wjWVUrB7KilnKSpITybjXox51U0c3LjlqyJElpVUxREW0pbaVklSQl0konxnjMiFS2LKWax/OD5LWNhHIpS6V0RWbzMOgBXm3rG54sGvktvqvyW3x7Ktg7ilWLatZrJ41McGPMXC2tivG3cTJBS5VkVtVisK53qPpqrEdblbRUtmSlgkcV06N/OQahoms+UMENADgttDwBAAAAFoNljDFj25llaYy7WwA9Au9+nIysVKlrcXdLFUcZq6x1M8Q+0YZfYGcfATeA08bcBYN0zh24XgAAAICTm/S8msB77hB4j4KQe7YRcAOYNuYuGBZzCgAAAGA8CLyBEfEL6ewi4AYwa5i7YBSN66Xx84yfYwAAAMDoCLyBIRByzyYCbgCzjrkLRtF5vTD/AAAAAEZH4A30QJA6m3hfAMwb5i4YxaDrhfAbAAAAGA6BNxDgF8nZQ8ANYN4xd8Eohr1emLMAAAAA/RF4Y6nxC+NsIeAGsGiYu2AUx7le6PcNAAAAtCPwxtIh5J4dBNwAFh1zF4ziJNcL8xsAAADAR+CNpcAvgbOBgBvAsmHuglGM63ph3gMAAIBlRuCNhcUve9NHwA1g2TF3wSgmcb3Q8gQAAADLZtK/h31oYnueIU7GVsHrWOgVZGecqYxnmd26GG1+nb3uNr9wOsLnv/M94H0AAOD0NX4Gh38+T4RXkG0X1DklDnMyltqnx44yR2wjeSrYGTGrBgAAwKxYisA7WdyVLvsTca9gqzPnbgXingq2Jcsa8BXe2CvIHrCu3ZWyLydC7ukh4AYAYD6Efz4fK/h2MrKsAcFzJKvdjT1F+xZ8OCqX0lpP+vvqO491Mh1z3qhytZJSHfNg6koAAAAwLVMLvL2C3TtEDk2iwxPtUddvPR2aiNsFuZJKKUtWNKdaKSXLspQqhbdIq2KMTK8vN69E5wHSld7rVtJjOEvzi5B7Ogi4AQCYf6P93A4KNrbroXlq7yKOaK4mBfPf1lcQkjtl1fObSkpyyiXVclFZVkqlWk7R8Fw7WZRxXbnNea+rfCI0f67klXeNiskJnBgAAABgCNMJvL2CLudWg4mxq3w95VeBeAXZKQXLK1rNXfYrr0ddPyRZDIXQ1ayS2WqPgLqqbOSYr6Xrl4bgqz1FXwqE3KePgBsAgGXSHmT7NSARZatGZncjtF6wzBhV0r2KOSpKJ/JBaF1UUp4K2425q6OyKj3WM6o2J8z7uhyu4l6NK6qg0KQsrZ3S2QAAAAB6uWsqR43EtKqDrsXe/p5q6S35BSFJradT2t73lM2OuP7avuzonjbcqtb2be3Eqto8tLWjDdVzOdV6Diqtitkc8XVkVTXZ0bZZMNx48nRxk0kAAJaYs6PcakWmOnz5dHJdsguekqHqDq+wrfrGriLNx5e1F9SHe4Wy4pvFwTttmwO7Oqj7IXeyaMQtYAEAADBtU2ppklSxoqDXX1R7G27zzx4T8VagF40nVDtwR18/klU1qNqOxFZVPwzKvmNZVcPtSdrakRQ1/K8OQ/T6bn71uGHmnKOS+/RQwQ0AAJqicSVKKVlH3kgyJLmpjb3wX0E62tnb0G4oAHe1od2tVUlSJFsc8JePvebA7W1Pml+jjBEAAAAYo6m1NLG348GfR7ra2Iv2vbFNIh4dff2waFw6cOUeSPFoaJIe6uE9+g0mW38m6uYTSlf69Pw+abuUGULIfToIuAEAQF+RoHhj60DRoW8MGVG2uqWDaEaOV5BtbSu+m1V4eprMth7797/pE2bb+1qrdt+3Jp32+3a3La+2HwMAAAA4LVMJvL39PWljLZgER5TdSqtU9mfsfkW3zz2oHWv9NpGYVutlleurikUkv3VJ0I+wUeV97BtMetrfq/k3wexR3T1aiD57CLknj4AbAAAMzXH8G0wmi3LzidZfMR4p+GvJoOXfoGKMtvvfdPTw7gqxnYys8rqKxTXpcnDzSwAAAGDKphJ4R2Krqu3tB3/m6N8kJxGPKrK2oUSpHEyWHZVLCW2sRUZev1tddfk30xnzK2lWend9uXmtjv14k0fIPVkE3AAA4NiSUjkorIjmVrU1xJ8RegXbL8Yor8uYXenyOAozHGUa+ywm5c+J11VegIIPAAAAzL/p3LQyWVSlbClq5fzHibzcbERSVrt5W1HLkiSlK8avQImMuL5XaN60MhtJqrh7KDuaU9Q+UFpSbODgSkpZpf5PpytDvURvf0+KzccNLbnx5ORwk0kAADA+SRWNUc9bSkayqjbvGOmpYEeVq0mJvCtjWsF4tmqUVSMIr/nz6hHajzgZS6lSWpWucfhja+43XQnCcAAAAOB0WcaYsd1M3bIsjXF3Y+FPyhVM5te0b+8oVg3doNLJyEqVlK4YFZOeCp3Ph3kF2TsxVXtM3r2CrWgu1FJlxF8eThsh9/h1htsS5xYAZt0szl0wu7heAAAAgJOb9Lx64QNvtBByjxfV2wAw/5i7YBRcLwAAAMDJTXpePZ2WJjg1hNzjQ8ANAAAAAAAAzDYC7wVEyD0eBNwAAAAAAADAfJlo4N2rpzGO56iwlZD75Ai4AQAAAAAAgPlGD+85Rsh9MgTcAADmLhgF1wsAAABwcvTwRhtC7uMj4AYAAAAAAAAWG4H3nGiEtYS0wyPgBgAAAAAAAJYLLU2wMAi4AQCjYu6CUXC9AAAAACdHSxOgDwJuAAAAAAAAAGEE3iPxVLAvS7tVZSPTHsvyIeAGAAAAAAAAMMiHpj2Ak3OUsSxZA79sFbzWFl7B9pcVMj3WzcjxV5IdWp5xJDk7ytVqykX779cuOCrYPcZgF+QJo7h1Mdr2dfa62/YFAAAAAAAAAGHTD7y9guyjwmAn0wqiuyRVNEam+VVROpGX27bMr8h2Mn74HD3Y8pfFpETeDa3nKp8I7TpdkTFGbj4hyVEmVWouM25eicSG1iKNl2HrsnZVzSaVrZqufaa3sqIofDACbgAAAAAAAAAnMfWWJs5OTqtbpk8Y7KlgR5VTQgmtnvhYyaKR2SzI3hlyg1JKVsn/33S6rHrelavLsu1t1WqrqpiiIvKD9O24q+ravuxMTNViMtiBo4yVkipGzUVookUJAAAAAAAAgHGaboW3V9B2Pa/NpOSH2x0tRBTxq6V3N7q2szvaiQxxMH//0ZxqpZTfjuRQquWiodYjUeVqoU3SFbn5hNIVo2KxqGo2IvegplqtJqmuw+D4yaJRNRuRs7Onjc1k6LWUtV5Jq5SyZI822IVEBTcAAAAAAACASZpq4O3s5KSNNb+629lRbrXSbAUysCI6klXVjHrjSD88d/OJoC1JVdlsMdR6pPFVVLJxjPAgHL/fd3m9sd6udNmS5Sfz8gq2tuO7Wtu3ZVmXpd1gX0n/GLu6vHR9vAm4AQAAAAAAAJymKbY0cVQupbVlgtQ6GleilJJVz8utTqrftaOdXE1KbCtTiGr9IKpUqXutRD5oT7IT025cKqUsqeIqnygpl7LU2iStSjUpORlFczUl8lIkW5XJdu+z3/JFQosSAAAAAAAAANM0tQpvr7Cten5TzRrqSFZVY2S2DhRttjSZwDHTaSW0ofhBNFSt3X6jy2pH6Xi62YM7rUrXDS49FcpxuZV0sLajjGWF2qR0tmlZHFRwAwAAAAAAAJglUwq8He3kVrUVDpYdR44kJYty8wnVD8fd/MPT/sGGdjfj0mpM2aLR5qEdhNEplWo5RY8VTEeULYYr0pMqNkLxSlqJvDtcm5Y5QMANAAAAAAAAYJZNJfD2CtsqpdfVlv8mpXIQOEc7w/DuHRzjppWdwXTQZqRHhXcrmD7U/l4tuOmkK6mkVL8bXC4gAm4AAAAAAAAA88Qyxpix7cyyNMzuMpatuDvqTSd7czJWzz7cXdIVmWLSD8t3YqpuHsqO5tQzs07klV/NKVdKKN8cp6eCvaNYNbipZedjJyP7cFNbffqCN/Y7uf7kJ0cPbgDAshl27gJIXC8AAADAOEx6Xj2VwBuzgYAbALDsmLtgFFwvAAAAwMlNel5918T2jJlDwA0AAAAAAABgkRF4LzACbgAAAAAAAADLhMB7gRBwAwAAAAAAAFhmBN5zjIAbAAAAAAAAAFoIvOcIATcAAAAWzWvPfVJvPuDo0cjvTHsoAAAAWAATC7w7w1n0Nii0JuAGAABYLm9d/aJeev3Af7Cyrk8//i3dN90hzZzXnvuk/vm2pZVYhZAcAAAAXSxjjBnbzixLY9zdUgqH3ATcAABMFnMXjGLS18tbVz+pl97d1GOfeVp3r0jveV/UlddTevLxp9tXvP0LveZ9Xf/cDMbj+t3Yd/SJ88sT/r7nfVEv6zsE3gAAAHNo0vNqWprMGEJuAACAZfSs3nz9U/rdx/2wW5LujnxV9x/+rd6SWlXet5/Vy899Re898Bd6LPWE7pb03s3v6eV/SOrNGG1BAAAAgOUNvL2C7MvSbjWriCSvYOuydlXNRiZxMBX8g2kiuwcAAMB8u/m3enMlpUdWJOkXeu1qo4J7XfeHVnvL+4re6wi27z7/tB59XHr+ua/rtfN/rftuflFXDg+az9//mQM9svI9Pf/cjm7L8hc+8J/05KUn/H2G26hIWllZ10Of+ZbuWwmP75v6yT+Um/t7SN/Uy//wN7otSysPfF2PXHpad4+ynp7Vy5Wv6M1gPIPak7znfVMvH/5NMPa47o99Rw/1WG+o1wEAAICFN0MtTRxlrLLWTVHJcQ3oyENmZJXXZYpSxkqp1GOVdMWoGC3Ijh5oyxQVLdiK5mq995fIy92VLkdzqoW3V0ZWKrz3hPJuK/z2w/Ytbeyl1LXrRF5uEMoDAIDxoqUJRjHR6+XmN/WTm/+Tnrz0hN/aRH+hxy5J1yp/q/tTjT7ez+rltsft3rr6SV1baYThv9DLlVLXuq8990ndjv2THjnvP37P+6Jevv1VPRJ5ollZ/t7N7+nlQ08P9egf7rdd+ZSkmH43ltYnzv+O3rv5rHT+iSDIHm295hj6tCdpju9SY7tf6C3v67p2+IoUCv5HfR0AAACYnkn/Hvahie15WF5Btl2QN3glFWxLGaff42NKFlXRtjKZsuKukTFGppJWIu/KmIrSSms9KSmSVbUipeyCXPkhtjFGxs0rka74/2+MTCOYDpa5+YQkR5lUqbnMuHklEhtaawu7d1XNJpWtmta+jKt8QkpvEXYDAAAsj2f15uv/Tp++1B0M6/Zrem8l0je8vXvlU6FHv6OHYoe65v0itP339KY2m2G39KyuHcb00KVWSCwFFeMx6aWrz/Y8zsoDX9WTj3+r2TP87h4h9ijr9RcaX+h13Rf5az30QJ/1RngdAAAAWExTb2ni7OS0umUU0UnT61F5KthR7W24zTYmXsFWNCclElFZBxUZU2ytnizKJCWvsNfctlGNbZWkZtW2JJVSwTIpnS6rnnfl6rJse1u12qoqpqiIJCdjaTvuqrq2LzsTU7XYqG13lLFSUsWoeGrl7gAAAJi+J7Sy8hW96aV1X2fVw8ondPftjp7eIe/dfkUKB76Rr+ruSklvRfwK57e8Hd0d+6fWCrdf03v6G71UKfceykpE0hNdi+9e6V7Wy7Dr9TUg4G8L94/5OgAAALCYpht4ewVt1/PaDeXKclrtPxJ5V9WsWuFyylIpnVe+ngs9rgQtScpar0iptm0jfgV5dE8bbnv/bCcT1cGWUTXpB8+pkoLK7khrHFZKSldUUcoPptsacKdVCbVfcTK2DptPVeTGt7UTqzYDaydTUy0IyA89KRmRkkWjpCQns6eNzapaQXpalUpaqZSler7zuAAAAFhkn/jMX+jlf0jqJ4dBv+2b39J95yXpCd3/wFd0zUvrvs72H7e/p2uvf0r3Px5eHlr//E917d1NPXIp9PTK53W3PD3Up0XK1A0I+NvC/Vl/HQAAADhVU21p4uzkpI21UMuOklLl9WbrD+V25CiibDVo71ExMsVsx+Nk97amotVc1G95EsmqarpvFpksBr21LT/slqRaLirLsvyvVF15199/smi0dRCVXfAkrSoeDY7XWDe0D0WyoUptBcG5pfJ6o1XJrnTZkhX0Y/EKtrbju1rbt2VZl6VdI2OKSiaLMsZoV5dlHdnyBQAAAHNtJaKV1/1wVytP6JHH/0lPpg70ZOog1IJEuu/SX+juw6Sev/qs3guWvXfTvyGlYt/RJzpu0HhfZFM6LOk1b0d3x57uaCnyO3rkM9K1576n926Hl/9Cb3lf1E+m3grkCb8tS+i1NsZ27fXwerP+OgAAAHCapljh7ahcSmvLdFRNN8LiSEyr2mtWQx8ttK2SWk9L20NsnOhTQd1Wsa1wNXZdWguO16vC2yvI3olpNy6VUpZUcZVPlJRLWaGbYqZV8UvLFc3VlMhLkWxVJts9vn7LAQAAsEBWntZDD3xSLz0X0WOfeVp3r0hveV/US7e/qicvhdtxPKFHHnf0mvd1Xal8Ndg2rt/9jNPsld1zv6//Oz12qftpnf+WHtH3dO0fPqk3bwcV5Yrr/lj7cd+6+km99LolyZJej+vN5v6/ricff3rk9d7zvqgrhwehgaT0k8bk+4H/1Dz23ZG/1iPeN/Vy5Su6LSsY23f0SOzrunKY0k9uB+sO+ToAAACw+KYWeHuFbdXzuyoeveopcZSxD7VZ7X2TSCdj63BzV6qvKhaRDlVSyiqF1kgov9m+TbpiVEx6KmyHw3FPBXvH/285LreS1uXD4PhWSiV1S9PLGwAAYOHdd8nR7179uq489x1/wcq6Pv14j7B25Xf0iUt/rU/0CrB77vef9OSAde8+/7QeOf+0HjnBPkZd7+7IX+vJIbv23R35lh6NfKtjaff2w7wOAAAALL4ptTRxtJNb1dZYe1OXVG7c99IraLuU0MbaCPv3DlXv+6Sjcn1Da9rXnuKKKqJs1cgYV/lEWhVjZHq0TRksomwxHK4nVTRB25NKOugn7j8m7AYAAFgGfpDdaGXy5OP0pAYAAABGNZXA2ytsq5Re1/A5bkRrGwmVUo3e152PJSktlYOe2tGcVitBAO0VZFu2Cr2aYCeLqmYj8gq2v82GdDnoyV1eDwXYTlml1ZjcUM9xJ2OpeWgnExqHJB1qf6+mUsqSXXDV3u87uAEnAAAAAAAAAGCsLGOMGdvOLEvD7C5j2Yq7o1ZED+IoY5W1HuqpffQmGVnBnSZ79fF2Mv6NKNMVo81DWzuxXcW3dxSrburQjupgI696Lqdao5e3k5G1HVd+NadcKaF88/X5LUxi1faWJs3HTkb24aa2DqKtG192SuTl9mm1AgAAjm/YuQsgcb0AAAAA4zDpefVUAu/xO0bgDQAAlh4BJkbB9QIAAACcHIE3AADAhDB3wSi4XgAAAICTm/S8eko3rQQAAAAAAAAAYLwIvAEAAADglLxR+KwOnv3ltIcxe65+Tbrx5rRHAQAAFsBd0x4AAAAAAIzbG4XP6vWb0pmn/pviT/z2tIdzbIvyOmbezUM9c/NjeurS2WmPZIHc0vM/elW/Ch59NHJJT0XOTHVEAIbF5xfzjR7eAABgaTF3wSgW9nr59a4Ovi/Fs5cX7rgfPPtlXdO35j4oXpTXMbvu6Pkfvap7PndJ8ZXGsnDYc0arn7ukuG7omZ9f179Iks4p8YWYLjRWv31Dz1yVnvrchc6dtxt2vWHdvqXnr76qX90OHq+c0+rK+7qx8vBMhVPvelf1vMYwpqPO3+3wexSyck6rl2Kh93fBjPu6mnt8fseJzy8mYdLzaiq8AQAAAABL613vVf1q5WPaaAtTzurRz13Uu23hzAU99YULOvj5VelSKCybmlt6/uqvdM+lx5pjf/fmoZ6/ekeKTHdkU7NyQU994SN6/ke/0YVQoPnuzUM9//OrUts/amBx8fmdS3x+MUYE3gAAAMAUvfODz+raVb9lxUP6nq4980PdkST9nu596lt6KFzV+8qf6YX/+kNJ0r1/9IIe0J/p2n/11z9z6Wt66A8v68ONdX+9q2vf/67euRk8Pv/7euBLf66P/1ZjhV/qjcL/rNeD51/4xndbxzn/NX22o/L6nR98Wdeu/vfm4zPnf18f/9Kf697fUrtfP6dr3y/qnZuNdX9P9z4V0QcvPRRUc0/muB88+2dd5+4Bje6DZ7+sV55pHe/eP3pBD923q4P/67vBviVd+r/12T98PHi9R51nSXpO177xx3qn8RoGtCcZ1+touvOM9OoP1Rz8mc9KekF68LtSuHvH4X+U3n699fjMZ6WHL0vhgr5bu9KrL/j///B3JYUen/t9KfaUdOM/StdD+3n4u9KZZ6SrP2wtO/e/S7FPS3pJuvKfW8sv/h/Shfv7vI6XpFcr0p3Gvh+QLn5c+s3HpUtPjfY62nesGzfv6KPnz/Vb4Qh3dPDzq6oHFZp7P7reemrlojaaYdtw6924ekW1m377gEd1Xc97bwfVjmf0YORhPRqusLz5G/1K7UH9PedjejRyVc93jPLG1auq3WxewfroyjnFL8V0IRwe3TzU3tW3JUkPXnpMcR3q+av+8T96/qIevXRB8q7qR15rPw9eekyPrnRUZZ5/WBsjtoY5enzDnufe7jkfU/z8Fd24LSn0moc6LwoCN+9t/cttqfFexPWqfy7OP6wvrPzK///QWN5tnqugwvgYx9XtG3r+6vW2CuAH9bYUeUyPnj/5eelpiOvgnhFfx1Hnb9TrZXz4/C7D5/eoz9FI71uf/bVVoDffi3NKfO5jutGs4j+jBy9dCj67w49v5NcLnxmjMe8OAABgopi7YBSTvF7u/PRL5pX8l8wrf/V35k5o+a2ffsm88tNfdK1/668+Y/4+/yXz9/k/Na/X/efv1EPb1v/UvJL/y7Z9GfMLc+uvvmT+ud6xs7f+0ryS/8ujx/dXf2fuvBVaVv9L80r+T82ttjX/zvzzn3ypOabmcX/6JfP3nccY43Gb63Uc85U/+UzP83e0X5h//pPO12bM6/nPtJ+/Uc5zeKx9xjT+13HTmNq3jXn7ZmvR+zeNefE/GPN2aLXr3zbm1X805v3Qsrd/bMyLfd6fV/+DMS9+23++se+3/7HjuD227Txu2PVvG3P9Zp8n/7H7dZib/jYv/vj4r8MYY/7tuvmx86J55d/6PPez612LX/lZj/X7rDvsPsP+1X3R/PhnL5ofv/i2+dfQ8uvui+bHbtuLM1ecmrnivt+2Xs/9vfi2+dfQmP/1jevmxz971fQayfUXa+YHP3vR/OBnr5pX3ng/WD88lvfNFad721d+VjNX3hgwhraxH3N8Q53ntzvG97657r5oftAx5mGP6489fOG+b667r/rvUfg1DXm9DP963zdXnBfNlTfCx3jfXOl1noe9/kZw1HUw9vM3bnx++fwG2w/zORr6fXvjVfPjn13veM/eN9dffLHj/L1trjgvmh84L4beB//nzfV/a9926PGNcB3Mg0n/HjbWCu+3L0R062J0nLtcamevu9MeAgAAAE7JnfOZVtVw4N4nvqV3vvE9vfPEn+vejvXPfDqj+BOt9T/8qdb/v/ETT/d+6c9b1d6SpN/WvZ9/Sm98f1f61Ch9s5/T689E9PFvP962vw9/6rLi+jO98IPnmuN+5wd/rA+e+m966FPh6uXf1r1P/D/67BMjHHKk4/Zazz+m3vqs3hj1sMH2Dzzl6dqzv9S9jUrsX+/qHX1N8U+11pr8eT7p63ize9GZ+6VLoap6vSRd/7j02Kfb1zv7lKRd6fCloBq7w8dS0oXQ8rPhde6XLr4h3XizVbF95xlJv99eVT6kWxf/F5298nPpbLj6+37pwp+o1ZfgmK/j9vv6F32k/5/J377eXo0oSTqj1dFfxkj+ZeXBrirLC5GHdeNH13Uj0vhT/7N69HMP68B7Vc//6I5fkbhyTquRi4qfb1Qk3tKB9xHFv3C2WZUrSfecv6CndKi9q7d6VnN+9PyDeipyNrR+eJ0zikfe1/PeHV1oVD7evqEbuqinOisXj3S88R3tbdV+dKX56KPnH9YX2o4x7HHvNNdrOaMLkZh0+4oORh7XKK/Xr+QMr6eVM3r0c4+NfNTj6n8dTOv8jYjPb7D+sn5+pVE+R8O8bwfe+7pwKda+P53RhcjHdHD1hnQ+XK1+x6+2P98a34WV3+jdtm2HGd+kzvNiG2vgfe6Gt5g38gEAAAAm7Mx9vVpc/LbOnPf0wa8ldbTw+PB9j/dYX5Ke052bke5WI5L0W5/Qh2/+v3pH6grQ+/r1a/pAP9S1b/yw9/PnH5IUCt57vo5jGPa4v35NH5x/qOfrOXPf7x378B9+IqMPh/6x4Z2fflcffvKF0BoTOM9jfx2flh5+UXr1/wzt7AHpY/9bKIi+KekF6coLPfegMx/399PpIz2WhV1ISVd+JF0IQv/rP/TbqBzXR/q0Omk47us4So8/tz/4+dXR9zOij6706sFyRvesvK93w3/Wv3JW8UtnFQ8evnv7lg6uXtUzty/5+muy6AAAIABJREFUN5i7/b7e7QiP2qx8RL3+FeKelcHhyT2RB3VPKAS64V3XPZFjBLHHHN/RWjcl9Ntp/Erv3j6rexrnbdjj3n5b7658pGe/53t6vkdHGOn1ntWjl36jZ65eVb35/Bk9eL5Hi4UJ6XsdTOv8jYrPb09L8/mVNMrn6Oj37Zbevf2R3i1EVj6ie27/RjcU+ndYndOFI/8RYYjxTew8LzZ6eAMAAAAz4M5bv5TUGRb/sn+o2tfjOnO+2DMkHxSq9vVb/6M+rGv6+Le7q8x7+eCtX0qfGkPoPexxB4TLd97679J9xx3A47r30h/rjWef1r2r/5/euPk1PfSH7c+P9zxP6HWcvSw91qg0f1O686YfgH8k6OF95n+Q9EZonXH5tHTuP0s3viCd+0fp/eNVdze9/2ZHhXeH476OlY/oo/pNewg1A/7ltt/7ud2dtrDlxtUrunG+vcfrPStn9WjknPZuBtuvnNM9el/xL4z7Jn1ndeH8qzrw7ujC+bd1cPtid1/aYUxsfC33nI8FVZA39IXPBf2nhz3uyjndc/t6R4jle/f2ndGvmVFf7/mYnvpC48EdvXv7jg6uXtXzK48d73yPywTPX+O+Fm33SpgzfH7H50Sf34YhP0dHv29ndc/Kr3r/vLj9ft9/3Dnx+E7hPC+iD017AJicWxejtJgBAACYE2duFnXwg+f0QWjZO89+Ux889fRowamkjz8Z0Tvf3/XD2IZf/1JvfP8ZffjJHoHgzWt6p7Hur5/TtcJn9cIPngsW/LYe+iPpjULH/vRLvfPsl0PrSfd+/mvSM9/UG6/8su247zz7Zzr4xpf/f/buN7at+873/Ce1jeoPS9mULTG2/tgZxurSRk3UFlbOegu3m5FduPCDYurZm/bewsGOBxgv2rmDBXbHQFEUQTV9sLg7La4fNAPEaGea3rgXvYBRI5Ju7sZotJbuyE2OCpuIbdaORCambIs2GVJSEAXaB/x3SJEij8T/fL8AAxF5eM7vHP7E/PTRV9+TPkZJj/sV7R726UHGtYtv82CThXzx83lND/7fn6nlxe9mtS7ZwHVeVxnOI/AT6c54+oaV6k78M+uWBiQZ5u0kaT7x+j9u8OCSer8h+UcT1d3Dhbdfj/+SFDK1aFmalwK/kCZ/khj3Bs/D1qkeW/zGlZsWXYzfVE2SoiFNTUzqshHa0Hbbo3MaN0IZf/oe8N1WxNWbEXjMGYa8GWNfUiC4oL5UC4NWDXkk70QgHtKYt/MZucdXpB5Xr+Tzy+vzy+7qyfoT/2JtYHzFXmcz5369YPNrKnXDvmKPG2//4PWFsra5I280RzVo9LG8if1FEmO7mbH/4s834jN02TBv1yq7WvNf541clw0r0/XTrJaDkvRF7f5ahcNuvn83oNa/f619HxXzvrldbQoYWceNLslrPJbdZT2OLm585ZsHjeyZ1RL2IHnmmWdoaVKDkqE3PcEBAMjE2gVWlHO+LL/9bd3TiJ7rek33/uV3ibzui9oxPKLnvpqulk5VvmVzfk+Hv58VsD76he69/jM9CSa3+YZ2v/QjPZujWnz57R/q3rj5uH+t576aGTYs3/qFPnrLtL882+nR73Xv9Z/rSfD91HatnmE997XvqiXr2KU87tp9jWi3LujW+PubqhSMX/Nv6MA/ZPfqTp5v4eu8/Pa34+PIJWtsJT2PwE+kxS9Li78zhcC7pV5TS5Ok0Lg0l71dVp/uO9+TFnIcp/UbkidPoH3ne9LC4dyV14GfSP6Pcr+u839L9dwuVRFPvp+HIj5Do8Gdma0Pgnd02UiebKsOHvPIrYDGJ/zxXruS+jyZ1YER3x1N+RYSz7eqz9WnIdfasvZC20V8hqY0oCGbX1OGebvMP8EPGJMK2Aak4G3NmcKSPs+AhpyZYWIkGJDX58/cLuu4AWNS14NaK0dbiMzXdOrkyeyetonr6svziwTnQEbP2WLGl97vOtcvmvkeZRwn+ZzpsWKPG2+rsKCn0eQ2A3LrtqY0EG89kWtsiX7M8hm6GZW2uzypbYs5bsRnaCq6U/Zo9na5W5oUO/8KsTIPSn399OgX8v6Hn2lps9XdfP+mNfn3b7HfR8W+b8mxTBmm/dk6ddCzP30viFzzzxbS1OhtzSUeTX4eWPk+t3Kd60G5fw4j8G4iBN8AAGRi7QIrKhF4u79aov7XQAMJ9T5f5p9hQpoanZP9mCf/zSsrKBm8DFeoTzM2hvdpc3Jdv/gvB6Xdf/ernL+crQfMi/rE+1Z55f45jJYmTcThvyuH/y6tTgAAAAAgxaEhT5tu+vizcKCalh6+L3n+um7DbgC1gwrvJmYOvan6BgA0I9YusKJc82VNm5I6vlEXUA7N9Jeqa9oSZLUOQPXxHm1OI1+/Rj63Rsb7Vh20NEFFNNMiEgCAJNYusIL5AlRHsqVJ+VubAACASqClCSqCdicAAAAAalny5xUAAID1UOGNnKj4BgA0A9YusIL5AlRerqpuKr0BAKhv5V5Xby3bnlHXkgtI+nwDAAAAqCW0NwEAAOuhpQnWlWx1QrsTAAAAAKgs78Skxn1L1R4Gqox5AADWUOGNomVXfVNRAQAA0DwCxqS8No+GXa0VOd7y29/WrfH3Jef3dPj7363IMVFISFOjtzWX+Gq7q3LzIRtV3gAAIB96eGPDCL4BAPWOtQusaPr5Eg1ofGJR7pP71VOK/T36hbyvS+71wuxitmk00ZCmjNuaiya+tnXqoG1RAdtA1cLlXCI+Q1MqwZiiAY0b0vCx3LMq1Pu83vqnX+Z9+Yt/9e/q6+eRAufbUIJ3dNlYyPlUn+eohpymB6JL8vpu62YwUcVsa9VB14DcztaC+5Kq+8uXDWm4eRDS1MRtzalXZxrmnACUEz28UbOo+AYAAGgith65nZPy+pbUU0/BUl0JacqYk91zVGds8UciwTuaMpYkV3VHVk1nTg5oavSxerJ+2RLxGZp6+486QqV3bXLu15mT8f9c9xck0XhYGnEO6ORJh+ySIsGApgxDgWSQ7dyvMydD+edBJc4HeUV8c5qzDeiMx1HtoQCAJAJvlAA3uAQAANgkU/Vin+eo3LqjKWNBTyVtd/ZqyNMje2LTgGHoejDdy3W7rVNuz3712LL2GQ1oyvBnVAr3aUFyxSsrA8akrgfjlZFD8mvKFz+e1Ko+14CGcgRTPc5OXTf8irj2p8Zj3awe/PSb+igY/+oPf/+z9FN52pcsv/1D3Rv/neJn/UXt+M6v9NwB0wa3fqg//MvvJEk7vvMH7dYPde9f4tu3er6n5/7yu2pJbvvoF7r3+s/0JJg85je0+6Uf6dld8S8f/PRwamw7vvOH9HFMx5Dn/9Hhv/xK3v3t0O+kF/+QOcZiBB9rTjtTYbck2Z37NeRaG+gVNQ+KmFfyGRo19Qbu8xzVkC2g8Ql/Yj5IcloPsgqPb0neCUM3E/Pz8qg//WKbtSrRZHuTO//0y0S7lU69cHK/eqKm87D16uSx9PdRvJJ+TnPR5Bhb1edqUyTYllF1W+g8iv8+snK+FlrH5Pg+P+jZL3fyOqfmQKdeOLZTgdRfD7Sqz+PJrLKukoDvtiJZ52h39mj4mDQ+cVtepyd9PgWZrx3zoJLzYLuNX4QCqB20NEFZUPUNAKgHrF1gRSXmS8CY1PVoq6Q2HXT1yu1sVSQYkpyJqkefoalon4ZcDtlTFcABTfkW5T5mrnpc0tTobckzoKFkS4DokqYMIxV4K7m/oCRbn4Y8jnSo7jPkzVWNGQ1ofOKxeo5ZCaDyKLalyX/4mZac39OBl76rll3S8q0f6t6/+PTs3/1KO3Zlbv7kjcO6F/yiJJd2v/iynj3Qr+Vbv5cOfCUeeN/6obxvPafnvm8KwDWrJ29c0JOD6RD9wU+/Lb30q1QInn/Ms7r39xek74zouQP9iW1mde/1b24s8E4EXHJ55Ha15v2lQvHzIK7QvIrPF/+aylnvxKQirqM5w7D1KnYtja+IliYO/383VfbmrvJNbhv89W8UsPVpOBHQBwxD16M7M0NOhTQ1Oie7x9QyQ0sK+G7renBnKnQs9jwsfR9ZbGWxbmV08I7GfW0ayji3JQWM2wo4zSFm/HznJB1MnHO8gvqx3Mc8a39ZVgb5zyP/+yll3zsgVNQ8iIfKt5kHFZwHJWtxBKBplHtd/bmy7RlNzeG/m6q0MFd+AwAAYH3bnX06c2x/KoCxp0LJkLy+Nrk96dAl/nyPhl3SdSNk2ku8EjEjMLW1aujY2vDyaSIUMm/b4xqQ3edXIHtwtjbZtaRINPuJMnJ+Twe+Hw+7JanlwI+0wykt59m89Ut/rcPf/5GeTQTQLcmwW9KDt3za8ZI57Jakfu342rCW3/pF6pEdX5KWHkrxavTD+sNPE889vCd96bjptbPxY5p3t6tfz31/I2G3JDk0dGxA9uhtTY1O6vLopC5P3JHXVFlqbR6k5Z9X8TNwuxblNVV6KxpQQL0bqPzc2PgKW9D10UldNlW8ZnP478r5b74lt+bi180w5FWfzmQEgVLAuK2IuT+0JKlVPS6PqcLW2nlY+j4qEa9vUT2enqxfjLSqx7VTEV/2UZfU5/GY3v8e9dikSJnGVrTooiK2trz3BbCvqRouPA+kVrmPeZgH9TQPAKDEaGmCsqLPNwAAgDV2W57WEdFFRRJhT062NknJ1zo05HmsccPQzdTzrepzrm1VkvvP0Ftlty3Gg+0KVH8W0lJ4k/S2XV/J88zvtRR0rakKlyTt2qeW4H/TE0k7JLV0ufTk5u+lrvt6om9ot8b14NF31XLzd2o5+CPTC7+i577z3+T9l2/qo+RDzi9qx5dG9NxX+y2M2sTmkNvjkDvxZSQaktcwNB5NVLlamgdpeedV8nlXn+yjfgVc8YrVgM8vu+uo9fFvcHyFJdpTJCp783H470q9z6vv17/UzWinTh7Lfay1QWoWi+dR+e+jkCLRttxVubY22aOPFZBMQXKnemqgfckaOceaFokuZV274uaBJPV4BtQ3YTAPVM55sCSvcVs3g9ILx6juBlA7CLxREfT5BgAA2CRbp+xalDvPn/6v4dyv4ZPJL5YUiS7JaxiasmVWeT+NLimrRjmxfY4QJbqoiFor0gKh9L6iVufPtfxI0ppWJfe17HxOO5JfH/hftOOt+1q+OS59aUQ7dEH3bv5eO4Lf0I6/zHrtgR/J/Q/JEHxWy49m9dHr39S9LutV3gFjUgFn5vtjtzk05OrU5WDifbI6D4rmUI/zdvympM4FeaMbqe5WyccX/5nBXEXr0NDJdQLzaEh3fv0b7f8335J7+qpGR+/ohWNre9xHcs57E4vnYen7qCQcstvmcoeoBaqmC3nyxmHdM5TZq75sTPMuRwslb7BVPTmD1MLzYMqYU8Tp0Umbn3lQNq1yezzq8RmaCnJDYwC1g5YmqKhkqxPanQAAAFjVqiGP5J0IZLUUWVLAZ+iy6U/rIz5Dlw3zdq2yK3dP6O3ROY0boYw/aY/fRK53bVASXdRTlTC4Cd7Tk0eJ/370e9376WH94Y3fl2jnaz37oktPXv9FPPROejSrB6+Pq+VFcy/xr6hV93Tvj9KOg/1qOTgs/fHneiJTKC5p+e1v6w9vmPfXrxb1rxefFTRnGFktTJYUCC6oz5kM94qfB1b1uHoln19en192V3aLhGJtYHzRRQWS20ZDmpqYLO48ogGNm7eLhjRuzEmuATn8d7UyeEpnjrXJO2HIaxpL/DxvZ17n6JICvjsaHzUSY7F2Hla/jzZ0vlncrjYFjKzxRZfkNR7L7tpozDmr5aAkfVG7v1busDuuxzMgu8/IuH6RYPxGk3INFL5fwDrzYNjVKrtzP/MAAJoMN61E1dHuBABQLaxdYEU550vAmNT1YI4nbL2mXrJxkWBAXp9fc6Ywu88Vv6FaahufoanoTtmj2dtltjRJ3mhsyObXlLGgp3m2M48zfQO5zVt++4e6N/67RMfxL2rH8F/rua9+JfHct3Vr/P3Elt/Qc//wI+3Q73Xv7/+9niTPaPi3cn+1P12Rms35PR3Ovinmo1/o3us/05Pk9XZ+Q7tf+tGaG1Quv/1t3frjcLx/uKQHPz2sJ1+KH8+8zb2Hw2oJmvanL2rH8MZamgSMSQVsA1Lwdub7Zr75aEIx88DKvMp8TadOnty/JvCO+AyNmvt8mzkHdMZjmoNFjC+93zua8pnnn2m74B1dNhZyH9N83IztWnXwmEfO/+F53finXyb2K/V5TNXziQrguehS6jXbnTs15OrJ6NVc9Pebhe+jdc9X1q6zogFNGabx2Tp10LM/HRLnuC5uW/zmqMke2Ntdpu/p5I1iS1Hdvc57l/FeSPGA1ndbN5Phs61VB839tTcxD9yKh+fMAwvzwCJuWgnAqnL/HEbgjZpB8A0AqDTWLrCiEeeLpZAiGtD4RDlaaQDlE+p9vuw/XzRS2Bf/RZO0++9+teaXQFhfI80DqyI+Q6PRvswQHgDWUe51NS1NUDOyW53Q7gQAAKB2BHx+Kdef5QM1LPnzBYqz9PB9yfPXhN2wxO7qU1/0ti5PBKo9FACQRIU3ahxV3wCAcmLtAisabb6saXeR/SfyQAMpV6U330eQmAcAYBUtTQARfAMAyoO1C6xgvgD1rRLtTQAAQGEE3oAJwTcAoJRYu8AK5gtQ/wi9AQCoPgJvIAdzHz4WrACAjWLtAiuYL0BjIPQGAKC6CLyBAqj6BgBsFGsXWMF8ARoHoTcAANVD4A0UieAbAGAVaxdYwXwBGguhNwAA1UHgDVhE8A0AKBZrF1jBfAEaD6E3AACVV+519day7RmokuSCleAbAAAAAAAAaC5UeKPhcYNLAEA+rF1gBfMFaExUeQMAUFm0NAFKiKpvAIAZaxdYwXwBGhehNwAAlUPgDZQBwTcAQGLtAmuYL0Bj21Tofeeizv/2/ytq0yPffF1n95f49QAA1BF6eANlQJ9vAAAAYOO8E5MKOD0adrVWeygl4/Df3Vzo3fW/6gcvn5Yz7wYfaey1/0Mflev1AABAEoE3mlx28G1+DAAAAEAtCGlq9LbmEl9td5UhaA/e0Xhwp4azQu+x117SlYfSnq/837qw878kqrD/J537v87rUGlH0NCKvY4BY1JeW2P9IgUAUHkE3oAyQ26qvgEAAHKIhjRl3NZcNPG1rVMHbYsK2AbKG05FAxo3pOFjPeU7Ri166NVvXpe+9bfuao8kJ/exoyrJyIp6fx0aOnlUQ5IiPkNTpThuhiVNGYvqOeaIH80Uejt3SnooPbtzt9TZqz2SPuzqJey2qNjr2OPqlXfCr4Brv5rsOx4AUEIE3kAW2p0AAABkC2nKmJPdc1RnbPFHIsE7mjKWJFd1R9aontwMSF86Wu1hNIWI77bmbDtTc1tKh97db/yFJGl3p6TO3XpW0oc7d+fe0cP/pFd+8p8KHu9Ivic2+/oa1r2zX1IR19HWI7dzUl7fknqo8gYAbBCBN5AHwTcAAEBC8LHmlBkI2p37NeQyV9ua20606uAxj9w2xSt4J/x6KknOAZ3xxKtoFQ1oyvBnVIz3aUFyHdWQU5KW5J0wdDPx/OVRf/rgtl6dyaoIDhiGrgeXUl9vt3XK7dmvHpuk4B1dNhZSVek3g0va7hzQkPOxpowFPVWr+jwDGnJuNGD7WPd/PakbRlghSVKH/uzEUb34tS+ktnj3H3+j6QeS48RJfetrX5AU0Fv/56T+JPNjkm79d/38l8nmHaP6+Vj6KBnbFRAwJnU9GG//MSS/pnwL8fdArepzDWjIHCYmr4+kPs9RuXUncV2k7c5eDXl6ZJdUVGuR1L469cKxnQqk/iqgVX0eT+K9lay+vwUVfdxsSwoEl7Td2bnmmWTorfN/q0OdkrRbu7ukPfkCb3p4F9BT1HXscXbquuFXxLU/Me/y+b3u/f2/1xN9UTu+8ys9d6D0IwYA1KdnVkt4S0zuXI9GRp9vAGg8rF1gRXPPl3jQKZdHbldr/hAqGtD4xGP1JMPupOAdXfa1mULMpfj+zCFzdElThmEKvE37LNDyIuIzNBXt05DLIXuqAj2gKd+i3McSrRESwbtc8RYs3glDN9WpFzz71RO9o8uGdPJkoYAth4cBvfW6V44/P6p9B76gHZL08GO9+/qk/vSloxkB9bv/OC69NKwvd6Vffv/Xv9GfvvQtvZgR1n2sd/9xcs22VkV8hqaCkmx9GvI4UucW8Bnyam0rmoAxqevRVkltOujqldvZqkgwJDkda65LvLVIvnY2IU2NzmlO0kHPQGI/AU0Zj+U+5on/EiLJYsuakh3XfPxcc9a8183cyBLWFfGexBF4A0C9Kve6mgpvoEj0+QYAAM3LoaFjA/L6bmtqdCleKWzrTIWiKbYeuZ1+XTcCcpvCba9vQX2u/ab9xSuxM0JUW6uGjm2khUdIXl+b3CczQ1m7s0fDuqPLRihdVW7r1bAr/t92m7Td1psIQdu0XYuKZI+pCO++/qH+7G+Htc/8YNcX9OWXevSn1/3S15KdrgMKPejQn2UF2E/mO+TYlbXTh379ST16cRNhd9JTW1/6/BN6XAMKjObuk7zd2Ze6RpJkdzq0MUvxanFncj896rE9VmSDeyvbcaOLeqq2dYNVR9aNLDPd0KWf/AfdWPN48oaM5X6+AdnaZNeSIlFJ6wbeX9Fz//CHCg0KAFBPCLyBDaDdCQAAaDo2h9weR+pGhZFoSF7D0Hg0s61Fj2dAfaO3NRXsiVdqB/26aRvQmYw+DQ4NeR5r3DB0M7X/VvU5s1ptFCO6qIgWdH10Ms+42yRtNLQt4KFXf+reo2/leu7Rxwp17zFtG9GTZ7+QGYw/9OYOthOv3VGCIW635bqerbLbFnMGinZbqa5Vp3ry9+Yoo+oc98g3X9fZ5O90Fq5o5J9MLVrUr9N/9Q86keyacueizv+2tK8HAABpBN7AJhB8AwCAZhAwJhVwZrYasdscGnJ16nJwSZI5VHXI7WrVqC8gt7NTAd+iDnpyhKjO/Ro+mfxiSZHokryGoSnb0XX6Ledg65Rdi3KfXFutXD0f693/GtbgS/9j6pGcN6HME2zf/+OcHN1ulcLTaPb7I8Wvd1vuFh/Nxtam7XpcsJp4/SpvlFR0URG1Fpyfy29/W7fG35ec39Ph73+3MmMDANSFz1V7AEAjcPjvphbByX8AAACNZM4w5DXdFDJ+s78F9eVoeWF39akv6pfX8OumrW9Nu4iIz9BlIxAPGSVJrbJrvd7giwokt42GNDUxqctGKPXaIY/knTDvLzE+n2HabgOCdzQ+OqnLo4a80RzPd/Vqx7xXb936OPXQk4cBvfWP8f7d5v7bT+fDphd+rCe3vPrNf52To7tjzW6fzHdoR/cXMrf9x3G9+9Di+CRtj85p3AhltPQI+G4r4uqtnV8QrPv+lpmtUz22+I0rC0ndxLJW3bmokZ+8pPM/+XuNLdTgdsVKtJkpFHg/+eP7kr6o3S8RdgMAMlHhDZQQfb4BAECj6nP1JYLq5COt6vN48lRjJ6u8F3XwWO4WGdsleY1JzZlC7z5Xjv3ZejTkuqOpiUldT203oDOmPtNy7teQAjn2l+hfHbyjy0Y8ibs8+lgHj3lkl/TUZ+hydEBnXJK0oOujhg4WvFGe2Rf04ktuvfX6qH7+y8RDz/Zp8M+P6sUDX8jYct+XDujGL0f18zFJ6pDD49YOSX8aG9Vb3Zk3rdz35x360y9/o58nvnZ4DujIS8Pat5Ge3s4BDdn8mhq9He+9nrh+5jY0AWNS14OJL4KTmks+Yes13Wg0/ouKUZ85GDZ02Zc+Tva1nktdz/hNT+ckaWJSAZepDU4R729ZjpvSqh5nq24GFyRX4V8BUOldfoHggra7POv303/0Cz0JSq3DI3o2uwc+AKDpPbNawltiNved64HcCL4BoHaxdoEVzBdrIj5DU9E+DedqZ4KKiPgMTWkgR8iLTCFNjc7JbuGXHenQm5tWllQ0oPGJwi2Klt/+tm79cVgHvv9dtVRscACAUin3upoKb6DM6PMNAACaT0hen9STp7obqC3xm6he9oXkLvIXNOlK719L4qaVpRLw+SWXp2C7nZav/kqHv1qRIQEA6hAV3kCFEXwDQO1g7QIrmC+FZbTGSOjzWLwJJUpizXuRbP2BkqK9CQAA1pV7XU3gDVSJ+YY3LJIBoDpYu8AK5guAXAi9AQCwhsAbaAJUfQNAdbB2gRXMFwD5EHoDAFA8Am+giRB8A0BlsXaBFcwXAOsh9AYAoDjctBJoItzgEgAAAAAAANg4KryBGkafbwAoL9YusIL5AqAQqrwBACiMliYAJFH1DQDlwNoFVjBfABSD0BsAgPUReAPIQPANAKXD2gVWMF8AFIvQGwCA/Ai8AeRE8A0Am8faBVYwXwBYQegNAEBuBN4A1kWfbwDYONYusIL5AsAqQm8AANYi8AZQNKq+AcAa1i6wohLzxTsxqZvq1AvH9qunrEcCUCmE3gAAZCLwBmAZwTcAFIe1C6yo1HwJGJMKOI9qyFn2QwGoEEJvAADSyr2u/lzZ9gygahz+u3L47yrU+3xGyxMAAFAfItGlag8BQAkl1+YAAKD8tlZ7AADKJ1lFQp9vAAAAoLqSoTfrcQAAyovAG2gC5kU17U4AAKgD0SVJrdUeBQAAAFB36OENNCmCbwBg7QJrKjZfoiGNT9zWU1uvTh7rkb38RwRQQVR5AwCaHTetBFBWBN8AmhlrF1hRyZtWejWgYY+j7McCUB2E3gCAZlbudTUtTYAmR59vAABqkI12JkAjo583AADlQ+ANQBJ9vgEAAIBKIvQGAKA8PlftAQCoPQ7/3dQC3Fz5DQAAyi8iyU6FN9AUkmtuAABQOvTwBlAQFd8AGhVrF1hR/vmyJO+EoZvq1AvH9qunjEcCUFuo9AYANBNuWgmgZhB8A2g0rF1gBfMFQDkRegMAmgWBN4Caww0uATQK1i6wgvkCoNwIvQEAzYA5rEgoAAAgAElEQVTAG0BNo+obQD1j7QIrmC8AKoHQGwDQ6Ai8AdQFgm8A9Yi1C6xgvgCoFEJvAEAjK/e6emvZ9gygqSQX5ATfAAAAAAAAqBYqvAGUBX2+AdQD1i6wgvkCoJKo8gYANCpamgCoe1R9A6hVrF1gBfMFQKURegMAGhGBN4CGQfANoNawdoEVzBcA1UDoDQBoNATeABoOwTeAWsHaBVYwXwBUC6E3AKCREHgDaFj0+QZQbaxdYAXzBUA1EXoDABoFgTeApkDVN4BqYO0CK5gvAKqN0BsA0AgIvAE0FYJvAJXE2gVWMF8A1AJCbwBAvSPwBtCUCL4BVAJrF1jBfAFQKwi9AQD1jMAbQFOjzzeAcmLtAiuYLwBqCaE3AKBelXtdvbVsewaAEjAv4qn6BgAAAAAAwHqo8AZQdwi+AZQKaxdYwXwBUGuo8gYA1CNamgBAHgTfADaLtQusYL4AqEWE3gCAekPgDQAFEHwD2CjWLrCC+QKgVhF6AwDqCYE3ABSJG1wCsIq1C6xgvgCoZYTeAIB6QeANABtA1TeAYrB2gRXMFwC1jtAbAFAPCLwBYBMIvgGsh7ULrGC+AKgHhN4AgFpH4A0AJUDwDSAX1i6wgvkCoF4QegMAahmBNwCUEH2+AZixdoEVzBcA9YTQGwBQqwi8AaBMqPoGwNoFVjBfANQbQm8AQC0q97p6a9n2DAA1Lrn4J/gGAAAAAABoDFR4A0ACwTfQfFi7wArmC4B6RJU3AKDW0NIEACqMPt9A82DtAiuYLwDqFaE3AKCWEHgDQBVR9Q00NtYusIL5AqCeEXoDAGoFgTcA1ACCb6AxsXaBFcwXAPWO0BsAUAsIvAGghhB8A42FtQusYL4AaASE3gCAaiPwBoAaRJ9voDGwdoEVzBcAjYLQGwBQTQTeAFDjqPoG6hdrF1jBfAHQSAi9AQDVQuANAHWC4BuoP6xdYAXzBUCjIfQGAFQDgTcA1BmCb6B+sHaBFcwXAI2I0BsAUGnlXldvLdueAaBJJX9goM83AAAAAABAZVHhDQAVQNU3UJtYu8AK5guARkWVNwCgkmhpAgANhOAbqC2sXWAF8wVAIyP0BgBUCoE3ADQggm+gNrB2gRXMFwCNjtAbAFAJBN4A0MAIvoHqYu0CK5gvAJoBoTcAoNwIvAGgCXCDS6A6WLvACuYLgGZB6A0AKCcCbwBoMlR9A5XD2gVWMF8ANBNCbwBAuRB4A0CTIvgGyo+1C6xgvgBoNoTeAIByIPAGgCZH8A2UD2sXWMF8AdCMCL0BAKVG4A0AkESfb6AcWLvACuYLgGZF6A0AKCUCbwDAGlR9A6XB2gVWMF8ANDNCbwBAqZR7Xb21bHsGAJRN8ocNgm8AAAAAAIA0KrwBoAEQfAMbw9oFVjBfADQ7qrwBAKVASxMAQNHo8w1Yw9oFVjBfAIDQGwCweQTeAIANoeobKIy1C6xgvgBAHKE3AGAzCLwBAJtC8A3kx9oFVjBfACCN0BsAsFEE3gCAkiD4BtZi7QIrmC8AkInQGwCwEQTeAICSos83kMbaBVYwXwBgLUJvAIBVBN4AgLKh6hvNjrULrGC+AEBuhN4AACsIvAEAZUfwjWbF2gVWMF8AID9CbwBAsQi8AQAVQ/CNZsPaBVYwXwBgfYTeAIBilHtdvbVsewYA1J3kDygE3wAAAAAAoB5R4Q0AyIsbXKLRsXaBFcwXACiMKm8AQCG0NAEA1ASqvtGIWLvACuYLABSH0BsAsB4CbwBATSH4RiNh7QIrmC8AUDxCbwBAPgTeAICaRPCNRsDaBVYwXwDAGkJvAEAuBN4AgJpGn2/UM9YusIL5AgDWEXoDALIReAMA6gZV36g3rF1gBfMFADaG0BsAYEbgDQCoOwTfqBesXWAF8wUANo7QGwCQROANAKhbBN+odaxdYAXzBQA2h9AbACAReAMAGgB9vlGrWLvACuYLAGweoTcAoNzr6q1l2zMAAAnmH2qo+gYAAAAAAOVChTcAoCoIvlELWLvACuYLAJQGVd4A0NxoaQIAaGgE36gm1i6wgvkCAKVD6A0AzYvAGwDQFOjzjWpg7QIrmC8AUFqE3gDQnAi8AQBNh6pvVAprF1jBfAGA0iP0BoDmQ+ANAGhaBN8oN9YusIL5AgDlQegNAM2FwBsA0PQIvlEurF1gBfMFAMqH0BsAmgeBNwAACQTfKDXWLrCC+QIA5UXoDQDNgcAbAIAs3OASpcLaBVYwXwCg/Ai9AaDxEXgDALAOqr6xGaxdYAXzBQAqg9AbABobgTcAAEUg+MZGsHaBFcwXAKgcQm8AaFzlXldvLdueAQCooOQPRATfAAAAAAA0Lyq8AQANiT7fKAZrF1jBfAGAyqLKGwAaEy1NAADYJKq+kQ9rF1jBfAGAyiP0BoDGQ+ANAECJEHwjG2sXWMF8AYDqIPQGgMZC4A0AQIkRfCOJtQusYL4AQPUQegNA4yDwBgCgTOjzDdYusIL5AgDVRegNAI2BwBsAgAqg6rs5sXaBFcwXAKg+Qm8AqH8E3gAAVBDBd3Nh7QIrmC8AUBsIvQGgvhF4AwBQBQTfzYG1C6xgvgBA7SD0BoD6ReANAEAV0ee7sbF2gRXMFwCoLYTeAFCfyr2u3lq2PQMA0ADMP0RR9Q0AAAAAQG2jwhsAAIsIvhsHaxdYwXwBgNpDlTcA1B9amgAAUKMIvusfaxdYwXwBgNpE6A0A9YXAGwCAGkef7/rF2gVWMF8AoHYRegNA/SDwBgCgjlD1XV9Yu8AK5gsA1DZCbwCoDwTeAADUIYLv+sDaBVYwXwCg9hF6A0DtI/AGAKCOEXzXNtYusIL5AgD1gdAbAGobgTcAAA2A4Ls2sXaBFcwXAKgfhN4AULsIvAEAaCDc4LK2sHaBFcwXAKgvhN4AUJsIvAEAaFBUfVcfaxdYwXwphRmFr72q5cRX2/b9QI5+Z1VHBKCxEXoDQO0p97r6c2XbMwAAWJfDf1cO/12Fep/PqPwGgKLEgop5RzQ/PVbtkVhwSB3HL6r7+EV17ttTml3GxhQqcA1i0+cV8s5opTRHBAAAQA0j8AYAoMoIvgFYtTJ7SaHp17TSfkrdgyeqPZya1z54UW3tV7VwbUThR8FqDwdABSXXWACA5kFLEwAAagx9viuHtQusqIn5EptR2PuqlnVane4T2tqea5sxhb1XtBxLfN1+RC26Ie29qI5d6c2WvSMKP/ww9fW29iNqc59Vi3mfjy5p/tYNSVLLgYtq1yVFbt3Qp5K2dZ2W3X1Cmh3Rwv30floOXFRH25hC01f0afLBrnPqdh/KGObK7IgiejlvS5PC4wsqNv2KorEcL24/nfsXAanrd0Qd2ecKoKHR2gQAagc9vAEAaGL0+S4v1i6wotrzJR4ASy0HXlbHrnx9r4MKX3tNMm8TCyrsfSUj8F6ZHVEkdkr2/kOp0Hzl0ZgiH3yktsGzallz7PMKx/ZIela2vV9X+y6nVh7NSLsOaWvquG/q88czXxubPq+VrKA9ab3A29L4YmMKeSWHhUr3lUfx4F77zsnRf6jwCwA0BEJvAKgN9PAGAKCJ0e4EQLyS+bzCsWfVcfzCOmG3JM1LUiKETmh3qmPQHDrPKHb/WbW5D2VUiG/ddUKOvVLYO5Nzz9u6Tql78KzaE8ffmgq7Jcmp9n0PtDhrahcSG9MnOp0z7F7fxsZnxdZdZ+U4fk5bHr6q+ekxensDTYL2JgDQHLYW3gQAAFRbshqJim+gGTnVPnhRW7wjCl8b0SfrVngfUseBdxW69YqiyYfa96il62V19Kcrvj/TDYWv3VA41y7ad0taW/W8pW39Suit/ae05dqbWu6PV2Avz17Rlr0XizrDDBscnxXmCu9uKryBppIMvVlLAUDjIvAGAKCOZAff5scANLYW9wW19M8o7H1F8x+s04N611k5jp9NfBHUSmxeMe8rCrclqrzbD2mLPlLb8bWtSzbnkD7f9aoWZ7+ulp0zWoydlt29gd2UbXzK7OE9eJEe3kCTIvQGgMZGSxMAAOpQstUJ7U6AJtN+SB2DF9XZJS1Ojyg8m9neY2V2RPPeMa2kbuTo1FZ1Z1W5ONVxQFqcNm8nSUEtz45ofhMtQ1r6T0v331Rs9oq27D2xweqaDYwv9lH6Jp2xGYWnz6/Zbnl2RPPTV6W9P1D3IDesBJod7U0AoHFx00oAABoE7U6sY+0CK2puvsSCis2+pqhOqdsdb8sRv9njYW2JXUkHwNqjln2mliYJK4/GFPsge7tT6jC1+Fj2nlf4YY5jt59Wd56bRMZfc0Sdx8+uCbxXZke0cP/D3OfTdS51HsWOL73fS4rcv6FP82wXmz6vT9rPye4+xJ+4AshApTcAVF6519UE3gAANBiC7+KxdoEVzBcAaEyE3gBQWQTeAABgQ+jzXRhrF1jBfAGAxkXoDQCVU+51NX/RBwBAgzL/0EbVNwAAAACgGVDhDQBAEyH4zsTaBVYwXwCgsVHlDQCVQUsTAABQcgTfcaxdYAXzBQAaH6E3AJQfgTcAACibZg++WbvACuYLADQHQm8AKC8CbwAAUHbNeoNL1i6wgvkCAM2D0BsAyofAGwAAVFQzVX2zdoEVzBcAhQUVvvaatg5eUHt7tceCzSL0BoDyIPAGAABV0QzBN2sXWMF8aQYzCl97VcuJr7bt+4Ec/c6qjgj1ZWV2RAuxU+p2H6r2UCxg3q+H0BsASo/AGwAAVFUjB9+sXWAF88WiWFCx2dcUjR1W9+CJao/GspXZEUX08uaDv9iYQl7JUYfXwKrY9Hl90n5Odvchbc27VUhTo7c1J0lq1cFjHrkV0PiEX08lSZ164eR+9SQ3jwY0bkjDx3py787qdhtV1HyeUfja1bqu7mbe57Ze6F3cvAcAmJV7Xc3nMQAAWFfyB7xm7fMNwLqV2UuK3H+gLfvqrdIVm9E+eFFbZke0cO2qWg68rI5duUJTh4aO9SqSEU73aPhkj7wThuQxhd01otj5vDJ7Vctdp9Rdp2E38nP47+YNvYub9wCASiLwBgAARTH/kNfIVd8ANiE2o7D3VS3rtDoHz2prruAvNqaw94qWY4mv24+oRTekvRfVsSu92bJ3ROGHH6a+3tZ+RG3us2ox7/PRJc3fuiFJajlwUe26pMitG/pU0rau07K7T0izI1q4n95Py4GL6mgbU2j6ij5NPth1znIwX3h8QcWmX1E0cZ7z166kX9x+2nrVe+pcj6hj8Mv6xPtq4hruUcuBCxnXTrEZxWav6pOHHybOcY+2dZ1KV6Am99V+RLb2B4o+/FDbus7JvuvdxPXbsya4K+r9kNTSf0EtO2cU9r6i+Q+OqCPHNsVZknfC0M1o/KvLo/70U7ZenUmF5cVtFzAmdT0obXd5NCS/pnwLiYryVvW5BjTkal07hGLmc8qMYvcl22CeecS8r/95/8/DCvU+r7b375Zx3gMASoGWJgAAYMPqPfhm7QIrmC/riwdDKlDhGL+hn8zbxIIKe1/JCP5WZkcUiZ2Svf9QKmRceTSmyAcfqW3wrFrWHPu8wrE9kp6Vbe/X1b7LqZVHM9KuZIuBoMLX3tTnj2e+NjZ9XitZgWPSeq0dLI2vpK0d4i0zliXZDrycOM8xRW79QW2DFzJCx5WYMyOgjV8jU+AYi4ef2ndOjv7ueEipRFC3eEnzt6TO42e11er5mq/To3gQGz+GKVjN034kXuHtkdumgtuuUcR2EZ+hqaAkW5+GPA7ZE48HfIa8GtCwKfQubj6bznXd3t3M+82pnXkf6n1e+u2Fjc17AEAKPbwBAEDNq9fgm7ULrGjG+WJuZQTUuhu/frtg4D0a7dMZjyP12HpzvM1/N2+omalQ7+7E84mwNv8+3l0TTkuKVyY/+vKaMH3Ze16L7euHqmsC7AJBdP7A2+L4igi8l73nFX6Y58mM6vP4TTV1IDOkj02PSO74Nc/bYzt7HFlfx69h4iadsTGFpj9S2/GzalnnfEO9z+vTsf9coDp+RuHp5F8HnOBP6wEgCz28AQBAzaPPN9CYzN/bhb6ni66IfXRJoUT7BUlS+x61dL2sDnMgZ267kC1HW4Rl73l9sit3xWpaZoBV6DV5gz+r4yt5pevaEM4c/MUfmFHYe1XLsXTrCbXvkXQ4s9K1mOBvA+9HUqUrvGWsv4kkbbdlti5JzuvsYy97R7TY+7wWC+8ypcN/Ic8zh9Rx4F2Fbr2iaPKhNfM+qM90Q+FrNxTOtYv23ZLWBqxb2tavIN7af0pbrr2p5f7EvJ+9oi17LxZ1Phk2OL71tLgvqsVd7NZH9Pl1vr+TPba3/PZsznlv2Xrn+8/D2nbiL6Q8n4nmed9NhTcAVAWBNwAAKBn6fAPNq8V9QS39RfSw3XVWjuNnE18EtRKbV8z7isJtifC5/ZC2KFllWUqH9PmuV7U4+3W17JzRYuy07EWHbSZlG1+pBBWeviodeFmdu5zpH/gSAbdlGznfVO/rI+oYvFhTvYyfRpckZffrXlIk2qYeU9De4r6glvdPpc8jb0/mdHV3MX8Rsc3035/pksLv3mXel0RQW/75rD775iVtk2ntUa5578/xi8AanvcA0Gw+V+0BAACAxuTw301VXNEWAWgS7YfUMXhRnV3S4vSIwrMzGU+vzI5o3jumleSN++TUVnVnVeE41XFAWpw2bydJQS3Pjmjem7lPK1r6T0v331Rs9oq27N1om4ENjC/2UfpmhbEZhafPb+o81jcvSdralg67V2IzCnvXqdJel7XzXZ4d0fz0VWnvD9Q9WKIb90UXFUiWRkdDmpqY1GUjtKHttkfnNG6EFDE9FvDdVsTVqzU15AXmsyStzF7Vctcptben/7+X/c8+cVafjv1H2d83Pf7+O/r8b4f12ZefT/x/8n/WZ/82XlUeWuffRjTTvP/8++m1R7nnffI4UpnmPQBgw+jhDQAAKqIWK75Zu8CKZp4vxbQ0WSMWVGz2NUWVvpFf/CZwh7UldiUdhGmPWvaZWjskrDwaU+yD7O1OqcPUIiBvD+B12mzEX3MkdWO6jGPOjmjh/oc5X5fZU7i48aX3e0mR+8k2Lvm3W9ejS5q/dSN1LNvgBbW3x3sbLyce3bYv3pIk2VIhGfRtaz+itr27tXjrij7VEXUckMJZ+9oym7iWXefU3R9MtDFJHqe4841Nn9cn7edkdx/KH6oG7+iysZD4olUHj3nkVkDjE349TTza5zmqIdN0iPjuaMq3kHi+VX2uPg25HMpWaLuIz9CUBjRk82vKMG83oCFXdtV3lhzzuXDv7rhSznuroXfy+7Yp5/2/HVfbu/+x7PM+1Pu8NPaf15/3AIAM3LQSAAA0lFrq883aBVY083zZUOAN1Jhk4D1cKNwu0srsiBZipwrcvLC6NlIV3kjf65X67OIzEgCsIfAGAAANq9pV36xdYEUzzxfCHDSCUgfejWqjVeS1itAbAGoPgTcAAGh41Qq+WbvAimaeLwQ5qHcBY1LXg6YHnAM641nbFgXW1UMVeaXWGXxWAkBxCLwBAEDTqHTwzdoFVjTzfCHEAVBK1aoiT36WlfMzjc9LACis3Otq7qkAAABqRvIHxGq3OgEAAOVj9f/vpQrIyx12AwBqAxXeAACgZpX7BpesXWBFM88XAiIA9WS9gLwSoTefmQCwPlqaAAAAqDxV36xdYEUzzxfCGwD1rtKfY3xuAkB+5V5Xf65sewYAACghh/9uqiprIzfIAgAAqJTkmqU2BRW+NqJYrNrjAIDyoIc3AACoK/T5BlA+Mwpfe1XLia+27fuBHP3Oqo5oYxrlPFCfQpoava25xFfbXR4Nu1qrO6IqVVvXas/wldnXtNx1St3t1R6JFY3yudYo5wHUNlqaAACAuraZPt+sXWBFM8+XDQU2saBis68pGjus7sET5RlYGa3MjiiilzcfRMTGFPJKjipdg5KdRwnFps/rk/ZzsrsPUYHV4CI+Q1MaqFzgHQ1o3JCGj/WkHtpY4GwO7Vt18JhHbgU0PuHXU0lSp144uV+po+Q4bsbekmMosN2mFfW5O6PwtavaOnhB7XUVeKfx+Vw+fD6jUsq9rmb+AgCAumb+IZaqb6A2rMxeUuT+A23Zd0rd7kPVHg5qTPvgRW2ZHdHCtatqOfCyOnbVTtiDxrLx6mqHho71KpIRTvdo+GSPvBOG5DGF3cXsrQLrkmI/d1dmr9ZhdTcqhc9nNAoCbwAA0DBodwJUWWxGYe+rWtZpdQ6e1dZcgUpsTGHvFS0ne8e2H1GLbkh7L6pjV3qzZe+Iwg8/TH29rf2I2txn1WLe56NLmr91Q5LUcuCi2nVJkVs39KmkbV2nZXefkGZHtHA/vZ+WAxfV0Tam0PQVfZp8sOuc5WC+8PiCik2/omjiPOevXUm/uP30xqveYzMKe69qOZY89h617HtWnz3cbb1KMTaj2OxVffLww8S12KNtXadyV/YV+b4Vu11L/wW17JxR2PuK5j84oo7s9zYpGtKUMae56FLigVb1udoUCbZlVslGA5oy/JqLJr62deqgZ7/cNknBO7psLMQfsy3qZnBJ250DGnI+1pSxoKdqVZ9nQENO61XIEd8dTfkW4lW/tk4d9OxUZCJeGdznOaqhRFYUMAxdDy6lXrfd1im3Z796bBs832LluC59WpBc6bEVPb7kdUycm1t3EtdP2u7s1ZCnR/YihxXxGRr1pY/X5zmqIZu5glqSc0BnPI4ix7ck74Shm4nzvDzq14t/9e/01j/9UpoI6Ey5KqpzHDfF1ms6bnHbBYxJXQ/G28AMyZ+eW2pVn2tAQ7kq5Yv53E2ZUey+ZBvM83nH5zOfz7Lw+QzUstUSKvHuAAAANmWhx7W60OPK+zxrF1jRzPNlve+jpKVbP14Nvv3j1acPH6yz1YPVp9nbRB+sPv3Xv1l9+jD90Kcf/Hh14Zax+mnU9NjD0dWFf31tdSnnsf9mNfivP14N/utrq9HEvj99aKx+mnHcta+NZh3X7NMPfry68EHuc7E0vujo6sK/juY+iGXG6tO3f5w6x7gHq0sf/Hg1mOcY653H6uqDjHNYXU1ey+x9Ffe+Fb9d1hgfvra68PbfrC58YGQ9s7A6+eZ7q7ceLJoeW1z1331v9Y13/KbD3l4de8e/Gs547eKq/733VieTQ/nYvzr25vXVsbsLq6uri6u33rm++sY7t1f9H8df/8abt7NeX1j47nurY+8tpF/3cWK/b763euvjHNuZH3vgXx175/aq37zDYs+3aIurk2++tzpp3t/Hi6uT71xPXxdL44vzv3d99Y133lt9453bqbGGHyzkvH7hu++tjt1dzPFMcnxrj3FrM+P72L86tqFrlUOefd16J/P9tXTcIrYL331vdeydrLm1urrqz3Eti/vcTfv0gx+vBm9lf58l8fm8Oc32+QxsTrnX1VR4AwCAhpVd8W1+DECpJCrldEQdx8+qZd1t5yVl/Zlpu1MdgxdND8wodv9ZtR3PrGLbuuuEHLqkee+MWnJU+23rOiVH/yHT9uZtnGrf90CR2aBakr1SY2P6RKfl2CWLNja+9Sx7zyv8MM+TpurGZe+r+mzfD7L+xNwZr8brt3TI1Guzq0Fb+k9r0Zu9XTHvm5XtMm3ddVaO419WePpVzT88rc7BE9oqKWDcVsTlyaq8blWPy6MzrvQjXt+iejz7s6qLW9Xj2imvEZCciSpbW6+GXfGKYbtN2m7rTVQIt2m7FhWRiq5QlkLy+trkPulIv8bWKrenV4GJx+tvJ8nu7NGw7uiyETJVMRd3vsWLV0RnnJOtVUPHjm5ofGbbnX2paxnffu02hbXK7VrUlG9JPcnK5WhAAfVqODXFNza+kon6M6uxE+M+WL4jSpKe2vrWnFePa0CBUb8Crv3qsfS5m1SgupvP55z4fM79+QzUOuYpAABoePT5BsrJGe/56R1R+NqIPlm35+chdRx4V6FbryjZYUHte9TS9bI6UkFHUJ/phsLXbiicaxftuyWtDSy2tK0fYmztP6Ut197Ucn88HFqevaIte9f/QT+nDY5vPS3ui2pxF7ftlrYS9lNd8+f3ktr3SDqctWER75ul7TKtPIq3OtC+c+ruz7x2dluhNiMhRaJta1uDSJKtTfboYwUkS/2WixJdVMTWtna/trbMgDm6qIgWdH10Mvd+bG2STMFxwfO1wqEhz2ONG4Zupo7Xqj6nqTWGxfGlx1makNnu6pM9FeJKAZ9fdpcpkN/g+Eomoy1JnHfCKN/xErbnnAetstsWFYlKsln53I0r3Lubz+dc+HzO//kM1DICbwAA0FTMVd8LPRsqmQOQQ4v7glr6i+j5ueusHMfPJr4IaiU2r5j3FYXbEj1E2w9piz5SW9FVi8U6pM93varF2a+rZeeMFmOnZS8yxMhQtvEV57PFoKRShCpBhaevSgdeVucuZ/oHw9iYQmsqCFX4fbO6nWTqPXxEHYMXc86XSHRJ0nohsEN221wiBMx6Kl8oXQr5wvRoVqW4rVN2Lcp9sribHBY+X4uc+zV8MvnFkiLRJXkNQ1O2RA9vi+MrPYd6nLfl9S2px7kgb7Q3o7d49cdXHU9zzoOlNb/cKfpzt2B1dwKfz5vSbJ/PQC37XLUHAAAAUA0O/111BnwK9T6f0fIEwCa0H1LH4EV1dkmL0yMKz85kPL0yO6J575hWkjfMklNb1Z1VheNUxwFpcdq8nSQFtTw7onlv5j6taOk/Ld1/U7HZK9qyd6N/lr2B8cU+St8kLDaj8PT5DZ1HfPyvKfYoaNp3UMuzlxS6NpI+RlESf97elg5TVmIzCntNN4tLPl7U+1b8dpLi12r6qrT3B+oezB3S9bh6Jd9teU03K1R0SQHfHY2PGgokyhTdrjYFjEA89DZt5zUey+7aREwavKPx0UldHjXkjWY/6ZDbtSivEVIk45immy5Kklo15JG8E1nj05ICPkOXjZDl8y1ufPEbQ17OuC6tsqt1TeuXYsdXLvHz9qqtinQAACAASURBVMvr88vuyr7x5QbGF11MX6toSFMTk7m3K3D9LCv2uEVstz06p3Hz3JIU8N1WxNW7Nvgv8Lkrpau729cJLfl8Fp/PCcV8PgO17plEo/DS7OyZZ1TC3QEAAJSVee1Cn28U0sxr3VDv89a/L2JBxWZfU1SnUj1OV2ZHFIkd1pbYFdMP/3vUsm/tn1SvPBpT7IPs7U6pw/Qn1Xl7q7afVvfgiZzDir/miDqPn80ZCCzc/zDn68y9WosdX3q/lxS5fyMRVOTfrihr/sx9j7Z1HZa9/0Sq32ux55H8U/VkgLKt/Yja9u7W4q0r+tTUG7jY963Y7WLT5/VJ+znZ3YcKh1rRkKaMOc1FkyFwq7Y7d2rI1SO7uaI7GtCU4ddcMki0deqgZ7/cNknBO7psLKRef/CYR3bfpK4HJTkHdMa1qPEJv54mnnMn9xu8o3FjYe3jJhHfHU35FuIht61TBz07FZmYkz1r+0gwIK/PND61qs/VpyFXVjuOYs+3iPFFfIamojtlj2Yf19TSxML4AkbimmXLavsR8Rka9S3l2FDx652j53Z83506eTK7F3vx40sf3/SerLPdutcvx5xxK5CYJ3F9nqMZ1ejFHrfQdhGfoSkNaMjm15Rh3m7t+7ZGjs9daUbha1e1dfBCwcCbz2c+ny19PgObUO51NYE3AABoWvnWLvT5Ri7NvNbdUOANNKWQpkbXBt5AsZKB93ChcLtIK7MjWoidygiEAaDayr2u5hc2AAAAWcx9vs1fAwCwnojvseZsO3WSsBs1Ymv/BXVXexAAUGFUeAMAgKZV7NqF4BtSc691qfAG8ohmtrmQrVMvePZn3FgQKNaatjF5WsAAQL2jpQkAAECZWF270Oe7uTXzWpfAGwAAAKVCSxMAAIAaYQ78qPoGAAAAgNpD4A0AALAB9PkGAAAAgNpD4A0AALAJBN8AAAAAUDs+V+0BAAAANAKH/64c/rsK9T6f0esbqL6gwtdGFItVexwAAABA+VHhDQAAUELZFd/mx4BqWJl9Tctdp9TdXu2RWDGj8LVXtZz4atu+H8jR76zqiAAAAFAfCLwBAADKgBtcouxiQcVmX1M0dljdgyfybDSj2H3JNniookPbvEPqOH5RHZJWZkcUKcUuY2MKeSVH3mslxabP65P2c7K7D/GDEgAAQJ1iHQcAAFBm9PlGqa3MXlLk/gNt2XdK3e78YfbK7NU6rO6unvbBi9oyO6KFa1fVcuBldeyiqhwAAKDeEHgDAABUCME3Ni02o7D3VS3rtDoHz2rrukF2geru2JjC3itaTvb2bj+iFt2Q9l5Ux670ZsveEUnS/LXzkqRt7UfU5j6rFvOxH13S/K0bkqSWAxfVrkuK3LqhTyVt6zotu/uENDuihfsfpl7ScuCiOtrGFJq+ok+TD3adWzfAz2XZO6Lww/R+144vqNj0K4omznP+2pX0i9tPr6mOb+m/oJadMwp7X9H8B0fUkX2uAAAAqGnPrK6urpZsZ888oxLuDgAAoKyqvXahz3d9qfZ8iQe7KrryeGV2RAuxfBXgQYWvvSaZ9xULKux9JSPwXpkdUSR2SjrxF6k5uvJoTJEPPlLb4Fm1rBnjeYVjeyQ9K9ver6t9l1Mrj2akXckWIUGFr72pzx/PfG1s+rxWsoJ283lE9HLOHt7J8dn7D6XC/7zjK6KlyZr9P4oH99p3To7+emsLAwAAUJvKva7+XNn2DAAAgHU5/HdT/0K9z2cE4EBaULHp8wrHnlXH8QtFttlIVHfnDWnnJWX9uWe7Ux2D5tB5RrH7z6otKzDfuuuEHHulsHcm5563dZ1S9+BZtSfGuXWXuR+2U+37HmhxNph+QWxMn+h0zrB7fenxmSvdC43Piq27zspx/Jy2PHxV89NjWtn0HgEAAFButDQBAACoAbQ7QX7OeG9p74jC10b0SREV3oV7dx9Sx4F3Fbr1iqLJh9r3qKXrZXX0pyu+P9MNha/d0DalW5qktO+WtDZQ39K2fiX01v5T2nLtTS33xyuwl2evaMvei+u+JifT+MK5ns8zPivMFd7dVHgDAADUBQJvAACAGkLwjXxa3BfU0l9Mb+kCvbuTdp2V4/jZxBdBrcTmFfO+onBbosq7/ZC26CO1HT+rRT2v7uMbCKVzOqTPd72qxdmvq2XnjBZjp2V3b2A3pvFlt1bZtFSv9CPqGLxID28AAIA6QksTAACAGpTd6oR2J5AktR9Sx+BFdXZJi9MjCs+ubduRrO5uXyekXZkd0bx3TCvJG1bKqa3qzqqGcarjgLQ4PZb16qCWZ0c0v4mWIS39p6X7byo2e0Vb9p7YYBVOenzp8ygwvthH6Zt0xmYUnj6/Zrvl2RHNT1+V9v5A3YPcsBIAAKDecNNKAADQtOpt7ULVd3XV3HyJBRWbfU1RmW9MOaPwtavaOnihYOAdiR3WltiVdACsPWrZZ2ppktz20ZgiX/7f9ek/D5u2O6UOU4uPZe95hR/mOFD7aXXnuUlk/DVH1Hn87JrAe2V2RAv3P8w9+K5zGTfiXHk0ptgH2eeROb70fi8pcv+GPs2zXWz6vD5pPye7+xB/CgsAAFAm5V5XE3gDAICmVa9rF4Lv6qiH+bIyO6KF2KmMQLgUQr3PM9/+//bupzeqK18b9p3GViouC7dMG5yQxCCRjmSOBEpsKc+jDBg86pwIiWHP3gEMmPANkDJC8jfwhEEYvLMzeAdIKCEjBq3TkUwiLD1Y6hMkUg0kNgiry/J2G1FR3oHLdvl/GWwM29c1Su1atfbau1ai7btWfgsAgB0h8AYA2CVv+rOL4PvVetPny8sQeAMAsFN2+7na/6kHAPCGWr3BZesxAACA/UjgDQDwhmsNua36BgAA9jOBNwBAiaxe9S34BgAA9hOBNwBACQm+AQCA/UjgDQBQYoJvAABgPxF4AwDsAza4BAAA9gOBNwDAPmKDSwAAoMwE3gAA+5RyJwAAQNkIvAEA9jnBNwAAUBYCbwAAkqjzDQAAvPkE3gAArKDONwAA8KYSeAMAsCHlTgAAgDeJwBsAgC0JvgEAgDeBwBsAgLap8w0AALzOBN4AAGybOt8AAMDrSOANAMBLUe4EAAB4XQi8AQDYEYJvAABgrwm8AQDYUep8AwAAe0XgDQDArlDnGwAAeNUE3gAA7DrlTgAAgFdB4A0AwCsj+AYAAHaTwBsAgFdOnW8AAGA3CLwBANgz6nwDAAA76Q97PQAAAEgWgu7eBz9l+oOPVqz8BtYqxi5luja518MAAHjtWOENAMBrRZ3vMhtP/dbVzDdfdR7/Kr0D/Xs6IgAAyuWt33///fcd6+ytt7KD3QEA7CrPLm+G1yX4fu3mSzGZovZ1ZotPc2T4i1091fQHH+34/W/URjKTCy8feBc3Mz2R9O7yPdjPirFLeVa9mIODp6yYAgBe2m4/V3teAQDgtWaDy7UatWuZuf9rDhw/myODp/Z6OJRcdXg0B2ojeXrrRionL6Snz6p8AOD1JfAGAOCNYIPLJMV46hNXM59zOTR8Ph3V9drcTH3ieuaL5uvqUCq5nRwbTU/fcrP5iZHUHz9aet1ZHUrX4PlUWvt8ci1Td2+nM0n9SVLNtczcvZ3nSToPn8vBwS+S2kie3l/up3JyND1dNzM9dj3PFw8evrjtYH7r8U2mGLuS2eZ1Tt26vvzh6rntrXpvXmeqQ+mu/prZx4/SefhiDvb92LzeoyuD3mI8Re1Gnj1+1LzGo+k8fHbFCuj5iUupP14o23Iw32Tm/u2ltpXjF9LTXNnebrsFbZSEWbyWDKVn+JM8m7janAtHUzl5ecUcSBZ/PGmeszqU7sFP0hhbOEfl5PKcqQxcTuVP46lPXMnUz0PpWT1XAABeE0qaAAD7lmeXN9+rDL73er4sBMDZYoXtZOq3vk5WhLOTqU9cWRF4N2ojmSnO5uDAqaXQvPHkZmZ+/iVdw+dTWdXr9Acf5fn/dz7Ju+k+9mWqff1pPBlP+hYD3snUb32Tt8+s/GwxdimNVUH7os1KmmxrfDtV0qRYCOlz/GJ6B44shOlpBrtz1zJ1Nzl05vzS9TaK/hU/OMxPXEq9WBm0N2ojmXmcpLoqDK+NZK7l2tttt+YebVgSZjz1Wzcyn6T75IXm93UzM3d/SNfw5aWgeuk+L56zmEwxcSWzxdF0D19OdYNAu/Fk4YePhXvl/zAAALZHSRMAANjA/tjgcnI5fD2zNoxeaSrJqof8an96hkdbDoynuP9uus6srMfc0fdFenMtUxPjqayzGrvz8NkV4WZHX2ub/lSP/5qZ2mQqiwFscTPPci6964Tdm3ux8W1mcRX1ulpXn1fPLV3jgWrSWf2yGQ6/l878kkYW723/mtX1lYFzmZtY2/3z6tqyM5WBC3l265vMDyx/n+22a9+jVE6Optq8/x19X+Tt6g/5ben9de5ztT/VwXN5NvbDpj139J1P75lPUh+7mqnH53Jo+At/WAIArw3PJQAAvPHKXee7f6GG8sRI6rdG8mzTFd6n0nPyx0zfvZLZxUPVo6kcbimNUUzmt9xO/dbt1NfrovpekrWB8oGuzUPmjoGzOdASzs7XrufAsdFNP7OuFxzfZiqDo6kMbn8oGyrGU5+4kfliueRKqkeTfLqmaWf1yDod9Kej+mt+K5JUt9eufUN5e7MfG4rJ/FZ9b22QXu3PgS16bl3hfcQKbwDgNSPwBgCgNMpc57syeDmVgTZqKPedT++Z880Xk2kUUykmrqTe1SwtUj2VA/klXVuuFt+uU3n78NXM1b5M5U/jmSvO5eCLhMy7Nr6dMpn62I3k5IUc6utf/oOqWVpltefFVJLVP1BMplG8m7er22+3Y6r9OVD8uFCru/V4MZnfssEfiks15IfSMzyqhjcA8Fr6w14PAAAAdkPvg5/S++CnTH/w0YqV32+06qn0DI/m0OFkbmwk9dr4ircbtZFMTdxMY3HDyvSnI0dWhZf96TmZzI21tkuSyczXRjI1sbLP7agMnEvuf5Oidj0Hjr1omYsXGF/xy/ImncV46mOXXuo6NtcsG9O1HHY3ivHUJ1o26WzRWdzI9MR4Gi3H5mtf57fjX64Imtttt3NOpXr818y1nrOYTLHBdczXRjI1diM59lWODNuwEgB4fdm0EgDYtzy77C8vu+L7tZsvxWSK2teZzXLt54VNCD/NgeL6cgCco6kcbylp0tR4cjPFz6vbnU1PS4mKxdrXnf/Pd3n+//5l+cPVlZsztlr4zFDLBo8t56yN5On9R+t+bkUt7TbHt9zvtczcv90Majdut6En1zJ19/bSebqHL+dArVn3+/DFHBmYzPTY9Txvvvf23EJJj8VguLM6lK5j72Xu7vU8b6m1vrix5MGub1rar/0+ttNuy/u3zrVUq+Op37qa+cXxHv+qZcPMlntXHUr34CdpjN1IR8umlcXYpTyrXlyxoSYAwIva7edqgTcAsG95dtmfXrTO936eL9MffFSa0jCv0mKQ3TuwUc317bV7NcZTv7Uy8AYA2Em7/VztB3oAAPaVMtf5hpfVqP2Y+eqnOSTsBgDeUFZ4AwD7lmcXFrUTfO/n+WKF9/YtloNZsqpky3bb7ZriZrNcS1N1kw1RAQB2gJImAAC7xLMLq20WfO/n+SLwBgBgpyhpAgAAr8hiqPuidb4BAIC9JfAGAIBV1qvzDQAAvP7+sNcDAACA11nvg5/S++CnPH3/hPAbAABecwJvAABow6GH99L74KdMf/CR4BvYwGTqt0ZSFHs9DgDYv5Q0AQCAbVhd51uN7zIZT/3W1cw3X3Ue/yq9A/17OiLeLI3a15k/fDZHqns9ku0w7wEoF4E3AAC8ABtcbqGYTFH7OrPFpzky/MVej6ZNp9JzZjQ9SRq1kczsRJfFzUxPJL1vzD14ccXYpTyrXszBwVOb/KE5ne+//Uf+mSR5J//x+ekM5mG++9uD/CtJcij/+z//nPcXm88+zHd3kr98/v763W233Ytqaz6Pp7ifdA+f2p0x7Brz/mW0N+8BeJX89xgAAF7Cehtc7vfgu1G7lpn7v+bA8bM5MvimhX+8qOrwaA7URvL01o1UTl5IT996q4R789nnH2RmRTj9fv7yn+9n4m93ktMtYfdrot353KjdeANXd/Oy2pv3ALxKAm8AANgh+77cSTGe+sTVzOdcDg2fT8d6wV9xM/WJ65lfrHFcHUolt5Njo+npW242PzGS+uNHS687q0PpGjyfSmufT65l6u7tJEnl5GiquZaZu7fzPEnn4XM5OPhFUhvJ0/vL/VROjqan62amx67n+eLBwxe3HcxvPb7JFGNXMtu8zqlb15c/XD23/VXvS9c6lJ7hT/Js4mrzHh5N5eTlFfcuxXiK2o08e/yoeY1H03n47PIK1MW+qkPprv6a2ceP0nn4Yg72/di8f0fXBHdtfR9JKgOXU/nTeOoTVzL181B61mnTnn9n4m938n9nF17917cPlt/q/iB/XQrL22v38M7f89+TyR9PnM5neZDv7z1trih/Jx+e+DifnXhn7RDamc9Ltljdbd6b9wC8Mm/9/vvvv+9YZ2+9lR3sDgBgV3l2YTteZL6UJfie/uCjLa9hIRjKFiscJ1O/9XXS2qaYTH3iyorgr1EbyUxxNgcHTi2FjI0nNzPz8y/pGj6fyppzX0q9OJrk3XQf+zLVvv40nownfYslBiZTv/VN3j6z8rPF2KU0VgWOixZKO1xYt5bxtsa3o6UdxlO/dSPzSbpPXmhe583M3P0hXcOXV4SOjaJ/RUC7cI9aAsdiIfzM8YvpHTiyEFKmGdTNXcvU3eTQmfPp2O71tt6nJwtB7MI5WoLVDcqPLKzwPp3B7mzZdo022s3cu5PvJ5N0f5jPTvfmYPP4w3t3MpGP85eW0Lu9+dxyrbWRPC02WgFu3r+cksx7AJbs9t9hVngDAMAu2R91vieXQ6MzG4dAC6aSrPojpNqfnuHRlgPjKe6/m64zK+vhdvR9kd5cy9TEeCrrhIqdh8+uCJc6+lrb9Kd6/NfM1CZTWQzyipt5lnPpXSf029yLjW8z8xOXUn+8wZtrVuE+WljV27d83rerP+S3FR/qX7MauTJwLnMTq/qunlu6ZweqSWf1y2Z4+F4680saSTpe4no7+s6n98wnqY9dzdTjczk0/MVyH7MPVq7GTpK8k//Y4DbslH91f5i/nu5dcez9Ex/n4bcP8vDEn/P+tubzoq1qd5v369mX8x6AV8J/dwEAYJe9qXW+W4P61n9eT2e+y1xGMtdGv7/lWp5t0WajvjqTTK/7ie82ON7q2po2m39mbftF2x3fVmPr3PCd9a7ro3WObX1P1xvHytcrz9V6jdv/Pla3+27FZohD2xjjUJvnaKfd/0mSNf/uvZOD3XOZmU3S3b9Qk3liJPVbI3nWxgrvrWt3n0rPyR8zffdKZhcPVY+mcvhCegaWV3z/ltup37qd+npdVN9LsjZgPdC1ecjcMXA2B259k/mBhfB+vnY9B46NbvqZdb3g+DZTGRxNZbDd1kN5e6uQvhhPfeJG5ovlEiSpHk3y6bbGtdDXi19v6wrvI1Z4A+wJgTcAALxCb1Kd79axtjXOpZrH7dawnUyjmEoxcbWltMP6ZRg2Mz9xKc/61i/RsLrdXPWr9P5pPNMTycFNVl5uXNphm+Pb8dIOP65TomIkGbycanVxfAvlM6p9/cvXt3ocq14v3ZuB/mbZh1/SdeZ8Ki/wfWw5D/awpMm3sx/mr2ve+XdmZrvyfst5K4OXUxlopybzVqu7m/rOp/fM+eaLxXl/JfWu5rytnsqBLN7znXQqbx++mrnal6n8aTxzxbkcbDtkbrFr49spk6mP3UhOXsihdeb9tr3I9bbO++FRNbwB9tAf9noAAACwH/U++Cm9D37K9Acfbbl6+o1RPZWe4dEcOpzMjY2kXhtf8XajNpKpiZtpLG7cl/505Miq0Lk/PSeTubHWdkkymfnaSKYmVva5HZWBc8n9b1LUrufAsRctM/AC4yt+Wd6ssBhPfezSS13H5prlM7qWQ79GMZ76RMtmhduyveudr41kauxGcuyrHBneoY37ZufycHFp9Ox0vv/b3/Nfd9ZZy91Guz/O/jPf3Zlesdr84b1/ZObEB1kTlW8xn5Pl1d3VTa7TvI95D8ArZdNKAGDf8uzCduz2fHmd63y3vcK7VTGZovZ1ZrO8kd/CJnCf5kBxfTkIy9FUjreUdmhqPLmZ4ufV7c6mp6VEwIY1gKstm9StsvCZoaWN6VacszaSp/cfrfu51TWF2xnfcr/XMnP/djN427jdpp5cy9Td20vn6h6+nGp1PPVbVzPfPNp5fGGF9mJJhcWgr7M6lK5j72Xu7vU8z1B6Tib1VX0dqDXv5eGLOTIwmemx63m+dJ72rrcYu5Rn1Ys5OHhq41B18n/yX3eeNl+8k//4/HQG8zDf/e1B/tU8+uHp/5XPWqbDzL3/yff3njbffycfnvgwn51YWYe7nXYz9+7k+3ycz7of5Ps7re0+zmctG1aua535vLiZYsfw5S0Db/N+n897AFbY7edqgTcAsG95dmE7XuV8ed3KnbxQ4A2vmcXA+y9bhdttatRG8rQ4u2pzRQBgK7v9XO0HSAAAeM28SXW+Yb/qGLicI3s9CABgDSu8AYB9y7ML27GX82Wvg28rvHnTPbzz9/z3ZMuB/o/z19Nry6IAALtPSRMAgF3i2YXteB3my17V+RZ4AwCwU5Q0AQAAkqwMufd61TcAALyOBN4AAPAGUucbAADWEngDAMAbTPANAADL/rDXAwAAAF5e74Of0vvgp0x/8NGKWt+wt/6d77+9k4nZvR7HqzKZ+q2RFMVejwMA9i8rvAEAoERWr/huPVY+46nfupr55qvO41+ld6B/T0fESjP3/pF/9n+Yv3Yvvr6Tb+/9O+n+IH/9/P29HdwuaNS+zvzhszlS3c2zmPcAsBkrvAEAoIQWV3zv2arvYjLFxEimxm7u4klOpefMaI6cGc2h40d38TwvobiZ6XbuQbvt9kAxdinTE+NpbPuT05m4l/zHid6lIwdPnM5fP/8gf2y3i9mH+e5vD3eu3Ytqaz6Pp7ifdA+c2r1xJDHvX40Xn/cA7DWBNwAAlNyrDr4btWuZHvs6jerZHBn+YtfPx+6qDo+mq3ojT2+NpP5ksu3Pzdz7Z/7Z/2EGu3dxcK9Au/O5UbuR+cNnU93V1d28Ki867wHYe2/9/vvvv+9YZ2+9lR3sDgBgV3l2YTvKNF+2u8Hl9Acftde2GE994mrmcy6HBr9IR0vw16iN5On9R0n13FJouHQsR9M9fHk5KHxyLVN3bydJKidHU821zNy9nedJOg+fy8HBL9bUZmzURjKTCy9c2mF+4lLqjxfKQxzMN5m5v3C+5Ggqxy+kp7XfYjxF7UaePX601Kbz8NkcHDzVMq7JFGNXMrteLeeWe9B+u8VxjqT++NHS687qULoGz6fSGrK2c/+W2gylZ/iTPJu4mvmieb0nL6enb53xLH2/Q+lZfc41pvP9t//Mwc9Prw28Zx/muzvJZ/1z+f7e0/wrSfJOPjx9Op8t3eZ/Z+Jvd/J/16v9vaIcSnvtHt75e/57MvnjidP5LA9WnvfEx/nsxDubXO/a+bzWeOq3bqSjdR7HvF9hX8x7ANqx28/VAm8AYN/y7MJ2lHG+tFvnu53AeyGQSionL6Snb4PwrbiZ6Ymkd1WYVYyNJIOX16yMnZ+4lHpxNMm76T72Zap9/Wk8GU/6Tu148LfUx+Mk1ZUh3nxtJHMr+p5Mo+hfEYAujHVtULfRNa/RRrtGbSQzxdkcHDi1dO7Gk5uZ+fmXdA2fT2VV+63v30JIO5+k++SF5vs3M3P3h3QNX94w2Gs8WQgSc/xiejco3zFz706+nf0wfz3du/bN2Yf57m8P8q/uD/Kfp9/Pwe5kZvJ/8v2duQx+fjrvd69qeyf5y1b1vttoN3PvTr6fTNL9YT473ZuDzeMP793JRD7OX1pC77bmc4tGbSRPi7M5MrjO/TDvN1ayeQ9Ae3b7udqmlQAAsE+1htjbXfW9rLlSM0PpObM2fHpZnYfPrgiXOvq2HzQtrmJd1+GLK0LK59W1oWVl4EKe3fom8wOL19e/ZrVvZeBc5ia2PbRtGE9x/910nVkZenb0fZHeXMvUxHgq64StW9+/RwurYfuW+3u7+kN+22QkHX3n03vmk9THrmbq8bkcGl698rhZu/vzdcLuRd0f5D8/f38pdD7Y/+e8330nM5ucdyf8q3ttCP/+iY/z8NsHeXjiz3n/heZzs3b38M6FoOb9ojdp3gPwuvDfZwAAYCno3n7w3Z/q8GgOTIykfmskz9pcEduuA10vHyJWBkdTGWyvbWf1yDpH+9NR/TW/FUmqaZY4uJH5YrnEQqpHk3z60mPdUDGZ33I79Vu3U1/v/ep7Sdbeq63v31DeXq+MwyZaV7oeWWel62Lt7r9uUbv74OZv74o/dq9TuiTv5GD3XGZmk3Rvfz4v1u4+soOlLsz7pjdo3gPw+hB4AwAAS140+K4MXk5lYDz1iSuZ+vnNrXX7vJhKsjrgnEyjeDdvVxf+uT52Izl5IYf6+pf/oGqWZtg11VM5kF/StQur6NvWWst4eHSD77eN1d176F+z/06yOvT+d2Zmu1aUUml/Pu/86u69YN5voq15D8Dr5A97PQAAAOD10/vgp/Q++GlFne8tVU+lZ3g0hw4nc2MjqdfG17YpfkjR3KiuUYynPnZp/Y3r9khncSPTE+NptBybr32d345/2QzcppIkHV3LoV+jGE994npzI791FL80N8bLQng2dilTE+vdm83a9afnZDI3djONFfdrMvO1kfX720HztZFMjd1Ijn2VI8Mb/5ixuLp7zUaVL2N2Lg8XN6Wcnc73f/t7/uvO9Au1++PsP/PdnekVpVMe3vtHZk58kDXVv9uYz4uru1fX4V7DvC/1vAfg9WLTSgBgwPqxSwAADzBJREFU3/LswnaYL9tUTKaofZ3ZrKwN3Khdy8z92wshWXUo3ce+TH6+ktki6Tz+VXoH+jeuPVxduTleozaSp/cfrdMwa2oUt2NxA8CDXd9k5m5zjDmayvEL6WnZFHCxtMFi0NdZHUrXsfcyd/d6nq9T+3nFNedoKsfPpmedkgjttGs8uZni5+vLAeE67dq6f0+uZeru7aU+uocvp1odT/3W1cwvXlfz+yjGLuVZ9eKKDQ3XN53vv/1nDn5+esPAe+benXx779/NV4fyv//zz3k/0/n+23/kn82jfzxxesUGkjP3/iff33uafyVJ3smHJz7MZyfWriDfqt3MvTv5Ph/ns+4H+f5Oa7uP89mJ9UqdtFh3Pi9sftgxvHbjydXM+zLPewC2a7efqwXeAMC+5dmF7TBfym8x+Osd2Lka5PvJzL07+XZ27aaQr4vFwPsvW4XbbWrURvK0WLvZ45vGvAfgVdvt52o/VAIAAPDSDp44nb/u9SBeoY6By1lvq0cAYG9Z4Q0A7FueXdgO86Xc1pRDeIHSELy+Ht75e/57suVA/8ev7Ur0V8m8B2AvKGkCALBLPLuwHeYLAAC8vN1+rv7DrvUMAAAAAACvkMAbAAAAAIBSEHgDAAAAAFAKHXs9AAAAYDdNpn7r63QMX061utdjeXWmP/hor4dAyfU++GmvhwAArEPgDQAAJdaofZ35w2dz5I0Ku8dTv3U1881Xnce/Su9A/7Z6EEYuKMYu5dnh7d8/AIA3lZImAADwJiomU0yMZGrs5iaNxlPcT7oHTr2yYe2MU+k5M5ojZ0Zz6PjRnemyuJnpTe9VOVWHR19Z2F2MXcr0xHgar+RsAADrE3gDAMAbplG7lumxr9Oons2R4S82aXcj84fP7qtSJuyd6vBouqo38vTWSOpPJvd6OADAPqWkCQAAvCmK8dQnrmY+53Jo+Hw6Ng2ym6u7hzdY3V3cTH3ieuaL5uvqUCq5nRwbTU/fcrP5iZHUHz9aet1ZHUrX4PlUWs/95Fqm7t5OklROjqaaa5m5ezvPk3QePpeDg18ktZE8vb/cT+XkaHq6bmZ67HqeLx48fDFHBre3Gn3r8U2mGLuS2eZ1Tt26vvzh6rlNfzBYY/E6q0Pprv6a2ceP0nn4Yg72/di83qOpnLyQnr7miupiPEXtRp49ftS8xqPpPHw2BwdPLf0hNj9xKfXHC2VbDuabzNy/vdS2cvxCepqrs9ttt6CNkjBL39lQeoY/ybOJq825cDSVk5dXzIFk4UeWpXNWh9I9+EkaYwvnqJxcnjOVgcup/Gk89Ykrmfp5KD2r5woAwC576/fff/99xzp7663sYHcAALvKswvbsdfzZSHYzcpAdRON2kieFmc3CJAXNrLMinB2MvWJKysC70ZtJDPF2RwcOLUUrjee3MzMz7+ka/h8KmvGeCn14miSd9N97MtU+/rTeDKe9C0GvJOp3/omb59Z+dli7FIaq4L21uuYyYV1y3Jsa3zFzUxPJL3bCbjXUyyE9Dl+Mb0DRxbC9DSD3blrmbqbHDpzful6G0X/ih8mFu7RyqC9URvJzOMk1VVheG0kcy3X3m67Nfdog/cWgvEbmU/SffJC8/u6mZm7P6Rr+PJSUL10nxfPWUymmLiS2eJoujfZDLXxZOGHj4V79aaV1QEAdstuP1db4Q0AAK+1yeVQ9czakHl9W6zuzlSSVX8MVPvTMzy6qo9303Xm1Ip2HX1fpDfXMjUxnso6YXrn4bMrws2OvtY2/ake/zUztclUFgPY4mae5Vx61wm7N/di49vM4irqdbWuPq+eW7rGA9Wks/plMxx+L535JY0s3tv+NavwKwPnMjextvvn1bU/TlQGLuTZrW8yP7D8vbfbrn2PFlblN+9/R98Xebv6Q35ben+d+1ztT3XwXJ6N/bBpzx1959N75pPUx65m6vG5HBr+wh+gAMCu87wBAACvtf5Uh0dzYGIk9VsjedbGCu/F2t1HNiwlcSo9J3/M9N0rmV08VD2ayuGW0hjFZH7L7dRv3U59vS6q7yVZGygf6No8ZO4YOJsDLeHsfO16Dhwb3fQz63rB8W2mMjiayuD2h7KhYjz1iRuZL5ZLrqR6NMmna5p2Vo+s00F/Oqq/5rciSXV77do3lLc3+7GhmMxv1ffWBunV/hzYoufWFd5HrPAGAF4RgTcAALwBKoOXUxlopzbyVqu7m/rOp/fM+eaLyTSKqRQTV1LvapYWqZ7KgfySrrZXlbfrVN4+fDVztS9T+dN45opzOfgiIfOujW+nTKY+diM5eSGH+vqX//BqllZZ7XkxlWT1DxmTaRTv5u3q9tvtmGp/DhQ/LtTqbj1eTOa3bPAH5VKt+aH0DI+q4Q0AvFJ/2OsBAAAAbaqeSs/waA4dTubGRlKvja9psri6e6O6ygttRjI1cTONxQ0r05+OHFkVXvan52QyN9baLkkmM18bydTE2nO3qzJwLrn/TYra9Rw49qJlLl5gfMUvy5t0FuOpj116qevYXLNsTNdy2N0oxlOfaNmks0VncSPTE+NptBybr32d345/uSJobrfdzjmV6vFfM9d6zmIyxQbXMV8bydTYjeTYVzkybMNKAODVs2klALBveXZhO167+VJMpqh9ndm01nRe2ISwY5ONBJPFTQg/zYHi+nIAnKOpHG8pabLY9snNFD+vbnc2PS0lKjasfV1duTljq4XPDLVs8LhyfE/vP1r3cytqabc5vuV+r2Xm/u1mULtxuw09uZapu7eXztM9fDkHas1rP3wxRwYmMz12Pc+b7709t1DSYzEY7qwOpevYe5m7ez3PW2qyL24sebDrm5b2a7+P7bTb8v6tcy3V6njqt65mfnG8x79q2TCz5d5Vh9I9+EkaYyvnWjF2Kc+qF1dsqAkAsNpuP1cLvAGAfcuzC9vxJsyXRm0kT4u1mxryelsMsnsHtqrN3l67V6O9H1cAAFbb7edqP7wDAEBJdAxcznpbGsJOa9R+zHz10xwSdgMArxkrvAGAfcuzC9thvrAb1pSDWVWyZbvtdk1xs1mupam62capAAAbU9IEAGCXeHZhO8wXAAB4ebv9XP2HXesZAAAAAABeIYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJSCwBsAAAAAgFIQeAMAAAAAUAoCbwAAAAAASkHgDQAAAABAKQi8AQAAAAAoBYE3AAAAAAClIPAGAAAAAKAUBN4AAAAAAJRCx14PAAAA3hRvvfXWXg8BAADYhMAbAADa8Pvvv+/1EAAAgC0oaQIAAAAAQCkIvAEAAAAAKAWBNwAAAAAApSDwBgAAAACgFATeAAAAAACUgsAbAAAAAIBSEHgDAAAAAFAK/z9cjCco9IqYHQAAAABJRU5ErkJggg==

[3]:data:image/png;base64,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
