## 接口描述

本接口（UnBindSubDomain）用于解绑自定义域名。
用户使用 API 网关绑定了自定义域名到服务中后，若想要解绑此自定义域名，可使用此接口。

## 输入参数

以下请求参数列表仅列出了接口请求参数，其它参数可参考 [公共请求参数](https://intl.cloud.tencent.com/document/product/628/18814)。

| 参数名称      | 是否必选 | 类型     | 描述          |
| --------- | ---- | ------ | ----------- |
| serviceId | 是    | String | 服务唯一 ID     |
| subDomain | 是    | String | 待解绑的自定义的域名 |

## 输出参数
| 参数名称 | 类型   | 描述                                                         |
| -------- | ------ | ------------------------------------------------------------ |
| code     | Int    | 公共错误码，0表示成功，其他值表示失败。详见错误码页面的 [公共错误码](https://intl.cloud.tencent.com/document/product/628/18822) |
| codeDesc | String | 业务侧错误码。成功时返回 Success，错误时返回具体业务错误原因 |
| message  | String | 模块错误信息描述，与接口相关                                 |


## 示例 
```
https://apigateway.api.qcloud.com/v2/index.php?
&<公共请求参数>
&Action=UnBindSubDomain
&serviceId=service-XXXX
&subDomain=testSubDomain
```
返回示例如下：
```
{
	"code": "0",
	"message": "",
	"codeDesc": "Success"
}
```
