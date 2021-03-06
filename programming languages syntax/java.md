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
        // 1. parameters 2. return type 3. exception list
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
> 4. method reference
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