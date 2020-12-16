# Spark Notes

### 参考资料

[翻译文档](http://spark.apachecn.org/#/docs/12)

## RDD操作

transformation & action 两个操作

_transformations（转换）_，它会在一个已存在的 dataset 上创建一个新的 dataset，和 _actions（动作）_，将在 dataset 上运行的计算后返回到 driver 程序

默认情况下，每次你在 RDD 运行一个 action 的时，每个 transformed RDD 都会被重新计算。但是，您也可用 `persist`（或 `cache`）方法将 RDD persist（持久化）到内存中；在这种情况下，Spark 为了下次查询时可以更快地访问，会把数据保存在集群上。此外，还支持持续持久化 RDDs 到磁盘，或复制到多个结点。

访问对象的方法和成员会导致整个对象被发送到集群中，解引用方法

```scala
def doStuff(rdd: RDD[String]): RDD[String] = {
  val field_ = this.field
  rdd.map(x => field_ + x)
}
```

- Implement the Function interfaces in your own class, either as an anonymous inner class or a named one, and pass an instance of it to Spark.
- Use [lambda expressions](http://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html) to concisely define an implementation.

推荐做法

- [Lambda expressions](https://docs.python.org/2/tutorial/controlflow.html#lambda-expressions), for simple functions that can be written as an expression. (Lambdas do not support multi-statement functions or statements that do not return a value.)
- Local `def`s inside the function calling into Spark, for longer code.
- Top-level functions in a module.