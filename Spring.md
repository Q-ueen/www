# 1、Spring是什么

spring是一个高度灵活的**轻量级框架**，其目的是降低企业级应用开发的复杂度。

MVC设计模式：

​	model 

​		模型

​		pojo : 封装类，一张表对应着一个实体类

​		dao  ：数据访问层，增（insert）删 (delete) 改 (update) 查 (select)

​		service：业务处理层，对dao层的增删改查操作做逻辑处理的

​						Dao dao = new Dao();

​	view

​		html  jsp

​	controller

​		处理请求和响应结果

​		访问service

​		Service s = new Service();



# 2、IOC 控制反转

**IOC （Inversion of Control） ：控制反转**，通过容器来控制对象的创建及维护，对象中成员变量的创建及维护。反转就是将对象的控制权转移给容器处理，目的是获得更好的扩展性和可维护性。

![image-20250303091115498](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303091115498.png)

# 3、入门程序编写

==新建maven项目：==

![image-20250303123535097](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303123535097.png)

==配置maven==

![image-20250303091521776](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303091521776.png)

- **导入包spring核心容器相关依赖**
  - ![image-20250303094408455](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303094408455.png)
  - ![image-20250303094435926](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303094435926.png)
- **普通java类的建立**
  - ![image-20250303123627361](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303123627361.png)
  - ![image-20250303123655369](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303123655369.png)
- **spring配置文件**
  - ![image-20250303102722816](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303102722816.png)
- **通过spring内置API接口初始化spring容器，并获取spring 容器管理的java类的实例。**

![image-20250303134916685](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303134916685.png)



# 4、实例化对象的方式

## 4.1 构造器

![image-20250303135753530](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303135753530.png)

![image-20250303141639781](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303141639781.png)





## 4.2 静态工厂

![image-20250303142252026](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303142252026.png)

![image-20250303142851090](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303142851090.png)



## 4.3 普通工厂

![image-20250303144806746](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303144806746.png)

![image-20250303144857175](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303144857175.png)



## 4.4 定义多个配置文件

![image-20250303145155687](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303145155687.png)



==注意：resource值只能为引入配置文件的相对路径（相对于主配置文件）。==



# 5、bean的管理

## 5.1 bean的作用域与初始化时间

![image-20250303150222953](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303150222953.png)

> ```
> bean的作用域和初始化时间：
>            scope 作用域：
>                 singleton 单实例的,默认（一个类的对象在内存中只有一个）
>                 prototype 多实例的（一个类的对象在内存中有多个）
>            lazy-init 初始化时间：
>                立即加载： 默认情况下是 false/default,称为是 “立即加载”，
>                         立即加载就是初始化容器时直接创建对象
>                延迟加载：true,代表的是，“延迟加载”，
>                        只有在scope=“singleton”时有效，第一次调用getBean()时创建对象
>                        多实例是每次调用getBean()都会创建一个对象，因此设置成延迟加载没有意义
> ```

### 5.1.1 bean的作用域

**1） 单实例的**

![image-20250303151754355](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303151754355.png)

![image-20250303151816372](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303151816372.png)

==结果为true,证明是一个对象==



**2）多实例的**

​	![image-20250303151857370](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303151857370.png)

![image-20250303151909704](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303151909704.png)

==结果为false,证明每次调用getBean()都会创建一个对象==

### 5.1.2 初始化时间

**1）立即加载**

​	![image-20250303152004690](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303152004690.png)

![image-20250303152127499](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303152127499.png)

![image-20250303152029522](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303152029522.png)

==默认情况下是立即加载，在加载容器时就创建对象了==

**2）延迟加载**

**没有调用getBean()：**

![image-20250303152055571](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303152055571.png)

![image-20250303152127499](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303152127499.png)

![image-20250303152216323](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303152216323.png)

==设置为延迟加载后，初始化容器，并没有创建对象，直接无参构造方法==

**调用getBean():**

![image-20250303152559331](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303152559331.png)

![image-20250303152608686](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303152608686.png)

==调用getBean()后才会，创建对象，执行构造方法==



## 5.2 bean初始化和销毁方法

![image-20250303154522532](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303154522532.png)

![image-20250303155218868](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303155218868.png)

![image-20250303155714891](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303155714891.png)

![image-20250303155250288](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303155250288.png)

# 6、依赖注入 DI

**依赖注入**：由外部容器动态地将依赖对象注入到另一个对象的组件中。spring采用这种方式为bean的属性赋值。
通俗的说spring容器不仅可以初始化对象，也可以为对象当中的成员变量赋值，初始化成员变量对象以及赋值的过程，不需手动编码，而是由spring容器去做。这种依赖容器初始化对象，并赋值给bean全局变量的方式叫依赖注入。

![image-20250303160156810](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303160156810.png)



​	![image-20250303160232812](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303160232812.png)



## 6.1 setter方法注入

setter方法注入：spring容器调用bean组件中属性对应的setter方法完成属性的注入（赋值）。

**根据属性的不同类型，可分为如下三种注入情况。**

1. 基本类型注入。
   - 基本类型注入泛指：
     - 当前bean组件的属性为基本类型 
       - byte short int long float double char boolean
     - 基本类型的封装类型
       - Byte Short Integer Long Float Double Charecter Boolean
     - String、StringBuffer类型，StringBuilder
   - ![image-20250303161303997](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303161303997.png)
2. spring组件类型注入。
   - 当前bean组件的属性为spring容器的其他bean组件，容器可以读取配置文件对当前属性进行赋值。
   - ![image-20250303161414995](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303161414995.png)
3. 集合类型注入。
   - 当前bean组件的属性为List Set Map、数组、Properties等。
   - List注入方式:
     - ![image-20250303161506020](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303161506020.png)
   - Set注入方式
     - ![image-20250303161528862](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303161528862.png)
   - map注入方式
     - ![image-20250303161614817](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303161614817.png)



```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!--
        依赖注入DI：
            给实体类的成员变量初始化
      -->
    <bean id="dog1" class="com.zretc.pojo.Dog">
        <property name="dog_name" value="旺财"/>
    </bean>
    <!-- Setter方式注入，实际上就是调用实体类中的setXxx()的方法   -->
    <bean id="boy1" class="com.zretc.pojo.Boy">
        <!--  1、基本类型的依赖注入 -->
        <property name="boy_name" value="大壮"/>
        <!--  2、bean类型的依赖注入  -->
        <property name="dog" ref="dog1"/>
            <!--   内部bean,不建议使用     -->
<!--        <property name="dog">-->
<!--            <bean id="dog2" class="com.zretc.pojo.Dog"/>-->
<!--        </property>-->
        <!--  3、集合  -->
        <property name="list">
            <list>
                <value type="java.lang.String">打篮球</value>
                <value>唱歌</value>
                <value>180</value>
                <ref bean="dog1"/>
            </list>
        </property>
        <property name="set">
            <set>
                <value type="java.lang.String">打篮球</value>
                <value>唱歌</value>
                <value>180</value>
                <ref bean="dog1"/>
            </set>
        </property>
        <property name="map">
            <!--  键值对  -->
            <map>
                <entry key="1" value="唱歌"/>
                <entry key-ref="dog1" value-ref="dog1"/>
                <entry key-ref="dog1" value="花花"/>
            </map>
        </property>
    </bean>
</beans>
```

