# 1、什么是SpringMVC

![image-20250311084628473](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311084628473.png)



# 2、SpringMVC 执行的流程

![image-20250311084808447](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311084808447.png)

![image-20250311090543760](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311090543760.png)



> 简单说：
>
> ​	用户发送请求，被DispatherServlet 拦截，通过HandlerMapping映射处理器，找到对应的Controller控制器
>
> ​	在控制器中处理请求与响应结果，将数据封装到ModelAndView中，在通过ViewResolver  指定页面的前缀与后缀，拼接
>
> ​	ModelAndView中的视图名称，找到要渲染的页面，最终将ModelAndView中的数据渲染到视图中。



# 3、项目演示

## 3.1 搭建项目

![image-20250311091119297](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311091119297.png)



![image-20250311091149504](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311091149504.png)



![image-20250311091448958](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311091448958.png)



引入依赖：

```xml
<dependencies>
        <!--servlet 依赖-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>
        <!--webmvc 依赖-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.0.5.RELEASE</version>
        </dependency>
    </dependencies>
```



tomcat部署项目

![image-20250311092435187](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311092435187.png)

![image-20250311092445047](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311092445047.png)

![image-20250311094857342](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311094857342.png)

springmvc的配置文件

```java
// springmvc的配置文件
@Configuration //配置文件
@ComponentScan("com.zretc.controller")
public class SpringMvcConfig {
}
```



核心配置文件，相当于web.xml

```java
import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;
// 相当于 web.xml
public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[0]; // spring 配置类
    }

    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class}; // springmvc配置类
    }

    @Override
    protected String[] getServletMappings() {// 由springmvc控制器处理的请求映射路径
        return new String[]{"/"}; // / 任意请求都会被拦截
    }
}
```

控制器

```java
@Controller
public class UserController {

    @RequestMapping("/selectAll") // 映射该方法的请求路径
    @ResponseBody // 将return的值响应到前端
    public String selectAll(){
        System.out.println("{'msg','selectAll'}");
        return "{'msg','selectAll'}";
    }
}
```



![image-20250311105636231](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311105636231.png)

![image-20250311140147343](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311140147343.png)

# 4、 配置文件

![image-20250311105822266](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311105822266.png)



![image-20250311105836890](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311105836890.png)

![image-20250311105948122](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311105948122.png)

![image-20250311140206967](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311140206967.png)



## 4.1 项目演示

引入依赖

```xml
<dependencies>
        <!--servlet 依赖-->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
            <scope>provided</scope>
        </dependency>
        <!--webmvc 依赖-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.0.5.RELEASE</version>
        </dependency>
    </dependencies>
```

spring配置文件

```java
@Configuration
// 一：精准扫描，service,dao
//@ComponentScan({"com.zretc.service","com.zretc.dao"})
// 二：扫描全包，排除controller
@ComponentScan(value = "com.zretc",
        excludeFilters = @ComponentScan.Filter(
                type = FilterType.ANNOTATION,
                classes = Controller.class
        ))
public class SpringConfig {
}
```

springmvc配置类

```java
// springmvc的配置文件
@Configuration //配置文件
@ComponentScan("com.zretc.controller")
public class SpringMvcConfig {
}
```



核心配置类：

```java
import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;
// 相当于 web.xml
public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[0]; // spring 配置类
    }

    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class}; // springmvc配置类
    }

    @Override
    protected String[] getServletMappings() {// 由springmvc控制器处理的请求映射路径
        return new String[]{"/"}; // / 任意请求都会被拦截
    }
}
```





# 5、请求映射路径



![image-20250311140239510](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311140239510.png)



![image-20250311140401564](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311140401564.png)

导入依赖

```xml
<dependencies>
        <!--    springmvc    -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.0.5.RELEASE</version>
        </dependency>
        <!--    servlet 请求和响应    -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
```



导入配置类：

![image-20250311140811985](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311140811985.png)



```java
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.FilterType;
import org.springframework.stereotype.Controller;

@Configuration
// 一：精准扫描，service,dao
//@ComponentScan({"com.zretc.service","com.zretc.dao"})
// 二：扫描全包，排除controller
@ComponentScan(value = "com.zretc",
        excludeFilters = @ComponentScan.Filter(
                type = FilterType.ANNOTATION,
                classes = Controller.class
        ))
public class SpringConfig {
}



// springmvc的配置文件
@Configuration //配置文件
@ComponentScan("com.zretc.controller")
public class SpringMvcConfig {
}


// 相当于 web.xml
public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class}; // spring 配置类
    }

    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class}; // springmvc配置类
    }

    @Override
    protected String[] getServletMappings() {// 由springmvc控制器处理的请求映射路径
        return new String[]{"/"}; // / 任意请求都会被拦截
    }
}
```



