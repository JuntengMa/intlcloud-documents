## Overview

The Superplayer SDK is an open-source Tencent Cloud player component. It can provide powerful playback functionality similar to Tencent Video with just a few lines of code. It has basic features such as landscape/portrait mode switching, definition selection, gestures, and small window playback, as well as special features such as video buffering, software/hardware decoding switching, and adjustable-speed playback. It supports more formats and has better compatibility and functionality than system-default players. In addition, it offers advanced capabilities like instant playback on splash screen, low latency, and video thumbnail.
 
## SDK Download

The VOD Superplayer SDK for iOS can be downloaded [here](https://github.com/tencentyun/SuperPlayer_iOS).

## Target Audience

This document describes Tencent Cloud's proprietary capabilities. Please make sure that you have activated the relevant [Tencent Cloud](https://intl.cloud.tencent.com/) services before reading it. If you haven't registered an account, please [sign up](https://intl.cloud.tencent.com/login) first.

## Quick Integration

This project supports installation through CocoaPods. You only need to add the following code to the `Podfile`:

```ruby
pod 'SuperPlayer'
```

Run `pod install` or `pod update`.

### Using player

The main class of the player is `SuperPlayerView`, and videos can be played back after it is created.
```objc
// Import the header file
#import <SuperPlayer/SuperPlayer.h>

// Create a player  
_playerView = [[SuperPlayerView alloc] init];
// Set the delegate to accept events
_playerView.delegate = self;
// Set the parent view. `_playerView` will be automatically added under `holderView`
_playerView.fatherView = self.holderView;
```

```objc
// Hotlink protection disabled
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329073;// Configure `AppId`
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = "5285890799710670616"; // Configure `FileId`
[_playerView playWithModel:model];
```
```objc
// To enable hotlink protection, you need to enter the `psign`, which is a signature for superplayer. For more information on the signature and how to generate it, please see https://intl.cloud.tencent.com/document/product/266/38099
SuperPlayerModel *model = [[SuperPlayerModel alloc] init];
model.appId = 1400329071;// Configure `AppId`
model.videoId = [[SuperPlayerVideoId alloc] init];
model.videoId.fileId = "5285890799710173650"; // Configure `FileId`
model.videoId.pSign = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhcHBJZCI6MTQwMDMyOTA3MSwiZmlsZUlkIjoiNTI4NTg5MDc5OTcxMDE3MzY1MCIsImN1cnJlbnRUaW1lU3RhbXAiOjEsImV4cGlyZVRpbWVTdGFtcCI6MjE0NzQ4MzY0NywidXJsQWNjZXNzSW5mbyI6eyJ0IjoiN2ZmZmZmZmYifSwiZHJtTGljZW5zZUluZm8iOnsiZXhwaXJlVGltZVN0YW1wIjoyMTQ3NDgzNjQ3fX0.yJxpnQ2Evp5KZQFfuBBK05BoPpQAzYAWo6liXws-LzU"; 
[_playerView playWithModel:model];
```



Run the code and you can see that the video is played back on the phone and most of the features in the UI are available.

### Selecting FileId

A video `FileId` is usually returned by the server after the video is uploaded:

1. After the video is published on the client, the server will return a `FileId` to the client.
2. When the video is uploaded to the server, the corresponding `FileId` will be included in the notification of upload confirmation.

If the file already exists in Tencent Cloud, you can go to [Media Assets](https://console.cloud.tencent.com/vod/media), find it, and view its `FileId`.



### Timestamping

When lengthy videos are played back, timestamps on the progress bar can help viewers find the points of interest easily. You can add timestamps by using the `AddKeyFrameDescs.N` parameter in the [ModifyMediaInfo](https://intl.cloud.tencent.com/document/product/266/37570) API.

After the call is made, new elements will be displayed in the player UI.


### Small window playback
A small window is a player that floats over the main window within the application. Small window playback is very simple to implement. You just need to call the following code in the appropriate position:

```objc
[SuperPlayerWindow sharedInstance].superPlayer = _playerView; // Set the player for small window playback
[SuperPlayerWindow sharedInstance].backController = self;  // Set the returned view controller
[[SuperPlayerWindow sharedInstance] show]; // Floating display
```

<img src="https://main.qcloudimg.com/raw/e2ee64230af1b9c3a79cad935afa8b6a.jpeg" width="350">

### Exiting playback

When the player is no longer needed, call `resetPlayer` to clear the internal state of the player and free up the memory.

```objc
[_playerView resetPlayer];
```

## More Features

To try out the complete features, scan the QR code below to download the Tencent Video Cloud toolkit or run the project demo directly.
<img src="https://main.qcloudimg.com/raw/ee8557feb41a36d90e2b2f454b39e29a.png" width="150">