```java
 @Test
    public void test06() {
//        获取容器
        ClassPathXmlApplicationContext ctxt = new ClassPathXmlApplicationContext("applicationContext5.xml");
        Boy boy = (Boy) ctxt.getBean("boy1");
        System.out.println(boy.getBoy_name());
        System.out.println(boy.getDog().getDog_name());
        List list = boy.getList();
        list.forEach((obj)-> System.out.println(obj));
        Set set = boy.getSet();
        set.forEach((obj)-> System.out.println(obj));
        Map map = boy.getMap();
        Set set1 = map.keySet();
        set1.forEach((obj)-> System.out.println(obj + ":" + map.get(obj)));
    }
```



![image-20250303163416708](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250303163416708.png)

## 6.2 构造器方式注入

构造器方法注入：spring在初始化bean组件时，调用含参数的构造器对全局变量进行复制，参数类型可以为基本类型、bean组件类型、集合类型，赋值方式与setter方法赋值方式一致。

```xml
<bean id="boy" class="com.chinasofti.constructor.Boy" >
	<constructor-arg  index="0" value="123"></constructor-arg>
	<constructor-arg  index="1" value="哈哈" type="java.lang.String"></constructor-arg>
	<constructor-arg index="1" ref="beanName"></constructor-arg>
</bean>
```



## 6.3 自动注入

![image-20250304140121188](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304140121188.png)

# 7、spring项目程序架构

- 接口：在表面上是由几个没有主体代码的方法定义组成的集合体，有唯一的名称，可以被类或其他接口所实现（或者也可以说继承）。

- 面向接口编程：在系统分析或架构设计中，每个层级的程序并不是直接提供程序服务，而是定义一组接口，通过实现接口来提供功能。面向接口编程实际是面向对象编程的一部分。

![image-20250304140218316](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304140218316.png)

## 7.1 面向接口编程

![image-20250304140239165](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304140239165.png)

## 7.2 spring的三层架构模式

![image-20250304140307024](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304140307024.png)



## 7.3 实现登录功能

### 7.3.1 项目目录

![image-20250304140344875](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304140344875.png)

### 7.3.2 代码

- pom.xml依赖

  - ```xml
     <dependencies>
        <!--  引入spring依赖  -->
        <dependency>
          <groupId>org.springframework</groupId>
          <artifactId>spring-context</artifactId>
          <version>6.1.3</version>
        </dependency>
        <!--  封装：getter setter 有参构造 无参构造  -->
        <dependency>
          <groupId>org.projectlombok</groupId>
          <artifactId>lombok</artifactId>
          <version>1.18.30</version>
        </dependency>
        <!--  mysql驱动  -->
        <dependency>
          <groupId>mysql</groupId>
          <artifactId>mysql-connector-java</artifactId>
          <version>8.0.25</version>
        </dependency>
        <dependency>
          <groupId>junit</groupId>
          <artifactId>junit</artifactId>
          <version>4.13.2</version>
        </dependency>
      </dependencies>
    ```

- pojo层

  - ```java
    @Data
    public class Admin {
        private String admin_name;
        private String admin_password;
    }
    ```

    

- dao层

  - ```java
    public interface AdminDao {
        Admin login(String admin_name,String admin_password);
    }
    
    package com.zretc.dao.impl;
    
    import com.zretc.dao.AdminDao;
    import com.zretc.pojo.Admin;
    import com.zretc.util.DBUtil;
    import java.sql.*;
    
    public class AdminDaoImpl implements AdminDao {
        private Connection conn;
        private PreparedStatement ps;
        private ResultSet rs;
        @Override
        public Admin login(String admin_name,String admin_password) {
            try {
                conn = DBUtil.getConn();
                // 查询
                ps = conn.prepareStatement("select * from admin where admin_name=? and admin_password=?");
                ps.setString(1,admin_name);
                ps.setString(2,admin_password);
                rs = ps.executeQuery();
                if (rs.next()){
                    Admin admin = new Admin();
                    admin.setAdmin_name(rs.getString(1));
                    admin.setAdmin_password(rs.getString(2));
                    return admin;
                }
            } catch (SQLException e) {
                throw new RuntimeException(e);
            }
    
            return null;
        }
    }
    
    ```

    

- service 层

  - ```java
    public interface AdminService {
        Admin login(String admin_name, String admin_password);
    }
    
    package com.zretc.service.impl;
    
    import com.zretc.dao.AdminDao;
    import com.zretc.dao.impl.AdminDaoImpl;
    import com.zretc.pojo.Admin;
    import com.zretc.service.AdminService;
    
    public class AdminServiceImpl implements AdminService {
        AdminDao dao;
    
        public void setDao(AdminDaoImpl dao) {
            this.dao = dao;
        }
    
        @Override
        public Admin login(String admin_name, String admin_password) {
            return dao.login(admin_name,admin_password);
        }
    }
    
    ```

- DBUtile

  - ```java
    package com.zretc.util;
    
    import java.sql.*;
    
    public class DBUtil {
        private static Connection conn;
        private static PreparedStatement ps;
        private static ResultSet rs;
    
        // 获取数据库连接对象
        public static Connection getConn() {
            try {
                // 加载驱动
                Class.forName("com.mysql.cj.jdbc.Driver");
                conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/zly", "root", "root");
                return conn;
            } catch (ClassNotFoundException | SQLException e) {
                throw new RuntimeException(e);
            }
        }
    
        // 关闭资源
        public static void closeAll(ResultSet rs, PreparedStatement ps, Connection conn) {
            try {
                if (rs != null) {
                    rs.close();
                }
                if (ps != null) {
                    ps.close();
                }
                if (conn != null) {
                    conn.close();
                }
            } catch (SQLException e) {
                throw new RuntimeException(e);
            }
        }
    }
    
    ```