index.jsp中页面跳转，发送请求，跳转到登录页面

```jsp
<html>
<body>
<%-- 发送请求 --%>
<%
    response.sendRedirect("/hello");
%>
</body>
</html>
```



HelloController

```java
@Controller
public class HelloController {
    // 映射请求路径，处理请求
    @RequestMapping("/hello")
    public String hello(){
        System.out.println("hello哈哈哈");
        // 跳转到登录页面
        return "/pages/login.jsp";
    }
    
}

```

新建pages目录，创建login.jsp 与 success.jsp页面

![image-20250311145702763](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311145702763.png)



login.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <form action="/login" method="post">
        username:<input type="text" name="username"/><br>
        password:<input type="password" name="password"/><br>
        <input type="submit" value="登录">
    </form>
</body>
</html>
```

success.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
登录成功
</body>
</html>
```



```java
@Controller
public class HelloController {
    // 映射请求路径，处理请求
    @RequestMapping("/hello")
    public String hello(){
        System.out.println("hello哈哈哈");
        // 跳转到登录页面
        return "/pages/login.jsp";
    }
    
    @RequestMapping("/login")
    public String login(HttpServletRequest request){
        String username = request.getParameter("username");
        System.out.println("username = " + username);
        // 获取请求参数
        // 访问service
        return "/pages/success.jsp";
    }
}
```

![image-20250311145856872](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311145856872.png)

![image-20250311145913324](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311145913324.png)

![image-20250311160420578](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311160420578.png)

用户下有登录、注册等功能都是 AdminController 处理的请求，可以加一个通用的请求路径，在控制层上

index.jsp

```jsp
<html>
<body>
<%-- 发送请求 --%>
<%
    response.sendRedirect("/admin/hello");
%>
</body>
</html>
```



login.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <form action="/admin/login" method="post">
        username:<input type="text" name="username"/><br>
        password:<input type="password" name="password"/><br>
        <input type="submit" value="登录">
    </form>
</body>
</html>
```



HelloController

```java
@Controller
@RequestMapping("/admin/")
public class HelloController {
    // 映射请求路径，处理请求
    @RequestMapping("hello")
    public String hello(){
        System.out.println("hello哈哈哈");
        // 跳转到登录页面
        return "/pages/login.jsp";
    }
    
    @RequestMapping("login")
    public String login(HttpServletRequest request){
        String username = request.getParameter("username");
        System.out.println("username = " + username);
        // 获取请求参数
        // 访问service
        return "/pages/success.jsp";
    }
}
```



## 5.1  视图解析器

指定视图的前缀与后缀，跳转页面时，只需要指定页面的名称



在SpringMvcConfig 中配置视图解析器

```java
// springmvc的配置文件
@Configuration //配置文件
@ComponentScan("com.zretc.controller")
@EnableWebMvc
public class SpringMvcConfig implements WebMvcConfigurer {
    // 视图解析器

    @Override
    public void configureViewResolvers(ViewResolverRegistry registry) {
        // 指定页面的前缀和后缀
        registry.jsp("/pages/",".jsp");
    }
}
```

控制器中只需要指定页面的名称，省略前缀与后缀

```java
@Controller
@RequestMapping("/admin/")
public class HelloController {
    // 映射请求路径，处理请求
    @RequestMapping("hello")
    public String hello(){
        System.out.println("hello哈哈哈");
        // 跳转到登录页面
//        return "/pages/login.jsp";
        return "login"; // 去掉前缀和后缀
    }
    
    @RequestMapping("login")
    public String login(HttpServletRequest request){
        String username = request.getParameter("username");
        System.out.println("username = " + username);
        // 获取请求参数
        // 访问service
//        return "/pages/success.jsp";
        return "success";
    }
}
```





# 6、获取请求参数与传递参数

![image-20250311151604691](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311151604691.png)



## 6.1 使用request对象传递参数

```java
    @RequestMapping("login")
    public String login(HttpServletRequest request){
        String username = request.getParameter("username");
        System.out.println("username = " + username);
        request.setAttribute("username",username);
        return "success";
    }
```

jsp页面的中的el表达式默认情况是关闭的，需要手动打开

success.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ page isELIgnored="false" %>  <%--默认el表达式是关闭状态，需要手动代开--%>
<html>
<head>
    <title>Title</title>
</head>
<body>
登录成功,欢迎您：${username}
</body>
</html>
```



## 6.2 使用ModelAndView 传递请求参数

- **addObject（key,value）** 存储数据

