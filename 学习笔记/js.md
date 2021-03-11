### 面向对象编程

继承 `inherent(object)`

删除属性 `delete o.x`

检测属性 `in, hasOwnProperty()`

getter & setter

序列化 `json.stringify(), json.parse()` 返回深拷贝

冻结 `Object.[seal(), freeze()]`

#### 创建对象

Object.create(`[prototype,{}]`)

```javascript
var Vehicle = function (p) {
  this.price = p;
};
var v = new Vehicle(500);
```



#### 属性

修改属性 `Object.defineProperty`

#### 原型属性

`isPrototypeOf`

`object.prototype`

`getPrototypeOf`

### 事件

#### 传播的三个阶段

当一个事件发生以后，它会在不同的DOM节点之间传播（propagation）。这种传播分成三个阶段：

- **第一阶段**：从window对象传导到目标节点，称为“捕获阶段”（capture phase）。
- **第二阶段**：在目标节点上触发，称为“目标阶段”（target phase）。
- **第三阶段**：从目标节点传导回window对象，称为“冒泡阶段”（bubbling phase）。

`stopPropagation`方法只会阻止当前监听函数的传播，不会阻止``节点上的其他`click`事件的监听函数。如果想要不再触发那些监听函数，可以使用`stopImmediatePropagation`方法。

#### Event对象

事件发生以后，会生成一个事件对象，作为参数传给监听函数。浏览器原生提供一个`Event`对象，所有的事件都是这个对象的实例，或者说继承了`Event.prototype`对象。