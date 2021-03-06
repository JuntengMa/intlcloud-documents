
## 容器服务计费说明
容器服务暂不收取服务本身费用，按用户实际使用的云资源收费。使用容器服务涉及以下产品，详情见对应产品计费模式。

- [云服务器计费模式](https://intl.cloud.tencent.com/document/product/213/2180)
- [云硬盘价格总览](https://intl.cloud.tencent.com/document/product/213/2255)
- [负载均衡计费说明](https://intl.cloud.tencent.com/zh/document/product/214/8848)

>! 容器服务基于 Kubernetes 且为声明式服务。如果您已在容器服务中创建负载均衡（CLB）、云硬盘（CBS） 盘等 IaaS 资源，现在不再需要使用 CLB 和 CBS，请在 TKE 控制台中删除对应的 Service 和 PersistentVolumeClaim 对象。如果您只在 CLB 控制台中删除 CLB 或者在 CBS 控制台中删除 CBS，容器服务会重新创建新的 CLB 和 CBS， 并继续扣除相关费用。

## 弹性容器服务计费说明
弹性容器服务采用后付费的按量计费模式。按照实际配置的资源及使用时间计算，无需提前支付费用。详情请参见 [弹性集群计费概述](https://intl.cloud.tencent.com/document/product/457/34054)。

