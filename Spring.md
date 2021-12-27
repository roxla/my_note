## Spring MVC

> **什么是MVC**
>
> - MVC是模型(Model)、视图(View)、控制器(Controller)的简写，是一种软件设计规范。
> - 是将业务逻辑、数据、显示分离的方法来组织代码。
> - MVC主要作用是**降低了视图与业务逻辑间的双向偶合**。
> - MVC不是一种设计模式，**MVC是一种架构模式**。当然不同的MVC存在差异。
>
> **Model（模型）：**数据模型，提供要展示的数据，因此包含数据和行为，可以认为是领域模型或JavaBean组件（包含数据和行为），不过现在一般都分离开来：Value Object（数据Dao） 和 服务层（行为Service）。也就是模型提供了模型数据查询和模型数据的状态更新等功能，包括数据和业务。
>
> **View（视图）：**负责进行模型的展示，一般就是我们见到的用户界面，客户想看到的东西。
>
> **Controller（控制器）：**接收用户请求，委托给模型进行处理（状态改变），处理完毕后把返回的模型数据返回给视图，由视图负责展示。也就是说控制器做了个调度员的工作。
>
> **最典型的MVC就是JSP + servlet + javabean的模式。**+ Spring + SpringMVC  **MVC三层架构**
>
> ****
>
> **Spring MVC 概述**
>
> Spring MVC是Spring Framework的一部分，是基于Java实现MVC的轻量级Web框架。
>
> 查看官方文档：https://docs.spring.io/spring/docs/5.2.0.RELEASE/spring-framework-reference/web.html#spring-web
>
> ****
>
> **我们为什么要学习SpringMVC呢?**
>
>  Spring MVC的特点：
>
> 1. 轻量级，简单易学
> 2. 高效 , 基于请求响应的MVC框架
> 3. 与Spring兼容性好，无缝结合
> 4. 约定优于配置
> 5. 功能强大：RESTful、数据验证、格式化、本地化、主题等
> 6. 简洁灵活
>
> Spring的web框架围绕**DispatcherServlet** [ 调度Servlet ] 设计
>
> DispatcherServlet的作用是将请求分发到不同的处理器。从Spring 2.5开始，使用Java 5或者以上版本的用户可以采用基于注解形式进行开发，十分简洁
>
> 正因为SpringMVC好 , 简单 , 便捷 , 易学 , 天生和Spring无缝集成(使用SpringIoC和Aop) , 使用约定优于配置 . 能够进行简单的junit测试 . 支持Restful风格 .异常处理 , 本地化 , 国际化 , 数据验证 , 类型转换 , 拦截器 等等......所以我们要学习
>
> **最重要的一点还是用的人多 , 使用的公司多**

### Spring MVC 的架构(未完成)

> 

### Spring MVC 配置

> **实现步骤**
>
> 1. 新建一个web项目
> 2. 导入相关jar包
> 3. 编写web.xml , 注册 DispatcherServlet
> 4. 编写springmvc配置文件
> 5. 接下来就是去创建对应的控制类 , controller
> 6. 最后完善前端视图和controller之间的对应
> 7. 测试运行调试

#### 配置 web.xml 文件(未完成)

