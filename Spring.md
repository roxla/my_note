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

> 
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
> 