- application.xml 配置文件

  - ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    
        <!--  创建dao  -->
        <bean id="dao" class="com.zretc.dao.impl.AdminDaoImpl"/>
        <!--  创建service  -->
        <bean id="service" class="com.zretc.service.impl.AdminServiceImpl">
            <!--  将dao依赖注入到service
                    name 属性对应的是实现类中的成员变量的名字
                    ref 对应的是bean组件的id
            -->
            <property name="dao" ref="dao"/>
        </bean>
    </beans>
    ```

    

- controller层

- ```java
  package com.zretc.controller;
  
  import com.zretc.pojo.Admin;
  import com.zretc.service.impl.AdminServiceImpl;
  import org.junit.Test;
  import org.springframework.context.ApplicationContext;
  import org.springframework.context.support.ClassPathXmlApplicationContext;
  
  public class AdminTest {
      // 登录
      @Test
      public void test01(){
          ApplicationContext ctxt = new ClassPathXmlApplicationContext("applicationContext2.xml");
          // 访问service
          AdminServiceImpl service = (AdminServiceImpl) ctxt.getBean("service");
          Admin admin = service.login("tom","123");
          if (admin != null){
              System.out.println("登录成功");
          }else{
              System.out.println("登录失败");
          }
      }
  }
  
  ```

- 运行结果

- ![image-20250304140951848](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304140951848.png)

# 8、注解配置文件

## 8.1 实例化bean

Spring3.0后为我们引入了组件自动扫描机制，它可以在类路径底下寻找标注了**@Component、@Service、@Controller、@Repository**注解的类，并把这些类纳入进spring容器中管理。它的作用和在xml文件中使用bean节点配置组件是一样的。

**@Component ：泛指组件，当组件不好归类的时候，我们可以使用这个注解进行标注，例如pojo下**

**@Service： 用于标注业务层组件,service**

**@Controller : 用于标注控制层组件, controller**

**@Repository ：用于标注数据访问组件，dao**

![image-20250304110253830](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304110253830.png)

**==value对应的就是bean标签中的id,如果不输入id，则默认值当前类首字母小写==**

- 要使用自动扫描机制，我们需要打开以下配置信息:

  - 1、引入AOP的jar包（之前的版本不用）。

    - ```xml
      <dependencies>
          <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>6.1.3</version>
          </dependency>
          <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.33</version>
          </dependency>
          <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.30</version>
          </dependency>
          <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
          </dependency>
        </dependencies>
      ```

      

  - 2、spring配置文件增加context命名空间与xsd的引用，使用注解，需要context组件解析配置文件。

    - ```xml
      <?xml version="1.0" encoding="UTF-8"?>
      <beans xmlns="http://www.springframework.org/schema/beans"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xmlns:context="http://www.springframework.org/schema/context"
             xsi:schemaLocation="http://www.springframework.org/schema/beans
              http://www.springframework.org/schema/beans/spring-beans.xsd
              http://www.springframework.org/schema/context
              http://www.springframework.org/schema/context/spring-context.xsd">
          
      	<!--  动态扫描指定包下的所有spring相关的注解  -->
          <context:component-scan base-package="com.zretc.*"/>
      </beans>
      ```

    - ![image-20250304110126112](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304110126112.png)

  - 3、增加context的动态扫描

    - ![image-20250304105641970](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304105641970.png)



## 8.2 注解依赖注入

### 8.2.1 setter方法注入

**基本类型setter方法注入**

- **@Value**注解

  - ```java
    @Value(value = "18")
    private Long age;
    ```

**bean组件类型setter方法注入**

-  **@Resoure**注解

  - ```xml
    <!--  初始化和销毁方法-@Resource  -->
    <dependency>
          <groupId>javax.annotation</groupId>
          <artifactId>javax.annotation-api</artifactId>
          <version>1.3.2</version>
     </dependency>
    ```

  - ```java
    @Resource(name="setterBasic")
    private SetterBasic setterBasic;
    ```

  - ==在属性上添加注解完成注入，可以省略setter方法==

### 8.2.2 自动匹配

- ```
  默认情况下按照类型匹配
  @Autowired // 根据类型注入，必须找到一个符合条件的对象，否则就会抛出异常
  @Autowired(required = false) // 如果找不到对应的类型就返回null
  AdminDao dao;
  ```

- ```
  // 按照名字匹配
  @Autowired
  @Qualifier("dao")  // dao必须是到层对应的value值
  AdminDao dao;
  ```

![image-20250304134342348](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304134342348.png)

![image-20250304135907443](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304135907443.png)



```java
@Data
@Component  // 相当于在配置文件中写了：<bean id="admin" class="com.zretc.pojo.Admin'/>
public class Admin {
    private String admin_name;
    private String admin_password;
}


@Repository("dao")  // 相当于在配置文件中写了：<bean id="dao" class="com.zretc.dao.impl.AdminDaoImpl'/>
//@Repository  // 相当于在配置文件中写了：<bean id="adminDaoImpl" class="com.zretc.dao.impl.AdminDaoImpl'/>
public class AdminDaoImpl implements AdminDao {
    ...
}

@Service("service")
public class AdminServiceImpl implements AdminService {
    // 依赖注入
//    @Resource(name="dao")

//    自动匹配
    // @Autowired // 根据类型注入，必须找到一个符合条件的对象，否则就会抛出异常
    // @Autowired(required = false) // 如果找不到就返回null

    // 按照名字匹配
    @Autowired(required = false)
    @Qualifier("dao")
    AdminDao dao;
    ...
    ...
}

 @Test
    public void test01(){
        ApplicationContext ctxt = new ClassPathXmlApplicationContext("applicationContext2.xml");
        // 访问service
        AdminServiceImpl service = (AdminServiceImpl) ctxt.getBean("service");
        Admin admin = service.login("tom","123");
        if (admin != null){
            System.out.println("登录成功");
        }else{
            System.out.println("登录失败");
        }
    }
