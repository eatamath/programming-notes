# Business Intelligence

数据集成后，做商业决策（分析）

采集 -> 集成 -> 建模 -> 分析决策(Data Analysis) -> presentation -> 进一步落仓，进一步分析

// terms in ppt

技术应该以 商业/产品/需求 为导向

系统达成的目标应该与商业业务需求相一致

short term/ long term decision making

various analysis methods

不同统计方法的发展催生了更多可实现业务（智能化业务）

算法是否满足业务的要求（性能、准确性）与契合场景（领域可解释性，应用部分规则）

系统 = 后台+统计+性能+可视化

**Applications**

系统要动态适应商业需求

- reporting 难点：变化
- dashboard and scorecard 难点：多数据源融合
- OLAP 

**课程重点**

性能+可视化是重点

性能：如何结合性能实现业务和分析方法

数据处理：根据业务需求找到可用数据，分析方法，结合业务领域伸缩调整

数据可视化：结论以不同方式呈现给不同的用户

> **BA=金融/会计+计算机+统计学**
>
> 而BA特点性的课程基本着重在Data上面，所谓大数据的部分，而MFE看到很少会有大量数据课程。
>
> A. Big-Data Analytics Techniques
>
> B. Consumer Data analytics 
>
> C. Financial & Risk analytics
>
> D. Healthcare Analytics 
>
> E. Statistical Modelling



## 资料

- 之前买的网课好像挺相似的
- 书籍
  - 商业数据分析
  - 商务智能与分析：决策支持系统
  - 决策分析基础

> BI方面的书籍，还是国外的最为经典。
> 与按行业的岗位划分类似，书籍亦会分为很多的类别，譬如技术类、理论类、项目管理类，还有具体一些领域的书譬如主数据、元数据、数据质量（这方面的确实有几本），遗憾的是多为英文著作。
> 理论方面的，BI理论，有两个极其重要的任务，一个是ralph kimball，一个是bill inmon，两位算是泰斗了，我们常说的先建数据集市还是先建数据仓库，从上往下还是从下往上实现数据仓库系统，以及ODS区域的功能等，都是这两位提出的，有意思的是，他们的理念是有相当大差异的，在国内的实践中，拥护各自的都有的，也有混合的，看需要把。
> ralph kimball有一系列的书，称之为toolkit系列，工具箱，譬如维度建模工具箱、ETL工具箱、数据仓库生命周期工具箱等等，最后一本也结合到了项目管理的。有中文版的，翻译欠佳，可读原本，有E文电子版。他的官网上还有很多成为KDT的笔记类的经验，也可以去读读。
> bill inmon有一本数据仓库，好像中文版到第四版了，比较基础，另外他也有些关于DW2.0等架构方面的阐述，初学者估计一时半会理解不上来。
> 再就是工具书了，工具书当然是跟工具结合的，有COGNOS方面的，有微软方面的，以及其他一些的。微软的更可以细分到具体工具如SSIS、SSAS、SSRS等等，还有一些是专门说一些技术方面的，譬如MDX，也曾有过专门的书的。其实我觉得如果要了解这方面，产品自带的哪些文档可以先看看，尤其是微软体系，文档讲解是极其好的。
> 另外就是一些比较偏门的书了，譬如之前提到的数据质量管理方面，这些领域建设目前也只在国内部分行业里有涉及。

## 想法

- 用什么工具进行大数据分析
- 简单的模型性能比较好，是否主要以线性模型为主？根据数据量来决定，尝试多种算法
- 是否需要领域知识

## 工具

- 数据可视化
  - 大屏
    - 帆软
  - echart
  - animated treemap

echarts + tableau

[message queue -> ] Kylin+flink -> [spark ->] hive

