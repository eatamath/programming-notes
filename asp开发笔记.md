



[C#的dapper使用](https://www.jianshu.com/p/c4ca2989d26a)

[mvc官方教程](https://docs.microsoft.com/zh-cn/aspnet/core/mvc/controllers/actions?view=aspnetcore-2.2)

[大概知识可以速成](https://www.cnblogs.com/powertoolsteam/p/MVC_four.html)

[Identity-用户登录、最简单的登录验证](https://blog.csdn.net/qq_25991955/article/details/100200599)

[分模块 Assemblies](https://zhuanlan.zhihu.com/p/26647289)

[.Net Core2.2 + EF Core + DI，三层框架项目搭建教程](https://www.cnblogs.com/han1982/p/11058788.html)

[Identity配置](https://www.twle.cn/l/yufei/aspnetcore/dotnet-aspnet-identity-migrations.html)

### Controller

[bind]

[frombody]

```
$.ajax({
        url: "@Url.Action("ExportJson")",
        type: "POST",
 //************************************
        data: {"json" : JSON.stringify(myObj)},
 //************************************
        contentType:"application/json",
        success: function (result) {

        }
    });
```

FormsAuthentication

### Model Layer

添加验证 attributes

[ValidateAntiForgeryToken]

dbcontext 的使用，dbservice配置

[column]

public async Task<IActionResult> Delete(int? id)





### View

@model IEnumerable<MvcMovie.Models.Movie>

@inject







### CLI

```cmd
dotnet new sln --name Template

cd Domain
dotnet add reference ../Data
cd ../
dotnet add reference ../Data


#### 数据库迁移
dotnet tool install --global dotnet-ef
dotnet add package Microsoft.EntityFrameworkCore.Design
dotnet ef migrations add InitialCreate
dotnet ef database update
```







### model

- customer type
- customer
- sales
- sales type



customer

- customer type

sales order

- branch
- customer
- sales type

shipment

- sales order

invoice

- invoice type
- shipement

payment receive

- invoice

vendor

- vendor type

purchase order

- branch
- vendor
- purchase type

goods receive note

- purchase order
- warehouse
- vendor delivery order
- vendor invoice

bill

- goods receive note
- vendor delivery order
- vendor invoice
- bill type

payment vaucher

- bill
- payment type
- payment source

product

- 

![image-20200625170105306](C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200625170105306.png)



![image-20200625170927599](C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200625170927599.png)

delete

- payment voucher
- 

 **Remove-Migration**

 **Add-Migration** 

**Update-Database**



gacutil /i D:\onedrive\eyisheng\OneDrive\code\eshop-1\eshop\eshop\StdAggService\bin\Debug\StdAggService.dll
regasm D:\onedrive\eyisheng\OneDrive\code\eshop-1\eshop\eshop\StdAggService\bin\Debug\StdAggService.dll

[C++调用C#类库](https://blog.csdn.net/liulv_yan/article/details/84105670)

[C++ 调用C#代码](https://blog.csdn.net/msapdev/article/details/5642419)

[COM [C++如何调用C#开发的dll](https://www.cnblogs.com/huangmianwu/p/6145044.html)]

错误

[C2338](https://blog.csdn.net/norsd/article/details/99983347)



### c++

[win32](https://www.cnblogs.com/xuejianxiyang/p/12801453.html)



CLR1 --- win322







![image-20200627095629630](C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200627095629630.png)

![image-20200627095646336](C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200627095646336.png)

![image-20200627095732166](C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200627095732166.png)