```



## 8.3 初始化和销毁方法配置

![image-20250304141529066](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304141529066.png)

- 导入依赖

  - ```xml
    <!--  初始化和销毁方法  -->
    <dependency>
          <groupId>javax.annotation</groupId>
          <artifactId>javax.annotation-api</artifactId>
          <version>1.3.2</version>
    </dependency>
    ```

- ```java
  @Data
  @Component   // <bean id="dog" class="com.zretc.pojo.Dog"/>
  public class Dog {
      // 名字
      @Value("旺财")
      private String dog_name;
  }
  
  
  @Data
  @Component
  @Scope("prototype") // 作用域，prototype多实例的
  public class Boy {
      @Value("小强")
      private String boy_name;
      // 一个男孩有一条狗
      @Autowired
      private Dog dog;
  
      // 初始化方法
      @PostConstruct // 单实例时在创建对象后执行一次，多实例时每一次调用getBean()时都会执行
      public void initMethod(){
          System.out.println("初始化方法。。。");
      }
  
      // 销毁方法
      @PreDestroy  // 当作用域为多实例时，不执行销毁方法，为单实例时，关闭容器前执行销毁方法
      public void destroyMethod(){
          System.out.println("销毁方法");
      }
  }
  
  
  public class MainTest {
      @Test
      public void test01(){
          ClassPathXmlApplicationContext ctxt = new ClassPathXmlApplicationContext("applicationContext.xml");
          // 获取Dog
          Dog dog = (Dog) ctxt.getBean("dog");
          // 获取Boy
          Boy boy = (Boy) ctxt.getBean("boy");
          Boy boy2 = (Boy) ctxt.getBean("boy");
          System.out.println(boy.getBoy_name() + "的狗叫" + dog.getDog_name());
          ctxt.close();
      }
  }
  ```

- ![image-20250304144730230](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304144730230.png)



# 9、AOP(面向切面编程)

AOP的核心组件：

- **切面（Aspect）**：切面是封装通用业务逻辑的组件，可以作用到其他组件上。
- **切入点（Pointcut）**：用于指定哪些组件哪些方法使用切面组件，Spring提供表达式来实现该指定。
- **通知（Advice）**：用于指定组件作用到目标组件的具体位置。
  - AOP前置通知：在目标组件的方法执行前执行的程序。
  - AOP后置通知：在目标组件的方法正常执行并返回参数后执行的程序。
  - AOP异常通知：在目标组件的方法抛出异常信息后执行的程序
  - AOP最终通知：在目标组件的方法正常执行后执行，或在异常通知之前执行。
  - AOP环绕通知：切面程序负责调用目标组件的运行，与struts中的拦截器功能类似，**可以完全取代之前的几个通知。**

![image-20250304151535560](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304151535560.png)

## 9.1 代码演示：

引入依赖

```xml
<dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>6.1.3</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
        </dependency>
        <!--   AOP面向切面编程依赖     -->
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.9.1</version>
        </dependency>
    </dependencies>
```



配置头文件，加入aop的命名空间

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:context="http://www.springframework.org/schema/context"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">
</beans>
```

==增加了AOP的命名空间与AOP的xsd规范，如不需要注解，可以省略context.xsd==

目标程序

```java
// 目标程序
public class Target {
    // 目标方法
    public String save(String name){
        System.out.println("目标方法被执行了。。。");
        return name;
    }
}
```



切面程序：存储各种通知

​		在类型为环绕通知的切面程序函数中，参数为org.aspectj.lang.ProceedingJoinPoint是JoinPoint的子类，

​		扩展了JoinPoint类，提供了proceed()函数，该函数的作用是调用目标组件,并返回目标组件返回的值。

```java
package com.zretc.pojo;


import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;

// 切面程序
public class AspectTest {
    // 通知 ： 新功能在目标方法的具体执行位置。
    // 前置通知：在目标方法之前执行就是前置通知
    public void doBefore(){
        System.out.println("前置通知。。。");
    }

    // 后置通知：在目标方法之后执行就是后置通知，如果目标方法发生异常则不执行
    // Joinpoint 该接口中封装了目标程序中目标方法的相关信息
    // retVal 返回值
    public void doAfterReturn(JoinPoint jp, Object retVal){
        System.out.println("后置通知。。。" + retVal);
        System.out.println("目标方法中的参数："+jp.getArgs()[0]);
        System.out.println("获取目标对象:"+jp.getTarget());
        System.out.println("获取目标方法的反射对象:"+jp.getSignature());
    }

    // 最终通知:在目标方法执行完以后执行,一定会执行的。
    public void doAfter(){
        System.out.println("最终通知。。。");
    }

    // 异常通知：在目标方法发生异常时执行
    public void doException(Exception e){ // e 就是目标方法发生的异常对象
        System.out.println("异常通知。。。");
    }

    // 环绕通知：可以代替以上几种通知
    public void doAround(ProceedingJoinPoint pjp){
        try {
            System.out.println("前置通知");
            // 目标对象
            Object obj = pjp.proceed();
            System.out.println("后置通知");
        } catch (Throwable e) {
            System.out.println("异常通知");
        } finally {
            System.out.println("最终通知");
        }
    }

    // 通知总结：前置通知，目标方法，如果有异常执行异常通知，不执行后置通知，最终通知
    //         如果没有异常，执行后置通知，不执行异常通知
}

```

配置文件，配置通知

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--  创建目标对象  -->
    <bean id="target" class="com.zretc.pojo.Target"/>
    <!--  创建切面程序  -->
    <bean id="aspectTest" class="com.zretc.pojo.AspectTest"/>

    <!--  配置AOP  -->
    <aop:config>
        <!--  配置切入点 ： 关联目标程序中的目标方法 
 						expression 切入点的表达式
						execution 函数式表达式，第一个* 代表的是返回值的类型是任意的，
											 第二个* 代表的是参数的类型是任意的
		-->
        <aop:pointcut id="pointcut"
                      expression="execution(* com.zretc.pojo.Target.save(*))"/>
        <!--  配置切面  -->
        <aop:aspect ref="aspectTest">
            <!-- 通知：新功能执行的具体位置 -->
            <!--  前置通知  -->
<!--            <aop:before method="doBefore" pointcut-ref="pointcut"/>-->
            <!--  后置通知  -->
<!--            <aop:after-returning method="doAfterReturn" returning="retVal"-->
<!--                                 pointcut-ref="pointcut"/>-->
            <!--  最终通知  -->
<!--            <aop:after method="doAfter" pointcut-ref="pointcut"/>-->
            <!--  异常通知  -->
<!--            <aop:after-throwing method="doException" pointcut-ref="pointcut"-->
<!--                                throwing="e"/>-->

            <!--  环绕通知  -->
            <aop:around method="doAround" pointcut-ref="pointcut"/>
        </aop:aspect>
    </aop:config>
</beans>
```



测试类：

```java
public class MainTest {
    @Test
    public void test01(){
        ApplicationContext ctxt = new ClassPathXmlApplicationContext("applicationContext.xml");
        // 获取目标程序
        Target target = (Target) ctxt.getBean("target");
        System.out.println(target.save("小强"));
    }
}
```



![image-20250304165148748](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250304165148748.png)



## 9.2 通知总结

```
执行顺序：
	发生异常：
		前置通知
		目标方法
		异常通知
		最终通知
	
	未发生异常：
		前置通知
		目标方法
		后置通知
		最终通知
		
