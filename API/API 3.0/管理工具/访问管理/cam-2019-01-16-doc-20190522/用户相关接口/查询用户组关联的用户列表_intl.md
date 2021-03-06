﻿## 1. API Description

API domain name: cam.tencentcloudapi.com.

This API queries the list of users associated with a user group

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/598/33158).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ListUsersForGroup |
| Version | Yes | String | Common parameter; the version of this API: 2019-01-16 |
| Region | No | String | Common parameter; optional for this API. |
| GroupId | Yes | Integer | User group ID. |
| Page | No | Integer | Page number. |
| Rp | No | Integer | Number of entries per page. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalNum | Integer | Total number of users associated with the user group. |
| UserInfo | Array of [GroupMemberInfo](/document/api/598/33167#GroupMemberInfo) | Sub-user information. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Querying the List of Users Associated with a User Group

#### Input Sample Code

```
https://cam.tencentcloudapi.com/?Action=ListUsersForGroup
&GroupId=2020
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalNum": 1,
    "UserInfo": [
      {
        "Uid": 1001408,
        "Uin": 100000545998,
        "Name": "testName",
        "PhoneNum": "",
        "CountryCode": "86",
        "PhoneFlag": 0,
        "Email": "",
        "EmailFlag": 0,
        "UserType": 3,
        "CreateTime": "2018-04-24 15:36:26",
        "IsReceiverOwner": 0
      }
    ],
    "RequestId": "576e68f4-49cf-451b-b717-a584cb68910a"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cam&Version=2019-01-16&Action=ListUsersForGroup)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/598/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| ResourceNotFound.GroupNotExist | The user group does not exist. |
