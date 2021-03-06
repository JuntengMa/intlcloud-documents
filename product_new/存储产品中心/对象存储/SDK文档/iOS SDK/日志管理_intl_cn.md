

## 简介

本文档提供关于日志管理的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                   |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | 设置日志管理 | 为源存储桶开启日志记录     |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | 查询日志管理 | 查询源存储桶的日志配置信息 |

## 设置日志管理

#### 功能说明

PUT Bucket logging 用于为源存储桶开启日志记录，将源存储桶的访问日志保存到指定的目标存储桶中。

#### 方法原型

在开始使用 COS 时，需要在指定的账号下先创建一个存储桶以便于对象的使用和管理，并指定存储桶所属的地域。创建存储桶的用户默认成为存储桶的持有者。若创建存储桶时没有指定访问权限，则默认为私有读写（private）权限。具体步骤如下：    

1. 实例化 QCloudPutBucketLoggingRequest
2. 调用 QCloudCOSXMLService 对象中的 PutBucketLogging 方法发出请求。
3. 从回调的 finishBlock 中的 outputObject 获取具体内容。

#### 请求示例

[//]: # (.cssg-snippet-objc-put-bucket-logging)
```
QCloudPutBucketLoggingRequest *request = [QCloudPutBucketLoggingRequest new];
QCloudBucketLoggingStatus *status = [QCloudBucketLoggingStatus new];
QCloudLoggingEnabled *loggingEnabled = [QCloudLoggingEnabled new];
loggingEnabled.targetBucket = @"examplebucket-1250000000";
loggingEnabled.targetPrefix = @"mylogs";
status.loggingEnabled = loggingEnabled;
request.bucketLoggingStatus = status;
request.bucket = @"examplebucket-1250000000";
[request setFinishBlock:^(id outputObject, NSError *error) {

}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketLogging:request];
```

Swift 代码示例：

[//]: # (.cssg-snippet-swift-put-bucket-logging)
```
let req = QCloudPutBucketLoggingRequest.init();

let status = QCloudBucketLoggingStatus.init();

let loggingEnabled = QCloudLoggingEnabled.init();

loggingEnabled.targetBucket = "examplebucket-1250000000";

loggingEnabled.targetPrefix = "";
status.loggingEnabled = loggingEnabled;
req.bucketLoggingStatus = status;
req.bucket = "examplebucket-1250000000";
req.finishBlock = {(result,error) in

    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
}

QCloudCOSXMLService.defaultCOSXML().putBucketLogging(req);

```

#### 参数说明

#### QCloudPutBucketLoggingRequest 请求参数说明

| 参数名称            | 描述                                                         | 类型                        | 是否必填 |
| ------------------- | ------------------------------------------------------------ | --------------------------- | -------- |
| bucket              | 开启日志功能的源存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | NSString *                  | 是       |
| bucketLoggingStatus | 说明日志记录配置的状态                                       | QCloudBucketLoggingStatus * | 是       |

#### QCloudBucketLoggingStatus 参数说明

| 参数名称       | 描述                                            | 类型                   | 是否必填 |
| -------------- | ----------------------------------------------- | ---------------------- | -------- |
| loggingEnabled | 存储桶 logging 设置的具体信息，主要是目标存储桶 | QCloudLoggingEnabled * | 是       |

#### QCloudLoggingEnabled 参数说明

| 参数名称     | 描述                           | 类型        | 是否必填 |
| ------------ | ------------------------------ | ----------- | -------- |
| targetBucket | 存放日志的目标存储桶           | NSString  * | 是       |
| targetPrefix | 日志存放在目标存储桶的指定路径 | NSString  * | 是       |



## 查询日志管理

#### 功能说明

GET Bucket logging 用于查询指定存储桶的日志配置信息。

#### 方法原型

在开始使用 COS 时，需要在指定的账号下先创建一个存储桶以便于对象的使用和管理，并指定存储桶所属的地域。创建存储桶的用户默认成为存储桶的持有者。若创建存储桶时没有指定访问权限，则默认为私有读写（private）权限。具体步骤如下：    

1. 实例化 QCloudGetBucketLoggingRequest
2. 调用 QCloudCOSXMLService 对象中的 GetBucketLogging 方法发出请求。
3. 从回调的 finishBlock 中的 outputObject 获取具体内容。



#### 请求示例

[//]: # (.cssg-snippet-objc-get-bucket-logging)
```
QCloudGetBucketLoggingRequest *getReq = [QCloudGetBucketLoggingRequest new];
getReq.bucket = @"examplebucket-1250000000";
[getReq setFinishBlock:^(QCloudBucketLoggingStatus * _Nonnull result, NSError * _Nonnull error) {
	NSLog(@"getReq result = %@",result.loggingEnabled.targetBucket);

}];
[[QCloudCOSXMLService defaultCOSXML]GetBucketLogging:getReq];
```

Swift 代码示例：

[//]: # (.cssg-snippet-swift-get-bucket-logging)
```
let req = QCloudGetBucketLoggingRequest.init();
req.bucket = "examplebucket-1250000000";
req.setFinish { (result, error) in

    if error != nil{
        print(error!);
    }else{
        print( result!);
    }
};
QCloudCOSXMLService.defaultCOSXML().getBucketLogging(req);

```

#### 参数说明

#### QCloudGetBucketLoggingRequest 请求参数说明

| 参数名称 | 描述                                                         | 类型       | 是否必填 |
| -------- | ------------------------------------------------------------ | ---------- | -------- |
| bucket   | 存放日志的目标存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | NSString * | 是       |

#### 返回结果说明

#### QCloudBucketLoggingStatus 参数说明

| 参数名称       | 描述                                            | 类型                   |
| -------------- | ----------------------------------------------- | ---------------------- |
| loggingEnabled | 存储桶 logging 设置的具体信息，主要是目标存储桶 | QCloudLoggingEnabled * |

#### 返回错误码说明

当 SDK 请求失败的时候，返回的 error 将不为空，并且包括了错误码、错误描述和其它一些调试必备的信息，以帮助开发者快速解决问题。

返回错误码（封装在返回的 error 里）主要包括两类：设备本身因为网络原因等返回的错误码，以及 COS 返回的错误码。

- 对于设备本身因为网络原因产生的错误码，都是负数并且是四位数，例如-1001，这类错误码由苹果公司定义，了解详情请参见 Foundation 框架中的 NSURLError.h 头文件内的定义，或者是 [苹果官方文档](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes) 说明。
- 对于 COS 返回的错误码，是基于 HTTP 的状态码而来的，也就是404，503这类。对于这类错误码，请参见 API [错误码]( https://intl.cloud.tencent.com/document/product/436/7730)  文档寻求解决方案。
- 对于 SDK 自定义的错误码，均为5位数且都是正数，如10000、20000等。对于这类错误码，请参见 SDK [错误码](https://intl.cloud.tencent.com/document/product/436/30610) 文档寻求解决方案。