注意：1、异常通知与后置通知不能同时存在
	 2、如果使用环绕通知就把前几种通知注释掉，两种方式选择其中一种
```



## 9.3 切入点

- 切入点表达式用于声明spring容器中哪些组件的函数是目标函数，也就是切面程序要作用到哪些组件的哪些函数上。

- 常用的切入点表达式分为：
  - **按类匹配**：匹配的java类中全部函数作为目标函数，使用`within`关键字。
  - **按函数匹配**：匹配的函数作为目标函数，使用`execution`关键字。
  - **按bean的id匹配**：匹配的bean中全部函数作为目标组件。使用`bean`关键字

### 9.3.1 按类匹配

```xml
匹配到类
<aop:pointcut id="targetPintcut" expression="within(com.chinasofti.Target)"/>
匹配到包下的类
<aop:pointcut id="targetPintcut" expression="within(com.chinasofti.*)"/>
匹配到包下及子包下的类	
<aop:pointcut id="targetPintcut" expression="within(com..*)"/>
```



### 9.3.2 按函数匹配

```xml
完整写法
返回类型  类的路径     类名     函数名  参数类型（用，分开）
<aop:pointcut id="targetPintcut" execution(String com.chinasofti.Target.save(String)) />
任意返回类型
<aop:pointcut id="targetPintcut" execution(* com.chinasofti.Target.save(String)) />
任意返回类型下指定包下任意类
<aop:pointcut id="targetPintcut" execution(* com.chinasofti.*.save(String)) />
任意返回类型下指定包下任意类任意函数
<aop:pointcut id="targetPintcut" execution(* com.chinasofti.*.*(String)) />
任意返回类型下指定包或子包下任意类任意函数任意参数
<aop:pointcut id="targetPintcut" execution(* com..*.*(..)) />
```



### 9.3.3 按bean的id匹配

```xml
根据bean组件名称匹配
<aop:pointcut id="targetPintcut" expression="bean(target)"/>

根据bean组件名称（含通配符）匹配
<aop:pointcut id="targetPintcut" expression="bean(target*)"/>
```



代码演示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--  创建目标对象  -->
    <bean id="target" class="com.zretc.pojo.Target"/>
    <!--  创建切面程序  -->
    <bean id="aspectTest" class="com.zretc.pojo.AspectTest"/>

    <!--  配置AOP  -->
    <aop:config>
        <!--  配置切入点 ： 关联目标程序中的目标方法  -->
<!--        <aop:pointcut id="pointcut" expression="execution(* com.zretc.pojo.Target.save(*))"/>-->
        <!--  按照函数匹配：
                    返回值是任意的，com包及其子包下的任意类中的任意方法，参数的个数类型是任意的
        -->
<!--        <aop:pointcut id="pointcut" expression="execution(* com..*.*(..))"/>-->
        <!-- 按照类匹配:
                com 这个包及其子包下的任意类
        -->
<!--        <aop:pointcut id="pointcut" expression="within(com..*)"/>-->

        <!-- 按照bean匹配
                bean组件的id 以 target开头的
         -->
        <aop:pointcut id="pointcut" expression="bean(target*)"/>
        <!--  配置切面  -->
        <aop:aspect ref="aspectTest">
            <!-- 通知：新功能执行的具体位置 -->
            <!--  前置通知  -->
<!--            <aop:before method="doBefore" pointcut-ref="pointcut"/>-->
            <!--  后置通知  -->
<!--            <aop:after-returning method="doAfterReturn" returning="retVal"-->
<!--                                 pointcut-ref="pointcut"/>-->
            <!--  最终通知  -->
<!--            <aop:after method="doAfter" pointcut-ref="pointcut"/>-->
            <!--  异常通知  -->
<!--            <aop:after-throwing method="doException" pointcut-ref="pointcut"-->
<!--                                throwing="e"/>-->

            <!--  环绕通知  -->
            <aop:around method="doAround" pointcut-ref="pointcut"/>
        </aop:aspect>
    </aop:config>
</beans>
```





## 9.4 AOP的注解配置

==@Aspect : 切面==

==@Before("execution(* com..*(..))")  前置通知==

==@AfterReturning(pointcut = "within(com..*)",returning = "retVal") 后置通知==

==@After("bean(target)") 最终通知==

==@AfterThrowing(pointcut = "within(com..*)",throwing = "e") 异常通知==

==@Around("within(com..*)") 环绕通知==

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--  动态扫描 -->
    <context:component-scan base-package="com.zretc.*"/>
    <!--  自动代理 AOP 相关的注解  -->
    <aop:aspectj-autoproxy/>
</beans>
```

目标程序：

```java
package com.zretc.pojo;

import org.springframework.stereotype.Component;

// 目标程序
@Component
public class Target { // 默认bean的id 是类名的首字母小写
    // 目标方法
    public String save(String name) {
        System.out.println("目标方法被执行了。。。");
//        int a = 10 / 0;
        return name;
    }
}

```



切面程序

```java
package com.zretc.pojo;


import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.*;
import org.springframework.stereotype.Component;

// 切面程序
@Aspect
@Component
public class AspectTest {
    // 通知 ： 新功能在目标方法的具体执行位置。
    // 前置通知：在目标方法之前执行就是前置通知
    @Before("execution(* com..*(..))") // 按照函数匹配，返回值是任意的，com包及其子包下的任意类中的任意方法，参数是任意的
    public void doBefore(){
        System.out.println("前置通知。。。");
    }

    // 后置通知：在目标方法之后执行就是后置通知，如果目标方法发生异常则不执行
    // Joinpoint 该接口中封装了目标程序中目标方法的相关信息
    // retVal 返回值
    @AfterReturning(pointcut = "within(com..*)",returning = "retVal")
    public void doAfterReturn(JoinPoint jp, Object retVal){
        System.out.println("后置通知。。。" + retVal);
        System.out.println("目标方法中的参数："+jp.getArgs()[0]);
        System.out.println("获取目标对象:"+jp.getTarget());
        System.out.println("获取目标方法的反射对象:"+jp.getSignature());
    }

    // 最终通知:在目标方法执行完以后执行,一定会执行的。
    @After("bean(target)")
    public void doAfter(){
        System.out.println("最终通知。。。");
    }

    // 异常通知：在目标方法发生异常时执行
    @AfterThrowing(pointcut = "within(com..*)",throwing = "e")
    public void doException(Exception e){ // e 就是目标方法发生的异常对象
        System.out.println("异常通知。。。");
    }

