## 操作场景
通过推流配置可以生成您在对应推流域名下的推流地址，往推流地址进行推流实现直播流传输到云直播服务，即实现直播视频上传。

## 前提条件
- 已登录 [云直播控制台](https://console.cloud.tencent.com/live)。
- 已添加 推流域名。

## 推流地址生成器
1. 进入[【域名管理】](https://console.cloud.tencent.com/live/domainmanage)选择需配置的推流域名或单击【管理】，进入域名详情页。
![](https://main.qcloudimg.com/raw/88a070c73b1bcd6a04195da768ace0c7.png)
2. 选择【推流配置】>【推流地址生成器】，进行如下配置：
	1. 选择过期时间，例如：`2019-10-31 23:59:59`。
	2. 填写自定义的流名称 StreamName，例如：`liveteststream`。
	3. 单击【生成推流地址】即可生成带着 StreamName 的 RTMP 推流地址。
![](https://main.qcloudimg.com/raw/29e4a0af31d1b37d91f6618453b6cc81.png)
>RTMP 推流地址格式为`rtmp://domain/live/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`，其中：
		- `domain`：直播推流域名。
		- `AppName`：直播的应用名称，默认为 live，可自定义。
		- `StreamName`：流名称，用户自定义，用于标识直播流。
		- `txSecret`：开启推流鉴权后生成的鉴权串。
		- `txTime`：推流地址设置的时间戳，是控制台推流地址的有效时间。

3. 您可在根据业务场景实现 [直播推流](https://intl.cloud.tencent.com/document/product/267/31558) 后，在 [流管理](https://intl.cloud.tencent.com/document/product/267/31068) 进行测试、禁用和删除。

> 
>- 生成的推流地址在设定的过期时间内均可使用，过期后可以重新生成新的推流地址。
>- 生成推流地址即可进行直播推流开播，但是观看直播要获取播放地址，具体请参见 [播放配置](https://intl.cloud.tencent.com/document/product/267/31058)。


## 推流地址示例代码
腾讯云为您提供的 PHP 和 Java 语言的推流地址示例代码，您可直接参考示例代码完成推流地址的接入。具体查看操作如下：
1. 进入【[域名管理](https://console.cloud.tencent.com/live/domainmanage)】。
2. 选择推流域名或单击右侧的【管理】，进入域名详情页。
3. 选择【推流配置】，下拉到底查看【推流地址示例代码】标签。
4. 单击切换标签按钮查看 PHP/Java 示例代码。

**推流示例代码（PHP）：**
```
/**
    * 获取推流地址
    * 如果不传key和过期时间，将返回不含防盗链的url
    * @param domain 您用来推流的域名
    *        streamName 您用来区别不同推流地址的唯一流名称
    *        key 安全密钥
    *        time 过期时间 sample 2016-11-12 12:00:00
    * @return String url
*/
function getPushUrl($domain, $streamName, $key = null, $time = null){
	if($key && $time){
		$txTime = strtoupper(base_convert(strtotime($time),10,16));
		//txSecret = MD5( KEY + streamName + txTime )
		$txSecret = md5($key.$streamName.$txTime);
		$ext_str = "?".http_build_query(array(
			       "txSecret"=> $txSecret,
			       "txTime"=> $txTime
		));
    }
	return "rtmp://".$domain."/live/".$streamName . (isset($ext_str) ? $ext_str : "");
}
echo getPushUrl("123.test.com","123456","69e0daf7234b01f257a7adb9f807ae9f","2016-09-11 20:08:07");
```
**推流示例代码（Java）：**
```
package com.test;
import java.io.UnsupportedEncodingException;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
public class Test {
    public static void main(String[] args) {
        System.out.println(getSafeUrl("txrtmp", "11212122", 1469762325L));
    }
    private static final char[] DIGITS_LOWER =
        {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f'};
    /*
    * KEY+ streamName + txTime
    */
    private static String getSafeUrl(String key, String streamName, long txTime) {
        String input = new StringBuilder().
                            append(key).
                            append(streamName).
                            append(Long.toHexString(txTime).toUpperCase()).toString();
        String txSecret = null;
        try {
            MessageDigest messageDigest = MessageDigest.getInstance("MD5");
            txSecret  = byteArrayToHexString(
                        messageDigest.digest(input.getBytes("UTF-8")));
        } catch (NoSuchAlgorithmException e) {
                e.printStackTrace();
        } catch (UnsupportedEncodingException e) {
                e.printStackTrace();
        }
        return txSecret == null ? "" :
                           new StringBuilder().
                           append("txSecret=").
                           append(txSecret).
                           append("&").
                           append("txTime=").
                           append(Long.toHexString(txTime).toUpperCase()).
                           toString();
        }
    private static String byteArrayToHexString(byte[] data) {
        char[] out = new char[data.length << 1];
        for (int i = 0, j = 0; i < data.length; i++) {
                out[j++] = DIGITS_LOWER[(0xF0 & data[i]) >>> 4];
                out[j++] = DIGITS_LOWER[0x0F & data[i]];
        }
        return new String(out);
    }
}
```
