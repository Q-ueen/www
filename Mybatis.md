# 1、Mybatis的发展史

MyBatis 本是apache的一个开源项目iBatis, 2010年这个项目由apache software foundation 迁移到了google code，并且改名为MyBatis 。2013年11月迁移到

Github，通俗说法Ibatis3 = MyBatis,iBATIS一词来源于“internet”和“abatis”的组合，是一个基于Java的持久层框架。iBATIS提供的持久层框架包括SQL Maps和

Data Access Objects（DAO）

![image-20250306134633779](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306134633779.png)



# 2、什么是 Mybatis 

MyBatis是一个**数据持久层(ORM)框架**。把**实体类和SQL语句**之间建立了**映射关系**，是一种**半自动化的ORM**实现。



# 3、MyBatis的优点：

- 基于SQL语法，简单易学
- 能了解底层组装过程
- SQL语句封装在配置文件中，便于统一管理与维护，降低了程序的耦合度
- 程序调试方便



**MyBatis和JDBC的区别：**

![image-20250306134948869](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306134948869.png)



# 4、Mybatis的结构特性

![image-20250306135354112](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306135354112.png)

![image-20250306135414893](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306135414893.png)





# 5、MyBatis基础代码结构



![image-20250306135830967](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306135830967.png)





# 6、MyBatis核心配置文件

![image-20250306142458875](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306142458875.png)



![image-20250306140334915](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306140334915.png)

![image-20250306140419927](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306140419927.png)



![image-20250306140451779](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306140451779.png)





# 7、Mybatis基本要素

![image-20250306164111284](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306164111284.png)





# 8、创建一个Mybatis项目

![image-20250306144753901](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306144753901.png)



![image-20250306140647842](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306140647842.png)

![image-20250306140900851](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306140900851.png)

![image-20250306141004048](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306141004048.png)



导入依赖：

```xml
<dependencies>
        <!--  导入mybatis依赖  -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.14</version>
        </dependency>
        <!--   驱动     -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.33</version>
        </dependency>
        <!--    juint    -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
        </dependency>
            <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.30</version>
        </dependency>
    </dependencies>
```



定义属性文件：

![image-20250306142948583](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306142948583.png)

```properties
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/zly
jdbc.user=root
jdbc.password=root
```



**创建一个mybatis的配置文件：**

![image-20250306142247153](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306142247153.png)



```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
</configuration>
```



将属性配置文件引入到mybatis总配置文件中：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--  引入属性文件  -->
    <properties resource="jdbc.properties"/>
    <!--  基础环境  -->
    <environments default="development">
        <environment id="development">
            <!--  事务管理器  -->
            <transactionManager type="JDBC"/>
            <!--  数据源  -->
            <dataSource type="POOLED">
                <property name="driver" value="${jdbc.driver}"/>
                <property name="url" value="${jdbc.url}"/>
                <property name="username" value="${jdbc.user}"/>
                <property name="password" value="${jdbc.password}"/>
            </dataSource>
        </environment>
    </environments>
</configuration>
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



在总配置文件中给实体类起别名：

![image-20250306163556048](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306163556048.png)

```xml
    <!--  给实体类起别名  -->
    <typeAliases>
        <!--   挨个实体类起别名     -->
        <!-- <typeAlias type="com.zretc.pojo.Dept" alias="dept"/>-->
        <!-- 给com.zretc.pojo下的所有实体类起别名,默认就是类名首字母小写 -->
        <package name="com.zretc.pojo"/>
    </typeAliases>
```



dao层接口

```java
public interface DeptDao {
    int insertDept(Dept dept);
    int deleteDept(Integer dept_id);
    int updateDept(Dept dept);
    List<Dept> selectAll();
    Dept selectById(Integer dept_id);
}
```



现在不需要dao层接口的实现类了，而是需要一个mapper文件

一个dao接口对应一个mapper文件

![image-20250306145526327](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306145526327.png)



第一步，先创建一个目录，存储mapper文件：

![image-20250306145615391](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306145615391.png)

![image-20250306151902722](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306151902722.png)

**在包下新建mapper文件**

![image-20250306163335097](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306163335097.png)

![image-20250306145755101](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306145755101.png)