    // 环绕通知：可以代替以上几种通知
//    @Around("within(com..*)")
//    public void doAround(ProceedingJoinPoint pjp){
//        try {
//            System.out.println("前置通知");
//            // 目标对象
//            Object obj = pjp.proceed();
//            System.out.println("后置通知");
//        } catch (Throwable e) {
//            System.out.println("异常通知");
//        } finally {
//            System.out.println("最终通知");
//        }
//    }

    // 通知总结：前置通知，目标方法，如果有异常执行异常通知，不执行后置通知，最终通知
    //         如果没有异常，执行后置通知，不执行异常通知
}

```



# 10、spring集成jdbc

Spring提供了一个**工具类JdbcTemplate** ，该类对jdbc的操作进行了轻量级别的封装。

优点如下：

- 直接使用sql语句操作数据库，效率很高。
- 支持数据库的分区，这是数据量大的项目的实现方案，hibernate无法实现。
- 使用java语言拼sql语句，效率很高，这是ibatis无法达到的。

缺点如下：

- sql语句直接写在java程序中，很难管理，但部分企业进行了封装，实现了sql语句的简单管理。编码量大。



## 10.1 JdbcTemplate

JdbcTemplate简介：封装了操作数据库的各种方法，该类包含一个**dataSource属性（数据源）**，只有在初始化数据源的情况下才能调用JdbcTemplate的方法。

**数据源：**数据源为主流连接池的数据源对象（例如C3P0，DBCP数据库连接池），因此在使用JdbcTemplate前，要创建数据源对象。

![image-20250305112940127](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250305112940127.png)



### 10.1.1 实现步骤

引入依赖

```xml
<dependencies>
        <!--   spring 依赖    -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>6.1.3</version>
        </dependency>
        <!--    驱动    -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.33</version>
        </dependency>
        <!--    数据源    -->
        <dependency>
            <groupId>c3p0</groupId>
            <artifactId>c3p0</artifactId>
            <version>0.9.1.2</version>
        </dependency>
        <!--    JdbcTemplate 依赖   -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>6.1.3</version>
        </dependency>
        <!--    测试    -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
        </dependency>
    </dependencies>
```



创建属性文件：

![image-20250305135947835](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250305135947835.png)

```properties
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/zly
jdbc.user=root
jdbc.password=root
```



配置文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">

    <!--  加载jdbc.properties文件  -->
    <context:property-placeholder location="jdbc.properties"/>
    <!--  数据源 c3p0 -->
    <bean id="ds" class="com.mchange.v2.c3p0.ComboPooledDataSource">
        <property name="jdbcUrl" value="${jdbc.url}"/>
        <property name="driverClass" value="${jdbc.driver}"/>
        <property name="user" value="${jdbc.user}"/>
        <property name="password" value="${jdbc.password}"/>
        <property name="initialPoolSize" value="3"/>
        <property name="maxPoolSize" value="10"/>
        <property name="minPoolSize" value="1"/>
        <property name="acquireIncrement" value="3"/>
        <property name="maxIdleTime" value="60"/>
    </bean>

    <!--  JdbcTemplate工具类 对数据库中数据进行增删改查 -->
    <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
        <!--    依赖注入数据源    -->
        <property name="dataSource" ref="ds"/>
    </bean>

    <!--  创建dao层对象  -->
    <bean id="deptDao" class="com.zretc.dao.DeptDao">
        <!--    依赖注入JdbcTemplate工具类    -->
        <property name="jdbcTemplate" ref="jdbcTemplate"/>
    </bean>
    
    <!--  创建service层对象  -->
    <bean id="deptService" class="com.zretc.service.DeptService">
        <!--    依赖注入dao    -->
        <property name="deptDao" ref="deptDao"/>
    </bean>
</beans>
```



实体类：

```java
@Data
public class Dept {
    private Integer dept_id;
    private String dept_name;
    private String dept_loc;
}
```

​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   

Dao层接口

```java
public interface DeptDao {
    int insertDept(Dept dept);
    int deleteDept(Integer dept_id);
    int updateDept(Dept dept);
    List<Dept> selectAll();
    Dept selectById(Integer dept_id);
}
```



### 10.1.2==JdbcTemplet常用API接口==

![image-20250305144513246](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250305144513246.png)

![image-20250305144646876](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250305144646876.png)



![image-20250305144715375](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250305144715375.png)

Dao层实现类

```
package com.zretc.dao;

import com.zretc.pojo.Dept;
import org.springframework.dao.DataAccessException;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.ResultSetExtractor;
import org.springframework.jdbc.core.RowMapper;

import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.List;

public class DeptDaoImpl implements DeptDao {
    private JdbcTemplate jdbcTemplate;

    public JdbcTemplate getJdbcTemplate() {
        return jdbcTemplate;
    }

    public void setJdbcTemplate(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    @Override
    public int insertDept(Dept dept) {
        return jdbcTemplate.update("insert into dept values(default,?,?)",dept.getDept_name(),dept.getDept_loc());
    }

    @Override
    public int deleteDept(Integer dept_id) {
        return jdbcTemplate.update("delete from dept where dept_id=?",dept_id);
    }

    @Override
    public int updateDept(Dept dept) {
        return jdbcTemplate.update("update dept set dept_name=?,dept_loc=? where dept_loc=?",
                dept.getDept_name(),dept.getDept_loc(),dept.getDept_id());
    }

    @Override
    public List<Dept> selectAll() {
        return jdbcTemplate.query("select * from dept", new RowMapper<Dept>() {
            @Override
            public Dept mapRow(ResultSet rs, int rowNum) throws SQLException {
                Dept dept = new Dept();
                dept.setDept_id(rs.getInt(1));
                dept.setDept_name(rs.getString(2));
                dept.setDept_loc(rs.getString(3));
                return dept;
            }
        });
    }

    @Override
    public Dept selectById(Integer dept_id) {
        // 注意：第二个参数必须是数组，不是可变参数
        return jdbcTemplate.query("select * from dept where dept_id=?", new Object[dept_id], new ResultSetExtractor<Dept>() {
            @Override
            public Dept extractData(ResultSet rs) throws SQLException, DataAccessException {
                if (rs.next()){
                    Dept dept = new Dept();
                    dept.setDept_id(rs.getInt(1));
                    dept.setDept_name(rs.getString(2));
                    dept.setDept_loc(rs.getString(3));
                    return dept;
                }
                return null;
            }
        });
    }

}

```



service层接口

```java
public interface DeptService {
    int insertDept(Dept dept);
    int deleteDept(Integer dept_id);
    int updateDept(Dept dept);
    List<Dept> selectAll();
    Dept selectById(Integer dept_id);
}
```

service层实现类

