# JAVA Web Configuration Guide



### java web配置tomcat

##### 1. add configuration

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20191115172614899.png" alt="image-20191115172614899" style="zoom: 50%;" />

##### 2. add artifacts --- fix

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20191115172951984.png" alt="image-20191115172951984" style="zoom:50%;" />

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20191115172915061.png" alt="image-20191115172915061" style="zoom: 50%;" />

##### 3. 配置 web 存放位置

新建文件夹-->绿色小加号-->Directory Content选择Web存放的位置，当然是Tomcat的webapps了,生成的war文件部署在该项目中才可以在Tomcat服务器上运行。直接运行在web文件夹下的index。jsp文件，做最后验证。 

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20191115173226401.png" alt="image-20191115173226401" style="zoom:67%;" />

##### 4. 添加并配置servlet

web.xml 

```xml
    <servlet>
        <servlet-name>TestServlet</servlet-name> // servlet-name
        <servlet-class>test.TestServlet</servlet-class> // find class
    </servlet>
    
    <servlet-mapping>
        <servlet-name>TestServlet</servlet-name> // servlet-name
        <url-pattern>/index</url-pattern> // url
    </servlet-mapping>
```



### Mybatis 配置

##### project structure 导入所有相关 jar

注意mybatis 版本

mybtais-3.5.3 jar 是最新的，不会有warning

##### 创建 mybatis-config.xml

创建config目录，并添加为 resources

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
  <environments default="development">
    <environment id="development">
      <transactionManager type="JDBC"/>
      <dataSource type="POOLED">
        <property name="driver" value="${driver}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
      </dataSource>
    </environment>
  </environments>
  <mappers>
    <mapper resource="org/mybatis/example/BlogMapper.xml"/>
  </mappers>
</configuration>
```

##### 数据库参数

加入odbc.jar

```txt
oracle
  driver="oracle.jdbc.driver.OracleDriver"
  url="jdbc:oracle:thin:@localhost:1521:数据库名"
sqlserver
  driver="com.microsoft.jdbc.sqlserver.SQLServerDriver"
  url="jdbc:microsoft:sqlserver://localhost:1433;DatabaseName=数据库名"
mysql
  driver="com.mysql.jdbc.Driver"
  url="jdbc:mysql://localhost/数据库名?[后接参数]"
db2
  driver="com.ibm.db2.jdbc.app.DB2Driver"
  url="jdbc:db2://localhost:5000/数据库名"
sybase
  driver="com.sybase.jdbc.SybDriver"
  url="jdbc:sybase:Tds:localhost:5007/数据库名"
```

##### 创建JavaBean对象

在pojo包下创建JavaBean对象 Item

```java
public class Item {
    public Integer ID;
    public String name;
    public Item(){}
    public Item(Integer id, String name){
        this.ID = id;
        this.name = name;
    }
}
```

同一个目录下创建 ItemMapper.xml 配置 sql 语句

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="test.testmybatis.pojo.Item">
    <select id="getAllItem" resultType="test.testmybatis.pojo.Item"> // 类别全称
    select * from items where id = #{id}
  </select>
</mapper>
```

##### 使用Mybatis

```java
InputStream inputStream = Resources.getResourceAsStream(resource);
SqlSessionFactory sqlSessionFactory = 
    new SqlSessionFactoryBuilder().build(inputStream);
SqlSession session = sqlSessionFactory.openSession();
Item itemList = session.selectOne("getAllItem",1);
```

### Spring 配置

##### 导入jar包

导入所有spring 相关jar包，并在config目录加 log4j.properties 文件

```properties
# Configure logging for testing: optionally with log file
#log4j.rootLogger=WARN,?stdout, Console

# 不能有空格!!!
log4j.rootLogger=WARN,logfile,Console

log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=?%d?%p?[%c]?-?%m%n


log4j.appender.logfile=org.apache.log4j.FileAppender
log4j.appender.logfile.File=target/spring.log
log4j.appender.logfile.layout=org.apache.log4j.PatternLayout
log4j.appender.logfile.layout.ConversionPattern=?%d?%p?[%c]?-?%m%n

log4j.appender.Console= org.apache.log4j.DailyRollingFileAppender 
log4j.appender.Console.File = /home/htmlfile/logs/ms.log 
log4j.appender.Console.Append = true 
log4j.appender.Console.DatePattern = '.'yyyy-MM-dd 
log4j.appender.Console.layout = org.apache.log4j.PatternLayout 
log4j.appender.Console.layout.ConversionPattern = %d %-5p - [%l] - %m%n
```

##### 配置applicationContext.xml

在config目录下创建 applicaitonContex.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">
// 创建java bean
    <bean id="beanItem" class="test.testmybatis.pojo.Item">
        <property name="ID" value="2" />
        <property name="name" value="hello world"/>
    </bean>

</beans>
```

##### 创建Bean 对象

注意要有 get;set; 方法

```java
package test.testmybatis.pojo;

public class Item {
    public Integer ID;
    public String name;

    public Item(){}

    public Item(Integer id, String name){
        this.ID = id;
        this.name = name;
    }

    public void toPrint(){
        System.out.println(this.ID.toString()+","+this.name);
    }


    public void setName(String name) {
        this.name = name;
    }

    public void setID(Integer id) {
        this.ID = id;
    }
}
```



### Intellij Idea 项目管理

##### 手动添加jar包

file -> project structure -> modules -> dependencies -> jar +

![image-20191117121044965](C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20191117121044965.png)

![image-20191117121053102](C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20191117121053102.png)



### SSM框架整合

##### 项目结构

 <img src="https://img-blog.csdn.net/20160717142542722?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center" alt="img" style="zoom:67%;" /> 



### 问题解决

##### 1. 下载spring jar失败

maven 配置的文件或仓库地址出错，setting.xml 或者 repo 地址

我使用了本地的maven 地址



### 参考资料

##### Intellij idea 项目部署和web 部署

原地址（ https://www.cnblogs.com/deng-cc/p/6416332.html ）

 <img src="https://images2018.cnblogs.com/blog/1007017/201806/1007017-20180608112951825-523459303.png" alt="img" style="zoom: 50%;" /> 

 <img src="https://images2018.cnblogs.com/blog/1007017/201806/1007017-20180608112952354-353366734.png" alt="img" style="zoom:67%;" /> 

 <img src="https://images2018.cnblogs.com/blog/1007017/201806/1007017-20180608112953353-1760596858.png" alt="img" style="zoom:67%;" /> 

 <img src="https://images2018.cnblogs.com/blog/1007017/201806/1007017-20180608112954536-1174911571.png" alt="img" style="zoom:50%;" /> 

 <img src="https://images2018.cnblogs.com/blog/1007017/201806/1007017-20180608112955842-1288884758.png" alt="img" style="zoom:50%;" /> 

 <img src="https://images2018.cnblogs.com/blog/1007017/201806/1007017-20180608112957001-279554549.png" alt="img" style="zoom:67%;" /> 

 <img src="https://images2018.cnblogs.com/blog/1007017/201806/1007017-20180608112957637-1700253389.png" alt="img" style="zoom:33%;" /> 

 <img src="https://images2018.cnblogs.com/blog/1007017/201806/1007017-20180608112959258-23352219.png" alt="img" style="zoom:33%;" /> 

 <img src="https://images2018.cnblogs.com/blog/1007017/201806/1007017-20180608113001088-1619262130.png" alt="img" style="zoom:33%;" /> 

