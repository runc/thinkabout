#### 配置

1、master节点数，建议3、5台，为基数

2、client节点数据，建议3台

3、node节点数，按照业务或者性能合理选择，报警阈值80%

4、分片数，提前预留，一般为node得背书，分片数不能动态改变，充分考虑业务提前预留

5、副本数，保证最低，资源充足，考虑增加，提升查询熟读和数据稳定性

#### 集群重启

1、关闭写服务，stop节点，start节点

2、滚动重启，停止集群分片分配通过api来操作，重启节点后重新加入分配分配

#### 索引相关

1、索引按照时间归档

2、尽量给索引添加别名，方便数据迁移

#### 大批量数据初始化

1、关闭副本，关闭自动刷新，也是近实时的原因

2、完成数据导入，开启副本和自动刷新

3、定期查看集群cache情况，做必要清理

4、清理索引，片迁移，保证node数据分布均匀


es高效运维策略:

1、索引 force merge

2、内存调整

3、gc调整

4、监控/索引管理

-- 
[EYou](https://elasticsearch.cn/slides/122#page=7)

xpack

1、meta诊断，作为系统元数据，放在堆内存中，量大频繁更新时容易引起gc

> 集群meta信息太多，短时间频繁更新，都会给集群带来极大的负担可能造成GC频繁，负载突增，甚至阻塞相关索引的读写，影响性能

>GET _cluster/stateGET.monitor*/_search?filter_path=hits.hits.fields,hits.hits.sort

2、

> 我司优化策略:

[elasticsearch日常使用经验分享](https://elasticsearch.cn/article/208)

[日增百亿elasticsearch集群调优](https://elasticsearch.cn/slides/169#page=26)