**在mapper文件中编写接口中对应的sql语句**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<!-- 映射的是哪个dao层 -->
<mapper namespace="com.zretc.dao.DeptDao">
    <!--
        <insert> 表签代表的是添加操作
        id 对应的是dao层接口中的函数名称
        parameterType 函数的参数类型，默认是包名+类名映射，
                      可以在总配置文件中使用typeAliases起别名，直接引用别名
                      如果参数是一个基本类型，可以省略不写
        #{} 代表的是将实体类中的成员变量映射给表中的字段，相当于？
        jdbcType=VARCHAR 该数据对应的数据库中的字段的类型，可以省略不写
     -->
    <insert id="insertDept" parameterType="dept">
        insert into dept
        values (default, #{dept_name,jdbcType=VARCHAR}, #{dept_loc})
    </insert>
</mapper>
```



将mapper文件，引入到总配置文件中：

![image-20250306163611378](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306163611378.png)

```xml
<!--  引入mapper文件  -->
    <mappers>
        <!--  引入单个mapper文件 -->
        <!--  <mapper resource="com/zretc/dao/DeptDao.xml"/>-->
        <!--  引入包下的所有mapper文件  -->
        <package name="com.zretc.dao"/>
    </mappers>
```



在测试类中，获取接口对象，调用添加方法：

```java
public class MainTest {
    @Test
    public void test01() throws IOException {
        // 获取mybatis的总配置文件
        // 1. 读取mybatis总配置文件
        Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
        // 2.获取SqlSessionFactory工厂
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
        // 3.获取SqlSession
        SqlSession sqlSession = sessionFactory.openSession(true);// true:自动提交
        // 4.获取接口对象
        DeptDao deptDao = sqlSession.getMapper(DeptDao.class);
        // 5.调用添加方法
        Dept dept = new Dept();
        dept.setDept_name("生产部");
        dept.setDept_loc("1楼101车间");
        deptDao.insertDept(dept);


        // 6.事务的提交
//        sqlSession.commit();
        // 7.关闭SqlSession
        sqlSession.close();
    }
}

```

![image-20250306163721063](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250306163721063.png)



在mapper文件中配置其他方法:

```java
public interface DeptDao {
    int insertDept(Dept dept);
    // @Param("id") 给参数起别名，在mapper文件中映射
//    int deleteDept(@Param("id") Integer dept_id);
    int deleteDept(Integer dept_id);
    int updateDept(Dept dept);
    List<Dept> selectAll();
    //Dept selectById(@Param("id") Integer dept_id);
	Dept selectById(Integer dept_id);
    List<Dept> selectByLike(@Param("dept_name") String dept_name);
}
```



```xml
<!--  删除功能
            当参数不是一个实体类时，映射方式：
                1、利用@param()映射表中的字段
                2、使用参数的下标（从0开始的）映射
    -->
    <delete id="deleteDept" parameterType="java.lang.Integer">
        <!--delete from dept where dept_id=#{id}-->
        delete from dept where dept_id=#{0}
    </delete>
    <!--  修改功能  -->
    <update id="updateDept" parameterType="dept">
        update dept
        set dept_name=#{dept_name},
            dept_loc=#{dept_loc}
        where dept_id = #{dept_id}
    </update>

    <!--  查询所有  -->
    <select id="selectAll" resultType="dept">
        select * from dept
    </select>

    <!--  根据部门编号查询所有  -->
    <select id="selectById" resultType="dept">
        select * from dept where dept_id = #{dept_id}
    </select>

    <!--  模糊查询  
			使用 concat() 函数进行字符串拼接，该函数的参数是可变的
	-->
    <select id="selectByLike" resultType="dept">
        select * from dept where dept_name like concat('%',#{dept_name},'%')
    </select>
```



测试类中进行测试：

```java
 // 删除功能
//        deptDao.deleteDept(15);

        // 修改
//        Dept dept = new Dept();
//        dept.setDept_id(14);
//        dept.setDept_name("生产部666");
//        dept.setDept_loc("1楼106车间");
//        deptDao.updateDept(dept);

        // 查询所有
//        List<Dept> depts = deptDao.selectAll();
//        depts.forEach(dept -> System.out.println(dept));

        // 根据部门编号查询
//        Dept dept = deptDao.selectById(14);
//        System.out.println(dept);

        // 模糊查询
        List<Dept> depts = deptDao.selectByLike("6");
        depts.forEach(dept -> System.out.println(dept));
```



# 9、SqlSession对象

SqlSession在 MyBatis中是非常强大的一个核心类，类中包含了所有执行语句的方法,提交或回滚事务,还有获取映射器实例的方法

![image-20250307090101750](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307090101750.png)



![image-20250307090201639](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307090201639.png)

![image-20250307094454089](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307094454089.png)

```java
    @Test
    public void test02() throws IOException {

        // 获取mybatis的总配置文件
        // 1. 读取mybatis总配置文件
        Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
        // 2.获取SqlSessionFactory工厂
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
        // 3.获取SqlSession
        SqlSession sqlSession = sessionFactory.openSession(true);// true:自动提交

        // 利用SqlSession来执行sql
        // 1.添加
//        Dept dept = new Dept();
//        dept.setDept_name("打包部");
//        dept.setDept_loc("1楼102车间");
//        sqlSession.insert("com.zretc.dao.DeptDao.insertDept",dept);

        // 2.删除
//        sqlSession.delete("com.zretc.dao.DeptDao.deleteDept",16);

        // 3.修改
//        Dept dept = new Dept();
//        dept.setDept_id(14);
//        dept.setDept_name("打包部");
//        dept.setDept_loc("1楼102车间");
//        sqlSession.update("com.zretc.dao.DeptDao.updateDept",dept);

//        4. 根据id查询
//        Dept dept = sqlSession.selectOne("com.zretc.dao.DeptDao.selectById",14);
//        System.out.println(dept);

        // 5. 查询所有
//        List<Dept> depts = sqlSession.selectList("com.zretc.dao.DeptDao.selectAll");
//        depts.forEach(dept -> System.out.println(dept));

        // 6.模糊查询
//        List<Dept> depts = sqlSession.selectList("com.zretc.dao.DeptDao.selectByLike","部");
//        depts.forEach(dept -> System.out.println(dept));

        // 7. selectMap 将部门名称作为键
        Map<String,Dept> deptMap = sqlSession.selectMap("com.zretc.dao.DeptDao.selectAll","dept_name");
        for (String s : deptMap.keySet()) {
            System.out.println(s + ":" + deptMap.get(s));
        }

        sqlSession.close();
    }
```



![image-20250307143637744](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307143637744.png)

```java
// 8、分页查询
        RowBounds rb = new RowBounds(2,3); 
        List<Dept> depts =  sqlSession.selectList("com.zretc.dao.DeptDao.selectAll",null,rb);
        depts.forEach(dept -> System.out.println(dept));
```

![image-20250307143953987](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307143953987.png)





# 10、动态sql

- **\<trim prefix="(" suffix=")" suffixOverrides=","></trim>**

  - trim 代表的是空格
  - prefix="(" 以指定字符开头
  - suffix=")" 以指定字符结尾
  - suffixOverrides="," 去掉最后一个指定的字符

- **\<if test=""></if>**

  - test 是条件表达式

  - ```xml
    <insert id="insertEmp" parameterType="emp">
        <!-- insert into emp(ename,hire_date,job_id,dept_id,interest)
        values('tom',now(),1,1,'唱歌，跳舞')-->
        <!--
            trim 代表的是空格
            prefix="(" 以指定字符开头
            suffix=")" 以指定字符结尾
            suffixOverrides="," 去掉最后一个指定的字符
        -->
        insert into emp
        <trim prefix="(" suffix=")" suffixOverrides=",">
            <if test="ename!=null">ename,</if>
            <if test="hire_date!=null">hire_date,</if>
            <if test="job_id!=null">job_id,</if>
            <if test="dept_id!=null">dept_id,</if>
            <if test="interest!=null">interest,</if>
        </trim>
        <trim prefix="values(" suffix=")" suffixOverrides=",">
            <if test="ename!=null">#{ename},</if>
            <if test="hire_date!=null">#{hire_date},</if>
            <if test="job_id!=null">#{job_id},</if>
            <if test="dept_id!=null">#{dept_id},</if>
            <if test="interest!=null">#{interest},</if>
        </trim>
    
        <!-- insert into emp(ename,hire_date) values('soso',now())-->
    </insert>
    ```

- **\<set>**  代替修改语句中的set关键字

  - ```xml
    <update id="updateEmp" parameterType="emp">
        update emp
        <set>
            <if test="ename!=null">ename=#{ename},</if>
            <if test="hire_date!=null">hire_date=#{hire_date},</if>
            <if test="job_id!=null">job_id=#{job_id},</if>
            <if test="dept_id!=null">dept_id=#{dept_id},</if>
            <if test="interest!=null">interest=#{interest},</if>
        </set>
        where empno = #{empno}
    </update>
    ```

- **\<foreach>  遍历循环**

  - ```xml
    collection 代表的是集合
    item 集合中的元素
    open 以指定字符开始
    close 以指定字符结束
    separator 分隔符
    
    <foreach collection="list" item="empno" open="(" close=")" separator=",">
          #{empno}
    </foreach>
    ```

-  **\<![CDATA[ sql ]]>**

  - ```xml
    mapper文件中写大于号或者小于号时，需要将sql语句放在 <![CDATA[ sql ]]> 标记中
     <![CDATA[
                select * from emp where empno < #{0}
     ]]>
    ```

- **\<where>** 代替条件中的where 关键字,可以自动去掉前缀或后缀

- **\<choose> \<when>  \<otherwise>** 相当于 if.. else if.. else..

- - ```xml
  
    <!-- 根据任意条件查询 -->
        <select id="selectByOther" resultType="emp" parameterType="emp">
            select * from emp
            <where>
                <!-- 相当于 if... else if... else... -->
                <choose>
                    <when test="empno!=null">empno=#{empno}</when>
                    <when test="ename!=null">ename=#{ename}</when>
                    <when test="hire_date!=null">hire_date=#{hire_date}</when>
                    <when test="job_id!=null">job_id=#{job_id}</when>
                    <when test="dept_id!=null">dept_id=#{dept_id}</when>
                    <when test="interest!=null">interest=#{interest}</when>
                    <otherwise>1=1</otherwise>
                </choose>
             </where>
         </select>
    ```
  
- **\<sql>**

  - ```xml
     <sql id="usually">
        empno,ename,hire_date,job_id,dept_id,interest
      </sql>
    select <include refid="usually"/> from emp
    ```



pojo实体类：

```java
@Data
public class Emp {
    private Integer empno;
    private String ename;
    private Date hire_date;
    private Integer job_id;
    private Integer dept_id;
    private String interest;
}
```



dao层接口：

```java
package com.zretc.dao;

import com.zretc.pojo.Emp;

import java.util.List;

public interface EmpDao {
    // 添加
    int insertEmp(Emp emp);
    // 修改
    int updateEmp(Emp emp);
    // 删除
    int deleteEmp(Integer empno);
    // 查询所有
    List<Emp> selectAll();
    // 根据编号查询
    Emp selectByNo(Integer empno);

    // 查询员工信息，员工编号等于值列表中的一个（例如：编号在1/2/6的员工）
    List<Emp> selectByIn(List<Integer> empno);

    // 查询员工编号是6以内的员工信息
    List<Emp> selectByBetween(Integer empno);

    // 根据任意条件查询
    List<Emp> selectByOther(Emp emp);

    // 多个条件
    List<Emp> selectByAllOther(Emp emp);
}

```

mapper文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd" >
<!-- 映射的是哪个dao层 -->
<mapper namespace="com.zretc.dao.EmpDao">
    <!--  添加 -->
    <insert id="insertEmp" parameterType="emp">
        <!-- insert into emp(ename,hire_date,job_id,dept_id,interest)
        values('tom',now(),1,1,'唱歌，跳舞')-->
        <!--
            trim 代表的是空格
            prefix="(" 以指定字符开头
            suffix=")" 以指定字符结尾
            suffixOverrides="," 去掉最后一个指定的字符
        -->
        insert into emp
        <trim prefix="(" suffix=")" suffixOverrides=",">
            <if test="ename!=null">ename,</if>
            <if test="hire_date!=null">hire_date,</if>
            <if test="job_id!=null">job_id,</if>
            <if test="dept_id!=null">dept_id,</if>
            <if test="interest!=null">interest,</if>
        </trim>
        <trim prefix="values(" suffix=")" suffixOverrides=",">
            <if test="ename!=null">#{ename},</if>
            <if test="hire_date!=null">#{hire_date},</if>
            <if test="job_id!=null">#{job_id},</if>
            <if test="dept_id!=null">#{dept_id},</if>
            <if test="interest!=null">#{interest},</if>
        </trim>

        <!-- insert into emp(ename,hire_date) values('soso',now())-->
    </insert>

    <!--修改-->
    <update id="updateEmp" parameterType="emp">
        update emp
        <set>
            <if test="ename!=null">ename=#{ename},</if>
            <if test="hire_date!=null">hire_date=#{hire_date},</if>
            <if test="job_id!=null">job_id=#{job_id},</if>
            <if test="dept_id!=null">dept_id=#{dept_id},</if>
            <if test="interest!=null">interest=#{interest},</if>
        </set>
        where empno = #{empno}
    </update>

    <!--删除-->
    <delete id="deleteEmp">
        delete from emp where empno = #{0}
    </delete>

    <!--  查询所有  -->
    <select id="selectAll" resultType="emp">
        select * from emp
    </select>

    <!--  根据id查询  -->
    <select id="selectByNo" resultType="emp">
        select * from emp where empno=#{0}
    </select>

    <!--查询员工信息，员工编号等于值列表中的一个（例如：编号在1/2/6的员工）-->
    <select id="selectByIn" resultType="emp">
        select * from emp where empno in
        <!--
            collection 代表的是集合
            item 集合中的元素
            open 以指定字符开始
            close 以指定字符结束
            separator 分隔符
        -->
        <foreach collection="list" item="empno" open="(" close=")" separator=",">
            #{empno}
        </foreach>
    </select>

    <!-- 查询员工编号是6以内的员工信息 -->
    <select id="selectByBetween" resultType="emp">
        <!-- mapper文件中写大于号或者小于号时，需要将sql语句放在 <![CDATA[ sql ]]> 标记中-->
        <![CDATA[
            select * from emp where empno < #{0}
        ]]>
    </select>

    <!-- 根据任意条件查询 -->
    <select id="selectByOther" resultType="emp" parameterType="emp">
        select * from emp
        <where>
            <!-- 相当于 if... else if... else... -->
            <choose>
                <when test="empno!=null">empno=#{empno}</when>
                <when test="ename!=null">ename=#{ename}</when>
                <when test="hire_date!=null">hire_date=#{hire_date}</when>
                <when test="job_id!=null">job_id=#{job_id}</when>
                <when test="dept_id!=null">dept_id=#{dept_id}</when>
                <when test="interest!=null">interest=#{interest}</when>
                <otherwise>1=1</otherwise>
            </choose>
         </where>
     </select>

    <!--  通用的字段  -->
    <sql id="usually">
        empno,ename,hire_date,job_id,dept_id,interest
    </sql>
    <!-- 多个条件 -->
    <select id="selectByAllOther" parameterType="emp" resultType="emp">
        <!--  select * from emp where ename='tom' and hire_date='2025-3-7'  -->
        <!--  select * from emp where ename='tom' or hire_date='2025-3-7' -->

        <!-- 引用通用的sql -->
        select <include refid="usually"/> from emp
        <!-- where会总去掉前缀和后缀 -->
        <where>
            <if test="empno!=null">and empno=#{empno}</if>
            <if test="ename!=null">and ename=#{ename}</if>
            <if test="hire_date!=null">and hire_date=#{hire_date}</if>
            <if test="job_id!=null">and job_id=#{job_id}</if>
            <if test="dept_id!=null">and dept_id=#{dept_id}</if>
            <if test="interest!=null">and interest=#{interest}</if>
        </where>
    </select>
 </mapper>
```

测试类：

```java
package com.zretc.controller;

import com.zretc.dao.EmpDao;
import com.zretc.pojo.Emp;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;

import java.io.IOException;
import java.io.Reader;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

public class EmpTest {
    @Test
    public void test01() throws IOException {
        // 获取mybatis的总配置文件
        // 1. 读取mybatis总配置文件
        Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
        // 2.获取SqlSessionFactory工厂
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
        // 3.获取SqlSession
        SqlSession sqlSession = sessionFactory.openSession(true);//
        EmpDao empDao = sqlSession.getMapper(EmpDao.class);
        // 添加
//        Emp emp = new Emp();
//        emp.setEname("soso2");
//        emp.setHire_date(new Date());
//        emp.setJob_id(1);
//        emp.setDept_id(14);
//        emp.setInterest("吃饭，睡觉，打豆豆");
//        empDao.insertEmp(emp);

        // 修改
//        Emp emp = new Emp();
//        emp.setEmpno(6);
//        emp.setEname("soso666");
//        emp.setHire_date(new Date());
//        empDao.updateEmp(emp);

        // 查询员工信息，员工编号等于值列表中的一个（例如：编号在1/2/6的员工）
//        List<Integer>  list = new ArrayList<>();
//        list.add(1);
//        list.add(2);
//        list.add(6);
//        for (Emp emp : empDao.selectByIn(list)) {
//            System.out.println(emp);
//        }

        // 查询员工编号是6以内的员工信息
//        List<Emp> emps = empDao.selectByBetween(6);
//        for (Emp emp : emps) {
//            System.out.println(emp);
//        }

        // 根据任意条件查询
//        Emp emp = new Emp();
////        emp.setEmpno(6);
////        emp.setEname("soso666");
////        emp.setHire_date(new Date());
//        for (Emp emp1 : empDao.selectByOther(emp)) {
//            System.out.println(emp1);
//        }

        // 多个连接条件
        Emp emp = new Emp();
//        emp.setEmpno(6);
//        emp.setEname("soso666");
        emp.setJob_id(1);
        emp.setDept_id(1);
        for (Emp emp1 : empDao.selectByAllOther(emp)) {
            System.out.println(emp1);
        }
        sqlSession.close();
    }
}

```



# 11、类型处理器 TypeHandlers

![image-20250307144734551](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307144734551.png)



![image-20250307144957968](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307144957968.png)



![image-20250307145217846](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307145217846.png)



![image-20250307145328513](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307145328513.png)



## 11.1 实现步骤

![image-20250307145354539](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307145354539.png)



将emp中的兴趣爱好字段，在java中定义成字符串数组类型，

## 11.2 **将java中的字符串数组 转成 数据库中的 字符串**，用 逗号进行分割



Emp中的字段 改成是数组：

```java
@Data
public class Emp {
    private Integer empno;
    private String ename;
    private Date hire_date;
    private Integer job_id;
    private Integer dept_id;
    private String[] interest;
}
```



定义类型转换器：

![image-20250307153116861](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307153116861.png)

```java
package com.zretc.typeHandler;

import org.apache.ibatis.type.BaseTypeHandler;
import org.apache.ibatis.type.JdbcType;

import java.sql.CallableStatement;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

// 字符串和数组之间的类型转换
// java --- 数组
// mysql --- varchar
public class StringAndArrayTypeHandler extends BaseTypeHandler<String[]> {

    @Override
    public void setNonNullParameter(PreparedStatement ps, int i, String[] parameter, JdbcType jdbcType) throws SQLException {
        // 往数据库中存储数据时，将java中的数组类型转成数据库中的varchar字符串
        // 数据库中的字符串：唱歌，跳舞，睡觉
        // 将数组中的元素按照逗号进行拼接
        String param = "";
        for(int j = 0;j < parameter.length;j++){
            // 最后一个元素不加逗号
            if(j == parameter.length - 1){
                param += parameter[j];
            }else{
                param += parameter[j] + ",";
            }
        }
        ps.setString(i,param);
    }

    @Override
    public String[] getNullableResult(ResultSet rs, String columnName) throws SQLException {
        // 查询时，将数据库中的字符串，转成java中的数组
        String param = rs.getString(columnName);
        // 兴趣爱好的字段允许有空值，因此需要非空判断
        if (param != null){
            // 将数据库中的 param 转成java中的数组
            // 按照 逗号 进行切割
            return param.split(",");
        }
        return new String[0];
    }

    @Override
    public String[] getNullableResult(ResultSet rs, int columnIndex) throws SQLException {
        // 查询时，将数据库中的字符串，转成java中的数组
        String param = rs.getString(columnIndex);
        // 兴趣爱好的字段允许有空值，因此需要非空判断
        if (param != null){
            // 将数据库中的 param 转成java中的数组
            // 按照 逗号 进行切割
            return param.split(",");
        }
        return new String[0];
    }

    @Override
    public String[] getNullableResult(CallableStatement cs, int columnIndex) throws SQLException {
        // 查询时，将数据库中的字符串，转成java中的数组
        // 查询时，将数据库中的字符串，转成java中的数组
        String param = cs.getString(columnIndex);
        // 兴趣爱好的字段允许有空值，因此需要非空判断
        if (param != null){
            // 将数据库中的 param 转成java中的数组
            // 按照 逗号 进行切割
            return param.split(",");
        }
        return new String[0];
    }
}

```



把类型转换器在 mybatis 总配置文件中注册：

![image-20250307153155185](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307153155185.png)

```xml
<!--  注册类型转换器  -->
    <typeHandlers>
        <package name="com.zretc.typeHandler"/>
    </typeHandlers>
```



在测试类中测试 添加 和 查询功能

```java
// 根据任意条件查询
        Emp emp = new Emp();
//        emp.setEmpno(6);
//        emp.setEname("soso666");
        emp.setHire_date(new Date());
        for (Emp emp1 : empDao.selectByOther(emp)) {
            System.out.println(emp1);
        }
```

![image-20250307153313569](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307153313569.png)



```java
// 添加
        Emp emp = new Emp();
        emp.setEname("soso2");
        emp.setHire_date(new Date());
        emp.setJob_id(1);
        emp.setDept_id(14);
        emp.setInterest(new String[]{"唱歌","睡觉","玩","敲代码"});
        empDao.insertEmp(emp);
```

![image-20250307153354511](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250307153354511.png)







## **11.3 将 日期转换成字符串**

```java
package com.zretc.typeHandler;

import org.apache.ibatis.type.BaseTypeHandler;
import org.apache.ibatis.type.JdbcType;

import java.sql.CallableStatement;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class MyDateTypeHandler extends BaseTypeHandler<Date> {
    // 将java中的Date 转成 年-月-日的日期
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
    @Override
    public void setNonNullParameter(PreparedStatement ps, int i, Date parameter, JdbcType jdbcType) throws SQLException {
        // 将日期转成字符串
        String hire_date = sdf.format(parameter);
        // 替换 i 位置的值
        ps.setString(i,hire_date);
    }

    @Override
    public Date getNullableResult(ResultSet rs, String columnName) throws SQLException {
        try {
            // 将数据库中的字符串，转成java中的Date
            String hire_date = rs.getString(columnName);
            return sdf.parse(hire_date);
        } catch (ParseException e) {
            throw new RuntimeException(e);
        }
    }

    @Override
    public Date getNullableResult(ResultSet rs, int columnIndex) throws SQLException {
        try {
            // 将数据库中的字符串，转成java中的Date
            String hire_date = rs.getString(columnIndex);
            return sdf.parse(hire_date);
        } catch (ParseException e) {
            throw new RuntimeException(e);
        }
    }

    @Override
    public Date getNullableResult(CallableStatement cs, int columnIndex) throws SQLException {
        try {
            // 将数据库中的字符串，转成java中的Date
            String hire_date = cs.getString(columnIndex);
            return sdf.parse(hire_date);
        } catch (ParseException e) {
            throw new RuntimeException(e);
        }
    }
}

```

# 12、ResultMap标签

![image-20250310090308745](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310090308745.png)

![image-20250310162856102](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310162856102.png)

![image-20250310162906190](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310162906190.png)

![image-20250310162916481](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310162916481.png)

![image-20250310162924586](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310162924586.png)

![image-20250310162934940](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310162934940.png)

!



![image-20250310162727924](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310162727924.png)



![image-20250310162749139](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310162749139.png)

![image-20250310162802203](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310162802203.png)









# 13、表与表之间的关系

- 一对一关系
  - 一个员工对应一个部门
  - tom -- > 销售部
- 一对多关系
  - 一个部门有多个员工
    - 销售部 --> tom,lisa
- 多对多关系
  - 一个员工有多个职务，一个职位对应多个员工
    - tom --> 经理，销售员
    - lisa --> 前台，销售员
    - jake --> 质检员，维修员
  - 一个学生有多个角色，一个角色对应多个学生
    - 学生--》班长，学委    
    - 班长 --》张三，李四
    - 学委 --》张三，王五



![image-20250310163132855](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310163132855.png)

## 13.1 一对一与一对多

- ![image-20250310163152109](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310163152109.png)



### 13.1.1 一对一

在Emp类中声明一对一关系

```java
@Data
public class Emp {
    private Integer empno;
    private String ename;
    private Date hire_date;
    private Integer job_id;
    private Integer dept_id;
    private String[] interest;

    // 一对一关系：一个员工对应一个部门
    private Dept dept;
}
```



在 EmpDao 中声明接口

```java
    // 查询员工对应的部门信息
    List<Emp> selectEmpAndDept();
```



在 EmpDao.xml 中写一对一的sql语句

```xml
    <!--  resultMap 映射  -->
    <resultMap id="resultMap" type="emp">
        <!-- id 主键字段
                column 查询结果的字段名
                property 使用setter依赖注入给java实体类的属性
        -->
        <id column="empno" property="empno"/>
        <result column="ename" property="ename"/>
        <result column="hire_date" property="hire_date"/>
        <result column="job_id" property="job_id"/>
        <result column="dept_id" property="dept_id"/>
        <result column="interest" property="interest"/>
        <!--  嵌套结果: 1) 一对一关系：使用result 映射对象的属性     -->
        <!--        <result column="dept_name" property="dept.dept_name"/>-->

        <!--   嵌套结果: 2)一对一关系：一个员工对应一个部门     -->
        <!--        <association property="dept" javaType="dept">-->
        <!--            <id column="dept_id" property="dept_id"/>-->
        <!--            <result column="dept_name" property="dept_name"/>-->
        <!--            <result column="dept_loc" property="dept_loc"/>-->
        <!--        </association>-->

        <!-- 嵌套结果:3)一对一关系：引入另一个mapper文件中的resultMap -->
        <!--        <association property="dept" resultMap="com.zretc.dao.DeptDao.resultMap"/>-->

        <!-- 嵌套查询；1) 一对一关系,引用另一条查询语句 -->
        <association property="dept" select="com.zretc.dao.DeptDao.selectById" column="dept_id"/>
    
    </resultMap>

	<!--  一对一关系：查询员工对应的部门信息  -->
    <select id="selectEmpAndDept" resultMap="resultMap">
        <!-- 嵌套结果： -->
        <!--  select e.*,d.* from emp e,dept d where e.dept_id = d.dept_id-->

        <!-- 嵌套查询： -->
        select * from emp
    </select>
```



测试类：

```java
    @Test
    public void test02() throws IOException {
            // 获取mybatis的总配置文件
            // 1. 读取mybatis总配置文件
            Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
            // 2.获取SqlSessionFactory工厂
            SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
            // 3.获取SqlSession
            SqlSession sqlSession = sessionFactory.openSession(true);//
            EmpDao empDao = sqlSession.getMapper(EmpDao.class);
            for (Emp emp : empDao.selectEmpAndDept()) {
                System.out.println(emp);
            }

            sqlSession.close();
    }
```

![image-20250310164450117](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310164450117.png)



### 13.1.2 一对多

Dept实体类中体现一对多关系

```java
@Data
public class Dept {
    private Integer dept_id;
    private String dept_name;
    private String dept_loc;
    // 一对多：一个部门对应多个员工
    private List<Emp> empList;

    public Dept(Integer dept_id,String dept_name,String dept_loc){
        this.dept_id = dept_id;
        this.dept_name = dept_name;
        this.dept_loc = dept_loc;
    }
}
```



在DeptDao 中声明接口

```java
    // 一对多：一个部门对应多个员工
    List<Dept> selectDeptAndEmp();
```



在DeptDao 中编写接口的sql语句

```xml
<resultMap id="resultMap" type="dept">
        <!--  setter注入      -->
        <!--        <id column="dept_id" property="dept_id"/>-->
        <!--        <result column="dept_name" property="dept_name"/>-->
        <!--        <result column="dept_loc" property="dept_loc"/>-->
        <!--   构造方法注入     -->
        <constructor>
            <idArg column="dept_id" javaType="java.lang.Integer"/>
            <arg column="dept_name" javaType="java.lang.String"/>
            <arg column="dept_loc" javaType="java.lang.String"/>
        </constructor>

        <!-- 嵌套结果: 一对多关系  -->
        <!--        <collection property="empList" resultMap="com.zretc.dao.EmpDao.resultMap"/>-->

        <!--   嵌套查询:一对多关系   -->
        <collection property="empList" select="com.zretc.dao.EmpDao.selectByDeptId" column="dept_id"/>
    </resultMap>

    <!--  一对多关系：一个部门对应多个员工  -->
    <select id="selectDeptAndEmp" resultMap="resultMap">
        <!--  一对多关系：嵌套结果  -->
        <!--select * from emp join dept using(dept_id)-->
        <!-- 嵌套查询 -->
        select * from dept
    </select>
```



嵌套查询的一对多关系中利用了 员工的 根据部门编号查询方法

在 EmpDao 中声明接口

```java
    // 根据部门编号查询所有员工
    List<Emp> selectByDeptId(Integer dept_id);
```

在 EmpDao 对应的mapper 文件中写sql语句

```xml
<!--  根据部门编号查询所有员工  -->
    <select id="selectByDeptId" resultType="emp">
        select *
        from emp
        where dept_id = #{0}
    </select>
```

测试类;

```java
 @Test
    public void test03() throws IOException {

        // 获取mybatis的总配置文件
        // 1. 读取mybatis总配置文件
        Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
        // 2.获取SqlSessionFactory工厂
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
        // 3.获取SqlSession
        SqlSession sqlSession = sessionFactory.openSession(true);// true:自动提交
        DeptDao dao = sqlSession.getMapper(DeptDao.class);
        // 查询部门对应的所有员工
        List<Dept> deptList = dao.selectDeptAndEmp();
        for (Dept dept:deptList){
            System.out.println(dept);
        }
        sqlSession.close();
    }
```

![image-20250310164554748](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310164554748.png)

# 13.1.3 多对多

```sql
-- 员工的家庭角色
-- 家庭角色表 Role
--  1 父亲
--  2 母亲
--  3 哥哥
--  4 弟弟
--  5 姐姐
--  6 妹妹
create table role(
     role_id int primary key auto_increment,
     role_name  varchar(99)
);
insert into role values(default,'父亲'),(default,'母亲'),
                       (default,'哥哥'),(default,'弟弟'),
                       (default,'姐姐'),(default,'妹妹');
-- emp_role 员工角色关系表
--  1  1   tom是一个父亲
--  1  3   tom是一个哥哥
--  2  2   lisa是一个妈妈
--  2  6   lisa是一个妹妹
--  4  6   kiki是一个妹妹
-- 一个角色对应多个员工，一个员工对应多个角色
create table emp_role(
    empno int,
    role_id int
);
insert into emp_role values(1,1),(1,3),
                           (2,2),(2,6),
                           (4,6),(3,4),
                           (5,5),(7,5),
                           (8,2),(9,2);


-- 查询员工对应的角色
-- 员工表的员工编号=关系表中的员工编号
-- 角色表的角色编号=关系表中的角色编号
select *
from emp e,role r,emp_role er
where e.empno = er.empno and r.role_id = er.role_id;
```



在 Emp 中声明多对多关系

```java
@Data
public class Emp {
    private Integer empno;
    private String ename;
    private Date hire_date;
    private Integer job_id;
    private Integer dept_id;
    private String[] interest;

    // 一对一关系：一个员工对应一个部门
    private Dept dept;

    // 多对多关系：员工有哪些家庭角色
    private List<Role> roleList;
}
```

在 EmpDao 中写多对多关系的接口

```java
    // 员工有哪些家庭角色
    List<Emp> selectRoleList();
```

在 EmpDao 的 mapper 文件中写对应的sql代码

```xml
<resultMap ...>
    ......
	 <!--   多对多关系： 员工有哪些家庭角色   -->
        <collection property="roleList" ofType="role">
            <id column="role_id" property="role_id"/>
            <result column="role_name" property="role_name"/>
        </collection>
</resultMap>    

<!--  员工有哪些家庭角色  -->
    <select id="selectRoleList" resultMap="resultMap">
        select *
        from emp e,
             role r,
             emp_role er
        where e.empno = er.empno
          and r.role_id = er.role_id
    </select>
```



测试类：

```java
@Test
    public void test03() throws IOException {
        // 获取mybatis的总配置文件
        // 1. 读取mybatis总配置文件
        Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
        // 2.获取SqlSessionFactory工厂
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
        // 3.获取SqlSession
        SqlSession sqlSession = sessionFactory.openSession(true);//
        EmpDao empDao = sqlSession.getMapper(EmpDao.class);
        for (Emp emp : empDao.selectRoleList()) {
            System.out.print(emp.getEname() + "---");
            // 所有的角色
            for (Role role : emp.getRoleList()) {
                System.out.print(role.getRole_name()+"  ");
            }
            System.out.println();
        }

        sqlSession.close();
    }
```

![image-20250310165827555](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310165827555.png)

![image-20250310165810158](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310165810158.png)





# 14、分页操作

```sql
-- 分页
-- 员工表，一页显示3行记录
-- 第一页：limit 3
select * from emp limit 3;
-- 第二页：limit 偏移量，记录数  注意：偏移量从0开始
--        limit 3,3  从第4行记录还是，显示3行
select * from emp limit 3,3;
-- 第三页：
select * from emp limit 6,3;
```



1、引入依赖

```xml
 <!--  导入分页的依赖PageHelper  -->
        <dependency>
            <groupId>com.github.pagehelper</groupId>
            <artifactId>pagehelper</artifactId>
            <version>5.3.2</version>
        </dependency>
```



2、mybatis的总配置文件，添加分页的插件

==注意顺序==

```xml
    <!--  分页的插件  -->
    <plugins>
        <plugin interceptor="com.github.pagehelper.PageInterceptor">
            <!--  value指定为mysql后，分页就会按照limit执行  -->
            <property name="helperDialect" value="mysql"/>
        </plugin>
    </plugins>
```



3、EmpDao 中声明分页查询的接口：

```java
   // 分页处理：一页显示3行记录
    @Select("select * from emp")
    List<Emp> selectByPageHelper();
```



4、EmpDao的mapper文件中写sql语句

```xml
 <!--  分页处理：一页显示3行记录  -->
    <select id="selectByPageHelper" resultMap="resultMap">
        select * from emp
    </select>
```



5、测试类

```java
 @Test
    public void test04() throws IOException {
        // 获取mybatis的总配置文件
        // 1. 读取mybatis总配置文件
        Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
        // 2.获取SqlSessionFactory工厂
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
        // 3.获取SqlSession
        SqlSession sqlSession = sessionFactory.openSession(true);//
        EmpDao empDao = sqlSession.getMapper(EmpDao.class);

        // 分页，需要有两个参数：1.当前页码  2.一页显示几行
        PageHelper.startPage(2,3);// 第2页，一页显示3行记录
        // 调用查询的接口
        // 当前集合中封装了，当前页码的多有员工信息
        List<Emp> emps = empDao.selectByPageHelper();
//        System.out.println("emps = " + emps);

        // 将查询到的数据封装到PageInfo的对象中
        PageInfo<Emp> pageInfo = new PageInfo<>(emps);
        // 当前页的数据
        List<Emp> list = pageInfo.getList();
        list.forEach(emp-> System.out.println(emp));

        // 获取总页数
        System.out.println("总页数：" + pageInfo.getPages());
        // 总记录数
        System.out.println("总记录数：" + pageInfo.getTotal());
        // 当前页面
        System.out.println("当前页面：" + pageInfo.getPageNum());
        // 当前页的记录数
        System.out.println("当前页的记录数：" + pageInfo.getPageSize());
        // 开始记录数（行号）
        System.out.println("开始记录数（行号）:" + pageInfo.getStartRow());
        // 结束记录数（行号）
        System.out.println("结束记录数（行号）:" + pageInfo.getEndRow());
        sqlSession.close();
    }
```

![image-20250310170623180](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310170623180.png)

![image-20250310170608116](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310170608116.png)





# 15、基于注解的映射处理

![image-20250310144833312](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310144833312.png)

![image-20250310145015667](C:\Users\ZRETC\AppData\Roaming\Typora\typora-user-images\image-20250310145015667.png)



## 15.1 配置文件

引入依赖：

```xml
<dependencies>
        <!--  导入mybatis依赖  -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.14</version>
        </dependency>
        <!--   驱动     -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.33</version>
        </dependency>
        <!--    juint    -->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.30</version>
            <scope>provided</scope>
        </dependency>
        <!--  导入分页的依赖PageHelper  -->
        <dependency>
            <groupId>com.github.pagehelper</groupId>
            <artifactId>pagehelper</artifactId>
            <version>5.3.2</version>
        </dependency>
    </dependencies>
```



属性文件：

```properties
jdbc.driver=com.mysql.cj.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/zly
jdbc.user=root
jdbc.password=root
```



mybatis总配置文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--  引入属性文件  -->
    <properties resource="jdbc.properties"/>
    <!-- 日志信息 -->
    <settings>
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>

    <!--  给实体类起别名  -->
    <typeAliases>
        <package name="com.zretc.pojo"/>
    </typeAliases>

    <!--  注册类型转换器  -->
    <typeHandlers>
        <package name="com.zretc.typeHandler"/>
    </typeHandlers>

    <!--  分页的插件  -->
    <plugins>
        <plugin interceptor="com.github.pagehelper.PageInterceptor">
            <!--  value指定为mysql后，分页就会按照limit执行  -->
            <property name="helperDialect" value="mysql"/>
        </plugin>
    </plugins>

    <!--  基础环境  -->
    <environments default="development">
        <environment id="development">
            <!--  事务管理器  -->
            <transactionManager type="JDBC"/>
            <!--  数据源  -->
            <dataSource type="POOLED">
                <property name="driver" value="${jdbc.driver}"/>
                <property name="url" value="${jdbc.url}"/>
                <property name="username" value="${jdbc.user}"/>
                <property name="password" value="${jdbc.password}"/>
            </dataSource>
        </environment>
    </environments>
    <!--  引入mapper文件  -->
    <mappers>
        <package name="com.zretc.dao"/>
    </mappers>
</configuration>
```



## 15.2 pojo

员工：

```java
package com.zretc.pojo;

import lombok.Data;

import java.util.Date;
import java.util.List;

@Data
public class Emp {
    private Integer empno;
    private String ename;
    private Date hire_date;
    private Integer job_id;
    private Integer dept_id;
    private String[] interest;

    // 一对一关系：一个员工对应一个部门
    private Dept dept;

    // 多对多关系：员工有哪些家庭角色
    private List<Role> roleList;
}

```

部门；

```java
package com.zretc.pojo;


import lombok.Data;

import java.util.List;

@Data
public class Dept {
    private Integer dept_id;
    private String dept_name;
    private String dept_loc;
    // 一对多：一个部门对应多个员工
    private List<Emp> empList;

    public Dept(Integer dept_id,String dept_name,String dept_loc){
        this.dept_id = dept_id;
        this.dept_name = dept_name;
        this.dept_loc = dept_loc;
    }

}


```

角色；

```java


package com.zretc.pojo;

import lombok.Data;

@Data
public class Role {
    private Integer role_id;
    private String role_name;
}
```



## 15.3 dao层

员工；

```java
package com.zretc.dao;

import com.zretc.pojo.Emp;
import org.apache.ibatis.annotations.*;

import java.util.List;

public interface EmpDao {
    @Insert("<script>" +
            "  insert into emp" +
            "        <trim prefix=\"(\" suffix=\")\" suffixOverrides=\",\">" +
            "            <if test=\"ename!=null\">ename,</if>" +
            "            <if test=\"hire_date!=null\">hire_date,</if>" +
            "            <if test=\"job_id!=null\">job_id,</if>" +
            "            <if test=\"dept_id!=null\">dept_id,</if>" +
            "            <if test=\"interest!=null\">interest,</if>" +
            "        </trim>\n" +
            "        <trim prefix=\"values(\" suffix=\")\" suffixOverrides=\",\">" +
            "            <if test=\"ename!=null\">#{ename},</if>" +
            "            <if test=\"hire_date!=null\">#{hire_date},</if>" +
            "            <if test=\"job_id!=null\">#{job_id},</if>" +
            "            <if test=\"dept_id!=null\">#{dept_id},</if>" +
            "            <if test=\"interest!=null\">#{interest},</if>" +
            "        </trim>" +
            "</script>")
    // 添加
    int insertEmp(Emp emp);
    // 修改
    @Update("<script>" +
            "        update emp" +
            "        <set>" +
            "            <if test=\"ename!=null\">ename=#{ename},</if>" +
            "            <if test=\"hire_date!=null\">hire_date=#{hire_date},</if>" +
            "            <if test=\"job_id!=null\">job_id=#{job_id},</if>" +
            "            <if test=\"dept_id!=null\">dept_id=#{dept_id},</if>" +
            "            <if test=\"interest!=null\">interest=#{interest},</if>" +
            "        </set>\n" +
            "        where empno = #{empno}" +
            "</script>")
    int updateEmp(Emp emp);
    // 删除
    @Delete("delete from emp where empno = #{0}")
    int deleteEmp(Integer empno);
    // 查询所有
    @Select("select * from emp")
    List<Emp> selectAll();
    // 根据编号查询

    @Select("select * from emp where empno = #{0}")
    Emp selectByNo(Integer empno);

    // 查询员工信息，员工编号等于值列表中的一个（例如：编号在1/2/6的员工）
    @Select("<script>" +
            " select * from emp where empno in"+
            "<foreach collection=\"list\" item=\"empno\" open=\"(\" close=\")\" separator=\",\">" +
            "            #{empno}" +
            "        </foreach>"+
            "</script>")
    List<Emp> selectByIn(List<Integer> empno);

    // 查询员工编号是6以内的员工信息
    @Select("<![CDATA[" +
            "            select * from emp where empno < #{0}" +
            "        ]]>")
    List<Emp> selectByBetween(Integer empno);

    // 根据任意条件查询
    @Select("<script>" +
            "select * from emp" +
            "        <where>"+
            "            <choose>" +
            "                <when test=\"empno!=null\">empno=#{empno}</when>" +
            "                <when test=\"ename!=null\">ename=#{ename}</when>" +
            "                <when test=\"hire_date!=null\">hire_date=#{hire_date}</when>" +
            "                <when test=\"job_id!=null\">job_id=#{job_id}</when>" +
            "                <when test=\"dept_id!=null\">dept_id=#{dept_id}</when>" +
            "                <when test=\"interest!=null\">interest=#{interest}</when>" +
            "                <otherwise>1=1</otherwise>" +
            "            </choose>" +
            "        </where>" +
            "</script>")
    List<Emp> selectByOther(Emp emp);

    // 多个条件
    @Select("<script>" +
            "select * from emp" +
            "        <where>" +
            "            <if test=\"empno!=null\">and empno=#{empno}</if>" +
            "            <if test=\"ename!=null\">and ename=#{ename}</if>" +
            "            <if test=\"hire_date!=null\">and hire_date=#{hire_date}</if>" +
            "            <if test=\"job_id!=null\">and job_id=#{job_id}</if>" +
            "            <if test=\"dept_id!=null\">and dept_id=#{dept_id}</if>" +
            "            <if test=\"interest!=null\">and interest=#{interest}</if>" +
            "        </where>" +
            "</script>")
    List<Emp> selectByAllOther(Emp emp);

    // 查询员工对应的部门信息
    @Select("select * from emp")
    @Results({
            @Result(column = "empno",property ="empno" ),
            @Result(column = "ename",property ="ename" ),
            @Result(column = "hire_date",property ="hire_date" ),
            @Result(column = "job_id",property ="job_id" ),
            @Result(column = "dept_id",property ="dept_id" ),
            @Result(column = "interest",property ="interest" ),
            @Result(column = "dept_id", // 查询时传递的参数
                    property = "dept",  // 查询结果映射的对象
                    one = @One(select = "com.zretc.dao.DeptDao.selectById"))
    })
    List<Emp> selectEmpAndDept();

    // 根据部门编号查询所有员工
    @Select("select * from emp where dept_id = #{0}")
    List<Emp> selectByDeptId(Integer dept_id);

    // 员工有哪些家庭角色
    @Select("select * from emp")
    @Results({
            @Result(column = "empno",property ="empno" ),
            @Result(column = "ename",property ="ename" ),
            @Result(column = "hire_date",property ="hire_date" ),
            @Result(column = "job_id",property ="job_id" ),
            @Result(column = "dept_id",property ="dept_id" ),
            @Result(column = "interest",property ="interest" ),
            @Result(column = "empno", // 查询时传递的参数
                    property = "roleList",  // 查询结果映射的对象
                    many = @Many(select = "com.zretc.dao.RoleDao.selectRoleByEmpno"))
    })
    List<Emp> selectRoleList();

    // 分页处理：一页显示3行记录
    @Select("select * from emp")
    List<Emp> selectByPageHelper();
}

```



部门：

```java
package com.zretc.dao;

import com.zretc.pojo.Dept;
import org.apache.ibatis.annotations.*;

import java.util.List;

public interface DeptDao {
    @Insert("insert into dept values (default, #{dept_name,jdbcType=VARCHAR}, #{dept_loc})")
    int insertDept(Dept dept);

    @Delete("delete from dept where dept_id=#{0}")
    int deleteDept(Integer dept_id);

    @Update(" update dept set dept_name=#{dept_name},dept_loc=#{dept_loc}" +
            " where dept_id = #{dept_id}")
    int updateDept(Dept dept);

    @Select("select * from dept")
    List<Dept> selectAll();

    @Select("select * from dept where dept_id = #{dept_id}")
    Dept selectById(@Param("dept_id") Integer dept_id);

    @Select("select * from dept where dept_name like concat('%', #{dept_name}, '%')")
    List<Dept> selectByLike(@Param("dept_name") String dept_name);

    // 一对多：一个部门对应多个员工
    @Select("select * from dept")
    @Results({
            @Result(column = "dept_id",property = "dept_id"),
            @Result(column = "dept_name",property = "dept_name"),
            @Result(column = "dept_loc",property = "dept_loc"),
            @Result(
                    property = "empList",
                    column = "dept_id", // 传递的参数根据部门编号，在员工表中查询所有的员工
                    many = @Many(select="com.zretc.dao.EmpDao.selectByDeptId")
            )
    })
    List<Dept> selectDeptAndEmp();
}

```



角色

```java
package com.zretc.dao;

import com.zretc.pojo.Role;
import org.apache.ibatis.annotations.Select;

import java.util.List;

public interface RoleDao {
    // 根据员工编号查询员工对应的角色
    @Select("select * " +
            "from role r,emp_role er " +
            "where r.role_id = er.role_id " +
            "and er.empno = #{0}")
    List<Role> selectRoleByEmpno(Integer empno);
}

```



## 15.4 类型处理器

数组转字符串

```java
package com.zretc.typeHandler;

import org.apache.ibatis.type.BaseTypeHandler;
import org.apache.ibatis.type.JdbcType;

import java.sql.CallableStatement;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

// 字符串和数组之间的类型转换
// java --- 数组
// mysql --- varchar
public class StringAndArrayTypeHandler extends BaseTypeHandler<String[]> {

    @Override
    public void setNonNullParameter(PreparedStatement ps, int i, String[] parameter, JdbcType jdbcType) throws SQLException {
        // 往数据库中存储数据时，将java中的数组类型转成数据库中的varchar字符串
        // 数据库中的字符串：唱歌，跳舞，睡觉
        // 将数组中的元素按照逗号进行拼接
        String param = "";
        for(int j = 0;j < parameter.length;j++){
            // 最后一个元素不加逗号
            if(j == parameter.length - 1){
                param += parameter[j];
            }else{
                param += parameter[j] + ",";
            }
        }
        ps.setString(i,param);
    }

    @Override
    public String[] getNullableResult(ResultSet rs, String columnName) throws SQLException {
        // 查询时，将数据库中的字符串，转成java中的数组
        String param = rs.getString(columnName);
        // 兴趣爱好的字段允许有空值，因此需要非空判断
        if (param != null){
            // 将数据库中的 param 转成java中的数组
            // 按照 逗号 进行切割
            return param.split(",");
        }
        return new String[0];
    }

    @Override
    public String[] getNullableResult(ResultSet rs, int columnIndex) throws SQLException {
        // 查询时，将数据库中的字符串，转成java中的数组
        String param = rs.getString(columnIndex);
        // 兴趣爱好的字段允许有空值，因此需要非空判断
        if (param != null){
            // 将数据库中的 param 转成java中的数组
            // 按照 逗号 进行切割
            return param.split(",");
        }
        return new String[0];
    }

    @Override
    public String[] getNullableResult(CallableStatement cs, int columnIndex) throws SQLException {
        // 查询时，将数据库中的字符串，转成java中的数组
        // 查询时，将数据库中的字符串，转成java中的数组
        String param = cs.getString(columnIndex);
        // 兴趣爱好的字段允许有空值，因此需要非空判断
        if (param != null){
            // 将数据库中的 param 转成java中的数组
            // 按照 逗号 进行切割
            return param.split(",");
        }
        return new String[0];
    }
}

```



日期转字符串

```java
package com.zretc.typeHandler;

import org.apache.ibatis.type.BaseTypeHandler;
import org.apache.ibatis.type.JdbcType;

import java.sql.CallableStatement;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class MyDateTypeHandler extends BaseTypeHandler<Date> {
    // 将java中的Date 转成 年-月-日的日期
    SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
    @Override
    public void setNonNullParameter(PreparedStatement ps, int i, Date parameter, JdbcType jdbcType) throws SQLException {
        // 将日期转成字符串
        String hire_date = sdf.format(parameter);
        // 替换 i 位置的值
        ps.setString(i,hire_date);
    }

    @Override
    public Date getNullableResult(ResultSet rs, String columnName) throws SQLException {
        try {
            // 将数据库中的字符串，转成java中的Date
            String hire_date = rs.getString(columnName);
            return sdf.parse(hire_date);
        } catch (ParseException e) {
            throw new RuntimeException(e);
        }
    }

    @Override
    public Date getNullableResult(ResultSet rs, int columnIndex) throws SQLException {
        try {
            // 将数据库中的字符串，转成java中的Date
            String hire_date = rs.getString(columnIndex);
            return sdf.parse(hire_date);
        } catch (ParseException e) {
            throw new RuntimeException(e);
        }
    }

    @Override
    public Date getNullableResult(CallableStatement cs, int columnIndex) throws SQLException {
        try {
            // 将数据库中的字符串，转成java中的Date
            String hire_date = cs.getString(columnIndex);
            return sdf.parse(hire_date);
        } catch (ParseException e) {
            throw new RuntimeException(e);
        }
    }
}

```



## 15.5 测试类

员工

```java
package com.zretc.controller;

import com.github.pagehelper.PageHelper;
import com.github.pagehelper.PageInfo;
import com.zretc.dao.EmpDao;
import com.zretc.pojo.Emp;
import com.zretc.pojo.Role;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;

import java.io.IOException;
import java.io.Reader;
import java.util.Date;
import java.util.List;

public class EmpTest {
    @Test
    public void test01() throws IOException {
        // 获取mybatis的总配置文件
        // 1. 读取mybatis总配置文件
        Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
        // 2.获取SqlSessionFactory工厂
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
        // 3.获取SqlSession
        SqlSession sqlSession = sessionFactory.openSession(true);//
        EmpDao empDao = sqlSession.getMapper(EmpDao.class);
        // 添加
//        Emp emp = new Emp();
//        emp.setEname("soso2");
//        emp.setHire_date(new Date());
//        emp.setJob_id(1);
//        emp.setDept_id(14);
////        emp.setInterest(new String[]{"唱歌","睡觉","玩","敲代码"});
//        empDao.insertEmp(emp);

        // 修改
//        Emp emp = new Emp();
//        emp.setEmpno(6);
//        emp.setEname("soso666");
//        emp.setHire_date(new Date());
//        empDao.updateEmp(emp);

        // 查询员工信息，员工编号等于值列表中的一个（例如：编号在1/2/6的员工）
//        List<Integer>  list = new ArrayList<>();
//        list.add(1);
//        list.add(2);
//        list.add(6);
//        for (Emp emp : empDao.selectByIn(list)) {
//            System.out.println(emp);
//        }

        // 查询员工编号是6以内的员工信息
//        List<Emp> emps = empDao.selectByBetween(6);
//        for (Emp emp : emps) {
//            System.out.println(emp);
//        }

        // 根据任意条件查询
//        Emp emp = new Emp();
////        emp.setEmpno(6);
////        emp.setEname("soso666");
//        emp.setHire_date(new Date());
//        for (Emp emp1 : empDao.selectByOther(emp)) {
//            System.out.println(emp1);
//        }

        // 多个连接条件
        Emp emp = new Emp();
//        emp.setEmpno(6);
//        emp.setEname("soso666");
        emp.setJob_id(1);
        emp.setDept_id(1);
        for (Emp emp1 : empDao.selectByAllOther(emp)) {
            System.out.println(emp1);
        }
        sqlSession.close();
    }

    @Test
    public void test02() throws IOException {
            // 获取mybatis的总配置文件
            // 1. 读取mybatis总配置文件
            Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
            // 2.获取SqlSessionFactory工厂
            SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
            // 3.获取SqlSession
            SqlSession sqlSession = sessionFactory.openSession(true);//
            EmpDao empDao = sqlSession.getMapper(EmpDao.class);
            for (Emp emp : empDao.selectEmpAndDept()) {
                System.out.println(emp);
            }

            sqlSession.close();
    }

    @Test
    public void test03() throws IOException {
        // 获取mybatis的总配置文件
        // 1. 读取mybatis总配置文件
        Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
        // 2.获取SqlSessionFactory工厂
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
        // 3.获取SqlSession
        SqlSession sqlSession = sessionFactory.openSession(true);//
        EmpDao empDao = sqlSession.getMapper(EmpDao.class);
        for (Emp emp : empDao.selectRoleList()) {
            System.out.print(emp.getEname() + "---");
            // 所有的角色
            for (Role role : emp.getRoleList()) {
                System.out.print(role.getRole_name()+"  ");
            }
            System.out.println();
        }

        sqlSession.close();
    }

    @Test
    public void test04() throws IOException {
        // 获取mybatis的总配置文件
        // 1. 读取mybatis总配置文件
        Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
        // 2.获取SqlSessionFactory工厂
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
        // 3.获取SqlSession
        SqlSession sqlSession = sessionFactory.openSession(true);//
        EmpDao empDao = sqlSession.getMapper(EmpDao.class);

        // 分页，需要有两个参数：1.当前页码  2.一页显示几行
        PageHelper.startPage(2,3);// 第2页，一页显示3行记录
        // 调用查询的接口
        // 当前集合中封装了，当前页码的多有员工信息
        List<Emp> emps = empDao.selectByPageHelper();
//        System.out.println("emps = " + emps);

        // 将查询到的数据封装到PageInfo的对象中
        PageInfo<Emp> pageInfo = new PageInfo<>(emps);
        // 当前页的数据
        List<Emp> list = pageInfo.getList();
        list.forEach(emp-> System.out.println(emp));

        // 获取总页数
        System.out.println("总页数：" + pageInfo.getPages());
        // 总记录数
        System.out.println("总记录数：" + pageInfo.getTotal());
        // 当前页面
        System.out.println("当前页面：" + pageInfo.getPageNum());
        // 当前页的记录数
        System.out.println("当前页的记录数：" + pageInfo.getPageSize());
        // 开始记录数（行号）
        System.out.println("开始记录数（行号）:" + pageInfo.getStartRow());
        // 结束记录数（行号）
        System.out.println("结束记录数（行号）:" + pageInfo.getEndRow());
        sqlSession.close();
    }
}

```



部门

```java
package com.zretc.controller;


import com.zretc.dao.DeptDao;
import com.zretc.pojo.Dept;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.RowBounds;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import org.junit.Test;

import java.io.IOException;
import java.io.Reader;
import java.util.List;

public class MainTest {
    @Test
    public void test01() throws IOException {
        // 获取mybatis的总配置文件
        // 1. 读取mybatis总配置文件
        Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
        // 2.获取SqlSessionFactory工厂
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
        // 3.获取SqlSession
        SqlSession sqlSession = sessionFactory.openSession(true);// true:自动提交
        // 4.获取接口对象
        DeptDao deptDao = sqlSession.getMapper(DeptDao.class);
        // 5.调用添加方法
//        Dept dept = new Dept();
//        dept.setDept_name("生产部");
//        dept.setDept_loc("1楼101车间");
//        deptDao.insertDept(dept);

        // 删除功能
//        deptDao.deleteDept(15);

        // 修改
//        Dept dept = new Dept();
//        dept.setDept_id(14);
//        dept.setDept_name("生产部666");
//        dept.setDept_loc("1楼106车间");
//        deptDao.updateDept(dept);

        // 查询所有
//        List<Dept> depts = deptDao.selectAll();
//        depts.forEach(dept -> System.out.println(dept));

        // 根据部门编号查询
        Dept dept = deptDao.selectById(14);
        System.out.println(dept);

        // 模糊查询
//        List<Dept> depts = deptDao.selectByLike("6");
//        depts.forEach(dept -> System.out.println(dept));
        // 6.事务的提交
//        sqlSession.commit();
        // 7.关闭SqlSession
        sqlSession.close();
    }

    @Test
    public void test02() throws IOException {

        // 获取mybatis的总配置文件
        // 1. 读取mybatis总配置文件
        Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
        // 2.获取SqlSessionFactory工厂
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
        // 3.获取SqlSession
        SqlSession sqlSession = sessionFactory.openSession(true);// true:自动提交

        // 利用SqlSession来执行sql
        // 1.添加
//        Dept dept = new Dept();
//        dept.setDept_name("打包部");
//        dept.setDept_loc("1楼102车间");
//        sqlSession.insert("com.zretc.dao.DeptDao.insertDept",dept);

        // 2.删除
//        sqlSession.delete("com.zretc.dao.DeptDao.deleteDept",16);

        // 3.修改
//        Dept dept = new Dept();
//        dept.setDept_id(14);
//        dept.setDept_name("打包部");
//        dept.setDept_loc("1楼102车间");
//        sqlSession.update("com.zretc.dao.DeptDao.updateDept",dept);

//        4. 根据id查询
//        Dept dept = sqlSession.selectOne("com.zretc.dao.DeptDao.selectById",14);
//        System.out.println(dept);

        // 5. 查询所有
//        List<Dept> depts = sqlSession.selectList("com.zretc.dao.DeptDao.selectAll");
//        depts.forEach(dept -> System.out.println(dept));

        // 6.模糊查询
//        List<Dept> depts = sqlSession.selectList("com.zretc.dao.DeptDao.selectByLike","部");
//        depts.forEach(dept -> System.out.println(dept));

        // 7. selectMap 将部门名称作为键
//        Map<String,Dept> deptMap = sqlSession.selectMap("com.zretc.dao.DeptDao.selectAll","dept_name");
//        for (String s : deptMap.keySet()) {
//            System.out.println(s + ":" + deptMap.get(s));
//        }


        // 8、分页查询
        RowBounds rb = new RowBounds(2, 3);
        List<Dept> depts = sqlSession.selectList("com.zretc.dao.DeptDao.selectAll", null, rb);
        depts.forEach(dept -> System.out.println(dept));
        sqlSession.close();
    }

    @Test
    public void test03() throws IOException {

        // 获取mybatis的总配置文件
        // 1. 读取mybatis总配置文件
        Reader reader = Resources.getResourceAsReader("mybatisConfig.xml");
        // 2.获取SqlSessionFactory工厂
        SqlSessionFactory sessionFactory = new SqlSessionFactoryBuilder().build(reader);
        // 3.获取SqlSession
        SqlSession sqlSession = sessionFactory.openSession(true);// true:自动提交
        DeptDao dao = sqlSession.getMapper(DeptDao.class);
        // 查询部门对应的所有员工
        List<Dept> deptList = dao.selectDeptAndEmp();
        for (Dept dept:deptList){
            System.out.println(dept);
        }
        sqlSession.close();
    }
}

```

