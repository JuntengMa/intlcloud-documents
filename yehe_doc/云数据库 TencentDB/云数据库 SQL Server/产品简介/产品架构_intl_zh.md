## 后台架构
架构图如下：
![](https://main.qcloudimg.com/raw/ece530a79e57cf0c0fd2d725772ceb1a.png)
云数据库 SQL Server 由一主一镜像的 SQL Server 数据库组成，跨机架部署，每个库对应一组监控 Agent，通过心跳对数据库进行实时监控。由独立部署的2组决策调度集群和配置集群组成，作为集群的管理调度中心，主要管理数据库节点组、接入网关集群、HDFS 的正常运行。Hadoop 分布式文件系统（HDFS） 提供数据灾备服务，提供冷备数据。接入网关集群，对外提供唯一的 IP，如果数据节点发送切换，IP 不会改变。

## 数据库镜像（Database Mirroring）
当前云数据库 SQL Server 默认采用数据库镜像（Database Mirroring）方案（高可用复制方案），提供秒级自动切换，“零”数据损失的可靠性。
![](https://main.qcloudimg.com/raw/c93d18bdf946afbaefb2f9d345186913.jpg)

## 节点自动恢复
云数据库 SQL Server 支持自动重建数据库节点，如果节点故障，系统将自动恢复重建故障节点。这里的节点切换对业务透明，且数据库访问的 IP 不会改变。
![](https://main.qcloudimg.com/raw/cd4b73ec5c53454a3248ac413078ef3f.png)

