>? 目前共享带宽包处于内测阶段，如需使用，请提交 [内测申请](https://intl.cloud.tencent.com/apply/p/86ulv50u1e8)。

## 限制说明
1. 一个地域仅可开通一个设备带宽包。
2. 在一个地域创建设备带宽包后，当前地域所有云服务器、负载均衡都将变为按带宽包计费，不可与其它计费模式共存。
3. 原有的包年包月带宽费用将按小时折算后进行退费。
4. 设备带宽包用户可以提 [工单申请](https://console.cloud.tencent.com/workorder/category) 修改账户类型为上移类型，以使用 IP 带宽包。

## 操作步骤
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1)。
2. 单击左侧导航的【共享带宽包】。
3. 选择地域，单击左上角的【+新建】。
4. 在弹窗中，输入名称、选择计费类型，单击【确定】完成创建。
![](https://main.qcloudimg.com/raw/6aac805bcb27daeb1a6ac01fd07c6078.png)
5. 创建完成后，为了防止产生高额费用，建议您为带宽包内的资源设置带宽上限。可参考如下操作：
 - 云服务器设置带宽上限：
    1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm/instance/index?rid=1)。
    2. 在操作栏下，选择【更多】>【资源调整】>【调整网络】进行带宽上限的设置。
    ![](https://main.qcloudimg.com/raw/1457ec84e27b2abb0c8b01cf214cc02c.png)
 - 负载均衡设置带宽上限：
    1. 登录 [负载均衡控制台](https://console.cloud.tencent.com/clb/index?rid=1&type=2%2C3)。
    2. 在操作栏下，选择【更多】>【调整带宽】进行带宽上限的设置。
