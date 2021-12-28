Spring MVC

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

> **概述**
>
> Maven 翻译为"专家"、"内行"，是 Apache 下的一个纯 Java 开发的开源项目。基于项目对象模型（缩写：POM）概念，Maven利用一个中央信息片断能管理一个项目的构建、报告和文档等步骤。
>
> Maven 是一个项目管理工具，可以对 Java 项目进行构建、依赖管理。
>
> Maven 也可被用于构建和管理各种项目，例如 C#，Ruby，Scala 和其他语言编写的项目。Maven 曾是 Jakarta 项目的子项目，现为由 Apache 软件基金会主持的独立 Apache 项目。

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

##### dao层

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

##### service层

> **新的 service 基类 IService2**
>
> ```java
> public interface IService2<T> extends IService<T> {
>     T getById2(Serializable id);
> 
>     T getOne2(Wrapper<T> queryWrapper);
> 
>     int count2(Wrapper<T> queryWrapper);
> 
>     List<T> list2(Wrapper<T> queryWrapper);
> 
>     List<T> list2();
> 
>     <E extends IPage<T>> E page2(E page, Wrapper<T> queryWrapper);
> }
> ```
>
> **新的 serviceimpl 基类 ServiceImpl2**
>
> ```java
> public class ServiceImpl2<M extends BaseMapper2<T>, T> extends ServiceImpl<M, T> implements IService2<T> {
> 
>     private M baseMapper2;
> 
>     @Autowired
>     public void setBaseMapper2(M baseMapper2) {
>         this.baseMapper2 = baseMapper2;
>     }
> 
>     @Override
>     public T getById2(Serializable id) {
>         return baseMapper2.selectById2(id);
>     }
> 
>     @Override
>     public T getOne2(Wrapper<T> queryWrapper) {
>         return baseMapper2.selectOne2(queryWrapper);
>     }
> 
>     @Override
>     public int count2(Wrapper queryWrapper) {
>         return baseMapper2.selectCount2(queryWrapper);
>     }
> 
>     @Override
>     public List list2(Wrapper queryWrapper) {
>         return baseMapper2.selectList2(queryWrapper);
>     }
> 
>     @Override
>     public List list2() {
>         return baseMapper2.selectAll2();
>     }
> 
>     @Override
>     public IPage page2(IPage page, Wrapper queryWrapper) {
>         return baseMapper2.selectPage2(page, queryWrapper);
>     }
> }
> ```
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
> 自己扩充一个 MyPage 类，该类继承 Page 类
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
> 使用我们扩充的类，返回值传到 JSP 界面上的其实是我们这个扩充的MyPage类对象
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

## 工作流

> 

### 工作流的生成

> **idea**的工作流插件有bug，对中文的支持不行，所以最好使用**eclipse**来进行工作流文件的生成
>
> **步骤**
>
> 1. 拷贝工作流画图插件到**eclipse的dropins**(不要新建文件夹)，重启
> 2. 新建**Activiti Diagram**(流程图)文件
>    - 该文件其实是用图形来书写 xml 文件
> 3. 在流程图文件中画流程
>    - 示例：![][1]
>    - Activiti提供了图形化的操作页面，我们可以拖动图形控件设计符合特定规则的流程
>      - StartEvent：开始事件
>      - EndEvent：结束事件
>      - UserTask：任务
>      - SequenceFlow：用于连接 Task
>      - ExclusiveGateway：条件判断
>    - 在 Properties 下，我们可以看到该工作流图以及每个节点、每条线的详细配置
>      - 点击文件空白处，进入 Process
>        - Id：整张图的 id，注意调整，数据库的列会记录，会影响代码中的 key
>          - 该示例中，设置 id 为**baoxiao**
>        - Name：整张图的名字，注意调整，数据库的列会记录，会影响代码中的 key
>          - 该示例中，设置 name 为**bao_xiao**
>        - Namespace：命名空间，一般会起自己公司的域名
>      - 点击连接的箭头，进入 Main config
>        - Condition：用于书写判断的表达式(**${result=="同意"}**)
>          - 如果有多个出口，需要写表达式区分，result是自己起的，和java代码相吻合即可
>          - 值建议和线条的名字相同
>      - 点击 UserTask，进入 Main config
>        - 这里配置的是指定谁能运行(或审批)这个任务
>          - Assignee：单人任务(**${userkey}**)
>            - ${userkey} 只是一个占位符，具体的值从 java 中传入；占位符的名称要和 java 中的对应
>          - Candidate use...ma separated)：多人任务(**${method.getPower("报销部门审批",userkey)}**)
>            - method：xml 配的 key，代表某个对象
>            - getPower：java 方法，负责去数据库查询生僻人有哪些，后面的参数，按需要自行组织
> 4. 右键文件空白处，选择 Export Diagram，**导出JPG格式图片**，需要一起上传数据库
>    - 不要调整图片的原始大小
> 5. 将**图片**和**流程图文件**打包成一个**ZIP**文件

### 工作流的上传

