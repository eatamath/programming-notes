### 链表

#### 方法论

用快慢指针进行bias定位



#### [19. 删除链表的倒数第 N 个结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

算法：快慢指针

单节点的边界情形思维不清楚

#### [206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

算法：反转链表

指针交换的代码顺序

#### [203. 移除链表元素](https://leetcode-cn.com/problems/remove-linked-list-elements/)

边界条件先考虑处理

### 队列

#### BFS

##### [200. 岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

BFS去递归，DFS

python队列的使用

`max`和`min`比`if-else`耗时

根据用户统计，BFS比DFS快



### 算法原理

#### 外排序

[胜者树与败者树](https://blog.csdn.net/whz_zb/article/details/7425152)

#### B树

作用

> 磁盘读取时间=磁盘寻道时间+磁盘旋转时间
>
> 若文件按100个记录的块进行存储，建立多层索引可以减少磁盘访问次数

结构

> 1. 所有节点孩子<=m
> 2. <u>内部节点 孩子[ceil(m/2),m]</u>
> 3. <u>根节点孩子[2,m]</u>
> 4. <u>非叶子节点 k个孩子 & k-1个key</u>
> 5. 叶子节点位于同一层
> 6. 信息有序

