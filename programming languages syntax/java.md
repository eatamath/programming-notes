# Java Notes

## Java Basics

### Operand

#### bit 操作

`>>`保持符号

`>>>`算术右移，补0，不一定保持符号

`&`, `|`, `^`

#### 递增操作

`++i op x`, `op ++i` 先加后 `op`

`i++ op x`, `op i++` 先`op`后加

### Variables

**Instance Variables (Non-Static Fields)** 

**Class Variables (Static Fields)** 

**Local Variables**

**Parameters** 

The important thing to remember is that parameters are always classified as "variables" not "fields".

数字之间可以用undash连接

#### Array

```java
// declares an array of integers
int[] anArray;
```

- The size of the array is not part of its type (which is why the brackets are empty)
-  the declaration does not actually create an array, only tell types
- 多维数组和c的初始化方式不同，（二维情形下）row是可变长度

### Operand

<img src="D:\onedrive\files\notes\img\image-20200921191207470.png" alt="image-20200921191207470" style="zoom:50%;" />

The unsigned right shift operator "`>>>`" shifts a zero into the leftmost position, while the leftmost position after `">>"` depends on sign extension.



### 重点

#### 数值型

直接量是在程序中直接出现的常量值。

将整数类型的直接量赋值给整数类型的变量时，只要直接量没有超出变量的取值范围，即可直接赋值，如果直接量超出了变量的取值范围，则会导致编译错误。

整数类型的直接量默认是 int 类型，如果直接量超出了 int 类型的取值范围，则必须在其后面加上字母 L 或 l，将直接量显性声明为 long 类型，否则会导致编译错误。

**浮点类型的直接量默认是 double 类型**，如果要将直接量表示成 float 类型，则**必须在其后面加上字母 F 或 f**。将 double 类型的直接量赋值给 float 类型的变量是不允许的，会导致编译错误。

#### 类型转换

不同的数字类型对应不同的范围，按照范围从小到大的顺序依次是：byte、short、int、long、float、double。

将小范围类型的变量转换为大范围类型称为拓宽类型，不需要显性声明类型转换。将大范围类型的变量转换为小范围类型称为缩窄类型，必须显性声明类型转换，否则会导致编译错误。

> 将字符类型转换成数字类型时，字符的统一码转换成指定的数值类型，此时需要判断字符的统一码是否超出转换成的数值类型的取值范围。C 选项的字符直接量超出了 short 的取值范围且没有显性声明类型转换，因此会导致编译错误。
>

布尔类型不能转换成其他基本数据类型，其他基本数据类型也不能转换成布尔类型。

byte是一个数字量

#### 方法

方法签名：名字+参数

Java 中只有值传递。值传递的含义是将实参的值传递给形参，当参数类型是基本数据类型时，传递的是实参的值，当参数类型是对象时，传递的是对象的引用，**但是不能让实参引用新的对象**。

使用**方法的重载**时，什么情况下会出现**编译错误**？出现歧义调用的时候会出现编译错误。如果一个方法调用有多个可能的匹配，且编译器无法判断哪个方法最匹配，则称为歧义调用。在编译器选择函数的时候是有**优先级**的,当两个的都可以的时候,一个不需要转换类型的优先级是要比转换成double类型的优先级高,所以不会有歧义,而第二题中两个都是需要将一个int转换成double,优先级相同,所以会造成歧义

## Classes and Objects

### classes basics

```java
class MyClass extends MySuperClass implements YourInterface {
    // field, constructor, and
    // method declarations
    public double calculateAnswer(double wingSpan, int numberOfEngines, double length, double grossTons) {
        // definition: 1. parameters 2. return type 3. exception list
        // signature = calculateAnswer(double, int, double, double)
        // 重载 (overloading) the method's name and the parameter types.
    }
}

/*
	note: interface 和 supperclass 的顺序不能改变
	1. MyClass obj field 能够覆盖掉继承的 obj
	2. MyClass.obj 可以继承自 interface.obj 和 superclass.obj
	3. private fields 和 public method 非常好
	4. 类名大写 & method 动词
*/
```

