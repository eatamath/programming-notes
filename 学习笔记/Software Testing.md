# Software Testing

### 软件工程前置知识

概要设计

High level design

- 数据建模（数据库设计）
- 行为建模（类的行为，Sequence Diagram）
- 功能建模（系统架构设计）



## Fundamentals of Testing

基本概念

error

defect / fault / bug 

failure / problem / issue / incident

debugging

**testing**

The whole process of systematically executing programs to demonstrate the correct implementation of the requirements, to increase confidence, and to detect failures is called testing.

**test cases**

A test case contains defined test conditions.

test object

test condition

test scenario

**test suite**

includes execution of one or more ➞test cases.

**Test objective or test type**
A test is named according to its purpose (for example, ➞load test).
**Test technique**
A test is named according to the technique used for specifying or executing the test
(for example, ➞business-process-based test).
**Test object**
The name of a test reflects the kind of the test object to be tested (for example, a GUItest or DB test [database test]).
**Test level**
A test is named after the level of the underlying life cycle model (for example, ➞system test).
**Test person**
A test is named after the personnel group executing the tests (for example, developer
test, ➞user acceptance test).
**Test extent**
A test is named after the level of extent (for example, partial ➞regression test, full test).

### software quality

➞functionality, ➞reliability, usability, ➞efficiency, ➞maintainability,
and portability.

Testing must consider all these factors, also called ➞quality characteristics
and ➞quality attributes

Testing should continue as long as costs of finding and correcting a defect are lower than the costs of failure

There exist many different methods and techniques for testing software.
Every technique especially focuses on and checks particular aspects of the test object

a combination of different test techniques is always necessary to detect failures with different causes

The product should provide only the required functionality.

### the fundamental test process

generic testing task

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200311115538560.png" alt="image-20200311115538560" style="zoom:50%;" />

#### Test Planing and Control

Planning of the test process starts at the beginning of the software
development project.

resource planing

determination of the test strategy (risk evaluation)

Define test intensity for subsystems and different aspects

> The intensity of testing depends very much on the test techniques that are used and the test coverage that must be achieved.

Prioritization of the tests

> The prioritization of tests guarantees that the critical software parts are
> tested first in case time constraints do not allow executing all the planned
> tests

Tool support

#### Test Analysis and Design

review the test basis

> The first task is to review the test basis, i.e., the specification of what
> should be tested. The specification should be concrete and clear enough to
> develop test cases

check testability

> As with analyzing the basis for a test, the test object itself also has to
> fulfill certain requirements to be simple to test. Testability has to be
> checked. This process includes checking the ease with which interfaces
> can be addressed (interface openness) and the ease with which the test
> object can be separated into smaller, more easily testable units.

consider the risk

traceability is important

> It is important to ensure ➞traceability between the specifications to
> be tested and the tests themselves. It must be clear which test cases test
> which requirements and vice versa.

logical and concrete test cases

> It is important to ensure ➞traceability between the specifications to
> be tested and the tests themselves. It must be clear which test cases test
> which requirements and vice versa.

## 课程项目

作业文档

开发test driver

测试用例在脚本

数据在文件

缺陷统计数据



## 项目测试

### 测试工具

#### java测试

##### JUnit测试用例

简单介绍

一个测试类中只能声明此注解一次，此注解对应的方法只能被执行一次
@BeforeClass 使用此注解的方法在测试类被调用之前执行
@AfterClass 使用此注解的方法在测试类被调用结束退出之前执行
一个类中有多少个@Test注解方法，以下对应注解方法就被调用多少次
@Before 在每个@Test调用之前执行
@After 在每个@Test调用之后执行
@Test 使用此注解的方法为一个单元测试用例，一个测试类中可多次声明，每个注解为@Test只执行一次
@Ignore 暂不执行的测试用例，会被JUnit4忽略执行

参考资料

