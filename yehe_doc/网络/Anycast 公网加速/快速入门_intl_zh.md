## 连接流程
![快速入门](https://main.qcloudimg.com/raw/b9848b8db42e252992cb4931c2e67999.png)
### 创建 Anycast 型 EIP
1. 登录 [EIP 控制台](https://console.cloud.tencent.com/cvm/eip)，单击【申请】。
2. 根据您的需求选择地域、带宽上限、数量，IP 地址类型选择 【加速 IP 地址】，再单击 【确定】 即可创建 Anycast 型 EIP。

### 绑定后端资源
登录 [EIP 控制台](https://console.cloud.tencent.com/cvm/eip) 后，选择 【更多】>【绑定】，绑定指定的资源，本文档以 CVM 为例。

### 用加速 EIP 连接公网
登录您已绑定的后端资源后，即可通过加速 EIP 连接公网，使用 Anycast 公网加速。本文档中已绑定 CVM，即登录 CVM 后即可使用 Anycast 公网加速。

## 其他常见操作
### 变更 Anycast 弹性公网 IP 配置
#### 调整带宽
>?仅带宽上移账户可在 EIP 控制台调整带宽，非带宽上移账户请在对应的 [云服务器](https://console.cloud.tencent.com/cvm/instance/index?rid=1) 或 [ NAT 网关](https://console.cloud.tencent.com/vpc/nat?rid=1) 上调整带宽。若您无法确定账户类型，请参见 [账户类型](https://intl.cloud.tencent.com/document/product/214/36999)。

1. 登录 [EIP 控制台](https://console.cloud.tencent.com/cvm/eip )。
2. 在 EIP 列表中，选择要使用的 EIP，单击【调整网络】 即可。
