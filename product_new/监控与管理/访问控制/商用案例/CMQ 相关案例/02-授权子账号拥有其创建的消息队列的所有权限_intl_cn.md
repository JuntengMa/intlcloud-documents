
企业帐号 CompanyExample 下有一个子账号 Developer，该子账号希望其可以访问自己创建的消息队列。

方案A：

企业帐号 CompanyExample 直接将预设策略 QCloudCmqQueueCreaterFullAccess 和 QCloudCmqTopicCreaterFullAccess 授权给子账号 Developer。授权方式请参考 [授权管理](https://intl.cloud.tencent.com/document/product/598/10602)。

方案B：

步骤1：通过策略语法方式创建以下策略。

```
{
    "version": "2.0",
    "statement":
    [
       {
           "effect": "allow",
           "action": "cmqtopic:*",
           "resource": "qcs::cmqtopic:::topicName/uin/${uin}/*"
       },
       {
           "effect": "allow",
           "action": "cmqqueue:*",
           "resource": "qcs::cmqqueue:::queueName/uin/${uin}/*"
       }
    ]
}
```

步骤2：将该策略授权给子账号。授权方式请参考 [授权管理](https://intl.cloud.tencent.com/document/product/598/10602)。

