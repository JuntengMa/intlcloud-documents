<span id="push"></span>
### 推流
 主播将本地视频源和音频源推送到腾讯视频云服务器，在有些场景中也被称为“RTMP 发布”。 
<span id="play"></span>
### 拉流
 拉流（直播播放）视频源是实时生成的，有人推流直播才有意义，一旦主播停播，直播 URL 也就失效了，而且由于是实时直播，所以播放器在播直播视频的时候是没有进度条的。 
<span id="push_domain"></span>
### 推流域名
指用于推送直播流的域名，必选配置，该域名必须在使用直播服务前完成注册并备案。配置完推流域名后，直播服务会生成对应的推流地址。
<span id="play_domain"></span>
### 播放域名
指用于播放直播流的域名，必选配置，该域名必须在使用直播服务前完成注册并备案。配置完播放域名后，直播服务会生成对应的播放地址。
<span id="cname"></span>
### 域名 CNAME
CNAME 域名是在腾讯云直播控制台接入加速域名后，系统给对应的域名分配一个以`.liveplay.myqcloud.com`为后缀的域名。用户需要在域名服务商处，配置一条 CNAME 记录，记录生效后，域名解析的工作就正式转向腾讯云云直播，该域名所有的请求都将转向腾讯云直播的边缘节点。
<span id="streamname"></span>
### StreamName
StreamName 是一路流的标识符，通常与某个域名一起唯一标识一路流。
<span id="appname"></span>
### AppName
直播的应用名称，用于区分直播流媒体文件存放路径，默认为 live，可自定义。
<span id="trans"></span>
### 转码
转码是将视频码流转换成另一个视频码流的过程，是一种离线任务。通过转码，可以改变原始码流的编码格式、分辨率和码率等参数，从而适应不同终端和网络环境的播放。使用转码功能可以实现：
- 适配更多终端：将原始视频转码成拥有更强终端适配能力的格式，使视频资源能够在更多设备上播放。
- 适配不同带宽：将视频转换成流畅、标清、高清或超清输出，用户可根据当前网络环境选择合适码率的视频播放。
- 节省带宽：采用更先进的编码方式转码，在不损失原始画质的情况下显著降低码率，节省播放带宽。
<span id="h264"></span>
### H.264
H.264 是由 ITU-T 视频编码专家组（VCEG）和 ISO/IEC 动态图像专家组（MPEG）联合组成的联合视频组（JVT，Joint Video Team）提出的高度压缩数字视频编解码器标准，同时也是 MPEG-4 第十部分。使用 H.264 转码优势如下：
- 可低于1Mbps的速度实现标清（分辨率在1280P*720以下）数字图像传送。
- 与其它现有的视频编码标准相比，在相同的带宽下提供更加优秀的图像质量。
- 既保留了以往压缩技术的优点和精华又具有其他压缩技术无法比拟的优点。
<span id="h265"></span>
### H.265
H.265 标准围绕着现有的视频编码标准 H.264，保留部分技术，同时优化改进。使用 H.265 转码优势如下：
- 可利用1Mbps - 2Mbps的传输速度传送720P（分辨率1280*720）普通高清音视频传送。
- 改善码流、编码质量、延时和算法复杂度之间的关系，达到最优化设置。

<span id="message"></span>
### 事件消息通知
指推流过程中，直播触发事件通知，腾讯云按照配置模板信息主动发送请求到客户的服务器，客户的服务器负责应答验证请求，相关应答协议请参见 [事件消息通知协议](https://intl.cloud.tencent.com/document/product/267/31566)。验证通过后即可获取包含回调信息的 JSON 数据包，获取后请解析并记录相关信息。 
<span id="link"></span>
### 防盗链
 指推流和播放 URL 中的 txSecret 字段，可防止攻击者伪造您的后台生成推流 URL 或者非法盗取您的播放地址进行谋利。

 <span id="record"></span>
 ### 直播录制
在推流过程中，将直播原始流经过转音视频封装（不修改音频、视频数据以及对应的时间戳等信息）得到的视频文件存储到云点播平台。使用该功能需提前开通 [云点播服务](https://intl.cloud.tencent.com/product/vod)。

 <span id="watermark"></span>
### 水印
在直播推流过程中，为保证视频版权不受侵犯，在转码过程中将设置好的水印合并到视频流中输出一个带有水印的视频流，水印内容可以为文字或图片。

 <span id="screenshot"></span>
### 截图
以固定时间间隔将直播推流视频画面截取下来，形成图片文件存储在对象存储 COS 中。开通截图功能需要先在您的 COS bucket 中授权云直播服务的数据写入权限，详情可参见 [COS bucket 授权给直播实现截图存储](https://intl.cloud.tencent.com/document/product/267/33384)。 

 <span id="yellow_confidence"></span>
### 鉴黄
基于截图功能，系统通过推流域名已关联的截图鉴黄模板，鉴别直播推流过程中主播是否出现违规的直播内容。相关文档可参见 [截图鉴黄配置](https://intl.cloud.tencent.com/document/product/267/31072)。

 
