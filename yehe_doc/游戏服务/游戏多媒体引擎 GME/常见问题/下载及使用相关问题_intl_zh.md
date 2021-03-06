### 如何下载 GME Demo 及 SDK？

请参考 [下载指引](https://intl.cloud.tencent.com/document/product/607/18521) 文档，下载相关 Demo 及 SDK。目前官网有 Unity 引擎 Demo，Cocos2D 引擎 Demo，Android 原生开发 Demo 及 iOS 原生开发 Demo。

### GME Demo 下载后，如何更换账号？
- 需要在控制台获取两个号码，分别为 SDKAppID、权限密钥。
- 使用客户自己申请的 AppID 的话需要在 AVChatViewController 中的 GetAuthBuffer 中修改实时语音的 Key。

### 房间内只有一个人，如何在本地体验效果？
如果要体验效果，请在另一个终端设备使用 demo 进入同一房间即可。

### 使用 Demo 时，报错：errinfo=priv map info error，怎么办？
相关进房参数出现错误，请检查 SDKAppID、权限密钥 是否已经替换。

### 如何使用已下载的 Demo？
您可以参考 Demo 使用文档。

### 如何取得日志？
**提供日志的时候，请同时提供出现问题的相关时间点。**
QAVSDK_ 带日期 .log，这个文件为日志文件。目录如下：

| 平台    | 路径                                                         |
| ------- | ------------------------------------------------------------ |
| Windows | %appdata%\Tencent\GME\ProcessName                            |
| iOS     | Application/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/Documents   |
| Android | /sdcard/Android/data/xxx.xxx.xxx/files                       |
| Mac     | /Users/username/Library/Containers/xxx.xxx.xxx/Data/Documents |


### 为什么下载的 SDK 文档和 Demo 里没有 Authbuffer 文件。
Authbuffer 此文件已合并，请在 SDK 里面全局搜索一下。


### tea 加密有没有 lib 文件？
我们为您提供 [Authbuffer 编译文档及 zip 包](https://intl.cloud.tencent.com/document/product/607/31461) 。


### cocos2d-x 版本与 Android、iOS 原生版本的 SDK，是否存在运行效率的区别？
运行效率上没有区别。


### 集成 GME SDK 并导出 Apk 后，启动程序发生黑屏现象，如何解决？
问题在于缺失了某些 lib 文件，请解压 Apk 后查看 lib 下的各个文件夹中库文件是否齐全。

### iOS SDK 支不支持模拟器调试？
支持的，请用官网最新包验证。

### 在 Xcode 导出可执行文件时，已添加 GMESDK.framework 库，编译时出现编译报错，如何解决？
工程文件中选择 Build Setting，在 "Other Linker Flags" 中，如果有使用 “-all_load” 标志的话，尝试删掉并重新编译。


### 使用 Unity SDK 后，导出 iOS 可执行文件时报错，提示与 armv7 相关，删除 armv7 后恢复正常，如何解决？
建议升级 Unity 版本，参考 [Unity 官网链接](https://forum.unity.com/threads/undefined-symbols-for-architecture-armv7-query_call_back-callback_func_type.830544/#post-5590516)。
如果您没有升级需求的话，不打包 armv7 架构即可。

### 下载 iOS Demo 后无法运行，如何解决？
下载官方 iOS Demo 后，在 Xcode（版本为10以上） 编译时出现类似“ld: warning: directory not found for option”等错误，需手动将 Demo 同级目录下的 “GME_SDK” 文件夹下的 “GMESDK.framework” 文件添加到工程的 Framework 列表中。

### 下载 Unity Demo 导出 PC 可执行文件时报错，如何处理？
如果使用过程中有 Found plugins with same names and architectures 类似报错，因为 GME SDK 默认提供 x86 架构的 SDK 版本及 x86_64 架构的 SDK 版本，请在 plugins 文件夹中删除其中一份。

### 下载 Unreal Demo 导出 PC 可执行文件时提示找不到dll，如何解决？
以导出 Windows x64 版本为例，导出可执行文件之后，将工程目录`UEDemo1\Plugins\GMESDK\Source\ThirdParty\GMESDKLibrary\x64`下的 dll 文件全量拷贝到可执行文件（.exe）同目录下。

### Windows 客户端需使用其他的播放器软件进行播放伴奏，例如 QQ 播放器，应如何解决？
请参考 Windows 平台播放器伴奏功能 进行调用。第三方播放器伴奏功能属于高级接口，需要 [提交工单](https://console.cloud.tencent.com/workorder/category)，并提供 tmg_adv_win.h 头文件。