1. [如何在intellij中使用JUnit编写测试用例](https://blog.csdn.net/weixin_44425934/article/details/99858528)

学习资料

1. 测试教程

### The General V-Model

The main idea behind the general V-model is that development and testing tasks are corresponding activities of equal importance.

[The test level called component test is not only characterized by the kind of test objects and the testing environment, the tester also pursues test objectives that are specific for this phase]

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200513100712626.png" alt="image-20200513100712626" style="zoom:50%;" />

**测试过程**

■ Component test
(see section 3.2) verifies whether each software ➞component correctly
fulfills its specification.
■ ➞Integration test
(see section 3.3) checks if groups of components interact in the way
that is specified by the technical system design.
■ System test
(see section 3.4) verifies whether the system as a whole meets the specified
requirements.
■ ➞Acceptance test
(see section 3.5) checks if the system meets the customer requirements,
as specified in the contract and/or if the system meets user needs and
expectations.

**verification & validation**

Verification activities examine whether specifications are correctly [Is the system correctly built?]
implemented and whether the product meets its specification, but not whether the resulting product is suitable for its intended use.

When validating, the tester judges whether a (partial) product really solves the specified task and whether it is fit or suitable for its intended use.

Verification shall assure that the outcome of a particular development level has been achieved correctly and completely, according to its specification.

In practice, every test contains both aspects.

（2）“验证(Verification)”的涵义
通过提供客观证据对规定要求已得到满足的认定。
（2）“确认（Validation）”的涵义
通过提供客观证据对特定的预期用途或应用要求已得到满足的认定。
（3）“验证”和“确认”之差别
“验证”和“确认”都是认定。可是，“验证”表明的是满足规定要求，而“确认”表明的是满足预期用途或应用要求，说简单点，“确认”就是检查终于产品是否达到顾客使用要求。

### Component Testing

#### test objects

Typical test objects are program modules/units or classes, (database) scripts, and other software components

Test objects may even be configuration data and database components.

测试的时候和别的组件独立

#### test environment

A test driver is a program that calls the component under test and then receives the test object’s reaction.

The main characteristic of component testing is that the software components are tested individually and isolated from all other software components of the system

debugging vs. testing

Debugging is finding the cause of failures and removing them, while testing is the systematic approach for finding failures.

Use of component testing frameworks (see [URL: xunit]) reduces the effort involved in programming test drivers and helps to standardize a project's component testing architecture.

examples of Junit for Java as well as nUnit and CppUnit for C++

#### test objectives

**Testing the functionality**

The most important task of component testing is to check that the entire functionality of the test object works correctly and completely as required by its specification (see ➞functional testing). Here, <u>functionality</u> means the input/output behavior of the test object. To check the correctness
and completeness of the implementation, the component is tested with a series of test cases, where each test case covers a particular input/output combination (partial functionality).

A component may then possibly be called or used in a wrong way

As we explained earlier, component testing is very closely related to development. The tester usually has access to the source code, which makes component testing the domain of white box testing (see section 5.2).

**Testing robustness**

和functional testing一样，但是关注遗漏的功能

- at least as many reasonable negative tests as positive ones
- test driver must be extended in order to be able to evaluate the test object’s
  exception handling
- test object’s exception handling (the analysis of ERR_CODE in the previous
  example) requires additional functionality

**testing efficiency**

various aspects such as use of memory, computing time, disk or network access time, and the time required to execute the component’s functions and algorithms

**testing maintainability**

how easy or how difficult it is to change the program or to continue developing it

一般用静态测试

#### test strategy

**white-box testing**

As we explained earlier, component testing is very closely related to development. The tester usually has access to the source code, which makes component testing the domain of white box testing

**black-box testing**

In reality, however, component testing is often done as a pure black box testing, which means that the code structure is not used to design test cases

On the one hand, real software systems consist of <u>countless elementary components</u>; therefore, code analysis for designing test cases is probably only feasible with very few selected components.

Often, the tester only recognizes these <u>larger units</u> as units that can be tested, even in component testing. Then again, these <u>units are already too large</u> to make observations and interventions on the code level with reasonable effort

“Test first” development



### Integration Testing

#### test objects

**integration**

Developers, testers, or special integration teams then <u>compose groups of these components to form larger structural units and subsystems</u>. This connecting of components is called integration

**integration testing**

Then the structural units and subsystems must be tested to make sure <u>all components collaborate correctly</u>. Thus, the goal of the integration test is to <u>expose faults in the interfaces and in the interaction</u> between integrated components

测试依据

The test basis may be the software and system design or system architecture, or workflows through several interfaces and use cases

When interfaces to external software systems are examined, we sometimes speak of ➞system integration testing, higher-level integration testing, or <u>integration testing in the large</u>

integration of components is then <u>integration test in the small</u>, sometimes called ➞component integration testing

不同的testing level

Component integration tests will test the interfaces between internal components or between internal subsystems.

System integration tests focus on testing interfaces between different systems and between
hardware and software.

**test objects**

Step-by-step, during integration, the different components are combined to form larger units (see section 3.3.5). Ideally, there should be an integration test after each of these steps. Each subsystem may then be the basis for integrating further larger units. Such units (subsystems) may be <u>test objects for the integration test later</u>.

External systems or acquired components

- commercial off-the-shelf (COTS) software products
  - In the integration test, however, these system components must be taken into account and their collaboration with other components must be examined.

The most important test objects of integration testing are internal interfaces between components.

#### test environments

As with component testing, <u>test drivers</u> are needed in the integration test. They send test data to the test objects, and they receive and log the results.

test driver可以重用上一个阶段的component test driver

**Monitors are necessary**

During integration testing, additional tools, called monitors, are required. ➞Monitors are programs that read and log data traffic between components.

#### test objectives

to reveal inter- Wrong interface formats face problems as well as conflicts between integrated parts

测试组件的接口部分可以用动态测试

faults in the data exchange or in the communication between the components

例子

- A component transmits syntactically incorrect or no data
- functional fault of a component, contradicting or misinterpreted specifications
- Data is transmitted correctly but at the wrong time

直接跳过 component test 进行 integration test 是可行的，但是存在弊端

非功能测试

Nonfunctional tests may also be executed during integration testing, if attributes mentioned below are important or are considered at risk.

#### integration strategy

效率

Efficiency is the relation between the cost of testing (the cost of test personnel and tools, etc.) and the benefit of testing (number and severity of the problems found) in a certain test level.

The test manager has to decide this and choose and implement an <u>optimal integration strategy</u> for the project.

一个ad hoc解决方案：一个组件准备好了就进行系统的 integration testing

制定最优方案时 Constraints for integration

- The <u>system architecture</u> determines how many and which components the entire system consists of and in which way they depend on each other.
- The <u>project plan</u> determines at what time during the course of the project the parts of the system are developed and when they should be ready for testing. The test manager should  be consulted when determining the order of implementation.
- The <u>test plan</u> determines which aspects of the system shall be tested, how intensely, and on which test level this has to happen.

> Because the integration strategy depends on delivery dates, the test manager should consult the project manager during project planning. The order of component implementation should be suitable for integration testing.

**常见策略**

- Top-down integration
  - The test starts with the top-level component of the system that calls other components but is not called itself
- Bottom-up integration
  - simulate higher-level components
- Ad hoc integration
  - The components are being integrated in the (casual) order in which they are finished.
- Backbone integration
  - A skeleton or backbone is built and components are gradually integrated into it

<u>Top-down and Bottom-up integration</u> in their pure form can be applied only to program systems that are structured in a <u>strictly hierarchical way</u>;

Any nonincremental integration—also called <u>big bang integration</u> should be <u>avoided</u>. Big bang integration means waiting until all software elements are developed and then throwing everything together in one step.



### System Testing

#### 概述

After the integration test is completed, the third and next test level is the system test. System testing checks if the integrated product meets the specified requirements. Why is this still necessary after executing component and integration tests?

系统是否满足需求

- 底层的测试注重技术测试
- 只有集成之后的系统才能测试功能

The test basis includes all documents or information describing the test object on a system level. This may be system requirements, specifications, risk analyses if present, user manuals, etc.

#### Test Objects and Test Environment

测试环境和产品环境尽可能相似

The system test not only tests the system itself, it <u>also checks system and user documentation</u>, like system manuals, user manuals, training material, and so on.

配置测试

数据质量测试

测试和生产环境分离

#### Test Objectives

测试主要面向

- 功能需求
- 非功能需求
- 遗漏的需求

主要问题

- 需求不清，具体行为不清
- 每个人的理解不同

### Acceptance Test

在执行和使用产品前要进行AT

客户参与

测试情形

- A commercial-off-the-shelf product (COTS) can be checked for acceptance during its integration or installation.
- Usability of a component can be acceptance tested during its component test.
- Acceptance of new functionality can be checked on prototypes before system testing.

根据风险判断投入的测试程度

The test basis for acceptance testing can be any document describing the system from the user or customer viewpoint, such as, for example, user or system requirements, use cases, business processes, risk analyses, user process descriptions, forms, reports, and laws and regulations as
well as descriptions of maintenance and system administration rules and processes.

#### Contract Acceptance Testing

whether the software system is free of (major) deficiencies

whether the service defined by the development contract has been accomplished and is acceptable

接受标准

The test criteria are the acceptance criteria determined in the development contract.

Additionally, conformance to any governmental, legal, or safety regulations must be addressed here.

acceptance testing is run in the customer’s actual operational environment

The same techniques used for test case design in system testing can be used to develop acceptance test cases.

#### Testing for User Acceptance

Such a test is especially recommended if the <u>customer and the user are different</u>.

Different user groups usually have completely different expectations of a new system. Users may reject a system because they find it “<u>awkward</u>” to use, which can have a negative impact on the introduction of the system. This may happen even if the system is completely OK from a functional point of view.

Present prototypes to the users early

#### Operational (Acceptance) Testing

Operational (acceptance) testing assures the acceptance of the system by the system administrators. It may include testing of backup/restore cycles (including restoration of copied data), disaster recovery, user management, and checks of security vulnerabilities.

#### Field Testing

the software producer may choose to execute a field test after the system test.

The objective of the field test is to identify influences from users’ environments that are not entirely known or specified and to eliminate them if necessary.

Testing done by representative customers

Such testing of preliminary versions by representative customers is also called alpha testing or beta testing.

Alpha tests are carried out at the producer’s location, while beta tests are carried out at the customer’s site.

### Generic Types of Testing

The following types of testing can be distinguished:

- Functional testing
- Nonfunctional testing
- Testing of software structure
- Testing related to changes

#### Functional Testing

Functional testing includes all kind of tests that verify a system’s input/output behavior.

Functional requirements specify the behavior of the system

#### Non-Functional Testing

they describe the attributes of the functional behavior or the attributes of the system as a whole

具体测试内容在书中

#### Testing of Software Structure

<u>Structural techniques (structure-based testing, white box testing) use information about the test object’s internal code structure or architecture.</u>

Typically, the control flow in a component, the call hierarchy of procedures, or the menu structure is analyzed.

The objective is to design and run enough test cases to completely cover all structural items.

具体内容在4、5章节

#### Testing related to Changes and Regression Testing

A regression test is a new test of a previously tested program following modification to ensure that <u>faults have not been introduced or uncovered</u> as a result of the changes made (uncovering masked defects).

regression testing may be performed at all test levels and applies to functional, nonfunctional, and structural test.

测试用例是可重用的

四个测试情形在书中

在对整个系统进行回归测试的时候，可以进行选择性测试，具体标准在书中

### Static Test

Static investigations like <u>reviews</u> and <u>tool-supported analysis of code and documents</u> can be used very successfully for improving quality.

Tool-supported static analysis is only <u>possible for documents</u> with a formal structure.

测试目标：

The goal of examination is to find <u>defects and deviations</u> from the existing specifications, standards to comply with, or even the project plan.

#### Reviews

Reviews are an efficient means to assure the quality of the examined documents. Ideally, they should be performed as soon as possible after a document is completed to find mistakes and inconsistencies early.

All documents can be subjected to a review or an inspection

peer reviews

测试时间

they should be performed as soon as possible <u>after a document is completed</u> to find mistakes and inconsistencies early. The verifying examinations at the end of a phase in the general V-model normally use reviews (so-called <u>phase exit reviews</u>).





### notes

测试策略

- 黑盒+白盒
- 静态测试
- walk through + review

类的测试

- 根据每个功能的输入输出覆盖测试，对每个方法进行测试
- 根据类的状态转移覆盖测试，和其他类的交互也要考虑





#### 等价类

根据变量划分成多个子集，子集满足等价关系，且并集满足全集

- 弱一般等价类：但缺陷假设，均匀分布
- 强一般等价类：多缺陷假设
- 弱健壮等价类：弱一般等价类的测试用例+每个变量取一个无效值*其余变量取有效值
- 强健壮等价类：

按照输入变量或输出变量划分等价类

分析有效区间数量

#### 动态测试

状态图

- 边覆盖
- 状态覆盖
- 业务流覆盖
- 操作覆盖
- 功能覆盖

构建状态树

测试GUI根据主要的控件构成的测试路径进行测试



### 白盒测试技术

#### 语句覆盖

语句覆盖：我们设计出来的测试用例要保证程序中的每一个语句至少被执行一次

最弱的覆盖，仅仅考虑对代码中的执行语句进行覆盖而没有考虑各种条件和分支

```java
public int foo(int a,int b)

{
return a/b; // b!=0
}
```

#### 判定覆盖

判定覆盖也被成为分支覆盖(Branch Coverage)，也就是说设计的测试用例要保证让被测试程序中的每一个分支都至少执行一次

复合条件无法对每个子条件进行拆分

#### 条件覆盖

条件覆盖于分支覆盖不同，条件覆盖要求所设计的测试用例能使每个判定中的每一个条件都获得可能的取值，即每个条件至少有一次真值、有一次假值。

但条件覆盖也有缺陷，因为它只能保证每个条件都取到了不同结果，但没有考虑到判定结果，因此有时候条件覆盖并不能保证判定覆盖。

#### 判定条件覆盖

判定条件覆盖，说白了就是我们设计的测试用例可以使得判断中每个条件所有的可能取值至少执行一次（条件覆盖），同时每个判断本身所有的结果也要至少执行一次（判定覆盖）。不难发现判定条件覆盖同时满足判定覆盖和条件覆盖，弥补了两者各自的不足，但是判定条件覆盖并未考虑条件的组合情况。

#### 组合覆盖

组合覆盖也叫做条件组合覆盖。意思是说我们设计的测试用例应该使得每个判定中的各个条件的各种可能组合都至少出现一次。显然，满足条件组合覆盖的测试用例一定是满足判定覆盖、条件覆盖和判定条件覆盖的。

Branch Condition Combination Coverage

#### 路径覆盖

路径覆盖，意思是说我们设计的测试用例可以覆盖程序中所有可能的执行路径。这种覆盖方法可以对程序进行彻底的测试用例覆盖，比前面讲的五种方法覆盖度都要高。

#### 圈复杂度

圈复杂度计算公式为：V(G)=e-n+2。其中，e表示控制流图中边的数量，n表示控制流图中节点的数量。
此外圈复杂度的计算还有更直观的方法，因为圈复杂度所反映的是“判定条件”的数量，所以圈复杂度实际上就是等于判定节点的数量再加上1，也即控制流图的区域数，
此外对应与控制流图区域数还有一个圈复杂度计算公式：V(G)=区域数=判定节点数+1。其中判定节点是控制流图中出现的判断条件。

#### 参考资料

[白盒测试技术：语句覆盖、条件覆盖（分支覆盖）、判定覆盖、条件-判定覆盖、组合覆盖、路径覆盖 的区别](https://www.cnblogs.com/jodyccf/p/12200343.html)

### 黑盒测试

#### 边界值测试

基本边界值 单缺陷 4n+1

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200701103746761.png" alt="image-20200701103746761" style="zoom:50%;" />

健壮性边界值 但缺陷 超范围

最坏情况边界分析 多缺陷 笛卡尔积 5^n

健壮最坏情况边界分析 7^n



#### 等价类

弱一般等价类 单缺陷 均匀分布

强一般等价类 多缺陷 

弱健壮

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200701130315598.png" alt="image-20200701130315598" style="zoom:50%;" />

强健壮

<img src="C:\Users\steve\AppData\Roaming\Typora\typora-user-images\image-20200701130327330.png" alt="image-20200701130327330" style="zoom:50%;" />

#### 错误推测法

#### 因果图法

考虑输入之间的关系和组合

#### 决策表法



### 静态测试

### 系统测试