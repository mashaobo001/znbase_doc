# **相关术语**
### **A**
**ACID**

​		ACID 是指数据库管理系统在写入或更新资料的过程中，为保证事务是正确可靠的，所必须具备的四个特性：原子性(atomicity)、一致性 (consistency)、隔离性（isolation）以及持久性（durability）。

-   原子性 (atomicity)
    指一个事务中的所有操作，或者全部完成，或者全部不完成，不会结束在中间某个环节。

-   一致性 (consistency)
    指在事务开始之前和结束以后，数据库的完整性没有被破坏。ZNBase
    在写入数据之前，会校验数据的一致性，校验通过才会写入内存并返回成功。

-   隔离性 (isolation)
    指数据库允许多个并发事务同时对其数据进行读写和修改的能力。隔离性可以防止多个事务并发执行时由于交叉执行而导致数据的不一致，主要用于处理并发场景。ZNBase
    目前只支持两种隔离级别，即读提交和串行化读。

-   持久性 (durability)
    指事务处理结束后，对数据的修改就是永久的，即便系统故障也不会丢失。在 ZNBase
    中，事务一旦提交成功，数据全部持久化存储到 存储层，此时即使 ZNBase
    服务器宕机也不会出现数据丢失。

### **B**
**Bloom Filter**

​		Bloom filter是由Howard Bloom在1970年提出的[二进制](https://baike.baidu.com/item/%E4%BA%8C%E8%BF%9B%E5%88%B6/361457)向量数据结构，它具有空间和时间效率，被用来检测一个元素是不是集合中的一个成员，rocksDB存储引擎使用Bloom filter来过滤查询的数据是否在SST文件中

### **C**
**Leader/Follower/Candidate**

​		raft中的server有三种状态，分别为Leader,负责接收客户端的读写请求；Flower被动的从Leader同步数据，当Leader失效时会进行选举产生新的Leader，在选举过程中Flower角色会转变为Candidate，参与选举投票竞选Leader

### **N**
**Node**

​		运行 ZNBase 的一个节点，多个节点组成一个集群

### **R**
**Raft**

​		Raft为一种一致性算法协议，Raft协议可以使得一个集群的服务器组成复制状态机，通过强Leader模式确保每一个range和它的其他副本保持数据的强一致性

**Range**

​		ZNBase 所有用户数据（包括数据表、索引等等）和几乎所有的系统数据都存储在一个巨大有序的 key-value 集合。根据连续的 key 划分成多个区间，每个区间是一个 Range
