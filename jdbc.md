# 1、什么是JDBC

JDBC（Java DataBase Connectivity）是由Sun Microsystem公司**提供的API**（Application Programming Interface应用程序编程接口）；

- 它为Java应用程序提供了一系列的类，使其能够快速高效地访问数据库；
- 这些功能是由一系列的类和对象来完成的，我们只需使用相关的对象，即可完成对数据库的操作;
- 这些类和接口都是在 **import java.sql.*;** 包下的。

![image-20250121084529135](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250121084529135.png)

# 2、JDBC 提供的 类与接口

- java.sql包中的一些接口

![image-20250121084911402](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250121084911402.png)

> PreparedStatement 继承自 Statement
>
> PreparedStatement  执行效率比 Statement  要
>
> PreparedStatement  有预编译的机制，可以避免sql注入的问题

DQL 语句 ： select

DML 语句 ：insert delete update



- java.sql包中的一些类

![image-20250121085357874](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250121085357874.png)

# 3、JDBC执行步骤

![image-20250121085553626](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250121085553626.png)

![image-20250121092448326](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250121092448326.png)

- 1、加载驱动程序

  - ```java
    Class.forName("com.mysql.cj.jdbc.Driver");
    ```

- 2、创建Connection对象

  - ```java
    // localhost 本地（127.0.0.1、IP地址）
    // 3306 mysql数据库的端口号
    String url = "jdbc:mysql://localhost:3306/数据库名"; 
    // 用户名
    String user = "root"; 
    // 密码
    String password = "root";
    Connection conn = DriverManager.getConnection(String url, String user,String password);
    ```

- 3、创建PreparedStatement对象

  - ```java
    // Statement sta = conn.createStatement();
    // DML 语句
    // int rows = sta.executeUpdate(String sql)
    // DQL 语句
    // ResultSet rs = sta.executeQuery(String sql)
    
    // ? 可以理解为是预编译
    PreparedStatement ps = conn.prepareStatement("update 表名 set first_name=?,salary=? where empid=?");
    ```

    

- 4、执行sql 语句

  - ```java
    // DML 语句
    // 替换 ？  ps.setXxx(x,y)  第一个参数？的位置，第二个参数是替换后的值
    ps.setString(1,"张三");
    ps.setInt(2,8000);
    ps.setInt(3,100);
    int rows = ps.executeUpdate();
    
    // DQL 语句
    ResultSet rs = ps.executeQuery();
    // next() 判断结果集中是否有下一行记录，有，返回true
    while(rs.next()){
        // 获取每一列（字段）的值
        int empid = rs.getInt("employee_id"); // 根据字段名获取值
        String first_name = rs.getString(2); // 根据字段的位置获取（位置是从1开始的）
    }
    ```

- 5、关闭资源

  - 先开的后关,后开的先关

  - ```java
    // 关闭Result
    rs.close();
    // 关闭PreparedStatement、
    ps.close();
    // 关闭Connection
    conn.close();
    ```



# 4、连接数据库的工具类

```java
package com.zretc3.util;

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
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "root", "root");
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



# 5、MVC设计模式

M 层 ： Model 模型

​			  pojo (实体类) -- 一张表对应一个实体类

​			  dao（增删改查）

​			  service (业务处理)

V 层 ：  View 视图

​			  html、jsp

C 层 :    Controller 控制层

​			 在Controller中访问service,在service中访问dao













