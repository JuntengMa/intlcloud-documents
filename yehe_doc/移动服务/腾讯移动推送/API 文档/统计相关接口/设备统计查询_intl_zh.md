
## 接口说明
**请求方式**：POST。
**调用频率限制**：200次/小时。

接口请求地址与服务接入点一一对应，请选择与您的应用服务接入点对应的请求地址。

广州服务接入点：
```shell
https://api.tpns.tencent.com/v3/statistics/get_device_stat_overview
```
中国香港服务接入点:
```shell
https://api.tpns.hk.tencent.com/v3/statistics/get_device_stat_overview
```
新加坡服务接入点:
```shell
https://api.tpns.sgp.tencent.com/v3/statistics/get_device_stat_overview
```
上海服务接入点:
```shell
https://api.tpns.sh.tencent.com/v3/statistics/get_device_stat_overview
```
**接口功能**：查询应用某个时间段内每天的“日新增设备数”、“日联网设备数”和“历史累计设备数”。

## 参数说明
#### 请求参数

| 参数名称  | 必选 | 类型   | 描述                                                         |
| --------- | ---- | ------ | ------------------------------------------------------------ |
| startDate | 是   | String | 查询开始日期<li>格式：YYYYMMDD<li>限制：只能查询最近3个月内的数据 |
| endDate   | 是   | String | 查询截止日期，格式：YYYYMMDD                                 |

#### 应答参数

| 参数名称                  | 类型      | 描述                                                |
| ------------------------- | --------- | --------------------------------------------------- |
| retCode                   | Integer       | 返回状态码                                          |
| errMsg                    | String    | 错误信息                                            |
| getDeviceStatOverviewData | Array | 返回结果，getDeviceStatOverviewData 结构变量见下表 |

#### getDeviceStatOverviewData

| 参数名称 | 类型   | 说明           |
| -------- | ------ | -------------- |
| date     | Integer | 数据日期       |
| accuUv   | Integer    | 累积设备量     |
| newUv    | Integer    | 日新增设备量   |
| activeUv | Integer    | 日在线设备峰值 |


## 示例说明
#### 请求示例
```json
{
    "startDate": "20190724",
    "endDate": "20190726"
}
```
#### 应答示例
```json
{
    "retCode": 0,
    "errMsg": "",
    "getDeviceStatOverviewData": [
        {
            "date": 20190724,
            "accuUv": 0,
            "newUv": 0,
            "activeUv": 0
        },
        {
            "date": 20190725,
            "accuUv": 0,
            "newUv": 5,
            "activeUv": 0
        },
        {
            "date": 20190726,
            "accuUv": 5,
            "newUv": 0,
            "activeUv": 2
        }
    ]
}
```

