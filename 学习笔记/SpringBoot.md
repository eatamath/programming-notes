# SpringBoot 开发笔记

## 环境搭建

spring initializer -> web [web]

删除.mvn、mvnw、mvnw.cmd文件

随后在IDE中右键项目 maven -》update project 

## Maven

## 生命周期

Maven 有以下三个标准的生命周期：

- **clean**：项目清理的处理
- **default**(或 **build**)：项目部署的处理
- **site**：项目站点文档创建的处理

### clean

**clean**的主要目的是清空项目工作中产生的一些中间件，比如上次打的jar包，临时文件等。该生命周期主要用于在build生命周期之前做清理工作。
 **clean**生命周期包含三个阶段：

| 阶段           | 处理   | 描述                                  |
| -------------- | ------ | ------------------------------------- |
| **pre-clean**  | 预清理 | 执行一些需要在clean之前完成的工作     |
| **clean**      | 清理   | 移除所有上一次构建生成的文件          |
| **post-clean** | 后清理 | 执行一些需要在clean之后立刻完成的工作 |

**在一个生命周期中，运行某个阶段的时候，它之前的所有阶段都会被运行**，因此`maven clean`命令会执行`pre-clean`和`clean`阶段，而`mvn post-clean`命令会执行clean生命周期的三个阶段：`pre-clean, clean, post-clean`。

### default (build)

build(构建)声明周期是maven的主要生命周期，主要用于构建应用。包括23个阶段，下面介绍常用的7种：

| 阶段         | 处理     | 描述                                                         |
| ------------ | -------- | ------------------------------------------------------------ |
| **validate** | 验证项目 | 验证项目是否正确且所有必须信息是可用的                       |
| **compile**  | 执行编译 | 源代码编译在此阶段完成                                       |
| **test**     | 测试     | 使用适当的单元测试框架运行测试。                             |
| **package**  | 打包     | 将编译后的代码打包成需要的格式，比如JAR                      |
| **verify**   | 检查     | 对集成测试的结果进行检查，以保证质量达标                     |
| **install**  | 安装     | 安装打包的项目到本地仓库，以供其他项目使用                   |
| **deploy**   | 部署     | 将在最终的build环境上面完成，拷贝最终的工程包到远程仓库中， 以共享给其他开发人员和工程 |

### site

Maven Site 插件一般用来创建新的报告文档、部署站点等。

| 阶段            | 处理                                                       |
| --------------- | ---------------------------------------------------------- |
| **pre-site**    | 执行一些需要在生成站点文档之前完成的工作                   |
| **site**        | 生成项目的站点文档                                         |
| **post-site**   | 执行一些需要在生成站点文档之后完成的工作，并且为部署做准备 |
| **site-deploy** | 将生成的站点文档部署到特定的服务器上                       |

经常用到的是**site**阶段和**site-deploy**阶段，用以生成和发布Maven站点。

## 框架原理

![img](https://img-blog.csdn.net/2018101916383312?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2tpbmdtYXg1NDIxMjAwOA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)



## 注意事项

1. 返回html页面需要加载模板引擎
2. 安装plugin需要maven更新项目

