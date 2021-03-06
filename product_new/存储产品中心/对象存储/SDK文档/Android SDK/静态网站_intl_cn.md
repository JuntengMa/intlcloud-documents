

## 简介

本文档提供关于静态网站的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名           | 操作描述                 |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | 设置静态网站     | 设置存储桶的静态网站配置 |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | 查询静态网站配置 | 查询存储桶的静态网站配置 |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | 删除静态网站配置 | 删除存储桶的静态网站配置 |

## 设置静态网站

#### 功能说明

PUT Bucket website 用于为存储桶配置静态网站。

#### 方法原型

```
PutBucketWebsiteResult putBucketWebsite(PutBucketWebsiteRequest request) throws CosXmlClientException, CosXmlServiceException;

void putBucketWebsiteAsync(PutBucketWebsiteRequest request,  CosXmlResultListener cosXmlResultListener);
```

#### 请求示例

```
String bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
PutBucketWebsiteRequest putBucketWebsiteRequest = new PutBucketWebsiteRequest(bucket);
putBucketWebsiteRequest.setIndexDocument("index.html");

// 使用同步方法
try {
    PutBucketWebsiteResult putBucketWebsiteResult = cosXmlService.putBucketWebsite(putBucketWebsiteRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 使用异步回调请求
cosXmlService.putBucketWebsiteAsync(putBucketWebsiteRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        PutBucketWebsiteResult putBucketWebsiteResult = (PutBucketWebsiteResult) result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### 参数说明

| 参数名称             | 描述                                                         | 类型   |
| -------------------- | ------------------------------------------------------------ | ------ |
| bucket               | 设置静态网站的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| IndexDocument        | 索引文档                                                     | String |
| ErrorDocument        | 错误文档                                                     | String |
| RedirectAllRequestTo | 重定向所有请求                                               | String |
| RoutingRules         | 重定向规则                                                   | List   |

#### 返回结果说明

| 成员变量 | 描述                                                     | 类型 |
| -------- | -------------------------------------------------------- | ---- |
| httpCode | HTTP Code， [200, 300)之间表示操作成功，否则表示操作失败 | int  |

## 查询静态网站配置

#### 功能说明

GET Bucket website 用于查询与存储桶关联的静态网站配置信息。

#### 方法原型

```
GetBucketWebsiteResult getBucketWebsite(GetBucketWebsiteRequest request)throws CosXmlClientException, CosXmlServiceException;

void getBucketWebsiteAsync(GetBucketWebsiteRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 请求示例

```
String bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
GetBucketWebsiteRequest getBucketWebsiteRequest = new GetBucketWebsiteRequest(bucket);
//设置签名校验 Host, 默认校验所有 Header
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
getBucketWebsiteRequest.setSignParamsAndHeaders(null, headerKeys);
// 使用同步方法
try {
    GetBucketWebsiteResult getBucketWebsiteResult = cosXmlService.getBucketWebsite(getBucketWebsiteRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 使用异步回调请求
cosXmlService.getBucketWebsiteAsync(getBucketWebsiteRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        GetBucketWebsiteResult getBucketWebsiteResult = (GetBucketWebsiteResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### 参数说明

| 参数名称 | 描述                                                         | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| bucket   | 查询静态网站配置的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果说明

| 成员变量             | 描述                                                     | 类型                 |
| -------------------- | -------------------------------------------------------- | -------------------- |
| httpCode             | HTTP Code， [200, 300)之间表示操作成功，否则表示操作失败 | int                  |
| websiteConfiguration | 返回 Bucket 对象 WebsiteConfiguration 信息               | WebsiteConfiguration |

## 删除静态网站配置

#### 功能说明

DELETE Bucket website 用于删除存储桶中的静态网站配置。

#### 方法原型

```
DeleteBucketWebsiteResult deleteBucketWebsite(DeleteBucketWebsiteRequest request) throws CosXmlClientException, CosXmlServiceException;

void deleteBucketWebsiteAsync(DeleteBucketWebsiteRequest request, CosXmlResultListener cosXmlResultListener);
```

#### 请求示例

```
String bucket = "examplebucket-1250000000"; //格式：BucketName-APPID
DeleteBucketWebsiteRequest deleteBucketWebsiteRequest = new DeleteBucketWebsiteRequest(bucket);
//设置签名校验 Host, 默认校验所有 Header
Set<String> headerKeys = new HashSet<>();
headerKeys.add("Host");
deleteBucketWebsiteRequest.setSignParamsAndHeaders(null, headerKeys);
// 使用同步方法
try {
    DeleteBucketWebsiteResult deleteBucketWebsiteResult = cosXmlService.deleteBucketWebsite(deleteBucketWebsiteRequest);
} catch (CosXmlClientException e) {
    e.printStackTrace();
} catch (CosXmlServiceException e) {
    e.printStackTrace();
}

// 使用异步回调请求
cosXmlService.deleteBucketWebsiteAsync(deleteBucketWebsiteRequest, new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        DeleteBucketWebsiteResult getBucketWebsiteResult = (DeleteBucketWebsiteResult)result;
    }

    @Override
    public void onFail(CosXmlRequest cosXmlRequest, CosXmlClientException clientException, CosXmlServiceException serviceException)  {
    }
});
```

#### 参数说明

| 参数名称 | 描述                                                         | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| bucket   | 被删除静态网站配置的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果说明

| 成员变量 | 描述                                                     | 类型 |
| -------- | -------------------------------------------------------- | ---- |
| httpCode | HTTP Code， [200, 300)之间表示操作成功，否则表示操作失败 | int  |
