

## Operation Scenarios
The SDK for Android is a set of APIs provided by TPNS Service for clients to implement message push. This document provides two integration methods, AndroidStudio Gradle, which is automatic, and Android Studio, which is manual.


## Directions
### Integration methods
#### AndroidStudio Gradle automatic integration

>Before configuring the SDK, make sure you have configured the Android platform application.

1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **Configuration Management** on the left sidebar to get the application package name, `AccessID`, and `AccessKey`.
2. Get the latest version number on the [SDK download](https://console.cloud.tencent.com/tpns/sdkdownload) page.
3. In the application's `build.gradle` file, configure the following content:

```
android {
    ......
    defaultConfig {

        // The package name registered in the console. Note that the application ID, the current application package name, and the application package name registered in the console must be the same.
        applicationId "your package name"
        ......

        ndk {
            // Choose to add .so files corresponding to the CPU type as needed.
            abiFilters 'armeabi', 'armeabi-v7a', 'arm64-v8a'
            // You can also add 'x86', 'x86_64', 'mips', and 'mips64'.
        }

        manifestPlaceholders = [

            XG_ACCESS_ID:"accessid of registered application",
            XG_ACCESS_KEY : "accesskey of registered application",
        ]
        ......
    }
    ......
}

dependencies {
    ......
    // Add the following dependencies:
    implementation 'com.tencent.jg:jg:1.1'
    implementation 'com.tencent.tpns:tpns:[VERSION]-release' //  TPNS [VERSION] is the current SDK version number. You can view the SDK version number on the SDK download page.

}
```
4. For integration method for clusters outside Mainland China, please see [Integration method for cluster outside Mainland China](https://intl.cloud.tencent.com/document/product/1024/30713) below.

>
- If the following notification pops up in Android Studio after you add the above-mentioned abiFilter configuration:
"NDK integration is deprecated in the current plugin. Consider trying the new experimental plugin." Add `android.useDeprecatedNdk=true` to the `gradle.properties` file in the project root directory.
- If you need to listen to messages, please see the `XGPushBaseReceiver` API or the `MessageReceiver` class in the demo. You can inherit XGPushBaseReceiver and configure the following content in the configuration file (do not process time-consuming operations in the receiver):
```xml
    <receiver android:name="com.tencent.android.xg.cloud.demo.MessageReceiver">
            <intent-filter>
                <!-- Receive message passthrough -->
                <action android:name="com.tencent.android.xg.vip.action.PUSH_MESSAGE" />
                <!-- Listen to results of registration, unregistration, tag setting/deletion, and notification clicks ->
                <action android:name="com.tencent.android.xg.vip.action.FEEDBACK" />
            </intent-filter>
        </receiver>
```
- For compatibility with Android P, you must add and use the Apache HTTP client library. To do this, add the following configuration to the AndroidManifest application node.
```
<uses-library android:name="org.apache.http.legacy" android:required="false"/>
```



#### Android Studio manual integration

**Configure the project**
Import the SDK into the project following the steps below:

1. Create or open an Android project. For more information on how to create an Android project, please see the "Development environment" section.
2. Copy all the .jar files in the libs directory under the TPNS SDK directory to the project's libs (or lib) directory.
3. .so files are necessary components of TPNS and support armeabi, armeabi-v7a, arm64-v8a, mips, mips64, x86, and x86_64 platforms. Add the appropriate platform currently supported by your .so files.
4. Open Androidmanifest.xml and add the following configurations. (It is recommended to modify the configurations according to the Demo in the download package.) Replace YOUR_ACCESS_ID and YOUR_ACCESS_KEY with the corresponding `AccessId` and `AccessKey` of your application. Make sure the configurations are completed as required; otherwise, the service may not work properly.


**Configure permissions**
The permissions required by the TPNS SDK to operate normally. Sample code is as follows:
```xml
    <!-- **Required** Permissions required by TPNS SDK VIP version-->
    <permission
        android:name="application package name.permission.XGPUSH_RECEIVE"
        android:protectionLevel="signature" />
    <uses-permission android:name="application package name.permission.XGPUSH_RECEIVE" />

    <!-- **Required** Permissions required by TPNS SDK -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

    <!-- **Common** Permissions required by TPNS SDK-->
    <uses-permission android:name="android.permission.WAKE_LOCK" />
    <uses-permission android:name="android.permission.VIBRATE" />
    <uses-permission android:name="android.permission.RECEIVE_USER_PRESENT" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.GET_TASKS" /> 
```


| Permission                                       | Required | Description                            |
| ---------------------------------------- | ---- | ---------------------------- |
| android.permission.INTERNET              | **Yes**   | Allows the program to access the internet, which may incur GPRS traffic        |
| android.permission.ACCESS_WIFI_STATE     | **Yes**   | Allows the program to get the current Wi-Fi access status and WLAN hotspot information |
| android.permission.ACCESS_NETWORK_STATE  | **Yes**   | Allows the program to get the network information status                 |
| android.permission.WAKE_LOCK             | No  | Allows the program to run in the background after the screen is off       |
| android.permission.VIBRATE               | No   | Allows the application to vibrate                       |
| android.permission.READ_PHONE_STATE      | No   | Allows the application to access the phone status                   |
| android.permission.RECEIVE_USER_PRESENT  | No   | Allows the application to receive screen-on or unlock broadcast          |
| android.permission.WRITE_EXTERNAL_STORAGE | No   | Allows the program to write to external storage                   |
| android.permission.RESTART_PACKAGES      | No   | Allows the program to end a task                     |
| android.permission.GET_TASKS             | No    | Allows the program to get task information                   |



#### Configuring component and application information

```xml
<application>
    <!-- Other application configurations -->
    <uses-library android:name="org.apache.http.legacy" android:required="false"/> 
    <!-- **Required** TPNS default notification -->
    <activity
        android:name="com.tencent.android.tpush.XGPushActivity">
        <intent-filter>
            <action android:name="android.intent.action" />
        </intent-filter>
    </activity>

    <!-- **Required** TPNS Receiver broadcast reception-->
    <receiver
        android:name="com.tencent.android.tpush.XGPushReceiver"
        android:process=":xg_vip_service">
        <intent-filter android:priority="0x7fffffff">
            <!-- **Required** TPNS SDK internal broadcast -->
            <action android:name="com.tencent.android.xg.vip.action.SDK" />
            <action android:name="com.tencent.android.xg.vip.action.INTERNAL_PUSH_MESSAGE" />
            <action android:name="com.tencent.android.xg.vip.action.ACTION_SDK_KEEPALIVE" />
            <!-- **Optional** System broadcast: network switching -->
            <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
            <!-- **(Optional)** System broadcast: splash screen -->
            <action android:name="android.intent.action.USER_PRESENT" />
            <!-- [Optional] Some common system broadcasts for increasing the possibility of TPNS service reactivation. You can also add broadcast customized by the application to launch the service -->
            <action android:name="android.bluetooth.adapter.action.STATE_CHANGED" />
            <action android:name="android.intent.action.ACTION_POWER_CONNECTED" />
            <action android:name="android.intent.action.ACTION_POWER_DISCONNECTED" />
        </intent-filter>
    </receiver>

    <!-- **Required** TPNS service -->
    <service
        android:name="com.tencent.android.tpush.service.XGVipPushService"
        android:persistent="true"
        android:process=":xg_vip_service"></service>

    <!-- **Required** Notification service, android:name should be changed to the current package name -->
        <service android:name="com.tencent.android.tpush.rpc.XGRemoteService"
            android:exported="false">
            <intent-filter>
                <!-- **Required** Modify to the current application package name.XGVIP_PUSH_ACTION -->
                <action android:name="application package name.XGVIP_PUSH_ACTION" />
            </intent-filter>
        </service>

    <!-- **Required** **Note** Modify authorities to package name.XGVIP_PUSH_AUTH -->
    <provider
        android:name="com.tencent.android.tpush.XGPushProvider"
        android:authorities="application package name.XGVIP_PUSH_AUTH" />

    <!-- **Required** **Note** Modify authorities to package name.TPUSH_PROVIDER -->
    <provider
        android:name="com.tencent.android.tpush.SettingsContentProvider"
        android:authorities="application package name.TPUSH_PROVIDER" />

    <!-- **Optional** Used to strengthen the keep-alive capability -->
    <provider
        android:name="com.tencent.android.tpush.XGVipPushKAProvider"
        android:authorities="application package name.AUTH_XGPUSH_KEEPALIVE"
        android:exported="true" />

    <!-- **(Optional)** Receiver implemented by the application, which is used to receive the message pass-through and call back the operation result. Add as needed -->
    <!-- YOUR_PACKAGE_PATH.CustomPushReceiver should be changed to your own receiver: -->
    <receiver android:name="application package name.MessageReceiver">
        <intent-filter>
            <!-- Receive message passthrough -->
            <action android:name="com.tencent.android.xg.vip.action.PUSH_MESSAGE" />
            <!-- Listen to results of registration, unregistration, tag setting/deletion, and notification clicks ->
            <action android:name="com.tencent.android.xg.vip.action.FEEDBACK" />
        </intent-filter>
    </receiver>

    <!-- MQTT START-->
    <service android:exported="false"
             android:process=":xg_vip_service"
             android:name="com.tencent.bigdata.mqttchannel.services.MqttService" />

    <!--**Note** Modify authorities to package name.XG_SETTINGS_PROVIDER. For example, the package name of demo is com.tencent.android.xg.cloud.demo -->
    <provider
        android:exported="false"
        android:name="com.tencent.bigdata.baseapi.base.SettingsContentProvider"
        android:authorities="application package name.XG_SETTINGS_PROVIDER" />

    <!-- MQTT END-->

    <!-- **Required** Change to the `AccessId` of your application, which is a 10-digit number beginning with "15" and cannot contain spaces -->
    <meta-data
        android:name="XG_V2_ACCESS_ID"
        android:value="Application AccessId" />
    <!-- **Required** Change to the `AccessKey` of your application, which is a 12-character string beginning with "A" and cannot contain spaces -->
    <meta-data
        android:name="XG_V2_ACCESS_KEY"
        android:value="Application AccessKey" />

</application>

<!-- **Required** Permissions required by TPNS SDK version 5.0 -->
<permission
    android:name="application package name.permission.XGPUSH_RECEIVE"
    android:protectionLevel="signature" />
<uses-permission android:name="application package name.permission.XGPUSH_RECEIVE" />

<!-- **Required** Permissions required by TPNS SDK -->
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />

<!-- **Common** Permissions required by TPNS SDK-->
<uses-permission android:name="android.permission.VIBRATE" />
<uses-permission android:name="android.permission.RECEIVE_USER_PRESENT" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```
<hr>

<span id="JWjieru"></span>
#### Integration method for cluster outside Mainland China
To switch the push cluster to Singapore or Hong Kong (China), please follow the above steps for integration and add the following metadata in the `application` tag in the `AndroidManifest` file:
```
<application>
        // Other Android components
        <meta-data
            android:name="XG_GUID_SERVER"
            android:value="Domain name outside Mainland China/guid/api/GetGuidAndMqttServer" />           
        <meta-data
            android:name="XG_STAT_SERVER"
            android:value="Domain name outside Mainland China/log/statistics/push" />        
        <meta-data
            android:name="XG_LOG_SERVER"
            android:value="Domain name outside Mainland China/v3/mobile/log/upload" /> 
</application>
```
**The domain names outside Mainland China are as follows:**
Hong Kong (China): `https://api.tpns.hk.tencent.com`
Singapore: `https://api.tpns.sgp.tencent.com`

#### Audio-Visual rich media usage (optional)
1. In the **Layout** directory of the application, create an .xml file with the name xg_notification.
2. Copy the following code into the file:
```
<?xml version="1.0" encoding="UTF-8"?>
-<RelativeLayout android:layout_height="wrap_content" android:layout_width="match_parent" android:id="@+id/xg_root_view" xmlns:android="http://schemas.android.com/apk/res/android">
<!--Notification background. The id name cannot be changed but others can be changed-->
<ImageView android:layout_height="match_parent" android:layout_width="match_parent" android:id="@+id/xg_notification_bg" android:scaleType="centerCrop"/>
<!--Notification icon. The id name cannot be changed but others can be changed. Required.-->
<ImageView android:layout_height="48dp" android:layout_width="48dp" android:id="@+id/xg_notification_icon" android:scaleType="centerInside" android:layout_marginLeft="5dp" android:layout_centerVertical="true" android:layout_alignParentLeft="true"/>
<!--Notification time. The id name cannot be changed but others can be changed. If the time is not displayed, you can remove this layout-->
<TextView android:layout_height="wrap_content" android:layout_width="wrap_content" android:id="@+id/xg_notification_date" android:textSize="12dp" android:layout_marginRight="5dp" android:layout_marginTop="5dp" android:layout_alignParentRight="true" android:layout_alignParentTop="true"/>
<!--Notification title. The id name cannot be changed but others can be changed. Required.-->
<TextView android:layout_height="wrap_content" android:layout_width="match_parent" android:id="@+id/xg_notification_style_title" android:layout_marginLeft="10dp" android:layout_marginTop="20dp" android:singleLine="true" android:layout_toRightOf="@id/xg_notification_icon" android:layout_toLeftOf="@id/xg_notification_date"/>
<!--Notification content. The id name cannot be changed but others can be changed. Required.-->
<TextView android:layout_height="wrap_content" android:layout_width="match_parent" android:id="@+id/xg_notification_style_content" android:layout_marginTop="1dp" android:singleLine="true" android:layout_toLeftOf="@id/xg_notification_date" android:layout_alignLeft="@+id/xg_notification_style_title" android:layout_below="@+id/xg_notification_style_title"/>
<!--Playback button for rich media notifications with audio or video. The id name cannot be changed but others can be changed. If audio-visual rich media is not used, remove this layout.-->
<ImageView android:layout_height="25dp" android:layout_width="25dp" android:id="@+id/xg_notification_audio_play" android:layout_alignLeft="@+id/xg_notification_style_title" android:visibility="gone" android:background="@android:drawable/ic_media_play" android:layout_alignParentBottom="true"/>
<!--Stop playback button for rich media notifications with audio or video. The id name cannot be changed but others can be changed. If audio-video rich media is not used, remove this layout.-->
<ImageView android:layout_height="25dp" android:layout_width="25dp" android:id="@+id/xg_notification_audio_stop" android:layout_marginLeft="30dp" android:layout_toRightOf="@+id/xg_notification_audio_play" android:visibility="gone" android:background="@android:drawable/ic_media_pause" android:layout_alignParentBottom="true"/></RelativeLayout>
```


#### Disabling session keep-alive

To disable session keep-alive, if you use the automatic gradle integration method, please configure the following node under the <application> tag of the `AndroidManifest.xml` file of your application, where ```xxx``` is a custom name; if you use manual integration, please modify the node attributes as follows:

```xml
   <!-- Add the following node to the AndroidManifest.xml file of your application, where xxx is a custom name: -->
   <!-- To disable the feature of keep-alive with TPNS application, please configure -->
   <provider
       android:name="com.tencent.android.tpush.XGPushProvider"
       tools:replace="android:authorities"
       android:authorities="application package name.xxx.XGVIP_PUSH_AUTH"
       android:exported="false" />    
```

### Debugging and device registration

**Enabling debug log data**
>When launching it, set this to `false`

```java
XGPushConfig.enableDebug(this,true);
```


**Registering a token**

```java
XGPushManager.registerPush(this, new XGIOperateCallback() {
    @Override
    public void onSuccess(Object data, int flag) {
        // The token may change when the device is uninstalled and then reinstalled
        Log.d("TPush", "The registration is successful, the device token is: " + data);
    }

    @Override
    public void onFail(Object data, int errCode, String msg) {
        Log.d("TPush", "The registration failed, error code: " + errCode + ", error message: " + msg);
    }
});
```
The log of a successful registration filtered by "TPush" is as follows:

```xml
XG register push success with token : 6ed8af8d7b18049d9fed116a9db9c71ab44d5565
```
<hr>

### Code obfuscation

If you apply obfuscated code by using tools such as proguard in your project, keep the following options; otherwise, the TPNS service will be made unavailable.

```xml
-keep public class * extends android.app.Service
-keep public class * extends android.content.BroadcastReceiver
-keep class com.tencent.android.tpush.** {*;}
-keep class com.tencent.bigdata.baseapi.** {*;}
-keep class com.tencent.bigdata.mqttchannel.** {*;}
-keep class com.tencent.tpns.dataacquisition.** {*;}
```


### Suggestions on integration
<span id="HQToken"></span>
#### Getting token (optional)
It is recommended that after you integrate the SDK, you use gestures or other methods to display the token in the application's less commonly used UI such as **About** or **Feedback**. Doing so will facilitate subsequent troubleshooting.
Sample code is as follows:
```java
// Get the token
XGPushConfig.getToken(getApplicationContext());
```