```java
package com.zretc.service;

import com.zretc.dao.DeptDaoImpl;
import com.zretc.pojo.Dept;

import java.util.List;

public class DeptServiceImpl implements DeptService{
    DeptDaoImpl deptDao;

    public DeptDaoImpl getDeptDao() {
        return deptDao;
    }

    public void setDeptDao(DeptDaoImpl deptDao) {
        this.deptDao = deptDao;
    }

    @Override
    public int insertDept(Dept dept) {
        return deptDao.insertDept(dept);
    }

    @Override
    public int deleteDept(Integer dept_id) {
        return deptDao.deleteDept(dept_id);
    }

    @Override
    public int updateDept(Dept dept) {
        return deptDao.updateDept(dept);
    }

    @Override
    public List<Dept> selectAll() {
        return deptDao.selectAll();
    }

    @Override
    public Dept selectById(Integer dept_id) {
        return deptDao.selectById(dept_id);
    }
}

```



配置文件中创建dao层对象和service层对象，病依赖注入

```xml
    <!--  创建dao层对象  -->
    <bean id="deptDao" class="com.zretc.dao.DeptDaoImpl">
        <!--    依赖注入JdbcTemplate工具类    -->
        <property name="jdbcTemplate" ref="jdbcTemplate"/>
    </bean>

    <!--  创建service层对象  -->
    <bean id="deptService" class="com.zretc.service.DeptServiceImpl">
        <!--    依赖注入dao    -->
        <property name="deptDao" ref="deptDao"/>
    </bean>
```



测试类：

```java
public class MainTest {
    @Test
    public void test01(){
        ApplicationContext ctxt = new ClassPathXmlApplicationContext("applicationContext.xml");
        // 访问service
        DeptServiceImpl service = (DeptServiceImpl) ctxt.getBean("deptService");
        int rows = service.deleteDept(9);
        if (rows > 0){
            System.out.println("删除成功");
        }else{
            System.out.println("删除失败");
        }
        List<Dept> depts = service.selectAll();
        depts.forEach(dept -> System.out.println(dept));
    }
}
```

![image-20250305151514354](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250305151514354.png)







### 10.1.3 注解

```java
@Repository
public class DeptDaoImpl implements DeptDao {
    @Autowired
    private JdbcTemplate jdbcTemplate;
    ......
        
        
@Service("deptService")
public class DeptServiceImpl implements DeptService{
    @Autowired
    DeptDaoImpl deptDao;
    .......
        
  
配置文件：
<!--  动态扫描  -->
<context:component-scan base-package="com.zretc.*"/>
```



# 11、jdbc的事务控制

## 11.1 事务概述

事务是一组操作的执行单元，相对于数据库操作来讲，事务管理的是一组SQL指令，比如增加，修改，删除等。**事务的一致性**，要求，这个事务内的操作必须全部执行成功，如果在此过程种出现了差错，比如有一条SQL语句没有执行成功，那么这一组操作都将全部回滚

简单来说：就是将多个sql语句看成是一个整体，要么都执行，要么都不执行。



## 11.2 事务的四大特性

**事务的四大特性ACID**：

- atomic(**原子性**):要么都发生，要么都不发生。
- consistent(**一致性**):数据应该不被破坏。 
- isolate(**隔离性**):用户间操作不相混淆
- durable(**持久性**):永久保存,例如保存到数据库中等



张三 要给 李四转账 1000 元

张三 1001  ===》 1

李四 1        ===》1001



## 11.3 事务管理方式

Spring提供了两种事务管理方式：

- **编程式事务管理**	
  - 通过**程序代码**来控制你的事务何时开始，何时结束等，结果是控制的颗粒度更细，但需要手写程序，另外在团队合作开发时，会出现事物管理混乱。
  - ![image-20250306085906679](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306085906679.png)
- **声明式事务管理**
  - 在Spring中，你只需要在**Spring配置文件**中做一些配置，即可将数据库的访问纳入到事务管理中，解除了和代码的耦合， 这是对应用代码影响最小的选择。当你不需要事务管理的时候，可以直接从Spring配置文件中移除该设置



## 11.4 spring的事务管理器

- **spring的事务管理器**： spring没有直接管理事务，只是开发了事物管理器调用第三方组件完成事物控制。
  - ![image-20250306090203324](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306090203324.png)
- Spring控制事物的方式：spring控制事物是**以bean组件的函数为单位的**，如果一个函数正常执行完毕，该函数内的全部数据库操作按照一次事物提交，如果抛出异常，全部回滚。
- 事物的传播策略：如两个bean组件都由spring控制事物，且组件的函数之间存在调用关系，即（bean1 函数a 调用了 bean2 函数b），spring提供了一组配置方式供开发者选择，这些配置方式称为事物的传播策略。
  - ![image-20250306090544808](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306090544808.png)
- 数据库的隔离级别：
  - **脏读**:一个事务读取了另一个事务改写但还未提交的数据,如果这些数据被回滚，则读到的数据是无效的。
  - **不可重复读**：在同一事务中，多次读取同一数据返回的结果有所不同。换句话说就是，后续读取可以读到另一事务已提交的更新数据。相反，“可重复读”在同一事务中多次读取数据时，能够保证所读数据一样，也就是，后续读取不能读到另一事务已提交的更新数据。
  - **幻读**：一个事务读取了几行记录后，另一个事务插入一些记录，幻读就发生了。再后来的查询中，第一个事务就会发现有些原来没有的记录。
  - ![image-20250306090929459](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306090929459.png)
- 只读事物与读写事物：
  - 与所访问的数据库以及数据库驱动程序相关，并不一定是一个强制选项（例如在只读事物中去更新事物时允许的）。但若在事物中声明了只读事物，将会暗示数据库驱动程序和数据库系统，这个事务并不包含更改数据的操作，那么驱动程序和数据库就有可能根据这种情况对该事务进行一些特定的优化，比方说不安排相应的数据库锁，不记录回滚日志等，以减轻事务对数据库的压力，毕竟事务也是要消耗数据库的资源的。
  - 使用场景：
    - **只读事物：单纯的数据库查询**
    - **读写事物：对数据进行增删改的操作。**



## 11.5 使用spring声明式事物控制分为如下几步

事务用到了AOP需要导入相关依赖

```xml
        <!--   aop面向切面编程     -->
        <dependency>
            <groupId>org.aspectj</groupId>
            <artifactId>aspectjweaver</artifactId>
            <version>1.9.9.1</version>
        </dependency>
```



在配置文件头信息上**增加tx命名空间与tx.xsd**：声明式事物控制需要引入tx标签，因此要引入此xsd文件。

