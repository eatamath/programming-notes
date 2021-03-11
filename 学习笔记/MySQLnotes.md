# MySQL notes

## 数据库管理

### 登陆

` mysql -u root -p `

`show databases;`

`use [db_name]`



### Grant 权限

`grant all privileges on [db_name.*] to [user_name@]'%' (with grant option)`

` docker exec -it [container-name] bash `

### 参考资料

[MySQL常用命令]( https://www.cnblogs.com/bluealine/p/7832219.html )

[常用权限管理命令]( https://www.jianshu.com/p/fd1cb8657702 )



## DML

### 表的管理

```mysql
create table `table_name`(
    `col1` int NOT NULL AUTO_INCREMENT,
    `col2` VARCHAR(20),
    `col3` DATETIME NOT NULL,
    PRIMARY KEY (`col1`,`col3`)
) ENGINE=InnoDB CHARSET=utf8;
```

```mysql
DROP TABLE table_name;
```

```mysql
INSERT INTO table_name (`col1`,`col2`,`col3`) VALUES (value1, value2, value3);
```

### 基本查询

通用语法

```mysql
SELECT column_name,column_name
FROM table_name
[WHERE Clause]
[LIMIT N][ OFFSET M]

SELECT field1, field2,...fieldN FROM table_name1, table_name2...
[WHERE condition1 [AND [OR]] condition2.....
```

null的处理

```mysql
select ifnull(col2,default_val) from table_name;
```

### 更新

通用语法

```mysql
UPDATE table_name SET field1=new-value1, field2=new-value2
[WHERE condition]
```

### 删除

通用语法

```mysql
DELETE FROM table_name [WHERE condition]
```

### 字符串匹配

在 where like 的条件查询中，SQL 提供了四种匹配方式。

1. **%**：表示任意 0 个或多个字符。可匹配任意类型和长度的字符，有些情况下若是中文，请使用两个百分号（%%）表示。
2. **_**：表示任意单个字符。匹配单个任意字符，它常用来限制表达式的字符长度语句。
3. **[]**：表示括号内所列字符中的一个（类似正则表达式）。指定一个字符、字符串或范围，要求所匹配对象为它们中的任一个。
4. **[^]** ：表示不在括号所列之内的单个字符。其取值和 [] 相同，但它要求所匹配对象为指定字符以外的任一个字符。
5. 查询内容包含通配符时,由于通配符的缘故，导致我们查询特殊字符 “%”、“_”、“[” 的语句无法正常实现，而把特殊字符用 “[ ]” 括起便可正常查询。

正则匹配通用语法

```mysql
SELECT field1 FROM table_name WHERE field1 REGEXP 'reg';
```

### UNION

通用语法

```mysql
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions]
UNION [ALL | DISTINCT] # union 不可重复; union all 可重复
SELECT expression1, expression2, ... expression_n
FROM tables
[WHERE conditions];
```

### 排序

通用语法

```mysql
SELECT field1, field2,...fieldN FROM table_name1, table_name2...
ORDER BY field1 [ASC [DESC][默认 ASC]], [field2...] [ASC [DESC][默认 ASC]]
```

### 分组

通用语法

```mysql
SELECT column_name, function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
WITH ROLLUP;
```

### JOIN ON

通用语法

```mysql
SELECT *
FROM table_a a 
[JOIN | NATURAL JOIN | LEFT JOIN | RIGHT JOIN | INNER JOIN | OUTER JOIN] # keep which side
table_b b
ON 
[a.field1=b.field1];
```

### TRANSACTION

- **原子性：**一个事务（transaction）中的所有操作，要么全部完成，要么全部不完成，不会结束在中间某个环节。事务在执行过程中发生错误，会被回滚（Rollback）到事务开始前的状态，就像这个事务从来没有执行过一样。
- **一致性：**在事务开始之前和事务结束以后，数据库的完整性没有被破坏。这表示写入的资料必须完全符合所有的预设规则，这包含资料的精确度、串联性以及后续数据库可以自发性地完成预定的工作。
- **隔离性：**数据库允许多个并发事务同时对其数据进行读写和修改的能力，隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致。事务隔离分为不同级别，包括读未提交（Read uncommitted）、读提交（read committed）、可重复读（repeatable read）和串行化（Serializable）。
- **持久性：**事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失。

事务控制

- SAVEPOINT identifier，SAVEPOINT 允许在事务中创建一个保存点，一个事务中可以有多个 SAVEPOINT；
- RELEASE SAVEPOINT identifier 删除一个事务的保存点，当没有指定的保存点时，执行该语句会抛出一个异常；
- ROLLBACK TO identifier 把事务回滚到标记点；
- SET TRANSACTION 用来设置事务的隔离级别。InnoDB 存储引擎提供事务的隔离级别有READ UNCOMMITTED、READ COMMITTED、REPEATABLE READ 和 SERIALIZABLE。

### ALTER

通用语法

```mysql
ALTER TABLE table_name DROP field1;
ALTER TABLE table_name ADD field2 [TYPE];
ALTER TABLE table_name MODIFY col new_col [NEW TYPE];
ALTER TABLE table_name ALTER col SET DEFAULT [NEW VALUE];
```





## docker

`docker run --name [container_name] -p 32xxx:3306 -e MYSQL_ROOT_PASSWORD=eyisheng -d mysql`