[一种流式计算处理方式](https://www.cnblogs.com/ChouYarn/p/11328900.html)

[一个简单的实时计算方案](https://blog.csdn.net/sxiaobei/article/details/80788378)

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200323152541012.png" alt="image-20200323152541012" style="zoom:67%;" />

## 数据可视化

- 刷新频率问题：
  - 不能等待所有数据来之后才刷新
  - 一种解决方案：新来的数据进行局部刷新，其他保持原来数值
- 数据缓存问题
- 图表的比例问题
  - 比例悬殊，长尾效应
  - 最大值的静态动态问题：不同的场景解决方法不同，取决于呈现用户的信息
- 加载性能问题
  - 例如：数据地图 google earth
  - 分布加载
- 数据渲染问题
  - 不同平台解决方案不同：硬件设施
  - 刷新的优化
- 搜索频率与cache
  - client
  - server 高频搜索item cache

掌握可视化工具（1-2种）

从业务角度出发 设计交互过程（client server）与可视化方案

高维数据的可视化

数据可视化是辅助分析工具

数据可视化给用户展示的结论是什么？用户能否从图表中学习到？

根据业务需求选择可视化工具、方法、图形

### 可视化工具

- Tableu
- PowerBI
- Echart
- d3 js

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200316135407966.png" alt="image-20200316135407966" style="zoom:50%;" />

地图工具

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200316135638634.png" alt="image-20200316135638634" style="zoom:50%;" />

时间线工具

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200316135918016.png" alt="image-20200316135918016" style="zoom:50%;" />

数据分析

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200316140010823.png" alt="image-20200316140010823" style="zoom:50%;" />

数据可视化案例

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200316140115052.png" alt="image-20200316140115052" style="zoom:50%;" />

## 商务智能平台

### 系统性能问题

数据库多媒体大文件分离，冗余存储

读写瓶颈问题 -- 需要架构优化

慢SQL查询导致数据库卡死

按照业务》技术对功能层块进行梳理

业务API + 平台服务（包括公共基础服务）

- 负载均衡
- 路由调度
- 模块化拆分
- 服务化组合
- 资源分层治理

【其他细节问题见PPT】



### 框架

数据可以来自第三方平台

- <u>需求</u>（投入产出比）
- <u>用户</u>
- 平台
- 技术
- 项目实施
- <u>投入产出</u>

数据是否能满足需求？

伪需求？低频需求？低价值需求？

### 实践

[用户画像](https://www.zhihu.com/question/19853605)

- 不同用户群体的需求差异

[竞品分析](https://www.zhihu.com/question/20086049)



从竞品分析开始，根据idea寻找数据需求，和技术限制（设备要求）

投入/产出分析

- 人
- 设备
- 环境
- 用户数量
- 定价

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200426135435325.png" alt="image-20200426135435325" style="zoom:50%;" />![image-20200426135605804](C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200426135605804.png)

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200426135435325.png" alt="image-20200426135435325" style="zoom:50%;" />![image-20200426135605804](C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200426135605804.png)

## 数据挖掘

### 文本分析

分析流程

- representation
- modeling

#### representation

- 词袋模型(tf-idf)
- encoding
- embeding

#### modeling

BERT通用语义模型

轻量化模型 模型蒸馏

#### 命名实体识别

实体对齐（相似度计算）

#### 事件抽取

文本 -> bert embedding -> dense layer -> classification results

#### 涉事主题识别

实体+事件 -> bert embedding -> dense layer -> classification results

### 算法工程部分

新闻文本 -[kafka]-> spark streaming -[elasticsearch]->结果入库

![image-20200525142754736](C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200525142754736.png)

![image-20200525142844515](C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200525142844515.png)

## 数据化运营阅读笔记

### 问题分析

#### 逻辑树

拆解问题

### 数据分析应用场景



### 业务

#### AB测试

对照实验 网页优化



## 项目工具

#### 图计算引擎

- sparkX
- pandagraph
- tux2
- plato
- PowerGraph

[图计算系统发展简史](https://zhuanlan.zhihu.com/p/80455017)

[OLAP比较常见的框架比较](https://www.zhihu.com/question/41541395/answer/130713893)

graphlab software license

Registered email address: **1652658@tongji.edu.cn**
Product key: **507A-09FB-C1E1-0379-057F-E1AB-5C76-D388**

[kylin](https://zhuanlan.zhihu.com/p/57055086)

geabase



![image-20200608135904704](C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200608135904704.png)