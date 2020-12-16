# MySQL notes

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



`docker run --name [container_name] -p 32xxx:3306 -e MYSQL_ROOT_PASSWORD=eyisheng -d mysql`