Variable的类型和术语

> - Member variables in a class—these are called *fields*.
> - Variables in a method or block of code—these are called *local variables*.
> - Variables in method declarations—these are called *parameters*.

argument 和 parameters 应该在 type 和 order 上对应

可变参数

```java
public PrintStream printf(String format, Object... args)
// args: array
```

引用类型参数：函数返回后，指向同一个对象，包括return的对象

内置类型参数：函数返回后，销毁

#### 构造函数

private constructor 导致只能在类内进行创建对象，那么可以用静态方法来进行创建，比如singleton模式

可以使用 this 调用其他的 constructor

#### 继承

默认constructor会调用superclass的non-argument constructor

默认constructor调用自己的 non-argument constructor

class 隐式继承 Object

constructor modifier

#### return type

返回 interface 对象需要 implement

方法实际返回类型可以向下（子类）进行转换

可以按照继承方向override一个method（通过返回类型）

```java
public parent parent.func();
public child child.func();
```

> This technique, called *covariant return type*, means that the return type is allowed to vary in the same direction as the subclass.



#### 垃圾回收

JVM自动回收；周期回收

set obj=null

类似引用指针

#### 访问控制

![image-20201217121627273](D:\onedrive\files\notes\notes\img\image-20201217121627273.png)

#### static成员

field: 类共有，不需要类的实例

instance method -> class obj/ class method

class method -x-> instance obj/ instance method / this

final: value 不变/不能override

constant 改变 需要重新编译使用他的类

#### 初始化

> 1. 尽可能一起初始化
> 2. 非static在constructor/initializer block初始化
> 3. static在static block/static method初始化

### nested class

> 1. 是一种成员
> 2. `private`, `public`, `protected`, or *package private*
> 3. 优点：聚集、封装、可维护
> 4. 序列化synthetic constructs版本问题
> 5. shadowing问题
> 6. 使用的场景见doc

inner class

> 1. 可访问enclosing class member
> 2. 实例关联
> 3. 初始化`OuterClass.InnerClass innerObject = outerObject.new InnerClass();`
> 4. 不能定义static成员

static nested class

> 1. 需要使用enclosing class instance进行操作
> 2. 类关联
> 3. 初始化`OuterClass.StaticNestedClass nestedObject = new OuterClass.StaticNestedClass();`

local class

> 1. 定义在`{block}`中
> 2. 可访问enclosing class member | static local class只能访问static member
> 3. 可访问 final/effectively final 局部变量/参数
> 4. 不能定义static成员，因为可以访问block中的实例 | 不能定义interface | 可以定义 static final 成员

anonymous class

> 1. 为简洁而生，定义+实例化，只需要使用一次local class
> 2. new [name of an interface to implement or a class to extend] (init argument to pass) { members definition }
> 3. 访问限制同local class
> 4. 类内还可以定义local class

lambda expression

> 1. 为了简单的anonymous class而生，构造过程见官方文档，实质上是anonymous method
>
> 2. ```java
>    // 类型可以省略
>    // 单个语句
>    p -> p.getGender() == Person.Sex.MALE 
>        && p.getAge() >= 18
>        && p.getAge() <= 25
>    // 多个语句
>    p -> {
>        return p.getGender() == Person.Sex.MALE
>            && p.getAge() >= 18
>            && p.getAge() <= 25;
>    }
>    // 多个参数
>    IntegerMath addition = (a, b) -> a + b;
>    ```
>
> 3. 访问enclosing scope局部变量和local class & anonymous class一样 | 不同地，没有shadowing，因为他的scope是 fake scope
>
> 4. Lambda expressions let you express instances of single-method classes more compactly.
>
> 5. method reference
>
>    1. ```java
>       // 方法调用
>       Arrays.sort(rosterAsArray,
>           (a, b) -> Person.compareByAge(a, b)
>       );
>       // 方法指针
>       Arrays.sort(rosterAsArray, Person::compareByAge);
>       ```
>
>    2. | Kind                                                         | Example                                |
>       | ------------------------------------------------------------ | -------------------------------------- |
>       | Reference to a static method                                 | `ContainingClass::staticMethodName`    |
>       | Reference to an instance method of a particular object       | `containingObject::instanceMethodName` |
>       | Reference to an instance method of an arbitrary object of a particular type | `ContainingType::methodName`           |
>       | <u>Reference to a constructor</u>                            | <u>`ClassName::new`</u>                |

