## 操作场景
腾讯云容器服务 TKE 支持通过创建 PV/PVC，并为工作负载挂载数据卷的方式使用腾讯云文件存储 CFS。本文介绍如何通过以下两种方式在集群中为工作负载挂载文件存储：
- [方式1：动态创建文件存储](#dynamicCFS)
- [方式2：使用已有的文件存储](#alreadyCFS)


## 准备工作
### 安装文件存储扩展组件
>?
>- 使用扩展组件功能前需 [提交工单](https://console.cloud.tencent.com/workorder/category) 进行申请。
>- 若您的集群已安装 CFS-CSI 的扩展组件，则请跳过此步骤。
>
1. 登录[ 容器服务控制台 ](https://console.cloud.tencent.com/tke2)，选择左侧导航栏中的【扩展组件】。
2. 在“扩展组件”管理页面上方选择需使用文件存储扩展组件的集群及其所在地域，并单击【新建】。
3. 在“新建扩展组件”页面，选择【CFS 腾讯云文件存储】并单击【完成】即可。



## 操作步骤
<span id="dynamicCFS"></span>
### 动态创建文件存储

当您需要动态创建文件存储时，可以按照以下步骤进行操作：
1. 创建文件存储类型的 StorageClass，定义需使用的文件存储模板。
2. 通过 StorageClass 创建 PVC，进一步定义所需的文件存储参数。
3. 创建工作负载数据卷时选择已创建的 PVC，并设置容器挂载点。
详细操作步骤请参见 [StorageClass 管理文件存储模版](https://intl.cloud.tencent.com/document/product/457/36154)。

<span id="alreadyCFS"></span>
### 使用已有的文件存储

当您需要使用已有文件存储时，可以按照以下步骤进行操作：
1. 通过已有的文件存储创建 PV。
2. 创建 PVC 时设置与上述创建的 PV 相同的 StorageClass 和容量。
3. 创建工作负载时，选择上述 PVC。
详细操作步骤请参见 [ PV 和 PVC 管理文件存储](https://intl.cloud.tencent.com/document/product/457/36155)。

## 相关信息

更多关于如何使用文件存储的信息请参见 [README_CFS.md](https://github.com/TencentCloud/kubernetes-csi-tencentcloud/blob/master/docs/README_CFS.md)。
