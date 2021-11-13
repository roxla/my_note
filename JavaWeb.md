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

### 状态码

> **200**：成功响应
>
> **302**：重定向
>
> **403**：没有权限访问
>
> **404**：找不到资源
>
> **500**：服务器内部错误

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
>      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>      xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee
>                          http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
>      version="4.0">
>    
>        <welcome-file-list>
>            <welcome-file>index.html</welcome-file>
>            <welcome-file>index.htm</welcome-file>
>            <welcome-file>index.jsp</welcome-file>
>        </welcome-file-list>
>    
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
>      	<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs" prefix="localhost_access_log" suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b" />
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
>    	<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs" prefix="localhost_access_log" suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b" />
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

## Servlet

> 是Web的规范
>
> 是Web的三大组件（Servlet/filter/listener）之一
>
> 是运行在服务器的一小段程序，用来接收请求，响应请求

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
> 
>     @Override
>     public void service(ServletRequest servletRequest, ServletResponse servletResponse) throws ServletException, IOException {
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
>     <!--给servlet起一个别名 -->
>     <servlet-name>Hello</servlet-name>
>     <servlet-class>com.gec.serlvet.Hello</servlet-class>
> </servlet>
> 
> <servlet-mapping>
>     <!--和servlet中的servlet-name不一致-->
>     <servlet-name>a</servlet-name>
>     <url-pattern>/hello</url-pattern>
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

### servlet定位过程(重点)

> 

### 请求方式

#### get请求

> 超链接 <a href="http">xx< /a>  
>
> 浏览器输入的地址

#### post请求

> 表单提交 <form method="post"> xxxx</form> 

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

### HttpServletRequest请求对象

> 

### 使用idea创建servlet

> ![][1]

### MIME类型

> 规定的类型在tomcat/conf/web.xml
>
> **示例**
>
> - 响应音频：mp3
>
>
> - 视频：mp4
>
>
> - word：word
>
>
> - 电子表格：xls

### HttpServletResponse

> 

#### HttpServletResponse响应对象

> 打印流：getWriter()
>
> 打印的方法：print/println(Object o)
>
> 设置响应类型：setContentType(String type)

#### HttpServletRequest的常用方法(重点)

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

### ServletConfig

> 

### ServletContext(重点)

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

### ServletResponse常用功能

#### 显示

> 

#### 下载

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
> 创建一个 cookie，cookie 是 servlet 发送到 Web 浏览器的少量信息，这些信息由浏览器保存，然后发送回服务器。cookie  的值可以唯一地标识客户端，因此 cookie 常用于会话管理。  
>
> 一个 cookie 拥有一个名称、一个值和一些可选属性，比如注释、路径和域限定符、最大生存时间和版本号。一些 Web 浏览器在处理可选属性方面存在  bug，因此有节制地使用这些属性可提高 servlet 的互操作性

#### Cookie的使用

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

#### 获取Cookie

> 



































****

base64:

[1]:data:image/png;base64,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