> **web.xml**
>
> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <web-app xmlns="http://java.sun.com/xml/ns/javaee"
>          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>          xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
>                              http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
>          version="3.0">
>     <servlet>
>         <servlet-name>springmvc</servlet-name>
>         <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
>         <init-param>
>             <param-name>contextConfigLocation</param-name>
>             <param-value>classpath:config/spring-mvc.xml</param-value>
>         </init-param>
>         <load-on-startup>1</load-on-startup>
>     </servlet>
>     <servlet-mapping>
>         <servlet-name>springmvc</servlet-name>
>         <url-pattern>/</url-pattern>
>     </servlet-mapping>
>     <servlet-mapping>
>         <servlet-name>default</servlet-name>
>         <url-pattern>*.js</url-pattern>
>         <url-pattern>*.css</url-pattern>
>         <url-pattern>*.html</url-pattern>
>         <url-pattern>/imgs/*</url-pattern>
>     </servlet-mapping>
>     <!-- 解决中文乱码的编码过滤器 -->
>     <filter>
>         <filter-name>encoding</filter-name>
>         <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
>         <init-param>
>             <param-name>encoding</param-name>
>             <param-value>UTF-8</param-value>
>         </init-param>
>     </filter>
>     <filter-mapping>
>         <filter-name>encoding</filter-name>
>         <url-pattern>/*</url-pattern>
>     </filter-mapping>
> </web-app>
> ```
>
> 

#### 配置 spring-mvc.xml 文件

> 在项目中的 src 目录下的 config 目录中添加 **springmvc-servlet.xml** 配置文件(文件名必须叫这个)
>
> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <beans xmlns="http://www.springframework.org/schema/beans"
>        xmlns:mvc="http://www.springframework.org/schema/mvc"
>        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>        xmlns:p="http://www.springframework.org/schema/p"
>        xmlns:context="http://www.springframework.org/schema/context"
>        xmlns:aop="http://www.springframework.org/schema/aop"
>        xsi:schemaLocation="http://www.springframework.org/schema/beans
>                            http://www.springframework.org/schema/beans/spring-beans.xsd
>                            http://www.springframework.org/schema/context
>                            http://www.springframework.org/schema/context/spring-context.xsd
>                            http://www.springframework.org/schema/mvc
>                            http://www.springframework.org/schema/mvc/spring-mvc.xsd
>                            http://www.springframework.org/schema/aop
>                            http://www.springframework.org/schema/aop/spring-aop.xsd
>                            ">
>     <context:component-scan base-package="com.roxla.it.web"/>
>     <mvc:annotation-driven/>
>     <!--  视图解析器  -->
>     <bean
>           class="org.springframework.web.servlet.view.InternalResourceViewResolver"
>           p:prefix="/WEB-INF/views/" p:suffix=".jsp"
>           p:viewClass="org.springframework.web.servlet.view.JstlView">
>     </bean>
> </beans>
> ```
>
> - `<context:component-scan>`中的`base-package`属性为需要扫描的包（含所有子包）
>   - `base-package="com.roxla.it.web"`表示扫描 web 包下的所有包和类
> - `<mvc:annotation-driven/>`：注解驱动
>   - `<mvc:annotation-driven/>`会自动注册 DefaultAnnotationHandlerMapping 与 AnnotationMethodHandlerAdapter 两个 bean，是 spring MVC 为 @Controllers 分发请求所必须的，即解决了 @Controller 注解使用的前提配置

#### 配置 spring-mvc 控制类

> **编写一个Java控制类 com.roxla.it.web.LinkController**
>
> ```java
> @Controller
> @RequestMapping("/link")
> public class LinkController {
>     private LinkService service = new LinkServiceImpl();
> 
>     @RequestMapping("/list")
>     public String showList(Model m) {
>         List<Link> links = service.findAll();
>         m.addAttribute("list", links);
>         return "link/list";
>     }
>     
>     @GetMapping("/del/{x}") // Resuful规范
>     public String delLink(@PathVariable("x") int lkid) {
>         service.remove(lkid);
>         return "redirect:/link/list";
>     }
> 
>     @GetMapping("/edit") // 简写
>     public String edit(int id, Model m) {
>         Link lk = service.findOne(id);
>         m.addAttribute("lk", lk);
>         return "link/edit";
>     }
> }
> ```
>
> - **@Controller** 是为了让 Spring IOC 容器初始化时自动扫描到(*在一个类上添加@Controller注解，表明了这个类是一个控制器类。是一个用于处理请求的处理器*)
> - @RequestMapping 是为了映射请求路径，这里因为类与方法上都有映射所以访问时应该是**/link/list**
> - 方法上的 @RequestMapping("/list") 类似于 Servlet 中的 service，也可以换成 @GetMapping 或 @PostMapping，分别为 doGet 和 doPost
>   - 相同的请求路径只能有一个 @GetMapping 和 @PostMapping
> - 方法中声明 Model 类型的参数是为了把数据传递给视图
> - 方法返回的结果是视图的名称**list**，加上[视图解析器](#View)中配置的前后缀变成WEB-INF/views/**list**.jsp

### Resuful规范

> 

#### 1

> @PathVariable() 注解
>
> ```java
> @GetMapping("/del/{x}")
> public String del(@PathVariable("x") int id) {
>     service.remove(id);
>     return "redirect:/story/list";
> }
> ```
>
> 

### Spring MVC 请求

#### get请求

> *请求处理*
>
> ```java
> @RequestMapping(value = "/link/add", method = RequestMethod.GET)
> public String add() {
>        return "/WEB-INF/views/link/add.jsp";
> }
> ```
>
> - @RequestMapping(value = "/list", method = RequestMethod.GET)
>   - value：请求路径
>   - method：请求类型
>
> **请求处理(简写)**
>
> ```java
> @GetMapping("/link/add")
> public String add() {
>     return "/WEB-INF/views/link/add.jsp";
> }
> ```
>
> - @GetMapping("/link/add")：相当于 Servlet 的 doGet 方法

#### post请求

> **表单格式**
>
> ```jsP
> <form action="" method="post">
>      <table>
>            <tbody>
>                <tr>
>                    <td>联系人姓名</td>
>                    <td><input name="name" type="text"></td>
>                </tr>
>                <tr>
>                    <td>联系人电话</td>
>                    <td><input name="phone" type="text"></td>
>                </tr>
>                <tr>
>                    <td><input type="submit" value="添加"></td>
>                    <td><input type="reset" value="重置"></td>
>                </tr>
>            </tbody>
>      </table>
> </form>
> ```
>
> **请求处理**
>
> ```java
> @PostMapping("/link/add")
> public String add(Link lk) {
>        LinkService service = new LinkServiceImpl();
>        service.add(lk);
>        return "redirect:/WEB-INF/views/link/add.jsp";
> }
> ```
>
> - @PostMapping("/link/add")：相当于 Servlet 的 doPost 方法

#### 参数传递

> 表单元素的 name 属性与 请求处理方法的参数名一致，就可以直接进行值的传递
>
> **如果方法的参数是一个对象，会调用该对象的 set 方法，将值直接传入对象的对应属性中**
>
> **如果方法的参数既有对象，又有变量；那么这几个参数都会被传值进去**
>
> ```java
> @PostMapping("/link/add")
> public String add(Link lk, String name, String phone) {
>     LinkService service = new LinkServiceImpl();
>     service.add(lk);
>     return "redirect:/link/list";
> }
> ```
>
> *如果提交的表单数据没有对应的 name 或是没有值，那么获取到的是 null*
>
> **如需要传递数据到页面，可以使用 Model**
>
> ```java
> @PostMapping("/link/list")
> public String showList(Model m) {
>     LinkService service = new LinkServiceImpl();
>     List<Link> links = service.findAll(lk);
>     m.setAttribute
>     return "redirect:/link/list";
> }
> ```
>
> **也可以传递一些原生对象；需要什么，就自己传什么**
>
> ```java
> @PostMapping("/link/list")
> public String showList(HttpServletRequest req) {
>     LinkService service = new LinkServiceImpl();
>     List<Link> links = service.findAll(lk);
>     req.setAttribute
>         return "redirect:/link/list";
> }
> ```

##### JSON 数据的接收与发送

###### 接收

> **@RequestBody注解**
>
> @RequestBody 主要用来接收前端传递给后端的 json 字符串中的数据的(请求体中的数据的)
>
> 一个请求，只有一个 RequestBody
>
> *加了这个注解，就相当于将 json 数据，通过反射，赋值给类中与 json key 值对应的属性*
>
> **示例**
>
> ```java
> @GetMapping("/ajax/user/add")
> public void addUser(@RequestBody User u){
>        service.add(u);
> }
> ```

###### 发送

> **@ResponseBody注解**
>
> @ResponseBody 表示方法的返回值直接以指定的格式写入 Http response body 中，而不是解析为跳转路径
>
> *加了这个注解，就相当于将返回值，自动变成 json*
>
> **示例**
>
> ```java
> @ResponseBody
> @GetMapping("/ajax/user/msg")
> public Map<String, Object> showMsg () {
>        Map<String, Object> map = new HashMap<>();
>        map.put("name", "zhangsan");
>        map.put("age", 23);
>        return map;
> }
> ```

###### @RestController注解

> @RestController 的作用等同于 @Controller + @ResponseBody
>
> **示例**
>
> ```java
> @RestController
> public class AjaxUserController {
>        private UserService service = new UserServiceImpl();
> 
>        @GetMapping("/ajax/user/add")
>        public void addUser(@RequestBody User u){
>            service.add(u);
>        }
> 
>        @GetMapping("/ajax/user/list")
>        public List<User> showAll() {
>            return service.findAll();
>        }
> 
>        @GetMapping("/ajax/user/one")
>        public User showOne(int id) {
>            return service.findOne(id);
>        }
> }
> ```

#### 转发与重定向

##### 转发

> 请求处理方法执行完成后，最终返回一个 ModelAndView 对象。对于那些返回 String，View 或 ModeMap 等类型的处理方法，Spring MVC 也会在内部将它们装配成一个 ModelAndView 对象，它包含了逻辑名和模型对象的视图
>
> ```java
> @GetMapping("/link/add")
> public String add(Link lk) {
>     LinkService service = new LinkServiceImpl();
>     service.add(lk);
>     return "/WEB-INF/views/link/add.jsp";
> }
> ```
>
> **return 的字符串即为转发的页面路径**

##### 重定向

> 若请求处理方法返回的是 String 类型，那么在返回值的路径前加上 **redirect:** 即为重定向页面
>
> ```java
> @PostMapping("/link/add")
> public String add(Link lk) {
>     LinkService service = new LinkServiceImpl();
>     service.add(lk);
>     return "redirect:/WEB-INF/views/link/add.jsp";
> }
> ```
>

##### <span id="View">视图解析器</span>

> **SpringMVC解析视图概述**
>
> 不论控制器返回一个String,ModelAndView,View都会转换为ModelAndView对象，由视图解析器解析视图，然后，进行页面的跳转
>
> - 请求处理方法执行完成后，最终返回一个 ModelAndView 对象。对于那些返回 String，View 或 ModeMap 等类型的处理方法，Spring MVC 也会在内部将它们装配成一个 ModelAndView 对象，它包含了逻辑名和模型对象的视图
> - Spring MVC 借助视图解析器（ViewResolver）得到最终的视图对象（View），最终的视图可以是 JSP ，也可能是 Excel、JFreeChart等各种表现形式的视图
> - 对于最终究竟采取何种视图对象对模型数据进行渲染，处理器并不关心，处理器工作重点聚焦在生产模型数据的工作上，从而实现 MVC 的充分解耦
>
> **使用**
>
> 在`spring-mvc.xml`文件中增加以下代码，解析器会自动将路径与 p:prefix 和 p:suffix 属性结合，生成完整的路径
>
> ```xml
> <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" p:prefix="/WEB-INF/views/" p:suffix=".jsp" p:viewClass="org.springframework.web.servlet.view.JstlView"></bean>
> ```
>
> - p:prefix：访问页面的前缀，指定页面存放的文件夹
> - p:suffix：文件的后缀名，常见的后缀名有 html，jsp，php，txt，mp3
>
> **示例**
>
> ```java
> @GetMapping("/link/add")
> public String add() {
>     return "link/add";
> }
> ```
>
> *视图解析器会自动将 return 的 link/add 与 配置文件中的 p:prefix 和 p:suffix 属性结合，组合成完整的路径 /WEB-INF/views/link/add.jsp，程序再按照该路径进行跳转或是重定向*

#### 日期格式转换

> **问题**
>
> 服务器 Date 类型的参数直接接收页面数据时会抛出异常(**错误码400**)，因为传入的参数是 String 类型的，而用来接收数据的参数是 java.util.Date 类型的，类型无法转换
>
> **解决方案**
>
> 可以使用 @DateTimeFormat 注解格式化参数，来解决上述问题
>
> ```java
> @DateTimeFormat(pattern = "yyyy-MM-dd")
> ```
>
> - pattern：指定要转换的日期时间格式
>
> *注意：@DateTimeFormat 注解的 pattern 属性值指定的日期时间格式是和传入的参数格式是对应的，如果格式不相同也会抛出异常(**错误码400**)*
>
> **示例**
>
> ```java
> @GetMapping("/test")
> public String test(@DateTimeFormat(pattern = "yyyy-MM-dd") Date date) {
>     System.out.println(date)
>     return "";
> }
> ```
>
> *可以将 @DateTimeFormat 注解写在实体类中，将值压入对象时会自动进行转换*
>
> **实体类**
>
> ```java
> public class User {
>     private Integer id;
>     private String loginName;
>     private String loginPwd;
>     private String hobbys;
>     @DateTimeFormat(pattern = "yyyy-MM-dd")
>     private Date birthday;
>     private String[] hobby;
>     ...
>     get
>     ...
>     set
>     ...
> }
> ```
>
> **Controller**
>
> ```java
> @PostMapping("/reg")
> public String reg(User u) throws IOException {
>     service.add(u);
>     return "redirect:/user/list";
> }
> ```

### Spring MVC 文件上传

> **配置 spring-mvc.xml**
>
> 添加代码
>
> ```xml
> <bean id="multipartResolver" class="org.springframework.web.multipart.commons.CommonsMultipartResolver" p:defaultEncoding="UTF-8" p:maxUploadSize="62914560" p:maxInMemorySize="4096"></bean>
> ```
>
> **控制器类代码**
>
> ```java
> @ResponseBody
> @PostMapping("/upload")
> public String reg(MultipartFile photo_file) throws IOException {
>     Map<String, Object> map = new HashMap<>();
>     if (!photo_file.isEmpty()) {
>         photo_file.transferTo(new File("E:/log/" + photo_file.getOriginalFilename()));
>         map.put("state", "上传成功");
>     } else {
>         map.put("state", "文件已存在");
>     }
>     return map;
> }
> ```
>
> - MultipartFile：
> - isEmpty()：
> - getOriginalFilename()：
>
> **form 配置**
>
> ```html
> <form action="upload" method="post" enctype="multipart/form-data">
>     <input name="photo_file" type="file">
>     <input type="submit" value="添加">
>     <input type="reset" value="重置">
> </form>
> ```
>

### Spring MVC 过滤器

> Spring MVC中的拦截器（Interceptor）类似于Servlet中的过滤器（Filter），它主要用于拦截用户请求并作相应的处理。例如通过拦截器可以进行权限验证、记录请求信息的日志、判断用户是否登录等。
>
> 要使用Spring MVC中的拦截器，就需要对拦截器类进行定义和配置。通常拦截器类可以通过两种方式来定义
>
> - 通过实现HandlerInterceptor接口，或继承HandlerInterceptor接口的实现类（如HandlerInterceptorAdapter）来定义
> - 通过实现WebRequestInterceptor接口，或继承WebRequestInterceptor接口的实现类来定义

#### 实现HandlerInterceptor接口

> **LoginInterceptor类**
>
> ```java
> public class LoginInterceptor implements HandlerInterceptor {
>     @Override
>     public boolean preHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o) throws Exception {
>         // 进来时候拦截
>         if (httpServletRequest.getSession().getAttribute("user") == null) {
>             httpServletResponse.sendRedirect("/PhoneBook/login");
>             return false;
>         }
>         return true;
>     }
> 
>     @Override
>     public void postHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, ModelAndView modelAndView) throws Exception {
>         // 回去时候拦截
>     }
> 
>     @Override
>     public void afterCompletion(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) throws Exception {
>         // 每次拦截后，必须要做的动作
>     }
> }
> ```
>
> **配置 spring-mvc.xml**
>
> 添加代码：
>
> ```xml
> <mvc:interceptors>
>     <mvc:interceptor>
>         <mvc:mapping path="/**"/>
>         <mvc:exclude-mapping path="/login"/>
>         <mvc:exclude-mapping path="/reg"/>
>         <bean class="com.roxla.it.web.interceptor.LoginInterceptor"></bean>
>     </mvc:interceptor>
>     <mvc:interceptor>
>         ...
>     </mvc:interceptor>
> </mvc:interceptors>
> ```
>
> - `<mvc:interceptors>`：元素用于配置一组拦截器，其子元素`<bean>`中定义的是全局拦截器，它会拦截所有的请求
> - `<mvc:interceptor>`：元素中定义的是指定路径的拦截器，它会对指定路径下的请求生效；每一个`<mvc:interceptor>`代表一个拦截器
> - `<mvc:mapping path="/**"/>`：用于配置拦截器作用的路径，该路径在其属性path 中定义。如上述代码中 path 的属性值 **/\**** 表示拦截所有路径；**/hello** 表示拦截所有以 **/hello** 结尾的路径
> - `<mvc:exclude-mapping path="/login"/>`：写在`mvc:exclude-mapping`的`path`中的页面请求不会被拦截
> - `<bean class="com.roxla.it.web.interceptor.LoginInterceptor">`：拦截器的实现类
>
> *注意：`<mvc:interceptor>`中的子元素必须按照上述代码中的配置顺序进行编写，即`<mvc:mapping>` `<mvc:exclude-mapping>`  `<bean>`，否则文件会报错*
>
> **可以在`<mvc:interceptors>`中配置多个拦截器，多个拦截器之间依据配置的先后顺序来执行**

## MyBatis

> **概述**
>
> MyBatis 是一款优秀的**持久层框架**它支持定制化 SQL、存储过程以及高级映射。
>
> **MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集**。
>
> MyBatis 可以使用简单的 XML 或注解来配置和映射原生类型、接口和 Java 的 POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。
>
> MyBatis 本是[apache](https://baike.baidu.com/item/apache/6265)的一个开源项目[iBatis](https://baike.baidu.com/item/iBatis), 2010年这个项目由apache software foundation 迁移到了google code，并且改名为MyBatis 。
>
> 2013年11月迁移到Github。  

### 配置MyBatis

#### 搭建数据库

> **sql语句**
>
> ```java
> CREATE DATABASE `mybatis`;
> 
> USE `mybatis`;
> 
> CREATE TABLE `user`(
>   `id` INT(20) NOT NULL PRIMARY KEY,
>   `name` VARCHAR(30) DEFAULT NULL,
>   `pwd` VARCHAR(30) DEFAULT NULL
> )ENGINE=INNODB DEFAULT CHARSET=utf8;
> 
> INSERT INTO `user`(`id`,`name`,`pwd`) VALUES 
> (1,'狂神','123456'),
> (2,'张三','123456'),
> (3,'李四','123890')
> ```

#### 新建项目

> 1. 新建一个 Web 项目
> 2. web/WEB-INF 文件夹下新建文件夹 lib
> 3. 在 lib 文件夹中拷贝入 mybatis 的 jar 包

#### 编写配置文件

> **src 文件夹下编写 mybatis 的核心配置文件  mybatis-config.xml**
>
> ```xml
> <?xml version="1.0" encoding="UTF-8" ?>
> <!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
> <configuration>
>     <environments default="development">
>         <environment id="development">
>             <transactionManager type="JDBC"/>
>             <dataSource type="POOLED">
>                 <property name="driver" value="com.mysql.jdbc.Driver"/>
>                 <property name="url" value="jdbc:mysql://localhost:3306/mystory?characterEncoding=utf-8"/>
>                 <property name="username" value="root"/>
>                 <property name="password" value="root"/>
>             </dataSource>
>         </environment>
>     </environments>
>     <mappers>
>         <mapper resource="mapper/PayMapper.xml"/>
>         <mapper resource="mapper/UserMapper.xml"/>
>     </mappers>
> </configuration>
> ```
>
> - property 标签内配置数据库的连接设置
> - mappers 标签内用于注册自己写的 mapper.xml 文件

#### 编写mybatis工具类

> **MyBatisUtil**
>
> ```java
> public class MyBatisUtil {
>        // 全局共享
>        private static SqlSessionFactory sqlSessionFactory = null;
>        // 定义一个线程变量(供一个线程共享的变量)
>        private static ThreadLocal<SqlSession> th = new ThreadLocal<>();
> 
>        static {
>            try {
>                String resource = "config/mybatis-cfg.xml";
>                InputStream inputStream = Resources.getResourceAsStream(resource);
>                sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
>            } catch (IOException e) {
>                e.printStackTrace();
>                throw new RuntimeException(e);
>            }
>        }
> 
>        public static SqlSession openSession() {
>            // 如果线程变量里已经有一个属于自己的 sqlSession，就用回它
>            if (th.get() != null)
>                return th.get();
>            // 如果线程变量没有值，就创建一个新的 sqlSession 放入线程变量，供后续使用
>            SqlSession sqlSession = sqlSessionFactory.openSession();
>            th.set(sqlSession);
>            return sqlSession;
> 
>        }
> 
>        public static void closeSession() {
>            SqlSession sqlSession = th.get();
>            if (sqlSession != null) {
>                sqlSession.close();
>                // 删掉关闭了的 sqlSession 的残留
>                th.remove();
>            }
>        }
> }
> ```
>
> 

### MyBatis动态查询

> mybatis 中对于时间参数进行比较时的一个bug： 如果拿传入的时间类型参数与空字符串''进行对比判断则会引发异常

## Spring

> **Spring框架的原理**
>
> *因为IOC，所以AOP*
>
> - IOC：负责对象的装配
>   - 灵活调整(积木一般进行组装)
>   - 装配方式：xml/注解/java装配
>   - 可以 (构造函数 数组)
>   - 改变了我们创建对象的习惯，不要自己 new 对方，等待容器安排，前提是必须注册到容器中
> - AOP：切面，非常简化
>   - 用法：配置一个切面类，在IOC配置中说明那些方法需要经过这个切面
>   - pointcut --> 等效拦截路径配置 --> css选择器

### 控制反转(IOC)

> 

### Spring配置

#### 基于XML的配置

##### 编写实体类

> **编写一个Hello实体类**
>
> ```java
> public class Hello {
>        private String name;
> 
>        public String getName() {
>            return name;
>        }
>        public void setName(String name) {
>            this.name = name;
>        }
> 
>        public void show(){
>            System.out.println("Hello,"+ name );
>        }
> }
> ```

##### 编写 spring 文件(applicationContext.xml)

> **applicationContext.xml**
>
> ```xml
> <?xml version="1.0" encoding="UTF-8" ?>
> <beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>           xmlns="http://www.springframework.org/schema/beans"
>           xmlns:aop="http://www.springframework.org/schema/aop"
>           xmlns:context="http://www.springframework.org/schema/context"
>           xmlns:tx="http://www.springframework.org/schema/tx"
>           xmlns:cache="http://www.springframework.org/schema/cache"
>           xmlns:p="http://www.springframework.org/schema/p"
>           xsi:schemaLocation="http://www.springframework.org/schema/beans
>                               http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
>                               http://www.springframework.org/schema/aop
>                               http://www.springframework.org/schema/aop/spring-aop-4.0.xsd
>                               http://www.springframework.org/schema/context
>                               http://www.springframework.org/schema/context/spring-context-4.0.xsd
>                               http://www.springframework.org/schema/tx
>                               http://www.springframework.org/schema/tx/spring-tx-4.0.xsd
>                               http://www.springframework.org/schema/cache
>                               http://www.springframework.org/schema/cache/spring-cache-4.0.xsd">
>      <!-- 使用spring创建对象，在spring中这些称为bean -->
>      <bean id="hello" name="hello2 h2,h3;h4" class="com.kuang.pojo.Hello">
>            <property name="name" value="Spring"/>
>      </bean>
> </beans>
> ```
>
> - `<bean>`：就是**java对象**，由 Spring 创建和管理(等价于**Hello hello = new Hello()**)
>   - **id**是**bean的标识符**，要唯一，如果没有配置**id**，**name**就是**默认标识符**
>   - 如果配置**id**，又配置了**name**，那么**name**是**别名**
>   - **name**可以设置**多个别名**,可以**用逗号，分号，空格隔开**
>   - 如果**不配置id和name**,可以根据**applicationContext.getBean(.class)**获取对象;
>   - class 是 bean 的**全限定名=包名+类名**
> - `<property>`：相当于给对象中的属性设置一个值
>   - **name**：调用该属性的**set方法**(类中要提供该属性的 set 方法)
>     - **name**属性的值必须该类中的**set方法**的**方法名去掉set后，将首字母变成小写**
>   - **value**：具体的值，基本数据类型
>   - **ref**：引用Spring容器中创建好的对象
>
> *`<property>`标签简写*
>
> ```xml
> <bean id="hello" name="hello2 h2,h3;h4" class="com.kuang.pojo.Hello" p:name="Spring" />
> ```
>
> - `<property>`标签可以使用`bean`标签中的 **p:** 属性来替代，**p:** 后面的内容为该类中的属性
> - **p:name**注入的是**value值**，**p:name-ref**注入的是**Spring容器中创建好的对象**
>
> 上面的写法等价于
>
> ```xml
> <bean id="hello" name="hello2 h2,h3;h4" class="com.kuang.pojo.Hello">
>     <property name="name" value="Spring"/>
> </bean>
> ```

##### 使用

> **main方法中使用**
>
> ```java
> ApplicationContext context = new ClassPathXmlApplicationContext("config/applicationContext.xml");
> Hello hello = (Hello) context.getBean("hello");
> hello.show();
> ```
>
> - ClassPathXmlApplicationContext：
> - getBean("hello")：
> - hello.show()：调用 hello 对象中的 show() 方法
>
> **结果**
>
> ```
> "Hello,Spring"
> ```
>
> *show() 方法中的 name 的值是通过 xml 文件中 property 的 value 属性注入进去的*

#### 基于注解的配置

##### 编写实体类

> **编写一个Hello实体类**
>
> ```java
> @Component("hello")
> public class Hello {
>        private String name;
> 
>        public String getName() {
>            return name;
>        }
>        @Value("Spring")
>        public void setName(String name) {
>            this.name = name;
>        }
> 
>        public void show(){
>            System.out.println("Hello,"+ name );
>        }
> }
> ```
>
> - @Component 是 Spring 容器中的基本注解，表示容器中的一个组件（bean），可以作用在任何层次
>   - @Component("hello") 等效于 XML 配置 `<bean id="hello" class="com.kuang.pojo.Hello"/>`
>   - 在注解后加上**@Component("hello")**时，注册的**这个类的bean的id就是hello**
> - @Value 将外部的值动态注入到 bean 中
>   - @Value("Spring") 等效于 XML 配置 `<property name="name" value="Spring"/>`

##### 编写 spring 文件(applicationContext.xml)

> **applicationContext.xml**
>
> ```xml
> <?xml version="1.0" encoding="UTF-8" ?>
> <beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>     xmlns="http://www.springframework.org/schema/beans"
>     xmlns:aop="http://www.springframework.org/schema/aop"
>     xmlns:context="http://www.springframework.org/schema/context"
>     xmlns:tx="http://www.springframework.org/schema/tx"
>     xmlns:cache="http://www.springframework.org/schema/cache"
>     xmlns:p="http://www.springframework.org/schema/p"
>     xsi:schemaLocation="http://www.springframework.org/schema/beans
>                         http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
>                         http://www.springframework.org/schema/aop
>                         http://www.springframework.org/schema/aop/spring-aop-4.0.xsd
>                         http://www.springframework.org/schema/context
>                         http://www.springframework.org/schema/context/spring-context-4.0.xsd
>                         http://www.springframework.org/schema/tx
>                         http://www.springframework.org/schema/tx/spring-tx-4.0.xsd
>                         http://www.springframework.org/schema/cache
>                         http://www.springframework.org/schema/cache/spring-cache-4.0.xsd">
> 	<!-- 扫描注解 -->
>     <context:component-scan base-package="com.roxla.it"/>
> </beans>
> ```
>
> - `<context:component-scan base-package="com.roxla.it"/>`
>   - 配置完这个标签后，spring就会去**自动扫描base-package对应的路径或者该路径的子包下面的java文件**，如果扫描到文件中**带有@Service，@Component，@Repository，@Controller**等这些注解的类，则把这些类**注册为bean**
>   - base-package：要扫描的范围，com.roxla.it 表示扫描 it 包下的所有包和类
>   - 在context中可以使用 resource-pattern 来过滤出特定的类
>     - `<context:component-scan base-package="cn.lovepi.spring" resource-pattern="anno/*.class"/>`

##### 使用

> **main方法中使用**
>
> ```java
> ApplicationContext context = new ClassPathXmlApplicationContext("config/applicationContext.xml");
> Hello hello = (Hello) context.getBean("hello");
> hello.show();
> ```
>
> **结果**
>
> ```
> "Hello,Spring"
> ```

### 运行流程

> 

### 依赖注入(DI)

autowire 自动注入

### Spring配置AOP

#### 基于XML的配置

##### 编写AOP类

> **编写一个用于打印日志的AOP**
>
> ```java
> public class LogAop implements MethodInterceptor {
>        @Override
>        public Object invoke(MethodInvocation inv) throws Throwable {
>            System.out.println("inv: " + inv);
>            // inv 指代调用该切面的类的代理
>            System.out.println("进入方法: " + inv.getThis().getClass().getSimpleName() + "的" + inv.getMethod().getName());
>            // 调用原装的方法
>            Object o = inv.proceed();
>            System.out.println("结束方法: " + inv.getThis().getClass().getSimpleName() + "的" + inv.getMethod().getName() + "返回" + o);
>            return o;
>        }
> }
> ```

#### 配置applicationContext.xml

> **applicationContext.xml**文件的 beans 中添加如下代码
>
> ```xml
> <bean class="ex02.aop.LogAop" id="logaop"/>
> <aop:config>
>  <aop:advisor advice-ref="logaop" pointcut="execution(public * ex02.impl..*Impl.*(..))"/>
> </aop:config>
> ```
>
> - `<bean>`：
> - `<aop:config>`：
> - `<aop:advisor>`：
>   - advice-ref：执行方法所在的类
>   - pointcut：表示拦截哪些方法，expression表达式匹配要拦截的方法
>     - 通过 pointcut 表达式可以选择拦截不同的类和方法
>

#### 基于注解的配置

##### 编写AOP类

> **编写一个用于打印日志的AOP**
>
> ```java
> @Aspect
> @Component("logaop") // 相当于 <bean id="logaop" class="" />
> public class LogAop {
>     @Around("execution(public * ex03.impl..*Impl.*(..))")
>        public Object logAop(ProceedingJoinPoint inv) throws Throwable {
>            System.out.println("进入方法: " + inv.getThis().getClass().getSimpleName() + "的" + inv.getSignature().getName());
>            // 调用原装的方法
>            Object o = inv.proceed();
>            System.out.println("结束方法: " + inv.getThis().getClass().getSimpleName() + "的" + inv.getSignature().getName() + "返回" + o);
>            return o;
>        }
>    }
> ```
> 
> - @Aspect：作用是把当前类标识为一个切面供容器读取
>- @Component：将类 LogAop 注册到 Spring 容器中
> - @Around：环绕增强，相当于实现 MethodInterceptor 接口

#### pointcut表达式

> **用于描述哪些类或方法需要被 aop 切入的表达式**
>
> - execute 表达式
> - within 表达式
> - this 表达式
> - target 表达式
> - args 表达式
>
> **pointcut表达式详解**
>
> https://www.cnblogs.com/itsoku123/p/10744244.html

##### execute表达式

> **表达式组成**
>
> ==修饰符（public,private..） 返回类型 包名.类名.方法名(参数列表，不填就是没有)==
>
> - **..**：表示有多个
>   - 写在包名后面表示包含子包；写在参数列表中表示任意参数
> - \* 的用法
>   - *package.func  (注意中间没有空格) 这就表示包名可能是不完整的，可能是前缀没有写（任意前缀）
>   - package*  (注意中间没有空格) 这就表示包名可能是不完整的，可能是后缀没有写（任意后缀）
>   - \* package.func （中间有空格）这就表示返回的类型是随意的
>   - ** package.func 这就表示修饰符和返回类型都随意
>
> **示例**
>
> ```xml
> public * it.service.impl..*Impl.*(..)
> ```
>
> 含义：拦截**it.service.impl**包或者子包中**以Impl结尾的所有类中**定义的所有的公共方法

###### 拦截任意公共方法

> ```xml
> execution(public * *(..))
> ```

###### 拦截以set开头的任意方法

> ```xml
> execution(* set*(..))
> ```

###### 拦截类或者接口中的方法

> ```xml
> execution(* com.xyz.service.AccountService.*(..))
> ```
>
> 拦截**AccountService**(类、接口)中定义的所有方法

###### 拦截包中定义的方法，不包含子包中的方法

> ```xml
> execution(* com.xyz.service.*.*(..))
> ```
>
> 拦截**com.xyz.service**包中所有类中任意方法，不包含子包中的类

###### 拦截包或者子包中定义的方法

> ```xml
> execution(* com.xyz.service..*.*(..))
> ```
>
> 拦截**com.xyz.service**包或者子包中定义的所有方法





@Resource(name = "flowerService") = @Autowired + @Qualifier("flowerService")

## Maven

> 1

### Maven的配置

> **下载Maven**
>
> 官方地址：http://maven.apache.org/download.cgi
>
> 
>
> **E盘新建文件夹 maven-rep 作为 Maven 仓库，用于存放下载的 jar 包**
>
> cmder command
>
> ```
> mkdir E:\maven\maven-rep
> ```
>
> **在 settings.xml 中配置 Maven 仓库的位置**
>
> settings.xml 文件在 ？ 中的 conf 文件夹中
>
> ```xml
> <localRepository>E:\maven\maven-rep</localRepository>
> ```
>
> **配置远程仓库的位置**
>
> 国内推荐使用**阿里的镜像源**仓库
>
> 在 settings.xml 的`<mirrors>`标签中添加如下代码
>
> ```xml
> <mirror>  
>        <id>nexus-aliyun</id>  
>        <mirrorOf>central</mirrorOf>    
>        <name>Nexus aliyun</name>
>        <!-- 阿里镜像源地址 -->
>        <url>http://maven.aliyun.com/nexus/content/groups/public</url>  
> </mirror>
> ```
>
> **调整 maven 工程的 jdk 的版本**
>
> 在 settings.xml 的`<profiles>`标签中添加如下代码
>
> 在这里配置可以避免后续在工程中多处调整
>
> ```xml
> <profile>  
>     <id>jdk18</id>  
>     <activation>  
>         <activeByDefault>true</activeByDefault>  
>         <jdk>1.8</jdk>  
>     </activation>  
>     <properties>  
>         <maven.compiler.source>1.8</maven.compiler.source>  
>         <maven.compiler.target>1.8</maven.compiler.target>  
>         <maven.compiler.compilerVersion>1.8</maven.compiler.compilerVersion>  
>     </properties>   
> </profile>
> ```

#### 在IntelliJ IDEA中配置maven

> 

https://mvnrepository.com/



## MyBatisPlus

### MyBatisPlus查询

> **根据数据库的列名进行查询**
>
> MyBatisPlus 提供了一种写法，可以避免像 MyBatis 那样对 dao 层进行方法的扩充
>
> ```java
> @Test
> public void testLogin() {
>        QueryWrapper<Users> qw = new QueryWrapper<>();
>        qw.eq("user_loginname", "wangwu").eq("user_loginpwd", "123");
>        Users u = dao.selectOne(qw);
>        System.out.println(qw);
> }
> ```
>
> *实际上是把条件写到了外面自行组装*
>
> **根据实体类的字段名进行查询**
>
> 这种写法可以根据实体类中的字段名进行查询，你可以不知道数据库的列名
>
> ```java
> @Test
> public void testLogin() {
>        QueryWrapper<Users> qw = new QueryWrapper<>();
>        qw.lambda().eq(Users::getUserLoginname, "wangwu").eq(Users::getUserLoginpwd, "123");
>        Users u = dao.selectOne(qw);
>        System.out.println(qw);
> }
> ```
>
> *如果进行跨表查询的话，这种方式还不行；用列名查询是没有任何问题的*

### MyBatisPlus自动生成mapper.xml

#### 添加 mapper.xml 模板

> **mapper.xml.btl 文件**
>
> ```xml
><?xml version="1.0" encoding="UTF-8"?>
> <!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
> <mapper namespace="${package.Mapper}.${table.mapperName}">
> 
> <% if(enableCache){ %>
>  <!-- 开启二级缓存 -->
>  <cache type="org.mybatis.caches.ehcache.LoggingEhcache"/>
>    
>    <% } %>
> <% if(baseResultMap){ %>
>  <!-- 通用查询映射结果 -->
>  <resultMap id="BaseResultMap" type="${package.Entity}.${entity}">
>    <% for(field in table.fields){ %>
>    <% /** 生成主键排在第一位 **/ %>
> <% if(field.keyFlag){ %>
>         <id column="${field.name}" property="${field.propertyName}" />
>    <% } %>
>    <% } %>
>    <% for(field in table.commonFields){ %>
>  <% /** 生成公共字段 **/ %>
>  <result column="${field.name}" property="${field.propertyName}" />
>    <% } %>
>    <% for(field in table.fields){ %>
> <% /** 生成普通字段 **/ %>
> <% if(!field.keyFlag){ %>
>         <result column="${field.name}" property="${field.propertyName}" />
>    <% } %>
>    <% } %>
>     </resultMap>
> <% } %>
>    <% if(baseColumnList){ %>
>  <!-- 通用查询结果列 -->
>  <sql id="Base_Column_List">
>    <% for(field in table.commonFields){ %>
>         ${field.name},
> <% } %>
>         ${table.fieldNames}
>  </sql>
>    
>    <% } %>
> 
> <!-- 每个表不同的 -->
>  <sql id="fromsql">
>      from ${table.name}
>     </sql>
>     <sql id="selectsql">
>         select <include refid="Base_Column_List"/>
>         <include refid="fromsql"/>
>     </sql>
>    
>     <select id="selectById2" resultMap="BaseResultMap">
>      <include refid="selectsql"/>
>         where
>          <% for(field in table.fields){ %>
>            <% /** 生成主键排在第一位 **/ %>
>            <% if(field.keyFlag){ %>
>                 ${field.name}=#{id}
>            <% } %>
>         <% } %>
>     </select>
>    
>     <!-- 可以重用的配置 -->
>  <sql id="wheresql">
>         <if test="ew!=null">
>             \${ew.customSqlSegment}
>         </if>
>     </sql>
>     <!-- 查询总行数 -->
>     <select id="selectCount2" resultType="int">
>         select count(1)
>         <include refid="fromsql"/>
>         <include refid="wheresql"/>
>     </select>
>    
>     <!-- 根据条件查找单个对象 -->
>  <select id="selectOne2" resultMap="BaseResultMap">
>         <include refid="selectsql"/>
>         <include refid="wheresql"/>
>     </select>
>     <!-- 根据条件查找一组对象 -->
>     <select id="selectList2" resultMap="BaseResultMap">
>         <include refid="selectsql"/>
>         <include refid="wheresql"/>
>     </select>
>     <!-- 根据条件分页查找 -->
>     <select id="selectPage2" resultMap="BaseResultMap">
>         <include refid="selectsql"/>
>         <include refid="wheresql"/>
>     </select>
>    
>     <!-- 查找全部对象 -->
>  <select id="selectAll2" resultMap="BaseResultMap">
>         <include refid="selectsql"/>
>     </select>
>    
>    </mapper>
> ```
> 
> 将该文件放到项目中的 resource 文件夹内
>

#### 修改 CreateCode.java 文件

> *将“输出xml文件”的注释解开*
>
> ```java
>//要想输出xml文件，需要额外自定义添加进去
> String templatePath = "/mapper.xml.btl";
> InjectionConfig cfg = new InjectionConfig() {
>        @Override
>        public void initMap() {
>        }
> };
>    // 自定义输出配置
>    List<FileOutConfig> focList = new ArrayList<>();
> // 自定义配置会被优先输出
> focList.add(new FileOutConfig(templatePath) {
>        @Override
>        public String outputFile(TableInfo tableInfo) {
>            // 自定义输出文件名 ， 如果你 Entity 设置了前后缀、此处注意 xml 的名称会跟着发生变化！！
>            return projectPath + "/src/main/resources/mapper/" + pc.getModuleName() + "/" + tableInfo.getEntityName() + "Mapper.xml";
>        }
> });
> 
>    cfg.setFileOutConfigList(focList);
> mpg.setCfg(cfg);
> ```
> 
>    - templatePath：模板文件所在路径
> - `projectPath + "/src/main/resources/mapper/" + pc.getModuleName() + "/" + tableInfo.getEntityName() + "Mapper.xml";`
>      - 生成的 mapper.xml 文件所在的路径
> 

#### 修改 applicationContext.xml 文件

> *将 mapper.xml 文件配置的注释解开*
>
> ```xml
><property name="mapperLocations" value="classpath:mapper/*.xml"/>
> ```
> 
> **运行 CreateCode.java 的代码，生成文件**

### MyBatisPlus添加外键

#### 在实体类中添加外键

> ```java
> @TableField(exist = false)
> private Users users;
> ```
>
> - @TableField(exist = false)
>   - 注解加在属性上，表示当前属性不是数据库的字段，但在项目中必须使用，这样在新增等使用的时候，mybatis-plus就会忽略这个，不会报错

#### 在 mapper.xml 文件中添加外键

> ```xml
> <resultMap id="BaseResultMap" type="com.roxla.it.entity.Links">
>        <id column="link_id" property="linkId"/>
>        <result column="link_name" property="linkName"/>
>        <result column="link_phone" property="linkPhone"/>
>        <result column="link_user_id" property="linkUserId"/>
>        <association property="users">
>            <id column="user_id" property="userId" />
>            <result column="user_nickName" property="userNickname" />
>            <result column="user_loginName" property="userLoginname" />
>            <result column="user_loginPwd" property="userLoginpwd" />
>        </association>
> </resultMap>
> ```

#### 修改 mapper.xml 文件中的查询语句

> **使用内连接进行多表查询**
> 
> ```xml
> <!-- 通用查询结果列 -->
> <sql id="Base_Column_List">
>        link_id, link_name, link_phone, link_user_id,
>        user_id, user_nickName, user_loginName, user_loginPwd
> </sql>
> 
> <!-- 每个表不同的 -->
> <sql id="fromsql">
>        from links lk join users u on lk.link_user_id=user_id
> </sql>
> ```
>
> *xml文件里面的方法名如果和内置的方法名相同，xml的优先级高，会覆盖内置的方法*

#### 使用扩充的方法触发 join 表的结果

> **要使用扩充的方法，需要先添加含有扩充方法的几个基类**

1

>**新的 dao 基类 BaseMapper2**
>
>```java
>public interface BaseMapper2<T> extends BaseMapper<T> {
>        public T selectById2(Serializable id);
>
>        public T selectOne2(@Param("ew") Wrapper<T> wrapper);
>
>        public List<T> selectAll2();
>
>        public List<T> selectList2(@Param("ew") Wrapper<T> wrapper);
>
>        public int selectCount2(@Param("ew") Wrapper<T> wrapper);
>
>        //带条件的，分页的方法
>        public IPage<T> selectPage2(IPage<T> page, @Param("ew") Wrapper<T> wrapper);
>}
>```
>
>



### MyBatisPlus分页

> **分页代码示例**
>
> ```java
> @GetMapping("/list")
> public String showList((String findname, 
>                            String findTel, 
>                            @RequestParam(value = "page",defaultValue = "1")int page
>                            Model m) {
>        QueryWrapper<Links> qw = new QueryWrapper<>();
>        // 可以设置前置条件，如果成立的话才添加到 where 中
>        qw.like(findName!=null, "link_name", findname).like(findTel!=null, "link_phone", findTel)
>            List<Links> list = service.list2(qw);
>        IPage<Links> iPage = service.page2(new Page<Links>(page, 3), qw);
>        m.addAttribute("info", iPage);
>        return "list";
> }
> ```
>
> *MyBatisPlus 的分页插件有点问题，可能会取不到部分分页的数据*
>
> **解决取不到分页数据**
>
> *自己扩充一个 MyPage 类，该类继承 Page 类*
>
> ```java
> public class MyPage<T> extends Page<T> {
>        public boolean getHasNext() {
>            return this.hasNext();
>        }
> 
>        public boolean getHasPrevious() {
>            return this.hasPrevious();
>        }
> 
>        public long getPages() {
>            return super.getPages();
>        }
> 
>        public MyPage() {}
> 
>        public MyPage(long current, long size) { super(current, size); }
> 
>        public MyPage(long current, long size, long total) { super(current, size, total); }
> 
>        public MyPage(long current, long size, boolean isSearchCount) { super(current, size, isSearchCount); }
> 
>        public MyPage(long current, long size, long total, boolean isSearchCount) { super(current, size, total, isSearchCount); }
> }
> ```
>
> *使用我们扩充的类，返回值传到 JSP 界面上的骑士是我们这个扩充的MyPage类对象*
>
> ```java
> @GetMapping("/list")
> public String showList(String findname, 
>                           String findTel, 
>                           @RequestParam(value = "page",defaultValue = "1")int page
>                           Model m) {
>        QueryWrapper<Links> qw = new QueryWrapper<>();
>        // 可以设置前置条件，如果成立的话才添加到 where 中
>        qw.like(findName!=null, "link_name", findname).like(findTel!=null, "link_phone", findTel)
>            List<Links> list = service.list2(qw);
>        IPage<Links> iPage = service.page2(new MyPage<Links>(page, 3), qw);
>        m.addAttribute("info", iPage);
>        return "list";
> }
> ```









