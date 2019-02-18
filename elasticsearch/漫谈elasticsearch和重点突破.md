> elasticsearch一些实践

```

其实在14年初结识了elasticsearch，那会估计是1.x的版本，
主要使用场景是聚划算运营后台商品数据检索这块，这里主要有两种方案，
一个是利用阿里内部服务于内部的终搜系统，主要是hadoop+solr，
利用hadoop分布式构建index，利用构建好的index +solr来多维度检索数据，
总之流程很冗长复杂，
即使后台团队尝试使用elasticsearch，这一状况有所改善，去掉了hadoop的索引构建任务，
但那会elasticsearch也不是非常好用,记得schema这块就处理得很不灵活，
以上算作是第一阶段的使用经验了，现在也基本忘记了所有细节了。

第2阶段使用，主要是15年创业的时候，在用户检索商品时使用，
主要用到的功能是对于elasticsearch api和中文检索(中文分词+同义词，近义词等插件）的使用，
在处理处理规模和并发量并没有太大的挑战。

第3阶段的使用，就是最近主导负责的一个企业分布式日志中心的产品了，
当然也有saas的产品形态,这个产品里对于elasticsearch主要是稳定性+海量数据检索分析上的，
至于如何具体使用在后面会仔细介绍下。

```

> elasticsearch架构上的分析

### 概念普及
```
集群（Cluster）一组拥有共同的 cluster name 的节点。
节点（Node) 集群中的一个 Elasticearch 实例。
索引（Index) 相当于关系数据库中的database概念，一个集群中可以包含多个索引。这个是个逻辑概念。
主分片（Primary shard） 索引的子集，索引可以切分成多个分片，分布到不同的集群节点上。分片对应的是 Lucene 中的索引。
副本分片（Replica shard）每个主分片可以有一个或者多个副本。
类型（Type）相当于数据库中的table概念，mapping是针对 Type 的。同一个索引里可以包含多个 Type。(在elasticsearch 6.x及其以后的版本已经废弃)
Mapping 相当于数据库中的schema，用来约束字段的类型，不过 Elasticsearch 的 mapping 可以自动根据数据创建。
文档（Document) 相当于数据库中的row。
字段（Field）相当于数据库中的column。
分配（Allocation） 将分片分配给某个节点的过程，包括分配主分片或者副本。如果是副本，还包含从主分片复制数据的过程。
```

### 服务发现和选主
### 弹性伸缩
### 分片和副本
### 恢复和容灾

### 数据库NOSQL

```
translog
schema less 
dsl,but not support sql (5.x) -jdbc-> sql (6.x)
```