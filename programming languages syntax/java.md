# Java Notes

## Java Basics

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