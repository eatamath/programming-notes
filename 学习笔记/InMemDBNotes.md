# InMem DB Notes

**TimesTen_18.1_Scaleout.pdf**

R in Mem DB 分布式只有 timesten

### zookeeper

zoo keeper 防止系统脑裂，奇数个结点

管理集群

db+zookeeper = grid

web app 不用关心数据在集群中的位置，数据在内部网络迁移

**建表分布选项**

- hash
- 



副本集 replica set 包含(2)个element

单个副本异常不会影响到集群

**instance**

数据 + 管理

**element**