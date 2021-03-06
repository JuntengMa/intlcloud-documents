## Feature Description
This API is used to delete friends. One-way deletion and two-way deletion are both supported.

## API Invocation Description
### Request URL example
```
https://console.tim.qq.com/v4/sns/friend_delete?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### Request parameters

The following table lists and describes only the parameters to be modified when this API is invoked. For details on other parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| v4/sns/friend_delete | The request API. |
| sdkappid | The SDKAppID assigned by the IM console when an app is created. |
| identifier| This must be the app admin account. For details, see [App Admins](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98). |
| usersig | The signature generated by the app admin account. For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | Enter a random 32-bit unsigned integer ranging from 0 to 4294967295. |


### Maximum invocation frequency

The maximum invocation frequency is 200 times per second.

### Request packet examples
- **One-way deletion**
```
{
    "From_Account":"id",
    "To_Account":["id1","id2","id3"],
    "DeleteType":"Delete_Type_Single"
}
```
- **Two-way deletion**
```
{
    "From_Account":"id",
    "To_Account":["id1","id2","id3"],
    "DeleteType":"Delete_Type_Both"
}
```

### Request packet fields

| Field | Type | Attribute | Description |
|----|----|----|-----|
|  From_Account | String | Required | The identifier for which a friend needs to be deleted.  |
| To_Account | Array | Required | The list of identifiers to be deleted. The number of To_Accounts in a single request cannot exceed 1,000. |
| DeleteType | String | Optional | The deletion mode. For details, see [Deleting a Friend](https://intl.cloud.tencent.com/document/product/1047/33521#.E5.88.A0.E9.99.A4.E5.A5.BD.E5.8F.8B). |

### Response packet example
```
{
    "ResultItem":
    [
        {
            "To_Account":"id1",
            "ResultCode":0,
            "ResultInfo":""
        },
        {
            "To_Account":"id2",
            "ResultCode":0,
            "ResultInfo":""
        },
        {
            "To_Account":"id3",
            "ResultCode":0,
            "ResultInfo":""
        }
    ],
    "ActionStatus":"OK",
    "ErrorCode":0,
    "ErrorInfo":"0",
    "ErrorDisplay":""
}
```

### Response packet fields

| Field | Type | Description |
|----|----|-----|
| ResultItem | Array | The result object array for batch friend deletion. |
| To_Account | String | The identifier of the friend to be deleted. |
| ResultCode | Integer | The processing result of To_Account. 0: succeeded. Others: failed. |
| ResultInfo | String | Error description for To_Account. If the processing was successful, the field is empty. |
| ActionStatus | String | The request packet processing result. OK: succeeded. FAIL: failed. |
| ErrorCode | Integer | The error code. 0: succeeded. Others: failed. |
| ErrorInfo | String | Detailed error information. |
| ErrorDisplay | String | Detailed information to be displayed on the client. |


## Error Codes

Unless a network error (such as error 502) occurs, the HTTP return code for this API is always 200. ErrorCode and ErrorInfo in the response packet represent the actual error code and error information, respectively.
For common error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API.

| Error Code | Description |
| ------ | ------------------------------------------------------------ |
| 30001 | A request parameter is incorrect. In this case, check request parameters based on the error description. |
| 30002 | The SDKAppIDs are inconsistent. |
| 30003 | The requested user account does not exist. |
| 30004 | The request requires app admin permissions. |
| 30006 | An internal server error occurred. In this case, try again. |
| 30007 | The network connection timed out. In this case, try again later. |
| 30008 | A write conflict occurred due to concurrent writes. In this case, we recommend that you use the batch mode. |
| 31704 | No friendship exists with the account to be deleted. |
| 31707 | The friend deletion request was filtered by the security policy. In this case, do not initiate friend deletion requests too frequently. |

## API Commissioning Tool
Use the [online commissioning tool for RESTful APIs](https://avc.cloud.tencent.com/im/APITester/APITester.html#v4/sns/friend_delete) to commission this API.

## References
- Adding a friend (<a href="https://intl.cloud.tencent.com/document/product/1047/34902">v4/sns/friend_add</a>)
- Importing friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34903">v4/sns/friend_import</a>)
- Updating friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34904">v4/sns/friend_update</a>)
- Deleting all friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34906">v4/sns/friend_delete_all</a>)
- Verifying friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34907">v4/sns/friend_check</a>)
- Pulling friends (<a href="https://intl.cloud.tencent.com/document/product/1047/34908">v4/sns/friend_get</a>)
- Pulling a specified friend (<a href="https://intl.cloud.tencent.com/document/product/1047/34910">v4/sns/friend_get_list</a>)

## Callbacks That May Be Triggered

<a href="https://intl.cloud.tencent.com/document/product/1047/34360">Callback after deleting a friend</a>
