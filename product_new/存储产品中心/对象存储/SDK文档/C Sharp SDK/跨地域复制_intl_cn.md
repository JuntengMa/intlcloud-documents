## 简介

本文档提供关于跨地域复制的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | 设置跨地域复制 | 设置存储桶的跨地域复制规则 |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | 查询跨地域复制 | 查询存储桶的跨地域复制规则 |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | 删除跨地域复制 | 删除存储桶的跨地域复制规则 |

## 设置跨地域复制

#### 功能说明

设置指定存储桶的跨地域复制规则。

#### 方法原型

```C#
PutBucketReplicationResult PutBucketReplication(PutBucketReplicationRequest request);
void PutBucketReplication(PutBucketReplicationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 请求示例

[//]: # (.cssg-snippet-put-bucket-replication)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  //设置连接超时时间，单位毫秒，默认45000ms
  .SetReadWriteTimeoutMs(40000)  //设置读写超时时间，单位毫秒，默认45000ms
  .IsHttps(true)  //设置默认 HTTPS 请求
  .SetAppid("1250000000") //设置腾讯云账户的账户标识 APPID
  .SetRegion("COS_REGION") //设置一个默认的存储桶地域
  .Build();

string secretId = "COS_SECRETID";   //云 API 密钥 SecretId
string secretKey = "COS_SECRETKEY"; //云 API 密钥 SecretKey
long durationSecond = 600;          //每次请求签名有效时长，单位为秒
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

string bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
string ownerUin = "100000000001"; //发起者身份标示: OwnerUin
string subUin = "100000000001"; //发起者身份标示: SubUin
PutBucketReplicationRequest request = new PutBucketReplicationRequest(bucket);
//设置 replication
PutBucketReplicationRequest.RuleStruct ruleStruct = 
  new PutBucketReplicationRequest.RuleStruct();
ruleStruct.id = "replication_01"; //用来标注具体 Rule 的名称
ruleStruct.isEnable = true; //标识 Rule 是否生效 :true, 生效； false, 不生效
ruleStruct.appid = "1250000000"; //APPID
ruleStruct.region = "ap-beijing"; //目标存储桶地域信息
ruleStruct.bucket = "destinationbucket-1250000000"; //格式：BucketName-APPID
ruleStruct.prefix = "34"; //前缀匹配策略
List<PutBucketReplicationRequest.RuleStruct> ruleStructs = 
  new List<PutBucketReplicationRequest.RuleStruct>();
ruleStructs.Add(ruleStruct);
request.SetReplicationConfiguration(ownerUin, subUin, ruleStructs);

// 使用同步方法
try
{
  PutBucketReplicationResult result = cosXml.PutBucketReplication(request);
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

#### 参数说明
| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| bucket  | 源存储桶，格式：BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | string                         |
| ownerUin  |发起者身份标示：OwnerUin  | string |
| subUin  |发起者身份标示：SubUin    | string |
| ruleStruct  |签名的请求参数    | RuleStruct |
| signStartTimeSecond | 签名有效期起始时间（Unix 时间戳），例如1557902800                 | long           |
| durationSecond      | 签名有效期时长（单位为秒），例如签名有效时期为1分钟：60                     | long           |
| headerKeys          | 签名的请求头                | `List<string>` |
| queryParameterKeys  | 签名的请求参数    | `List<string>` |


#### 返回结果说明
通过 PutBucketReplicationResult 返回请求结果。

| 成员变量 | 类型 | 描述                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP Code， [200，300)之间表示操作成功，否则表示操作失败 |

>操作失败时，系统将抛出 [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) 或 [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) 异常。




## 查询跨地域复制

#### 功能说明

查询指定存储桶的跨地域复制规则。

#### 方法原型
```C#
GetBucketReplicationResult GetBucketReplication(GetBucketReplicationRequest request);
void GetBucketReplication(GetBucketReplicationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 请求示例
[//]: # (.cssg-snippet-get-bucket-replication)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  //设置连接超时时间，单位毫秒，默认45000ms
  .SetReadWriteTimeoutMs(40000)  //设置读写超时时间，单位毫秒，默认45000ms
  .IsHttps(true)  //设置默认 HTTPS 请求
  .SetAppid("1250000000") //设置腾讯云账户的账户标识 APPID
  .SetRegion("COS_REGION") //设置一个默认的存储桶地域
  .Build();

string secretId = "COS_SECRETID";   //云 API 密钥 SecretId
string secretKey = "COS_SECRETKEY"; //云 API 密钥 SecretKey
long durationSecond = 600;          //每次请求签名有效时长，单位为秒
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

string bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
GetBucketReplicationRequest request = new GetBucketReplicationRequest(bucket);

//使用同步方法
try
{
  GetBucketReplicationResult result = cosXml.GetBucketReplication(request);
  // 存储桶的跨区域复制配置
  ReplicationConfiguration conf =  result.replicationConfiguration;
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

#### 参数说明
| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| bucket  | 查询跨地域复制的存储桶，格式：BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | string                         |
| signStartTimeSecond | 签名有效期起始时间（Unix 时间戳），例如1557902800                 | long           |
| durationSecond      | 签名有效期时长（单位为秒），例如签名有效时期为1分钟：60                     | long           |
| headerKeys          | 签名的请求头                | `List<string>` |
| queryParameterKeys  | 签名的请求参数    | `List<string>` |

#### 返回结果说明
通过 GetBucketReplicationResult 返回请求结果。

| 成员变量 | 类型 | 描述                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP Code， [200，300)之间表示操作成功，否则表示操作失败 |
|replicationConfiguration|[ReplicationConfiguration](https://github.com/tencentyun/qcloud-sdk-dotnet/blob/master/QCloudCSharpSDK/COSXML/Model/Tag/ReplicationConfiguration.cs)|跨地域配置信息|


>操作失败时，系统将抛出 [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) 或 [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) 异常。


## 删除跨地域复制

#### 功能说明

删除指定存储桶的跨地域复制规则。

#### 方法原型
```C#
DeleteBucketReplicationResult DeleteBucketReplication(DeleteBucketReplicationRequest request);
void DeleteBucketReplication(DeleteBucketReplicationRequest request, COSXML.Callback.OnSuccessCallback<CosResult> successCallback, COSXML.Callback.OnFailedCallback failCallback);
```

#### 请求示例
[//]: # (.cssg-snippet-delete-bucket-replication)
```C#
CosXmlConfig config = new CosXmlConfig.Builder()
  .SetConnectionTimeoutMs(60000)  //设置连接超时时间，单位毫秒，默认45000ms
  .SetReadWriteTimeoutMs(40000)  //设置读写超时时间，单位毫秒，默认45000ms
  .IsHttps(true)  //设置默认 HTTPS 请求
  .SetAppid("1250000000") //设置腾讯云账户的账户标识 APPID
  .SetRegion("COS_REGION") //设置一个默认的存储桶地域
  .Build();

string secretId = "COS_SECRETID";   //云 API 密钥 SecretId
string secretKey = "COS_SECRETKEY"; //云 API 密钥 SecretKey
long durationSecond = 600;          //每次请求签名有效时长，单位为秒
QCloudCredentialProvider qCloudCredentialProvider = new DefaultQCloudCredentialProvider(secretId, 
  secretKey, durationSecond);

CosXml cosXml = new CosXmlServer(config, qCloudCredentialProvider);

string bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
DeleteBucketReplicationRequest request = new DeleteBucketReplicationRequest(bucket);

//使用同步方法
try
{
  DeleteBucketReplicationResult result = cosXml.DeleteBucketReplication(request);
  Console.WriteLine(result.GetResultInfo());
}
catch (COSXML.CosException.CosClientException clientEx)
{
  Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
  Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

#### 参数说明

| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| bucket  | 删除跨地域复制的存储桶，格式：BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | string                         |
| signStartTimeSecond | 签名有效期起始时间（Unix 时间戳），例如1557902800                 | long           |
| durationSecond      | 签名有效期时长（单位为秒），例如签名有效时期为1分钟：60                     | long           |
| headerKeys          | 签名的请求头                | `List<string>` |
| queryParameterKeys  | 签名的请求参数    | `List<string>` |


#### 返回结果说明
通过 DeleteBucketReplicationResult 返回请求结果。

| 成员变量 | 类型 | 描述                                                     |
| -------- | ---- | -------------------------------------------------------- |
| httpCode | int  | HTTP Code， [200，300)之间表示操作成功，否则表示操作失败 |

>操作失败时，系统将抛出 [CosClientException](https://intl.cloud.tencent.com/document/product/436/30599) 或 [CosServerException](https://intl.cloud.tencent.com/document/product/436/30599) 异常。
