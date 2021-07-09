# JPush-React-Native

## ChangeLog
1. 安卓升级到3.8.6并集成厂商通道
2. 苹果升级到3.5.2

安卓使用Google Play版本
IOS使用noidfa版本

#### 安卓已集成厂商通道 华为 小米 OPPO VIVO 具体参照[官方教程](https://docs.jiguang.cn//jpush/client/Android/android_guide/)
华为通道集成 
在根级 build.gradle 中添加规则，以纳入 HMS 服务插件 和 华为 的 Maven 代码库
```
buildscript {
  repositories {
    google()
    jcenter()
    mavenCentral()
    maven {url 'http://developer.huawei.com/repo/'}
  }

  dependencies {
    classpath 'com.huawei.agconnect:agcp:1.4.2.300'
  }
 }

allprojects {
      repositories {
          google()
          jcenter()
          mavenCentral()
          maven {url 'http://developer.huawei.com/repo/'}
      }
  }
```
在应用 module 的 build.gradle 文件底部添加 apply plugin 代码行，以启用 gradle 插件：
```
apply plugin: 'com.huawei.agconnect'
```
####以下需要在应用 module 的 gradle 中 defaultConfig 节点manifestPlaceholders中添加如下代码:
#####小米通道集成
```
  XIAOMI_APPKEY : "MI-您的应用对应的小米的APPKEY", // 小米平台注册的appkey,注意不要将前缀去掉 MI-appkey
  XIAOMI_APPID : "MI-您的应用对应的小米的APPID", // 小米平台注册的appid，注意不要将前缀去掉 MI-appid
```
#####OPPO通道集成
```
  OPPO_APPKEY : "OP-您的应用对应的OPPO的APPKEY", // OPPO平台注册的appkey
  OPPO_APPID : "OP-您的应用对应的OPPO的APPID", // OPPO平台注册的appid
  OPPO_APPSECRET: "OP-您的应用对应的OPPO的APPSECRET"//OPPO平台注册的appsecret
```
#####VIVO通道集成
```
  VIVO_APPKEY : "您的应用对应的VIVO的APPKEY", // VIVO平台注册的appkey
  VIVO_APPID : "您的应用对应的VIVO的APPID", // VIVO平台注册的appid
```

## 1. 安装

* 注意：项目需要使用指定jcore-react-native，需要安装
```shell
npm install jcore-react-native@ylls520/jcore-react-native#refs/tags/2.1.1-JD --save
或
```
```shell
yarn add jcore-react-native@ylls520/jcore-react-native#refs/tags/2.1.1-JD
```

```shell
npm install jpush-react-native@ylls520/jpush-react-native#refs/tags/3.1.0-JD --save
```
  或
```shell
yarn add jpush-react-native@ylls520/jpush-react-native#refs/tags/3.1.0-JD-JD
```
安装完成后连接原生库
进入到根目录执行<br/>
```shell
react-native link
```
或
react-native link jpush-react-native
react-native link jcore-react-native
```
## 2. 配置

### 2.1 Android

* build.gradle

  ```
  android {
        defaultConfig {
            applicationId "yourApplicationId"           //在此替换你的应用包名
            ...
            manifestPlaceholders = [
                    JPUSH_APPKEY: "yourAppKey",         //在此替换你的APPKey
                    JPUSH_CHANNEL: "yourChannel"        //在此替换你的channel
            ]
        }
    }
  ```

  ```
  dependencies {
        ...
        implementation project(':jpush-react-native')  // 添加 jpush 依赖
        implementation project(':jcore-react-native')  // 添加 jcore 依赖
    }
  ```

* setting.gradle

  ```
  include ':jpush-react-native'
  project(':jpush-react-native').projectDir = new File(rootProject.projectDir, '../node_modules/jpush-react-native/android')
  include ':jcore-react-native'
  project(':jcore-react-native').projectDir = new File(rootProject.projectDir, '../node_modules/jcore-react-native/android')
  ```

* AndroidManifest.xml

  ```
  <meta-data
  	android:name="JPUSH_CHANNEL"
  	android:value="${JPUSH_CHANNEL}" />
  <meta-data
  	android:name="JPUSH_APPKEY"
  	android:value="${JPUSH_APPKEY}" />    
  ```

### 2.2 iOS
注意：您需要打开ios目录下的.xcworkspace文件修改您的包名

### 2.2.1 pod

```
pod install
```

* 注意：如果项目里使用pod安装过，请先执行命令

  ```
  pod deintegrate
  ```

### 2.2.2 手动方式

* Libraries

  ```
  Add Files to "your project name"
  node_modules/jcore-react-native/ios/RCTJCoreModule.xcodeproj
  node_modules/jpush-react-native/ios/RCTJPushModule.xcodeproj
  ```

* Capabilities

  ```
  Push Notification --- ON
  ```

* Build Settings

  ```
  All --- Search Paths --- Header Search Paths --- +
  $(SRCROOT)/../node_modules/jcore-react-native/ios/RCTJCoreModule/
  $(SRCROOT)/../node_modules/jpush-react-native/ios/RCTJPushModule/
  ```

* Build Phases

  ```
  libz.tbd
  libresolv.tbd
  UserNotifications.framework
  libRCTJCoreModule.a
  libRCTJPushModule.a
  ```

## 3. 引用

### 3.1 Android

参考：[MainApplication.java](https://github.com/jpush/jpush-react-native/tree/master/example/android/app/src/main/java/com/example/MainApplication.java)

### 3.2 iOS

参考：[AppDelegate.m](https://github.com/jpush/jpush-react-native/tree/master/example/ios/example/AppDelegate.m) 

### 3.3 js

参考：[App.js](https://github.com/jpush/jpush-react-native/blob/dev/example/App.js) 

## 4. API

详见：[index.js](https://github.com/jpush/jpush-react-native/blob/master/index.js)

## 5.  其他

* 集成前务必将example工程跑通
* 如有紧急需求请前往[极光社区](https://community.jiguang.cn/c/question)
* 上报问题还麻烦先调用JPush.setLoggerEnable(true}，拿到debug日志

 