```java
    // 使用ModelAndView 存储数据，指定跳转的页面
    @RequestMapping("login")
	// 表单中的数据自动赋值给函数的参数上
    public ModelAndView login(String username){
        ModelAndView mav = new ModelAndView("success");// 构造参数是跳转的页面名称
        // 存储数据
        mav.addObject("username",username);
         // 设置跳转的路径
//        mav.setViewName("success");
        return mav;
    }
```



注意：表单中的数据自动赋值给函数的参数上
			函数的参数名称必须要与表单中的name属性相同，才能自动映射数据。



==@RequestParam 注解，获取请求参数==

```
当表单中的name属性与方法的形参不同时，可以使用@RequestParam映射
```

将 login.jsp 中的name属性改了

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <form action="/admin/login" method="get">
        username:<input type="text" name="admin_name"/><br>
        password:<input type="password" name="admin_password"/><br>
        <input type="submit" value="登录">
    </form>
</body>
</html>
```



```java
    // 使用ModelAndView 存储数据，指定跳转的页面
    @RequestMapping("login")
    // 当表单中的name属性与方法的形参不同时，可以使用@RequestParam映射
    public ModelAndView login(@RequestParam("admin_name") String username){
        ModelAndView mav = new ModelAndView("success");// 构造参数是跳转的页面名称
        // 存储数据
        mav.addObject("username",username);
        // 设置跳转的路径
//        mav.setViewName("success");
        return mav;
    }
```



## 6.3 使用Model对象传递请求参数

- **addAttribute（） 存储数据**

```
将表单中的数据直接映射给实体类中的成员变量
前提：表单的name属性必须与实体类的变量名相同
```

login.jsp 的name属性必须与实体类变量名一致

```java
    // 使用Model传递参数
    @RequestMapping("login")
    // 将表单中的数据直接映射给实体类中的成员变量
    // 前提：表单的name属性必须与实体类的变量名相同
    public String login(Admin admin, Model model){
//        model.addAttribute("username",admin.getAdmin_name());
        // 直接将对象添加到model中
        model.addAttribute("admin",admin);
        return "success";
    }
```



success.jsp

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ page isELIgnored="false" %>  <%--默认el表达式是关闭状态，需要手动代开--%>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%--登录成功,欢迎您：${username}--%>
登录成功,欢迎您：${admin.admin_name} , ${admin.admin_password}
</body>
</html>
```

![image-20250311155218516](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311155218516.png)



**请求时的中文乱码;**

![image-20250311155330688](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311155330688.png)



**在核心配置文件中注册过滤器;**

```java
// 相当于 web.xml
public class ServletContainersInitConfig extends AbstractAnnotationConfigDispatcherServletInitializer {
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class[]{SpringConfig.class}; // spring 配置类
    }

    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class[]{SpringMvcConfig.class}; // springmvc配置类
    }

    @Override
    protected String[] getServletMappings() {// 由springmvc控制器处理的请求映射路径
        return new String[]{"/"}; // / 任意请求都会被拦截
    }

    // 注册过滤器--解决post请求的中文乱码问题
    @Override
    protected Filter[] getServletFilters() {
        CharacterEncodingFilter character = new CharacterEncodingFilter();
        character.setEncoding("utf-8");
        return new Filter[]{character};
    }
```

![image-20250311155720933](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311155720933.png)

![image-20250311155705262](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311155705262.png)



## 6.4 使用ModelMap传递请求参数

- addAttribute（） 存储数据

```java
    // 使用ModelMap传递参数
    @RequestMapping("login")
    // 将表单中的数据直接映射给实体类中的成员变量
    // 前提：表单的name属性必须与实体类的变量名相同
    public String login(Admin admin, ModelMap model){
//        model.addAttribute("username",admin.getAdmin_name());
        // 直接将对象添加到model中
        model.addAttribute("admin",admin);
        return "success";
    }
```



## 6.5 直接通过实体类映射

- 将表单中的数据直接映射给实体类中的**成员变量**
- 前提：表单的**name属性**必须与实体类的**变量名相同**

```java
    // 使用实体类映射
    @RequestMapping("login")
    // 将表单中的数据直接映射给实体类中的成员变量
    // 前提：表单的name属性必须与实体类的变量名相同
    public String login(Admin admin){
        return "success";
    }
```



==@ModelAttribute 给实体类起别名==，在前端中使用别名获取请求参数，如果没有起别名，默认就是类名首字母小写。

```java
    // 使用实体类映射
    @RequestMapping("login")
    // 将表单中的数据直接映射给实体类中的成员变量
    // 前提：表单的name属性必须与实体类的变量名相同
    public String login(@ModelAttribute("aa") Admin admin){
        return "success";
    }
```



