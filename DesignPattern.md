## Design Pattern



### Creational Patterns

#### Abstract Factory 抽象工厂

一个工厂创建一类事物，工厂的抽象就是抽象工厂，工厂的工厂

Color [red, green, blue] 和 Shape [circle, rectangle, triangle] 是两个类别 [java - interface]

类别工厂ColorFactory 和 ShapeFactory 的工厂是 Abstract Factory

```java
public interface Color{}
public interface Shape{}

public class Red implements Color{}
public class Yellow implements Color{}

// 抽象工厂
public abstract class AbstractFactory{
    public abstract Color getColor(param);
    public abstract Shape getShape(param);
}

// 类别工厂
public class ShapeFactory extends AbstractFactory{
    @Override
    public Shape getShape(param){
        return new Red();
        // else
        // return new Yellow();
    }
   @Override
   public Color getColor(String colorType){
      return null;
   }
}
```

优点：

缺点：拓展性差；

#### Factory Method 工厂模式

一个工厂创建一类事物，就是这个类别的工厂

抽象工厂是基于工厂模式的

```java
public interface Color{}

public class ColorA implements Color{}
public class ColorB implements Color{}

public class ColorFactory{
    public Color getColor(){
        return new ColorA();
        // or
        // return new ColorB();
    }
}

// in main function
ColorFactory colorFactory = new ColorFactory(); // 获取工厂
Color color1 = colorFactory.getColor(); // 获取实例
color1.func();
```

优点：封装细节，只需要接口

缺点：增加产品工作量大

#### Singleton 单例模式

只有一个实例，类自己创建实例，全局访问

```java
public class Singleton{
    private static Singleton instance = new Singleton();
    
    private Singleton(){} // 无法实例化
    
    public static Singleton getInstance(){return instancce;}
    
    // other methods...
}

// in main function
Singleton obj = Singleton.getInstance();
obj.func();
```

优点：避免频繁创建和销毁；

缺点：没有接口，不能继承

#### Builder 制造者

导演指定pipeline, 实现细节在builder中，builder可以制造出不同的东西

通过pipeline访问不同的builder，每个builder根据自己的methods造出来的obj不同

```java
// target obj
class Item{
    // methods...
}

// 抽象 builder
public abstract class ItemBuilder{
    protected Item item;
    
    // init & get
    public void createItem(){};
    public Item getItem(){};
    
    // build functions
    public abstract void step1();
    public abstract void step2();
    public abstract void step3();
}

// concrete builder 1
public Item1 extends ItemBuilder{
    public void step11(){};
    public void step12(){};
}
// concrete builder 2
public Item2 extends ItemBuilder{
    public void step21(){};
    public void step22(){};
}

// director
class Waiter{
    private ItemBuilder itembuilder;
    
    // global pipeline functions...
}
```

**意图：**将一个复杂的构建与其表示相分离，使得同样的构建过程可以创建不同的表示。

**主要解决：**主要解决在软件系统中，有时候面临着"一个复杂对象"的创建工作，其通常由各个部分的子对象用一定的算法构成；由于需求的变化，这个复杂对象的各个部分经常面临着剧烈的变化，但是将它们组合在一起的算法却相对稳定。

#### Prototype 原型模式

行为类似数据库，通过一个cache对obj进行load和get操作，并且get时clone操作

```java
// 可以直接 extends Cloneable
public interface Item{
    void clone();
}

/* 另一种方法
// 一类obj的抽象
public abstract class AbstractItem implements Cloneable{
    // members...
    @Override
    void clone(){
        // implement clone...
    }
}
*/

public class Item1 implements Item{}
public class Item2 implements Item{}

public class ItemCache{
    private static final Map<String, Item> prototypes = new HashMap<>();
    
    static{
        prototypes.put('item1',new Item1());
        prototypes.put('item2',new Item2());
    }
    
    public static Item getPrototype(String type){
        try{
            return prototypes.get(type).clone(); // clone item
        }
        catch(Exception ex){}
    }
}

// in main function
Item item1 = ItemCache.getPrototype("item1");
```





### 参考资料

1. [菜鸟教程](https://www.runoob.com/design-pattern/builder-pattern.html)

2. [DP Cookbook](https://sourcemaking.com/design_patterns/prototype)

