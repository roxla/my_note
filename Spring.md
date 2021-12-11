## Spring MVC

> **概述**
>
> 

### Spring MVC 的架构

> 

### Spring MVC 配置

#### 配置 web.xml 文件

> spring-mvc.xml

#### 配置 spring-mvc.xml 文件

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
>        LinkService service = new LinkServiceImpl();
>        service.add(lk);
>        return "redirect:/link/list";
> }
> ```
>
> 如需要传递数据到页面，可以使用 Model
>
> ```java
> @PostMapping("/link/list")
> public String showList(Model m) {
>        LinkService service = new LinkServiceImpl();
>        List<Link> links = service.findAll(lk);
>        m.setAttribute
>        return "redirect:/link/list";
> }
> ```
>
> 也可以传递一些原生对象；需要什么，就自己传什么
>
> ```java
> @PostMapping("/link/list")
> public String showList(HttpServletRequest req) {
>        LinkService service = new LinkServiceImpl();
>        List<Link> links = service.findAll(lk);
>        req.setAttribute
>            return "redirect:/link/list";
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

##### 视图解析器

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

> 
>
> ```java
> @DateTimeFormat(pattern = "yyyy-MM-dd")
> ```
>
> 

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

> 
>
> **LoginInterceptor类**
>
> ```java
> public class LoginInterceptor implements HandlerInterceptor {
>     @Override
>        public boolean preHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o) throws Exception {
>            // 进来时候拦截
>            if (httpServletRequest.getSession().getAttribute("user") == null) {
>                httpServletResponse.sendRedirect("/PhoneBook/login");
>                return false;
>            }
>            return true;
>        }
>    
>     @Override
>        public void postHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, ModelAndView modelAndView) throws Exception {
>            // 回去时候拦截
>        }
>    
>     @Override
>        public void afterCompletion(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) throws Exception {
>            // 每次拦截后，必须要做的动作
>        }
>    }
> ```
> 
>**配置 spring-mvc.xml**
> 
>添加代码：
> 
>```xml
> <mvc:interceptors>
> <mvc:interceptor>
>    <mvc:mapping path="/**"/>
>      <mvc:exclude-mapping path="/login"/>
>      <mvc:exclude-mapping path="/reg"/>
>      <bean class="com.roxla.it.web.interceptor.LoginInterceptor"></bean>
>    </mvc:interceptor>
>  </mvc:interceptors>
> ```
> 
>- `<mvc:interceptors>`：
> - `<mvc:interceptor>`：
> - `<mvc:mapping path="/**"/>`：
> - `<mvc:exclude-mapping path="/login"/>`：
> - `<bean class="com.roxla.it.web.interceptor.LoginInterceptor">`：
> 
>**可以配置多个拦截器**
> 
>多个拦截器之间根据上下的顺序来确定执行的先后

## MyBatis

> **概述**
>
> 