#### 在 pom.xml 中添加 jar 包
> **pom.xml**
> 
> ```xml
> <properties>
>     <activiti-version>5.18.0</activiti-version>
> </properties>
> ...
> <dependency>
>     <groupId>org.activiti</groupId>
>     <artifactId>activiti-engine</artifactId>
>     <version>${activiti-version}</version>
> </dependency>
> <dependency>
>     <groupId>org.activiti</groupId>
>     <artifactId>activiti-spring</artifactId>
>     <version>${activiti-version}</version>
> </dependency>
> ```

#### 创建数据库表

> 在 maven 仓库中的**activiti-engine-5.18.0.jar 的 org.activiti.db.create**下，将**activiti.mysql.create.engine.sql，activiti.mysql.create.history.sql，activiti.mysql.create.identity.sql**三个文件中的**脚本拷贝到工程所使用的数据库表**中，运行脚本，生成**24张表**。
>
> *用代码建表*
>
> 实际流程与手动建表一致，只是使用代码进行自动化实现
>
> ```java
> public class ActivitiTest {
>     ProcessEngine processEngine = ProcessEngines.getDefaultProcessEngine();
> 
>     @Test
>     public void createTables(){
>         ProcessEngineConfiguration processEngineConfiguration = ProcessEngineConfiguration.createStandaloneProcessEngineConfiguration();
>         processEngineConfiguration.setJdbcDriver("com.mysql.jdbc.Driver");
>         processEngineConfiguration.setJdbcUrl("jdbc:mysql://localhost:3306/lpinfo-activiti?useUnicode=true&amp;characterEncoding=utf8");
>         processEngineConfiguration.setJdbcUsername("root");
>         processEngineConfiguration.setJdbcPassword("root");
>         processEngineConfiguration.setDatabaseSchemaUpdate(ProcessEngineConfiguration.DB_SCHEMA_UPDATE_CREATE_DROP);
>         processEngineConfiguration.buildProcessEngine();
>     }
> }
> ```

#### 在applicationContext.xml中添加activiti的配置，或新建.xml文件再import进来

> **applicationContext-activiti.xml**
>
> ```xml
> <?xml version="1.0" encoding="UTF-8"?>
> <beans xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>        xmlns="http://www.springframework.org/schema/beans" 
>        xmlns:aop="http://www.springframework.org/schema/aop"
>        xmlns:context="http://www.springframework.org/schema/context" 
> 
>        xmlns:tx="http://www.springframework.org/schema/tx"
>        xmlns:cache="http://www.springframework.org/schema/cache"
>        xmlns:p="http://www.springframework.org/schema/p"
>        xsi:schemaLocation="http://www.springframework.org/schema/beans 
>                            http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
>                            http://www.springframework.org/schema/aop
>                            http://www.springframework.org/schema/aop/spring-aop-4.0.xsd
>                            http://www.springframework.org/schema/context
>                            http://www.springframework.org/schema/context/spring-context-4.0.xsd
>                            http://www.springframework.org/schema/tx
>                            http://www.springframework.org/schema/tx/spring-tx-4.0.xsd
>                            http://www.springframework.org/schema/cache 
>                            http://www.springframework.org/schema/cache/spring-cache-4.0.xsd">
>     <!-- spring负责创建流程引擎的配置文件 -->
>     <bean id="processEngineConfiguration" class="org.activiti.spring.SpringProcessEngineConfiguration">
>         <!-- 数据源 -->
>         <property name="dataSource" ref="dataSource" />
>         <!-- 配置事务管理器，统一事务 -->
>         <property name="transactionManager" ref="txManager" />
>         <!-- 设置建表策略，如果没有表，自动创建表 -->
>         <property name="databaseSchemaUpdate" value="true" />
>         <property name="beans">
>             <map>
>                 <entry key="method" value-ref="workflowbrige" />
>             </map>
>         </property>
>     </bean>
>     <!-- 创建流程引擎对象 工作流的核心对象 -->
>     <bean id="processEngine" class="org.activiti.spring.ProcessEngineFactoryBean">
>         <property name="processEngineConfiguration" ref="processEngineConfiguration" />
>     </bean>
>     <!-- 
>  相当于下面的代码
>  RepositoryServicie repositoryService = processEngine.getRepositoryService();
>  RuntimeServicie repositoryService = processEngine.getRuntimeServicie();
>  TaskServicie taskServicie = processEngine.getTaskServicie();
>  HistoryServicie historyServicie = processEngine.getHistoryServicie();
>   -->
>     <!-- 由流程引擎对象，提供的方法，创建项目中使用的Activiti工作流的Service -->
>     <bean id="repositoryService" factory-bean="processEngine" factory-method="getRepositoryService" />
>     <bean id="runtimeService" factory-bean="processEngine" factory-method="getRuntimeService" />
>     <bean id="taskService" factory-bean="processEngine" factory-method="getTaskService" />
>     <bean id="historyService" factory-bean="processEngine" factory-method="getHistoryService" />
>     <bean id="formService" factory-bean="processEngine" factory-method="getFormService" />
> </beans>
> ```
>
> *新建的 .xml 文件中配置的id要和 applicationContext.xml 文件中配置的id一致*
>

