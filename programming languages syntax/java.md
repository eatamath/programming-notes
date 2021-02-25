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

尽可能一起初始化

非static在constructor/initializer block初始化

static在static block/static method初始化

### nested class