enum

> pass

## Annotations

Annotations can be applied to declarations: declarations of classes, fields, methods, and other program elements.

内置的annotations: java.lang & java.lang.annotation

例子

```java
class UnmodifiableList<T> implements
    @Readonly List<@Readonly T> { ... }

@Documented
@interface ClassPreamble{
    String author();
    int currentVersion() default 1;
    String[] reviewers();
}

@ClassPreamble(
        author="eyisheng",
        reviewers = {"eyisheng", "jvm"}
)
public class AnnotatedClass{
    public void display(){
        System.out.println("hi");
    }
}
```

使custom annotation出现在Javadoc-generated documentation中，使用@Documented

#### 常用annotations

@Deprecated / @deprecated

编译器会warning

@Override

非强制要求，可被用于查错，若annotated method没有成功override，编译器会error

annotations of annocations = meta-annotation

`@Target`,`@Retention`,`@Documented`

containing annotation type [repeatable annotation]



## Interfaces and Inheritance

### Interface

可以包含：方法签名，常量，默认方法(default)/静态方法(static)【有方法体】，nested type

能extends很多interface，类只能extends一个类

methods成员默认都是public

constant 变量默认都是public, static, final

interfaceClass继承的method可以由interface instance直接调用，否则应该先cast instance为interfaceClass

#### 接口变更

添加方法

```java
public interface Dolt{
    void print();
    void display();
}
// 1. 继承接口
public interface DoltPlus extends Dolt{
    void newMethod();
}
// 2. 默认方法/静态方法
public interface Dolt{
    void print();
    void display();
    default void newMethod(){
        // body
    };
}
```

接口继承

interface2 extends interface1

对于default method

- 默认继承default为default
- redeclare default为abstract
- redefine default并override

### Inheritance

java的层级继承体系

#### constructor的调用

默认调用父类的non-arg constructor，没有就报错

```java
public MountainBike(int startHeight,
                    int startCadence,
                    int startSpeed,
                    int startGear) {
    super(startCadence, startSpeed, startGear); // 显示调用
    seatHeight = startHeight;
}  
```

#### 成员继承

public, protected, package-private

static/instance member hiding 命名隐藏

#### 类型转换

parent = child;

child = (child)parent;

```java
// 验证类型，因为是运行时检查的
if (obj instanceof MountainBike) {
    MountainBike myBike = (MountainBike)obj;
}
```

#### override

instance method - subclass:: return type/subtype + method signature

static method - subclass/superclass:: method signature

【根据static/instance的特点】

interface method

> 1. default/abstract ~ instance 【根据实例的意义】【调用方式】
>
> 2. class instance > interface default【根据default存在的意义】
>
> 3. already overriden by candidates X, 格式继承
>
> 4. default-default/abstract冲突 - 手动定义override重写，否则报错
>
> 5. inherited [class instance method > interface abstract method]
>
> 6. interface static method 不继承
>
> 7. 用Interface.super调用指定method
>
>    ```java
>    public interface OperateCar {
>        default public int startEngine(EncryptedKey key) {
>            // Implementation
>        }
>    }
>    public interface FlyCar {
>        default public int startEngine(EncryptedKey key) {
>            // Implementation
>        }
>    }
>    public class FlyingCar implements OperateCar, FlyCar {
>        public int startEngine(EncryptedKey key) {
>            FlyCar.super.startEngine(key); // 多个parent要用Type.super
>            OperateCar.super.startEngine(key);
>        }
>    }
>    ```
>
> 8. modifier 顺着继承链只能变成 more access
>
> 9. |                          | Superclass Instance Method     | Superclass Static Method       |
>    | ------------------------ | ------------------------------ | ------------------------------ |
>    | Subclass Instance Method | Overrides                      | Generates a compile-time error |
>    | Subclass Static Method   | Generates a compile-time error | Hides                          |

