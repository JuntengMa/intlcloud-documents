## 简介

对象存储 COS 控制台提供了按存储桶标签筛选存储桶列表的功能，该功能依赖于腾讯云标签服务。

假设企业帐号 CompanyExample（OwnerUin 为100000000001，Owner_appid 为1250000000）下有一个子账号 jason.read，企业帐号 CompanyExample 需要授予该子账号拥有拉取标签列表操作权限，下面将为您详细介绍如何进行授权操作。



## 相关说明
若您希望通过子账号在控制台上按存储桶标签筛选存储桶列表，则子账号需要拥有 GetResourceTags、GetResourcesByTags 和 GetTags 操作权限，您可以在 [访问管理](https://console.cloud.tencent.com/cam/policy) 控制台，通过创建自定义策略的形式为子账号授予这些操作权限。



## 操作步骤

1. 使用企业账号 CompanyExample 登录到 [访问管理](https://console.cloud.tencent.com/cam/policy) 控制台，进入到策略配置页面。
2. 授予子账号 jason.read 拥有拉取标签列表的权限，可通过**策略生成器**或**策略语法**实现。
 - **通过策略生成器**
（1）进入 [访问管理](https://console.cloud.tencent.com/cam/policy) 策略配置页面。
（2）单击【新建自定义策略】>【按策略生成器创建】。
（3）进入授权配置页面，配置信息如下：
    - **效果**：选择为允许，默认不变。
    - **服务**：选择为标签。
    - **操作**：可根据您的业务需要进行勾选，此处勾选 GetResourceTags、GetResourcesByTags 和 GetTags 这三个操作权限。
    - **资源**：此处我们输入`*`，您也可以根据实际环境填写，详情请参见 [资源描述方式](https://intl.cloud.tencent.com/document/product/598/10606)。
![](https://main.qcloudimg.com/raw/6ef8573a92f3c59b7c0f633b935273da.png)
（4）单击【添加声明】，您可在下方查看已配置的权限。
（5）单击【下一步】，输入策略名称并单击【创建策略】，即可完成创建。
 - **通过策略语法**
（1）进入 [访问管理](https://console.cloud.tencent.com/cam/policy) 策略配置页面。
（2）单击【新建自定义策略】>【按策略语法创建】。
（3）您可以选择空白模板或者已有的标签模板创建，此处我们选择【QcloudTAGFullAccess】模板。
![](https://main.qcloudimg.com/raw/b5117e831228f59427f03d91a6fdf646.png)
（4）单击【下一步】，可以看到模板策略默认为 `tag:*`。此处我们将 action 修改为 `name/tag:GetResourceTags`、`name/tag:GetResourcesByTags` 和 `name/tag:GetTags` 操作权限，策略语法如下所示。
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/tag:GetResourceTags",
                "name/tag:GetResourcesByTags",
                "name/tag:GetTags"
            ],
            "resource": [
                "*"
            ]
        }
    ]
}
```
（5）单击【创建策略】，即可完成创建。
3. 将策略关联子账号 jason.read。在策略页面，找到步骤2创建的策略，在其右侧单击【关联用户/组】。
4. 在关联用户/组窗口中，勾选子账号 jason.read，并单击【确定】，即可将子账号 jason.read 关联至该策略。
![](https://main.qcloudimg.com/raw/4818cbb813fce18bc8d6fd6062e35e55.png)
5. 子账号 jason.read 登录控制台，在 [存储桶列表](https://console.cloud.tencent.com/cos5/bucket) 页面，选择**标签**并输入**标签键**进行搜索，即可查询到带有此相同标签的存储桶列表，如下图所示。
![](https://main.qcloudimg.com/raw/3f31b5273da16e7728ab40209cfedfa9.png)