#### 修改 web.xml 文件

> **将下面代码中的 classpath:applicationContext.xml 修改为 classpath:applicationContext*.xml**
>
> ```xml
> <context-param>
>  <param-name>contextConfigLocation</param-name>
>     <!-- 使用通配符 * 配置一次性加载多个文件 -->
>     <param-value>classpath:applicationContext*.xml</param-value>
>    </context-param>
> ```
>    

#### 添加上传用的页面

> **ApproveController.java**
>
> ```java
> @Controller
> public class ApproveController {
>     @Autowired
>     private ApproveService service;
> 
>     @GetMapping("/admin/deploy")
>     public String deploy() {
>         return "admin_design";
>     }
> 
>     @PostMapping("/admin/deploy")
>     public String deploy(String name, MultipartFile design) throws IOException {
>         service.addDeploys(name, design.getInputStream());
>         return "redirect:/admin/deploy_list";
>     }
> 
>     @GetMapping("/admin/deploy_list")
>     public String deployList(Model m) {
>         List<Deployment> list = service.findDeploys();
>         m.addAttribute("list", list);
>         return "admin_design_list";
>     }
> 
>     @GetMapping("/admin/del")
>     public String del(String id) {
>         service.removeDeploy(id);
>         return "redirect:/admin/deploy_list";
>     }
> }
> ```
>
> **admin_design.jsp**
>
> ```jsp
> <%@ page language="java" contentType="text/html; charset=UTF-8"
>     pageEncoding="UTF-8"%>
> <!DOCTYPE html>
> <html><head>
>     <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
>     <title>新增工作</title>
>     <style>
>         #main{margin:0 auto;width:50%}
>         table{width:100%;border-spacing: 10px 30px;border-top:1px solid #ccc;border-bottom:1px solid #ccc}
>         th{border-bottom:2px solid #ccc;}
>         td{text-align:left;width:50%}
>         tr td:first-child{text-align:right;}
>         tr:last-child td:last-child{padding-left:20px}
>         h1{text-align:center}
>         input[type=text]{border-width:0px 0px 2px 0px;border-color:black}
>         input:focus{border-color:red}
>     </style>
>     <script>
>     </script>
>     </head>
>     <body>
>         <div id="main">
>             <h1>新增流程</h1>
>             <form action="" method="post" enctype="multipart/form-data">
>                 <table>
>                     <tbody>
>                         <tr>
>                             <td>流程名称</td>
>                             <td><input type="text" name="name"/></td>
>                         </tr>
>                         <tr>
>                             <td>流程文件</td>
>                             <td>
>                                 <input type="file" name="design"/>
>                             </td>
>                         </tr>
>                         <tr>
>                             <td><input type="submit" value="添加流程"></td>
>                             <td><input type="reset" value="重置"></td>
>                         </tr>
>                     </tbody>
>                 </table>
>             </form>
>         </div>
>     </body>
> </html>
> ```
>
> **admin_design_list.jsp**
>
> ```jsp
> <%@ page language="java" contentType="text/html; charset=UTF-8"
>     pageEncoding="UTF-8"%>
> <%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
> <%@taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %>
> <!DOCTYPE html>
> <html><head>
>     <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
>     <title>设计流程列表</title>
>     <style>
>         th{border-bottom:2px solid #ccc;}
>         td{border-bottom:1px solid #ccc; text-align:center}
>         h1{text-align:center}
>         tr td:last-child {text-align:left;width:300px;}
>         tr td:last-child a:first-child{margin-left:50px}
>     </style>
>     <script>
>     </script>
>     </head>
>     <body>
>         <h1>设计流程列表</h1>
>         <c:if test="${ispower}">
>             <a href="deploy">新增流程设计</a>
>         </c:if>
>         <table align="center" width="60%" cellspacing="0px">
> 
>             <tbody>
>                 <tr>
>                     <th>编号</th>
>                     <th>类型</th>
>                     <th>名字</th>
>                     <th>租户</th>
>                     <th>申请时间</th>
>                     <th>操作 <a href="/baoxiao/web/admin/adddesign">新增记录</a></th>
>                 </tr>
> 
>                 <c:forEach var="a" items="${list}">
>                     <tr>
>                         <td>${a.id}</td>
>                         <td>${a.category}</td>
>                         <td>${a.name}</td>
>                         <td>${a.tenantId}</td>
>                         <td><fmt:formatDate value="${a.deploymentTime}" pattern="yyyy/MM/dd HH:mm"/> </td>
>                         <td>
>                             <a href="del?id=${a.id}">删除</a>
>                         </td>
>                     </tr>
>                 </c:forEach>   
>             </tbody>
>         </table>
>     </body>
> </html>
> ```
>
> 

### 工作流的使用

> 1







****

base64:

[1]:data:image/png;base64,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