success.jsp

```jsp
<body>
<%--登录成功,欢迎您：${username}--%>
登录成功,欢迎您：${aa.admin_name} , ${aa.admin_password}
</body>
```



## 6.6 嵌套pojo参数 

请求参数名与形参对象属性名相同，按照对象层次结构关系即可接收**嵌套POJO属性参数**

**Address**

```java
@Data
public class Address {
    private String city;
}
```



**Admin**

```java
@Data
public class Admin {
    private String admin_name;
    private String admin_password;
    // 用户的地址
    private Address address;
}
```



**login.jsp**

```jsp
<body>
    <form action="/admin/login" method="post">
        username:<input type="text" name="admin_name"/><br>
        password:<input type="password" name="admin_password"/><br>
        city:
        <select name="address.city">
            <option value="大连">大连</option>
            <option value="鞍山">鞍山</option>
            <option value="沈阳">沈阳</option>
        </select>
        <input type="submit" value="登录">
    </form>
</body>
```

**HelloController**

```java
    // 使用实体类映射
    @RequestMapping("login")
    // 将表单中的数据直接映射给实体类中的成员变量
    // 前提：表单的name属性必须与实体类的变量名相同
    public String login(@ModelAttribute("aa") Admin admin){
        return "success";
    }
```



**success.jsp**

```jsp
<body>
<%--登录成功,欢迎您：${username}--%>
登录成功,欢迎您：${aa.admin_name} , ${aa.admin_password} ,${aa.address.city}
</body>
```



![image-20250311163636934](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311163636934.png)

![image-20250311163643476](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311163643476.png)



## 6.7 使用数组类型的参数传递参数

![image-20250311164520763](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311164520763.png)

![image-20250311164710296](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311164710296.png)



```java
@Data
public class Admin {
    private String admin_name;
    private String admin_password;
    // 用户的地址
    private Address address;
    // 兴趣爱好
    private String[] like;
}
```



login.jsp

```jsp
<body>
    <form action="/admin/login" method="post">
        username:<input type="text" name="admin_name"/><br>
        password:<input type="password" name="admin_password"/><br>
        city:
        <select name="address.city">
            <option value="大连">大连</option>
            <option value="鞍山">鞍山</option>
            <option value="沈阳">沈阳</option>
        </select>
        <br>
        兴趣：
        <input type="checkbox" name="like" value="睡觉">睡觉
        <input type="checkbox" name="like" value="看书">看书
        <input type="checkbox" name="like" value="吃饭">吃饭
        <br>
        <input type="submit" value="登录">
    </form>
</body>
```



success.jsp

```jsp
<body>
<%--登录成功,欢迎您：${username}--%>
登录成功,欢迎您：${aa.admin_name} , ${aa.admin_password} ,
${aa.address.city}, ${aa.like}
<%
    String[] like = request.getParameterValues("like");
    for (String ll : like) {
%>
        <p><%=ll%></p>
<%
    }
%>
</body>
```

![image-20250311165223596](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311165223596.png)



**也可以直接映射到数组类型的形参中，前提是形参的名字必须与表单的name一致**

```java
    // 使用实体类映射
    @RequestMapping("login")
    // 将checkbox中选中的数据直接存储到like这个数组中
    public String login(String[] like){
        return "success";
    }
```

![image-20250311165834859](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311165834859.png)



## 6.8 使用集合映射数据

```java
    //使用集合映射
    @RequestMapping("login")
    // 将checkbox中选中的数据直接存储到like这个数组中
    public String login(List<String> like){
        return "success";
    }
```

![image-20250311170114044](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311170114044.png)

==**解决方案：使用 @RequestParam**==

```java
    //使用集合映射
    @RequestMapping("login")
    // 将checkbox中选中的数据直接存储到like这个数组中
    public String login(@RequestParam List<String> like){
        return "success";
    }
```

![image-20250311170339920](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311170339920.png)

![image-20250311170311918](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311170311918.png)

![image-20250311170322219](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250311170322219.png)





# 7、请求转发和响应重定向

![image-20250312090256403](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312090256403.png)

## 7.1 请求转发