![image-20250306091523072](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306091523072.png)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xmlns:tx="http://www.springframework.org/schema/tx"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd
        http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx.xsd">
    
</beans>
```



配置事物控制管理器：j**dbc的事物控制管理器为DataSourceTransactionManager** 

```xml
    <!--  事务管理器  -->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <!--    依赖注入数据源    -->
        <property name="dataSource" ref="ds"/>
    </bean>
```



**配置事物通知**：配置哪些函数委托spring进行事物管理，以及事物管理的隔离级别、传播行为、是否只读事物属性。建议大家在需要更新数据的函数上配置隔离级别为数据库默认级别，传播行为采用required，读写事物。而只是查询的函数使用只读事物，效率更高。

![image-20250306092921763](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306092921763.png)



```xml
    <!--  配置事务通知  -->
    <tx:advice id="txAdvice" transaction-manager="transactionManager">
        <tx:attributes>
            <!--
                * 代表的是以。。。开的头，例如insertDept  insertEmp
                isolation="DEFAULT" 事务的隔离级别是默认的
                propagation="REQUIRED" 事务的传播策略
                read-only="false" 只读还是读写操作
                    false代表的是读写，DML
                    true 代表的是只读，DQL
            -->
            <tx:method name="insert*" isolation="DEFAULT" propagation="REQUIRED" read-only="false"/>
            <tx:method name="delete*" isolation="DEFAULT" propagation="REQUIRED" read-only="false"/>
            <tx:method name="update*" isolation="DEFAULT" propagation="REQUIRED" read-only="false"/>
            <tx:method name="select*" read-only="true"/>
        </tx:attributes>
    </tx:advice>
```



**配置事物的切入点**：也就是spring的哪些组件要配置事物通知。
	在spring的三层架构中，建议把事物控制放在service层。

```xml
    <!--  配置事务的切入点  -->
    <aop:config>
        <!--  切入点  -->
        <aop:pointcut id="txPointcut" expression="within(com.zretc.service.*)"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="txPointcut"/>
    </aop:config>
```

service实现类中抛出异常：

在添加的功能中存在删除的功能，同时抛出异常，这样就会被事务管理器拦截，并回滚。

```java
    @Override
    public int insertDept(Dept dept) {
        deleteDept(12);
        // 抛出异常
        int i = 10/0;
        return deptDao.insertDept(dept);
    }
```



测试类

```java
    @Test
    public void test02() {
        ApplicationContext ctxt = new ClassPathXmlApplicationContext("applicationContext.xml");
        // 访问service
        // 动态代理必须针对接口:
        // DK动态代理的原理是根据定义好的规则，用传入的接口创建一个新类，这就是为什么采用动态代理时为什么只能用接口引用指向代理，而不能用传入的类引用执行动态类。
        DeptService service = (DeptService) ctxt.getBean("deptServiceImpl");
        Dept dept = (Dept) ctxt.getBean("dept");
        dept.setDept_name("406教室");
        dept.setDept_loc("406");
        service.insertDept(dept);
    }
```

![image-20250306110517106](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306110517106.png)



运行后，抛出异常，数据库没有编号，回滚了

![image-20250306110554261](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306110554261.png)

![image-20250306110605874](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306110605874.png)



## 11.6 使用注解完成事物控制

- ==**@Transactional**==// 在接口上声明后。代表这个类下的所有方法都会开启事务

  

- 配置文件上增加

  - ```xml
    <!--1 启用spring的自动扫描功能-->                        
     <context:component-scan base-package="com.zretc.*"/>
                                                       
    <!--5  采用@Transactional注解方式使用事务 -->
    <tx:annotation-driven transaction-manager="transactionManager" />                                                   
    ```

    

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:context="http://www.springframework.org/schema/context"
         xmlns:aop="http://www.springframework.org/schema/aop" xmlns:tx="http://www.springframework.org/schema/tx"
         xsi:schemaLocation="http://www.springframework.org/schema/beans
          http://www.springframework.org/schema/beans/spring-beans.xsd
          http://www.springframework.org/schema/context
          http://www.springframework.org/schema/context/spring-context.xsd
          http://www.springframework.org/schema/aop
          http://www.springframework.org/schema/aop/spring-aop.xsd
          http://www.springframework.org/schema/tx
          http://www.springframework.org/schema/tx/spring-tx.xsd">
  
      <!--  加载jdbc.properties文件  -->
      <context:property-placeholder location="jdbc.properties"/>
      <!--  数据源 c3p0 -->
      <bean id="ds" class="com.mchange.v2.c3p0.ComboPooledDataSource">
          <property name="jdbcUrl" value="${jdbc.url}"/>
          <property name="driverClass" value="${jdbc.driver}"/>
          <property name="user" value="${jdbc.user}"/>
          <property name="password" value="${jdbc.password}"/>
          <property name="initialPoolSize" value="3"/>
          <property name="maxPoolSize" value="10"/>
          <property name="minPoolSize" value="1"/>
          <property name="acquireIncrement" value="3"/>
          <property name="maxIdleTime" value="60"/>
      </bean>
  
      <!--  JdbcTemplate工具类 对数据库中数据进行增删改查 -->
      <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
          <!--    依赖注入数据源    -->
          <property name="dataSource" ref="ds"/>
      </bean>
  
      <!--  事务管理器  -->
      <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
          <!--    依赖注入数据源    -->
          <property name="dataSource" ref="ds"/>
      </bean>
      
      <!--  动态扫描  -->
      <context:component-scan base-package="com.zretc.*"/>
      <!--  事务注解的驱动  -->
      <tx:annotation-driven transaction-manager="transactionManager"/>
  </beans>
  ```

  

- 在业务层的方法上增加**@transactional**注解。

  - ```java
    //在需要被事物管理的方法上配置注解
    @Transactional(propagation=Propagation.REQUIRED,isolation=Isolation.DEFAULT,readOnly=true)
    public void save () throws Exception {
    }
    
    ```

```java
@Transactional // 在接口上声明后。代表这个类下的所有方法都会开启事务
public interface DeptService {

    @Transactional(isolation = Isolation.DEFAULT,propagation = Propagation.REQUIRED,readOnly = false)
    int insertDept(Dept dept);
    @Transactional(isolation = Isolation.DEFAULT,propagation = Propagation.REQUIRED,readOnly = false)
    int deleteDept(Integer dept_id);
    @Transactional(isolation = Isolation.DEFAULT,propagation = Propagation.REQUIRED,readOnly = false)
    int updateDept(Dept dept);
    @Transactional(readOnly = true)
    List<Dept> selectAll();
    @Transactional(readOnly = true)
    Dept selectById(Integer dept_id);
}
```

