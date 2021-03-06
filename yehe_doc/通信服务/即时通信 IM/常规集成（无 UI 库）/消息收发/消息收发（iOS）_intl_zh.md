## 消息的分类
腾讯云 IM 消息按照消息的发送目标可以分为：“单聊消息”（又称 “C2C 消息”）和“群聊消息” 两种：

| 消息分类 | API 关键词 | 详细解释 |
|---------|---------|---------|
| 单聊消息 | C2CMessage | 又称 C2C 消息，在发送时需要指定消息接收者的 UserID，只有接受者可以收到该消息。 |
| 群聊消息 | GroupMessage | 在发送时需要指定目标群组的 groupID，该群中的所有用户均能收到消息。|

按照消息承载的内容可以分为：“文本消息”、“自定义（信令）消息”，“图片消息”、“视频消息”、“语音消息”、“文件消息”、“位置消息”、“群 Tips 消息”等几种类型。

| 消息分类 | API 关键词 | 详细解释 |
|---------|---------|---------|
| 文本消息 | TextElem | 即普通的文字消息，该类消息会经过腾讯云 IM 的敏感词过滤，包含的敏感词消息在发送时会报80001错误码。 |
| 自定义消息 | CustomElem | 即一段二进制 buffer，通常用于传输您应用中的自定义信令，内容不会经过敏感词过滤。 |
| 图片消息 | ImageElem | SDK 会在发送原始图片的同时，自动生成两种不同尺寸的缩略图，三张图分别被称为原图、大图、微缩图。 |
| 视频消息 | VideoElem | 一条视频消息包含一个视频文件和一张配套的缩略图。 |
| 语音消息 | SoundElem | 支持语音是否播放红点展示。 |
| 文件消息 | FileElem | 文件消息最大支持100MB。 |
| 位置消息 | LocationElem | 地理位置消息由位置描述、经度（longitude ）和维度（latitude）三个字段组成。 |
| 群 Tips 消息 | GroupTipsElem | 群 Tips 消息常被用于承载群中的系统性通知消息，例如有成员进出群组，群的描述信息被修改，群成员的资料发生变化等。 |

## 收发简单消息
[V2TIMManager.h](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html) 中提供了一组简单的消息收发接口，虽只能用于文本消息和自定义（信令）消息的收发，但使用方法特别简单，只需要几分钟即可完成对接。

### 发送文本和信令消息（简化接口）
调用 [sendC2CTextMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a50d63810093eccc0491d058d0b883618) 或者  [sendGroupTextMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a07788874071937fac6c7093185b145f7) 可以发送文本消息，其中文本消息会经过即时通信 IM 的敏感词过滤，包含的敏感词消息在发送时会报80001错误码。
调用 [sendC2CCustomMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a5fc3b87e9782e679c08926d07e486b90) 或者 [sendGroupCustomMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a537560a58d49aad36406f6d9db6ded65) 可以发送 C2C 自定义（信令）消息，自定义消息本质是一段二进制 buffer，通常用于传输您应用中的自定义信令，内容不会经过敏感词过滤。

### 接收文本和信令消息（简化接口）
通过  [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68) 可以监听简单的文本和信令消息，复杂的图片、视频、语音消息则需要通过 [V2TIMManager + Message.h](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html) 中定义的 [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) 实现。

> [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68)  与 [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) 请勿混用，以免产生逻辑 BUG。

### 经典示例：直播群中收发弹幕消息
直播场景下，在直播群中收发弹幕消息是非常普遍的交互方式，其实现方式非常简单，通过简单消息接口即可满足：