```java
@Controller
@RequestMapping("/admin/")
public class HelloController {

    // 映射请求路径，处理请求
    @RequestMapping("hello")
//    @ResponseBody // 将return 后的值响应到前端
    public String hello(){
        System.out.println("hello哈哈哈");
        // 跳转到登录页面
//        return "/pages/login.jsp";
        return "login"; // 去掉前缀和后缀
    }    
	//使用集合映射
    @RequestMapping("login")
    // 将checkbox中选中的数据直接存储到like这个数组中
    public String login(@RequestParam List<String> like){
        // 1.请求转发到
        //    可以传递请求参数，请求路径不变
        return "forward:method";
        // 2. 响应重定向
            // 不能传递请求参数，请求路径改变
//        return "redirect:method";
    }

    // 请求转达与响应重定向
    @RequestMapping("method")
    public String method(){
        return "success";
    }
```

![image-20250312092228129](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312092228129.png)



## 7.2 响应重定向

```java
@Controller
@RequestMapping("/admin/")
public class HelloController {

    // 映射请求路径，处理请求
    @RequestMapping("hello")
//    @ResponseBody // 将return 后的值响应到前端
    public String hello(){
        System.out.println("hello哈哈哈");
        // 跳转到登录页面
//        return "/pages/login.jsp";
        return "login"; // 去掉前缀和后缀
    }    
	//使用集合映射
    @RequestMapping("login")
    // 将checkbox中选中的数据直接存储到like这个数组中
    public String login(@RequestParam List<String> like){
        // 1.请求转发到
        //    可以传递请求参数，请求路径不变
//        return "forward:method";
        // 2. 响应重定向
            // 不能传递请求参数，请求路径改变
        return "redirect:method";
    }

    // 请求转达与响应重定向
    @RequestMapping("method")
    public String method(){
        return "success";
    }
```

加一个条件判断不为空的情况下，在遍历数据，否则会抛出空指针

```jsp
<body>
<%--登录成功,欢迎您：${username}--%>
登录成功,欢迎您：${aa.admin_name} , ${aa.admin_password} ,
${aa.address.city}, ${aa.like}
<%
    String[] like = request.getParameterValues("like");
    if(like != null){
        for (String ll : like) {
%>
         <p><%=ll%></p>
<%
        }
    }
%>
</body>
```

![image-20250312092301296](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312092301296.png)





# 8、响应数据

![image-20250312092827369](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312092827369.png)



导入依赖：

```xml
<dependencies>
        <!--  springmvc的依赖  -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.0.5.RELEASE</version>
        </dependency>
        <!--  请求Servlet  -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>4.0.1</version>
        </dependency>
        <!--    封装    -->
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.30</version>
        </dependency>
        <!--    json格式的数据转换    -->
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.15.3</version>
        </dependency>
    </dependencies>
```





# 8.1 响应数据的格式

==@ResponseBody // 将return后的结果响应到客户端==

### 8.1.1 响应文本

响应的数据可以是一个普通的文本

index.jsp

```jsp
  <body>
    <%
        response.sendRedirect("/index");
    %>
  </body>
```



HelloController

```java
@Controller
public class HelloController {
    @RequestMapping("/index")
    public String index(){
        return "success"; // 跳转到 /pages/success.jsp 页面中
    }

    @RequestMapping("/toText")
    @ResponseBody // 将return后的结果响应到客户端
    public String toText(){
        return "{'data':'text'}";
    }
}
```

![image-20250312101257988](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312101257988.png)

success.jsp

```jsp
<body>
成功页面
<button onclick="method()">发送请求，将数据响应到客户端</button>
<script>
    function method(){
        location.href='/toText';
    }
</script>
```

![image-20250312101339630](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312101339630.png)

![image-20250312101347075](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312101347075.png)



### 8.1.2  Json数据传输参数

![image-20250312100149433](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312100149433.png)



#### 8.1.2.1 Json普通数组

![image-20250312102047727](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312102047727.png)

pom.xml文件中引入依赖

```xml
<!--    json格式的数据转换    -->
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.15.3</version>
        </dependency>
```



开启springmvc 注解的支持

![image-20250312102147021](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312102147021.png)

![image-20250312102402483](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312102402483.png)

![image-20250312102200892](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312102200892.png)



**参数前添加 @RequestBody**

![image-20250312102346452](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312102346452.png)

![image-20250312102413460](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312102413460.png)

controller中定义请求方法：

```java
    // json格式的数组/集合参数传输数据
    @RequestMapping("/listParamForJson")
    @ResponseBody // 将数据响应到客户端
    public String listParamForJson(@RequestBody List<String> like){ // @RequestBody 将json格式的数据映射到当前参数中
        System.out.println("like = " + like);
        return "{'data':'json格式的数组/集合参数传输数据'}";
    }
```



使用 ApiFox 演示json 格式的数据传输

第一步：创建一个目录

![image-20250312102605843](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312102605843.png)

![image-20250312102644295](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312102644295.png)

第二步：添加接口

![image-20250312103152728](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250312103152728.png)