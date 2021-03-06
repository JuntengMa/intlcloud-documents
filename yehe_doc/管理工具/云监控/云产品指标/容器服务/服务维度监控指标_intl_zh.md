## 命名空间

Namespace=QCE/DOCKER

##  监控指标

| 指标中文名                | 指标英文名                | 单位 | 指标含义                             | 维度                              |
| ------------------------- | ------------------------- | ---- | ------------------------------------ | --------------------------------- |
| 服务 CPU 使用情况         | ServiceCpuUsed            | 核   | 服务内所有容器实例 CPU 使用之和      | clusterId、serviceName、namespace |
| 服务 CPU 使用率（占集群） | ServiceCpuUsageForCluster | %    | 服务使用 CPU 占集群比率              | clusterId、serviceName、namespace |
| 服务内存使用情况          | ServiceMemUsed            | MiB  | 服务内所有容器实例内存使用之和       | clusterId、serviceName、namespace |
| 服务内存使用率（占集群）  | ServiceMemUsageForCluster | %    | 服务使用内存占集群比率               | clusterId、serviceName、namespace |
| 服务网络入流量            | ServiceInFlux             | MB   | 服务内所有实例在该时间窗口入流量之和 | clusterId、serviceName、namespace |
| 服务网络出流量            | ServiceOutFlux            | MB   | 服务内所有实例在该时间窗口出流量之和 | clusterId、serviceName、namespace |
| 服务网络入带宽            | ServiceInBandwidth        | Mbps | 服务内所有实例的入带宽之和           | clusterId、serviceName、namespace |
| 服务网络出带宽            | ServiceOutBandwidth       | Mbps | 服务内所有实例的出带宽之和           | clusterId、serviceName、namespace |
| 服务网络入包量            | ServiceInPackets          | 个/s | 服务内所有实例的入包量之和           | clusterId、serviceName、namespace |
| 服务网络出包量            | ServiceOutPackets         | 个/s | 服务内所有实例的出包量之和           | clusterId、serviceName、namespace |

>每个指标对应的统计粒度（Period）可取值不一定相同，可通过 [DescribeBaseMetrics](https://intl.cloud.tencent.com/document/product/248/33882) 接口获取每个指标支持的统计粒度。

## 各维度对应参数总览

| 参数名称                       | 维度名称    | 维度解释                                                     | 格式                                 |
| ------------------------------ | ----------- | ------------------------------------------------------------ | ------------------------------------ |
| Instances.N.Dimensions.0.Name  | clusterId   | 集群 ID的维度名称                                            | 输入String 类型维度名称：clusterId   |
| Instances.N.Dimensions.0.Value | clusterId   | 具体的集群 ID，[查询集群列表](https://intl.cloud.tencent.com/document/product/457/32025) 接口中返回的 clusterId（集群的 ID）字段 | 输入集群具体 ID，例如 ：cls-xxxxx    |
| Instances.N.Dimensions.1.Name  | serviceName | 为服务名称                                                   | 输入String 类型维度名称：serviceName |
| Instances.N.Dimensions.1.Value | serviceName | 具体的服务名称，[查询服务列表](https://intl.cloud.tencent.com/document/product/457/32025) 接口中返回的 serviceName（服务名）字段 | 输入具体服务名称，例如： test        |
| Instances.N.Dimensions.2.Name  | namespace   | 命名空间的维度名称                                           | 输入String 类型维度名称：namespace   |
| Instances.N.Dimensions.2.Value | namespace   | 具体的空间名称，查询服务列表 接口中返回的 namespace（命名空间）字段 | 输入命名空间具体名称，例如： default |

## 入参说明

查询容器服务服务维度监控数据，入参取值如下：
&Namespace=QCE/DOCKER
&Instances.N.Dimensions.0.Name=clusterId
&Instances.N.Dimensions.0.Value 为集群 ID
&Instances.0.Dimensions.1.Name=namespace
&Instances.0.Dimensions.1.Value 为命名空间
&Instances.0.Dimensions.2.Name=serviceName
&Instances.0.Dimensions.2.Value 为服务名称