1. 主播调用 [createGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a3bbcf819c1ec70e520b7f9a42cfbb989) 创建一个直播群（AVChatRoom），并在“正在直播”的房间列表中记录群组 ID。
2. 观众选择自己喜欢的主播，并调用 [joinGroup](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a) 加入该主播创建的直播群。
3. 消息的发送方可以通过 [sendGroupTextMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a07788874071937fac6c7093185b145f7) 群发弹幕文本消息。
4. 消息的接收方可以通过 [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68) 注册简单消息监听器，并通过监听回调函数  [onRecvGroupTextMessage](http://doc.qcloudtrtc.com/im/protocolV2TIMSimpleMsgListener-p.html) 获取文本消息。

为直播间增加“点赞飘心”的功能，“点赞飘心”属于一条指令，操作步骤如下：
1. 定义一个的自定义消息类型，例如一个 JSON 字符串：` { "command": "favor", "value": 101 }`。
2. 通过 [sendGroupCustomMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a537560a58d49aad36406f6d9db6ded65) 接口进行消息的发送，并通过  [onRecvGroupCustomMessage](http://doc.qcloudtrtc.com/im/protocolV2TIMSimpleMsgListener-p.html#ad01776119c059bff49b804c8152c70d9) 进行接收。

## 收发富媒体消息
图片、视频、语音、文件、地理位置等类型的消息称为“富媒体消息”。相比于简单消息，富媒体消息的收发相对复杂：
- 在发送时，富媒体消息需要先用对应的 `create` 函数创建一个  [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html) 对象，再调用对应的 `send` 接口发送。
- 在接收时，富媒体消息需要先判断 `elemType`，并根据 `elemType` 获取对应的 `Elem` 进行二次解析。


### 发送富媒体消息
本文以图片消息为例，介绍发送一条富媒体消息的过程：
1. 发送方调用 [createImageMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a23033a764f0d95ce83c52f3cdeea4137) 创建一条图片消息，获取消息对象 [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html)。
2. 发送方调用 [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) 接口将刚才创建的消息对象发送出去。

### 接收富媒体消息

1. 接收方调用 [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) 接口设置高级消息监听。
2. 接收方通过监听回调 [onRecvNewMessage](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html) 获取图片消息 [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html)。
3. 接收方解析  [V2TIMMessage](http://doc.qcloudtrtc.com/im/interfaceV2TIMMessage.html) 消息中的 `elemType` 属性，并根据其类型进行二次解析，获取消息内部 Elem 中的具体内容。

### 经典示例：收发图片
发送方创建一条图片消息并发送：
```
// 获取本地图片路径
NSString *imagePath = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"png"];
// 创建图片消息
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createImageMessage:imagePath];
// 发送图片消息
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"userA" groupID:nil 
priority:V2TIM_PRIORITY_DEFAULT 
onlineUserOnly:NO offlinePushInfo:nil progress:^(uint32_t progress) {
   // 图片上传进度（0 - 100）
} succ:^{
   // 图片消息发送成功
} fail:^(int code, NSString *msg) {
   // 图片消息发送失败
}];
```

接收方识别一条图片消息并将解析中包含的原图、大图和微缩图：
```
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
  if (msg.elemType == V2TIM_ELEM_TYPE_IMAGE) {
    V2TIMImageElem *imageElem = msg.imageElem;
    // 一个图片消息会包含三种格式大小的图片，分别为原图、大图、微缩图(SDK内部自动生成大图和微缩图)
    // 大图：是将原图等比压缩，压缩后宽、高中较小的一个等于720像素。
    // 缩略图：是将原图等比压缩，压缩后宽、高中较小的一个等于198像素。
    NSArray<V2TIMImage *> *imageList = imageElem.imageList;
    for (V2TIMImage *timImage in imageList) {
        NSString *uuid = timImage.uuid; // 图片 ID
        V2TIMImageType type = timImage.type; // 图片类型
        int size = timImage.size; // 图片大小（字节）
        int width = timImage.width; // 图片宽度
        int height = timImage.height; // 图片高度
        // 设置图片下载路径 imagePath，这里可以用 uuid 作为标识，避免重复下载
        NSString *imagePath = [NSTemporaryDirectory() stringByAppendingPathComponent:
						    [NSString stringWithFormat: @"testImage%@",timImage.uuid]];
        if (![[NSFileManager defaultManager] fileExistsAtPath:imagePath]) {
                [timImage downloadImage:imagePath 
								progress:^(NSInteger curSize, NSInteger totalSize) {
                    NSLog(@"图片下载进度：curSize：%lu,totalSize:%lu",curSize,totalSize);
                } succ:^{
                    NSLog(@"图片下载完成");
                } fail:^(int code, NSString *msg) {
                    NSLog(@"图片下载失败：code：%d,msg:%@",code,msg);
                }];
        } else {
                // 图片已存在
        }
    }
  }
}
```

> 更多消息解析示例代码请参考 [常见问题 > 5. 各类型消息应该如何解析](#msgAnalyze)。

## 设置 APNS 离线推送（offlinePushInfo）

当接收方的 App 被 kill 或者被切到后台时，IM SDK 无法通过正常的网络连接收取新消息。如需实现在此场景下接收方仍能感知到新消息，需要使用苹果提供的 APNs 服务，即“苹果离线推送”，更多详细请参见 [开启 iOS 离线推送](https://intl.cloud.tencent.com/document/product/1047/34347)。

### 设置 APNS 离线推送的标题和声音
您可以在发送消息时，通过 [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) 接口中的 **offlinePushInfo** 字段，设置 APNS 离线推送的标题和声音。

```
// 创建一条图片消息发送给 groupA，并且自定义推送 Title、推送声音
NSString *imagePath = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"png"];
// 创建图片消息
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createImageMessage:imagePath];
V2TIMOfflinePushInfo *pushInfo = [[V2TIMOfflinePushInfo alloc] init];
// 自定义推送的标题和声音（01.caf 是一个示例文件，需要链接进 Xcode 工程，这里只需要填写带后缀的文件名）
pushInfo.title = @"自定义推送 Title 展示";
pushInfo.iOSSound = @"01.caf";
[[V2TIMManager sharedInstance] sendMessage:msg receiver:nil groupID:@"groupA" priority:V2TIM_PRIORITY_DEFAULT 
onlineUserOnly:NO offlinePushInfo:pushInfo progress:^(uint32_t progress) {
} succ:^{
    // 消息发送成功
} fail:^(int code, NSString *msg) {
    // 消息发送失败
}];
```

### 点击推送消息跳转到对应的聊天窗口
如需实现该功能，发送消息时需设置离线推送对象 `offlinePushInfo` 的扩展字段 `ext`，收到消息的用户打开 App 时可以通过 `didReceiveRemoteNotification` 系统回调获取到扩展字段 `ext`，再根据 `ext` 内容跳转到对应的聊天界面。

本文以 “denny 给 vinson 发送消息” 的场景为例。
- 发送方：denny 需在发送消息时设置推送扩展字段 `ext`：
```
// denny在发送消息时设置 offlinePushInfo，并指定 ext 字段
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createTextMessage:@"文本消息"];
V2TIMOfflinePushInfo *info = [[V2TIMOfflinePushInfo alloc] init];
info.ext = @"jump to denny";
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"vinson" groupID:nil priority:V2TIM_PRIORITY_DEFAULT
onlineUserOnly:NO offlinePushInfo:info progress:^(uint32_t progress) {
} succ:^{
} fail:^(int code, NSString *msg) {
}];
```

- 接收方：vinson 的 App 虽然不在线，但可以接收到 APNS 离线推送，当 vinson 点击推送消息时会启动 App：
<pre><code><span class="hljs-comment">// vinson 启动 App 后会收到以下回调</span>
<span class="hljs-selector-tag">-</span> (void)<span class="hljs-selector-tag">application</span><span class="hljs-selector-pseudo">:(UIApplication</span> *)<span class="hljs-selector-tag">application</span> <span class="hljs-selector-tag">didReceiveRemoteNotification</span><span class="hljs-selector-pseudo">:(NSDictionary</span> *)<span class="hljs-selector-tag">userInfo</span> 
<span class="hljs-selector-tag">fetchCompletionHandler</span><span class="hljs-selector-pseudo">:(void</span> (^)(UIBackgroundFetchResult result))<span class="hljs-selector-tag">completionHandler</span> {
    <span class="hljs-comment">// 解析推送扩展字段 desc</span>
    <span class="hljs-selector-tag">if</span> ([userInfo[@<span class="hljs-string">"ext"</span>] <span class="hljs-attribute">isEqualToString</span>:@<span class="hljs-string">"jump to denny"</span>]) {
        <span class="hljs-comment">//跳转到和 denny 的聊天界面</span>
    }
}</code></pre>

## 设置消息为只能在线接收（onlineUserOnly）

某些场景下，您可能希望发出去的消息只被在线用户接收，即当接收者不在线时就不会感知到该消息。您只需在 
[sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a6ea32e6c119c1d771ee1123c5fb2dbae) 时，将参数 `onlineUserOnly` 设置为 `YES` ，此时发送出去的消息与普通消息相比，会有如下差异点：
- 不支持离线存储，即如果接收方不在线就无法收到。
- 不支持多端漫游，即如果接收方在一台终端设备上一旦接收过该消息，无论是否已读，都不会在另一台终端上再次收到。
- 不支持本地存储，即本地的云端的历史消息中均无法找回。

**经典示例：实现“对方正在输入”功能**
在 C2C 单聊场景下，您可以通过 [sendMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) 接口发送 "自己正在输入" 的提示性消息，接收方收到该消息时可以在 UI 界面展示 "对方正在输入"，示例代码如下：
```
// 给 userA 发送 "自己正在输入" 的提示消息
NSString *customStr = @"{\"command\": \"textInput\"}";
NSData *customData = [customStr dataUsingEncoding:NSUTF8StringEncoding];
V2TIMMessage *msg = [[V2TIMManager sharedInstance] createCustomMessage:customData];
[[V2TIMManager sharedInstance] sendMessage:msg receiver:@"userA" groupID:nil
priority:V2TIM_PRIORITY_DEFAULT onlineUserOnly:YES offlinePushInfo:nil progress:^(uint32_t progress) {
} succ:^{
    // 消息发送成功
} fail:^(int code, NSString *msg) {
    // 消息发送失败
}];

```

## 撤回消息
发送方通过 [revokeMessage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a2ef856a792923811e9d16ed7a101336a) 接口可以撤回一条已经发送成功的消息。默认情况下，发送者只能撤回2分钟以内的消息，您可以按需更改消息撤回时间限制，具体操作请参见 [消息撤回设置](https://intl.cloud.tencent.com/document/product/1047/34419)。
消息的撤回同时需要接收方 UI 代码的配合：当发送方撤回一条消息后，接收方会收到消息撤回通知 [onRecvMessageRevoked](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html)，通知中包含被撤回消息的 `msgID`，您可以根据 `msgID` 判断 UI 层是哪一条消息被撤回了，然后把对应的消息气泡切换成 "消息已被撤回" 状态。

### 发送方撤回一条消息

```
[[V2TIMManager sharedInstance] revokeMessage:msg succ:^{
     // 撤回消息成功
} fail:^(int code, NSString *msg) {
     // 撤回消息失败
}];
```

### 接收方感知消息被撤回
1. 调用 [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) 设置高级消息监听。
2. 通过 [onRecvMessageRevoked](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html) 接收消息撤回通知。

```
- (void)onRecvMessageRevoked:(NSString *)msgID {
      // msgList 为当前聊天界面的消息列表
      for(V2TIMMessage *msg in msgList){
         if ([msg.msgID isEqualToString:msgID]) {
             //msg 即为被撤回的消息，您需要修改 UI 上相应的消息气泡的状态
         }
     }
 }
```

## 给消息增加已读回执
在 C2C 单聊场景下，当接收方通过 [markC2CMessageAsRead](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#acb3a67bd2fa131b50c611a48fa78f34d) 接口将来自某人的消息标记为已读时，消息的发送方将会收到“已读回执”，表示“xxx 已经读过我的消息了”。

>目前仅 C2C 单聊消息支持已读回执，群聊场景暂不支持。虽然群聊消息也有对应的 [markGroupMessageAsRead](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a7fc79e30877b8d77fbdfa24e057376dc) 接口，但群消息的发送者目前无法收到已读回执。

### 接收方标记消息已读

```
//将来自 haven 的消息均标记为已读
[[V2TIMManager sharedInstance] markC2CMessageAsRead:@"haven" succ:^{
} fail:^(int code, NSString *msg) {
}];
```

### 发送方感知消息已读
消息已读回执的事件通知位于高级消息监听器  [V2TIMAdvancedMsgListener](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html) 中，如需支持感知消息已读，需要先通过 [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) 设置监听器，然后通过 [onRecvC2CReadReceipt](http://doc.qcloudtrtc.com/im/protocolV2TIMAdvancedMsgListener-p.html) 回调即可感知接收方的已读确认。

```
- (void)onRecvC2CReadReceipt:(NSArray<V2TIMMessageReceipt *> *)receiptList {
      // 接收方可能一次性会收到多个已读回执，因此这里采用数组的回调形式
      for (V2TIMMessageReceipt *receipt in receiptList) {
          // 消息接收者 receiver
          NSString * receiver = receipt.userID;
          // 已读回执时间，聊天窗口中时间戳小于或等于 timestamp 的消息都可以被认为已读
          time_t timestamp = receipt.timestamp;
      }
}
@end
```

## 查看历史消息
您可以调用 [getC2CHistoryMessageList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#abca63ad64f69aa4f424cf11849a9b89e) 获取单聊历史消息，调用 [getGroupHistoryMessageList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0) 获取群聊历史消息。如果当前设备网络连接正常，SDK 会默认从服务器拉取历史消息；如果没有网络连接，SDK 会直接从本地数据库中读取历史消息。

### 分页拉取历史消息
SDK 支持分页拉取历史消息，一次分页拉取的消息数量不宜太大，否则会影响拉取速度， 建议一次最多拉取20条。
本文以分页拉取名为 `groupA` 的群的历史消息，每次分页拉取 20 条为例，示例代码如下：

```
// 第一次拉取 lastMsg 传 nil，表示从最新的消息开始拉取 20 条消息
[[V2TIMManager sharedInstance] getGroupHistoryMessageList:@"groupA" count:20 
lastMsg:nil succ:^(NSArray<V2TIMMessage *> *msgs) {
    // 分页拉取返回的消息默认是按照从新到旧排列
    if (msgs.count > 0) {
        // 获取下一次分页拉取的起始消息
        V2TIMMessage *lastMsg = msgs.lastObject;
	    // 拉取剩下的20条消息
        [[V2TIMManager sharedInstance] getGroupHistoryMessageList:@"groupA" count:20 
				lastMsg:lastMsg succ:^(NSArray<V2TIMMessage *> *msgs) {
            // 拉取消息结束
        } fail:^(int code, NSString *msg) {
            // 拉取消息失败
        }];
    }
} fail:^(int code, NSString *msg) {
    // 拉取消息失败
}];
```

现实场景中的分页拉取，通常由用户的滑动操作触发的，用户每下拉一次消息列表就触发一次分页拉取。但原理上跟上述示例代码类似，都是以 `lastMsg` 作为分页的标记，以 `count` 控制每次拉取的消息条数。

### 历史消息的注意事项
- 历史消息存储时长如下：<ul style="margin:0;"><li>体验版：免费存储7天，不支持延长</li><li>专业版：免费存储7天，支持延长</li><li>旗舰版：免费存储30天，支持延长</li></ul>延长历史消息存储时长是增值服务，您可以登录 <a href="https://console.cloud.tencent.com/im">即时通信 IM 控制台</a> 修改相关配置，具体计费说明请参见 <a href="https://intl.cloud.tencent.com/document/product/1047/34350">增值服务资费</a>。
- 只有会议群（Meeting）（对应老版本的 ChatRoom 群）才支持拉取到用户**入群之前**的历史消息。
- 直播群（AVChatRoom）中的消息均不支持本地存储和多终端漫游，因此对直播群调用 [getGroupHistoryMessageList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a9e242ba327377fe74b83e8d5572d39a0) 接口是无效的。

## 删除消息
对于已经接收到的消息，可以调用 [deleteMessageFromLocalStorage](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a2bb42528f4d166ac826914094655841c) 接口进行本地删除。

### 删除本地消息

```
[[V2TIMManager sharedInstance] deleteMessageFromLocalStorage:msg succ:^{
      // 消息删除成功
} fail:^(int code, NSString *msg) {
     // 消息删除失败
}];
```

> App 卸载重装后已经删除的消息为什么又回来了？
> 由于 IM 目前只支持删除本地消息，所以当 App 卸载重装后，云端消息依然存在，重新拉取历史消息依然会返回这些被删除的本地历史消息。

### 删除云端消息
目前暂不支持删除云端消息，删除消息会导致云端建立反向映射关系，影响系统整体性能。


## 设置消息权限
### 只允许好友间收发消息
SDK 默认不限制非好友之间收发消息。如果您希望仅允许好友之间发送单聊消息，您可以在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) >【功能配置】>【登录与消息】>【好友关系检查】中开启"发送单聊消息检查关系链"。开启后，用户只能给好友发送消息，当用户给非好友发消息时，SDK 会报20009错误码。

### 屏蔽某人的消息
如果您想屏蔽某人的消息，请调用 [addToBlackList](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Friendship_08.html#a67d998da5085b5004bb6aa8d4322022c) 接口把该用户加入黑名单，即拉黑该用户。
当消息发送者被拉黑后，发送者默认不会感知到“被拉黑”的状态，即发送消息后仍展示发送成功（实际上此时接收方不会收到消息）。如果需要被拉黑的发送者收到消息发送失败的提示，请在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) >【功能配置】>【登录与消息】>【黑名单检查】中关闭"发送消息后展示发送成功"，关闭后，被拉黑的发送者在发送消息时，SDK 会报20007错误码。

### 屏蔽某个群组的消息
如果您想屏蔽某个群组的消息，请调用 [setReceiveMessageOpt](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Group_08.html#a4974b44d56778b1d5a3df613bee09c87) 接口，设置群消息接收选项为 `V2TIM_GROUP_NOT_RECEIVE_MESSAGE` 状态。

## 敏感词过滤
SDK 发送的文本消息默认会经过即时通信 IM 的敏感词过滤，如果发送者在发送的文本消息中包含敏感词，SDK 会报 80001 错误码。
![](https://main.qcloudimg.com/raw/63625c5252348205993ec5f33b087dec.png)

## 常见问题
### 1. 为什么会收到重复的消息？
- 请检查 [addSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a428fe7bf82be1592141d77dfa756ec68) 与 [addAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a517a6f56909fdad2004b4679b715186a) 是否混用。如果混用，当收到文本消息或自定义消息时，两个监听都会回调，会导致收到重复消息。
- 请检查同一个监听对象是否重复 `add`，如果监听对象不再使用，请主动调用对应的 [removeSimpleMsgListener](http://doc.qcloudtrtc.com/im/interfaceV2TIMManager.html#a8f6f9900006bf7ad5bd9bdb8ba0914eb) 或 [removeAdvancedMsgListener](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#a77ec89edbdf500431cbda5ee7aa50920) 接口移除多余的监听器。

### 2. App 卸载重装后已经删除的消息为什么又回来了？
由于 IM 目前只支持删除本地消息，所以当 App 卸载重装后，云端消息依然存在，重新拉取历史消息依然会返回这些被删除的本地历史消息。

### 3. App 卸载重装后已读回执为什么失效了？
在单聊场景下，接收方如果调用 [markC2CMessageAsRead](http://doc.qcloudtrtc.com/im/categoryV2TIMManager_07Message_08.html#acb3a67bd2fa131b50c611a48fa78f34d) 设置消息已读，发送方收到的已读回执里面包含了对方已读的时间戳 `timestamp`，SDK 内部会根据 `timestamp` 判断消息对方是否已读， `timestamp` 目前只在本地保存，程序卸载重装后会丢失。

### 4. 有多个 Elem 的消息应该如何解析？
出于降低消息复杂度的考虑，SDK API 2.0 接口不再支持创建包含多个 Elem 的 Message 对象。如果您收到了来自老版本的包含多个 Elem 的 Message 对象，可以按照以下步骤解析：
1. 正常解析出第一个 `Elem` 对象。
2. 通过第一个 `Elem` 对象的 [nextElem](http://doc.qcloudtrtc.com/im/interfaceV2TIMElem.html) 方法获取下一个 `Elem` 对象。如果下一个 `Elem` 对象存在，会返回 `Elem` 对象实例，如果不存在，会返回 `nil`。

```
- (void)onRecvNewMessage:(V2TIMMessage *)msg {
    // 查看第一个 Elem
    if (msg.elemType == V2TIM_ELEM_TYPE_TEXT) {
        V2TIMTextElem *textElem = msg.textElem;
        NSString *text = textElem.text;
        NSLog(@"文本信息 : %@", text);
        // 查看 textElem 后面还有没更多 Elem
        V2TIMElem *elem = textElem.nextElem;
        while (elem != nil) {
            // 判断 elem 类型
            if ([elem isKindOfClass:[V2TIMCustomElem class]]) {
                V2TIMCustomElem *customElem = (V2TIMCustomElem *)elem;
                NSData *customData = customElem.data;
                NSLog(@"自定义信息 : %@",customData);
            }
            // 继续查看当前 elem 后面还有没更多 elem
            elem = elem.nextElem;
        }
        // elem 如果为 nil，表示所有 elem 都已经解析完
    }
}
```

<span id ="msgAnalyze"></span>
### 5. 各种不同类型的消息应该如何解析？
解析消息相对复杂，我们提供了各种类型消息解析的 [示例代码](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKitDemo/TUIKitDemo/SampleCode/message.m)，您可以直接把相关代码拷贝到您的工程，然后根据实际需求进行二次开发。
