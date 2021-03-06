﻿以下将描述如何在腾讯移动推送（Tencent Push Notification Service，TPNS）中进行访问管理（Cloud Access Management，CAM）授权。
## TPNS 可授权的资源
资源级权限是指能够指定用户对哪些资源具有执行操作的能力。TPNS 可授权的资源类型为“应用”，意味着您可以以应用为粒度在 CAM 中进行资源级授权，描述方法为：
```
qcs::tpns::uin/1000000000:app/*
```
其中 * 表示以 App 为粒度的所有资源，可替换为 Access ID，应用的 Access ID 可在控制台 TPNS 的 [产品管理](https://console.cloud.tencent.com/tpns) 模块中找到，1000000000 为主账号的腾讯云账号 ID 举例，真实 uin 请在控制台 [账号信息](https://console.cloud.tencent.com/developer) 页面中找到账号 ID 并将之替换。

同时授权多个资源请以逗号（，）分隔。


## TPNS 可授权的操作
在 CAM 策略语句中，您可以从支持 CAM 的任何服务中指定任意的 API 操作。对于 TPNS，请使用以 `name/tpns:` 为前缀的 API，例如：`name/tpns:CreateProduct`。
如果您要在单个语句中指定多个操作的时候，请使用逗号将它们隔开，如下所示：
``` 
"action":["tpns:action1","tpns:action2"]
``` 
您也可以使用通配符指定多项操作。例如，您可以指定名字以单词 "Describe" 开头的所有操作，如下所示：
``` 
"action":["tpns:Describe*"]
``` 
如果您要指定 TPNS 中所有操作，请使用 * 通配符，如下所示：
``` 
"action"：["tpns:*"]
```

可授权操作列表：
>仅支持对支持资源级的操作进行应用的授权。

| 操作名称 | 描述 | 是否支持资源级|
| --- | --- | --- |
| AddChannelInfo | 添加厂商通道 |是|
| CancelPush | 取消定时推送任务 |是|
| CreateApp | 新建应用 |否|
| CreateAppTrialRequest | 申请产品试用 |是|
| CreateProduct | 创建产品 |否|
| DeleteAppInfo | 删除应用 |是|
| DeleteProductInfo | 删除产品 |否|
| DescribeApnsCertInfo | 查询 apns 证书信息 |是|
| DescribeAppAllTags | 查询所有 tag 信息 |是|
| DescribeAppInfo | 查询 App 信息 |是|
| DescribeAppVipInfo | 查询 Vip 信息 |是|
| DescribeChannelInfo | 查询厂商通道信息 |是|
| DescribeProductInfo | 查询产品信息 |否|
| DescribeTagTokenNums | 查询 tag 下面的设备数量 |是|
| DownloadPushPackage | 推送号码包下载 |是|
| DescribeAccountByToken | 查询设备上绑定的账号 |是|
| DescribeAccountPushStatInfo | 查询账号下总推送量 |否|
| DescribeAccountPushStatInfoAllZone | 查询所有集群下各应用的应发消息总量 |否|
| DescribeAppSecretInfo | 查询AppSecret信息 |是|
| DescribeDeviceStatOverview | 查询应用累积和日活设备概览数 |是|
| DescribeProductDeviceStatWithRatioOverview | 查询应用对应的统计信息 |是|
| DescribePushPackaDescribeoken | 上传号码包获取 COS 临时 token |是|
| DescribePushTaskGroupStatAllChannel | 查询各通道推送的聚合数据 |是|
| DescribePushTaskStatAllChannel | 查询各个推送通道的数据 |是|
| DescribeTagsByToken | 查询设备上绑定的标签 |是|
| DescribeTokenInfos | 查询 tokenInfo 信息 |否|
| DescribePushInfos | 查询推送列表 |是|
| ModifyAppInfo | 更新应用信息 |是|
| ModifyProductInfo | 更新产品信息 |否|
| CreatePush | 创建推送 |是|
| UpdateAppStatus | 更新应用状态 |是|
| UploadCert | iOS证书上传 |是|
| UploadPushPackage | 推送号码包上传 |是|

## 示例-运营人员策略
下面按照日常推送运营人员的权限提供策略语法示例，假设应用创建人的个人账号信息中，账号 ID/uin 为1000000000，我们给运营人员开通子账号，并授以应用 Access ID 为1500000000 的以下操作权限：
- 所有查询操作。
- 取消定时推送任务。
- 创建推送。
- 推送号码包上传接口。
- 推送号码包下载。


对应的策略语法则为：
（实际创建时，请注意先将注释删除）
```
//授权运营人员以特定应用的操作权限
{
    "version": "2.0",
    "statement": [
        { //对支持资源级授权的操作进行授权
            "action": [
                "tpns:Describe*",
                "tpns:CancelPush",
                "tpns:DownloadPushPackage",
                "tpns:CreatePush",
                "tpns:UploadPushPackage"
            ],
            "resource": [
                "qcs::tpns::uin/1000000000:app/1500000000"
            ],
            "effect": "allow"
        },
        { //对不支持资源级授权的操作进行授权，此段申明为每次授权必填项
            "action": [
                "tpns:Describe*"
            ],
            "resource": [
                "qcs::tpns::uin/1000000000:other/*"
            ],
            "effect": "allow"
        }

     ]
}
```

创建策略完成后，可以在 CAM [策略管理](https://console.cloud.tencent.com/cam/policy) 中找到该策略并将其关联到子用户，完成权限配置。