field member

> 1. 同名就hide，不管类型
> 2. 通过super

#### 多态

通过父指针调用子类override的method

```java
public class TestBikes {
  public static void main(String[] args){
    Bicycle bike01, bike02, bike03;
    // print的结果不同
    bike01.printDescription();
    bike02.printDescription();
    bike03.printDescription();
  }
}
```

The Java virtual machine (JVM) calls the appropriate method for the object that is referred to in each variable. It does not call the method that is defined by the variable's type. 

#### Object

`equals()`判断对象引用要相同【java是值系统】

#### 其他

1. constructor调用的方法一般用final【防止篡改】
2. abstract class vs. interface
   1. modifier不同：abstract class更多可能性
   2. fields不同：abstract class non-static/non-final
   3. 继承不同：interface multiple inheritance

## Collections

### 基本操作

遍历

```java
lst.stream().forEach(x->operation(x));
```

`java.util.Collections` 是一个包装类。它包含有各种有关集合操作的静态方法（对集合的搜索、排序、线程安全化等），大多数方法都是用来处理线性表的。此类不能实例化，就像一个工具类，服务于 Java 的 Collection 框架。



collections分类标准

1. 元素是否重复
2. 元素是否有序
3. 有多少个null element

[java collection 常用类型](https://blog.csdn.net/weixin_42574142/article/details/87125363)



## generic 泛型

### 基本用法

generic type [interface, class]

generic class `class name<T1, T2, ..., Tn> { /* ... */ }`

raw type

```java
Box<String> stringBox = new Box<>();
Box rawBox = stringBox;               // OK
```

## Exception 异常处理

try with resources

```java
// 资源会自动关闭
static String readFirstLineFromFile(String path) throws IOException {
    try (BufferedReader br =
                   new BufferedReader(new FileReader(path))) {
        return br.readLine();
    }
}
```

因为The class `BufferedReader`, in Java SE 7 and later, implements the interface `java.lang.AutoCloseable`

可以使用 `finally` block to ensure that a resource is closed

## Concurrency 并发

线程安全

> Java语言中得各种操作共享数据可以分成五类，按安全程度由强到弱，来排序：
>
> **不可变**：不可变的对象一定是线程安全的，无论对象的方法实现还是方法的调用者都不需要在采取安全措施。
>
> 如果共享数据是一个基本数据类型，那么只要在定义的时候使用final关键字修饰就可以保证它不可变；如果是共享数据是一个对象，需要对象自行保证其行为不会对其状态产生任何影响。
>
> **绝对线程安全**：绝对线程安全是不管运行是环境如何，调用者都不需要任何额外的同步措施。通常需要付出很大的甚至不切实际的代价。
>
> **相对线程安全**：就是通常意义的线程安全，确保这个对象单独的操作是操作安全的。Java语言中，大部分声称线程安全的类都属于这种类型，如：Vector、Hashtable等。
>
> **线程兼容**：指的是本身对象并不是线程安全的，但是可以通过调用端的正确使用同步手段来保证对象的安全使用。通常我们说一个类不是线程安全的，指的就是这种状态，如：ArrayList、HashMap等。
>
> **线程对立**：无论调用端是否采取了同步措施，都无法在多线程环境中并发使用代码。
>
> - **同步：指的是在多个线程并发访问共享数据时，保证共享数据在同一个时刻只能被一个线程使用。**
> - **互斥指的是实现同步的一种手段，临界区互斥量和信号量都是主要的互斥实现方式。**

### Atomic Action

线程安全：Atomic actions cannot be interleaved, so they can be used without fear of thread interference.

- **Reads and writes** are atomic for reference variables and for most **primitive variables (all types except `long` and `double`)**.
- **Reads and writes** are atomic for *all* variables declared `volatile` (*including* `long` and `double` variables).

当一个共享变量被volatile修饰时，它会保证修改的值会立即被更新到主存，当有其他线程需要读取时，它会去内存中读取新值。

可见性

> 而普通的共享变量不能保证可见性，因为普通共享变量被修改之后，什么时候被写入主存是不确定的，当其他线程去读取时，此时内存中可能还是原来的旧值，因此无法保证可见性。
>
> 另外，通过synchronized和Lock也能够保证可见性，synchronized和Lock能保证同一时刻只有一个线程获取锁然后执行同步代码，并且在<u>释放锁之前会将对变量的修改刷新到主存</u>当中。因此可以保证可见性。

有序性

> 　　在Java内存模型中，允许编译器和处理器对指令进行重排序，但是重排序过程不会影响到单线程程序的执行，却会影响到多线程并发执行的正确性。
>
> 　　在Java里面，可以通过volatile关键字来保证一定的“有序性”（具体原理在下一节讲述）。另外可以通过synchronized和Lock来保证有序性，很显然，synchronized和Lock保证每个时刻是有一个线程执行同步代码，相当于是让线程顺序执行同步代码，自然就保证了有序性。

rationale

> 　　前面讲述了源于volatile关键字的一些使用，下面我们来探讨一下volatile到底如何保证可见性和禁止指令重排序的。
>
> 下面这段话摘自《深入理解Java虚拟机》：“观察加入volatile关键字和没有加入volatile关键字时所生成的汇编代码发现，加入volatile关键字时，会多出一个lock前缀指令”
>
> 　　lock前缀指令实际上相当于一个内存屏障（也成内存栅栏），内存屏障会提供3个功能：
>
> 　　1）它确保指令重排序时不会把其后面的指令排到内存屏障之前的位置，也不会把前面的指令排到内存屏障的后面；即在执行到内存屏障这句指令时，在它前面的操作已经全部完成；
>
> 　　2）它会强制将对缓存的修改操作立即写入主存；
>
> 　　3）如果是写操作，它会导致其他CPU中对应的缓存行无效。

example

> 1. 假如某个时刻变量inc的值为10，
> 2. 线程1对变量进行自增操作，线程1先读取了变量inc的原始值，然后线程1被阻塞了；
> 3. 然后线程2对变量进行自增操作，线程2也去读取变量inc的原始值，由于线程1只是对变量inc进行读取操作，而没有对变量进行修改操作，所以不会导致线程2的工作内存中缓存变量inc的缓存行无效，所以线程2会直接去主存读取inc的值，发现inc的值时10，然后进行加1操作，并把11写入工作内存，最后写入主存。
> 4. 然后线程1接着进行加1操作，由于已经读取了inc的值，注意此时在线程1的工作内存中inc的值仍然为10，所以线程1对inc进行加1操作后inc的值为11，然后将11写入工作内存，最后写入主存。
> 5. 那么两个线程分别进行了一次自增操作后，inc只增加了1。

解决方法

```java
// original
public volatile int inc = 0;
public void increase() {
    inc++;
}
// use lock
public  void increase() {
    lock.lock();
    try {
        inc++;
    } finally{
        lock.unlock();
    }
}
// use synchronized
public synchronized void increase() {
    inc++;
}
// use AtomicInteger
public  AtomicInteger inc = new AtomicInteger();
public  void increase() {
    inc.getAndIncrement();
}
```

atomic是利用CAS来实现原子性操作的（Compare And Swap），CAS实际上是利用处理器提供的CMPXCHG指令实现的，而处理器执行CMPXCHG指令是一个原子性操作。



### Synchronized

1. First, it is **not** possible for two invocations of synchronized methods on the same object to **interleave**.
2. Second, when a synchronized method exits, it automatically establishes a **happens-before relationship** with *any **subsequent invocation*** of a synchronized method for the same object.

- reentrant synchronization: Recall that a thread cannot acquire a lock owned by another thread. But a thread *can* acquire a lock that it already owns.

> **原子性**：确保线程互斥的访问同步代码。synchronized保证只有一个线程拿到锁，进入同步代码块操作共享资源，因此具有原子性。
>
> **可见性**：保证共享变量的修改能够及时可见。执行 synchronized时，会对应执行 lock 、unlock原子操作。lock操作，就会清空工作空间该变量的值；执行unlock操作之前，必须先把变量同步回主内存中。
>
> **有序性**：synchronized内的代码和外部的代码禁止排序，至于内部的代码，则不会禁止排序，<u>但是由于只有一个线程进入同步代码块，因此在同步代码块中相当于是单线程的</u>，根据 as-if-serial 语义，即使代码块内发生了重排序，也不会影响程序执行的结果。
>
> **悲观锁**：synchronized是悲观锁。每次使用共享资源时都认为会和其他线程产生竞争，所以每次使用共享资源都会上锁。
>
> **独占锁（排他锁）**：synchronized是独占锁（排他锁）。该锁一次只能被一个线程所持有，其他线程被阻塞。
>
> **非公平锁**：synchronized是非公平锁。线程获取锁的顺序可以不按照线程的阻塞顺序。允许线程发出请求后立即尝试获取锁。
>
> **可重入锁**：synchronized是可重入锁。持锁线程可以再次获取自己的内部的锁。
>
> 1. 悲观锁 or 乐观锁：是否一定要锁
> 2. 共享锁 or 独占锁（排他锁）：是否可以有多个线程同时拿锁
> 3. 公平锁 or 非公平锁：是否按阻塞顺序拿锁
> 4. 可重入锁 or 不可重入锁：拿锁线程是否可以多次拿锁

```java
public class SyncTest {
    public static void main(String[] args) {
        // lock (obj)
        synchronized (SyncTest.class) {
        }
    }
    // lock this
    public synchronized void fun(){}
    // lock class
    public synchronized static void fun(){}
}
```

#### 常见错误

**只有同步代码块与同步方法的锁对象是同一个对象对象时，才能保证同一时刻，只有一个线程访问共享资源。**

```java
class MySyncClass implements Runnable{
    private static int i=0;
    private synchronized void add(){
        i++;
    }
    /* 锁整个类
    private static synchronized void add(){
    	i++;
    }
    */
    @Override
    public void run(){
        while (true){
            this.add();
        }
    }
    
    public static void main(String[] args) throws Exception {
        Thread t1 = new Thread(new SyncWrong());
        Thread t2 = new Thread(new SyncWrong());
        /* 只创建一个对象
        SyncWrong wrong = new SyncWrong();
        Thread t1 = new Thread(wrong);
        Thread t2 = new Thread(wrong);
        */
        t1.start();
        t2.start();
        t1.join();
        t2.join();
        System.out.println(i);
    }
}
```

**每个访问共享资源的代码都必须被同步。**

```java
class Resource{

    private static int i = 0;

    public synchronized void add() {
        i++;
    }
    public void reduce() { // public synchronized void reduce
        i--;
    }
}
```

对于上述代码，add 和 reduce 都对共享资源 i 进行了处理，你必须同步这两个方法（将 reduce 改造为同步方法）。如果不这样做，那么reduce()方法就会完全忽略这个对象锁，也就是在当前线程获得到锁，执行add操作时，其他线程可以随意的调用 reduce方法，从而导致并发修改的问题。
**私有化共享资源**

```java
class Resource{
    public static int i = 0;
    public synchronized void add() {
        i++;
    }
	public synchronized void get() {
        return i;
    }
    /*
    private static int i = 0;
    public synchronized int get(){return i;}
    */
}
```

上述代码的问题在于任何线程都可以通过 Resource.i 来获取共享变量的值，若当前线程获得锁，正在执行add同步方法的内容，其他线程通过 Resource.i 则会忽略锁，可能获取到中间结果。正确的方法是将 共享资源 i 私有化（用 private 修饰）, 然后提供一个被同步的获取方式。


### Thread

创建方式

- 直接实例化Thread
- 通过Exector

```java
class MyThread extends Thread{
    @Override
    public void run(){
        System.out.println(MyThread.class);
    }
}

class MyRunnable implements Runnable{
    @Override
    public void run() {
        System.out.println(MyRunnable.class);
    }
}

// in main function
ThreadTutorial threadTutorial = new ThreadTutorial();
(new Thread(threadTutorial.new MyRunnable())).start();
(threadTutorial.new MyThread()).start();
```

Sleeping [时间并不可靠]

```java
void function() throws InterruptedException{
    Thread.sleep(10);
}
```

注意会抛异常

#### interrupt 中断

中断是通过调用Thread.interrupt()方法来做的. 这个方法通过修改了被调用线程的中断状态来告知那个线程, 说它被中断了. 对于非阻塞中的线程, 只是改变了中断状态, 即Thread.isInterrupted()将返回true; 对于可取消的阻塞状态中的线程, 比如等待在这些函数上的线程, Thread.sleep(), Object.wait(), Thread.join(), 这个线程收到中断信号后, 会抛出InterruptedException, 同时会把中断状态置回为true.但调用Thread.interrupted()会对中断状态进行复位。

```java
// 因为可能被中断，所以需要处理异常
while (true){
    try {
        Thread.sleep(4000);
    } catch (InterruptedException e) {
        // We've been interrupted: no more messages.
        return;
    }
}

// 自定义run
while (true) {
    heavyCrunch(inputs[i]);
    if (Thread.interrupted()) {
        // We've been interrupted: no more crunching.
        // or throw new InterruptedException();
        return;
    }
}
```

 *interrupt status* 会在throw InterruptedException后被置位，而`isInterrupted`不会

#### join

调用`t.join()`后必须等待t执行完成，和sleep一样可能被中断

```java
Thread t = new Thread(threadTutorial.new MyRunnable());
t.start();
t.join(1000);
Thread.sleep(1000); // t仍在执行
t.interrupt();
```

### Deadlock & Livelock

**产生死锁的四个必要条件**：

- （1） 互斥条件：一个资源每次只能被一个进程使用。
- （2） 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
- （3） 不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺。
- （4） 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。

活锁

A thread often acts in response to the action of another thread. If the other thread's action is also a response to the action of another thread, then *livelock* may result. As with deadlock, livelocked threads are unable to make further progress.

饥饿

If one thread invokes this method frequently, other threads that also need frequent synchronized access to the same object will often be blocked.

### 待研究

下面就来具体介绍下happens-before原则（先行发生原则）：

- 程序次序规则：一个线程内，按照代码顺序，书写在前面的操作先行发生于书写在后面的操作
- 锁定规则：一个unLock操作先行发生于后面对同一个锁额lock操作
- volatile变量规则：对一个变量的写操作先行发生于后面对这个变量的读操作
- 传递规则：如果操作A先行发生于操作B，而操作B又先行发生于操作C，则可以得出操作A先行发生于操作C
- 线程启动规则：Thread对象的start()方法先行发生于此线程的每个一个动作
- 线程中断规则：对线程interrupt()方法的调用先行发生于被中断线程的代码检测到中断事件的发生
- 线程终结规则：线程中所有的操作都先行发生于线程的终止检测，我们可以通过Thread.join()方法结束、Thread.isAlive()的返回值手段检测到线程已经终止执行
- 对象终结规则：一个对象的初始化完成先行发生于他的finalize()方法的开始

实质上是指令重排不能造成RW,RW,WW冲突



### 参考资料

[Java并发深度总结：synchronized 关键字](https://blog.csdn.net/qq_42080839/article/details/109848719)

[Java并发编程：volatile关键字解析](https://www.cnblogs.com/dolphin0520/p/3920373.html)