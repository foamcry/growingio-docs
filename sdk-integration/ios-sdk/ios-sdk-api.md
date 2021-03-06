---
description: >-
  GrowingIO 提供了初始化配置项 API 和运行时 API 来自定义 SDK
  的采集，满足不同场景的定制采集。同一种含义的API，只需要调用一次即可，比如您关闭SDK的采集功能，可以在初始化中配置，也可以在运行时配置，只需调用一次相关API即可。
---

# IOS SDK API

{% hint style="success" %}
注意：以下所有API说明为相应接口的使用方法和基本功能，具体的函数定义及详细说明请参考Growing.h。
{% endhint %}

## GrowingIO 初始化配置项 API

```text
  GrowingIO 初始化配置项均在AppDelegate.m文件中的didFinishLaunchingWithOptions方法中 SDK 初始化代码块中设置，下面将分类并描述含义。
```

## 示例代码

```text
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
    [Growing startWithAccountId:@"0a1b4118dd954ec3bcc69da5138bdb96"];
    //开启日志输出
    [Growing setEnableLog:YES];
    return YES；
}
```

## 基础配置 API

### 1,初始化项目并设置采样率:\(startWithAccountId：withSampling）

```text
  初始化方法，accountId 为项目ID，sampling 为采样率，例：若设置sampling = 0.01，则 1% 的设备会被采集数据,每次启动会根据用户设置的采样率判断设备是否在采集的范围之内。​
```

| 参数名称 | 参数类型 | 是否必须 | 说明 |
| :--- | :--- | :--- | :--- |
| accountId | NSString | 是 | 项目ID |
| sampling | CGFloat | 否 | 采样率 |

原型：+ \(void\)startWithAccountId:\(NSString \*\)accountId withSampling:\(CGFloat\)sampling;

### 2，初始化项目:\(startWithAccountId\)

```text
    初始化方法，accountId 为项目ID，默认采样率为 100%。
```

| 参数名称 | 参数类型 | 是否必须 | 说明 |
| :--- | :--- | :--- | :--- |
| accountId | NSString | 是 | 项目ID |

原型：+ \(void\)startWithAccountId:\(NSString \*\)accountId;

### 3，URL schemes 处理方法:（handlerUrl）

```text
     URL schemes 处理方法，通过参数不同区分圈选、MobileDebugger、DeepLink等。
```

| 参数名称 | 参数类型 | 是否必须 | 说明 |
| :--- | :--- | :--- | :--- |
| url | NSString | 是 | URL schemes |

原型：+ \(BOOL\)handleUrl:\(NSURL\*\)url;

## SDK 功能API

<table>
  <thead>
    <tr>
      <th style="text-align:left">配置API</th>
      <th style="text-align:left">默认值</th>
      <th style="text-align:left">说明</th>
      <th style="text-align:left">
        <p>最低</p>
        <p>版本</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>| sdkVersion | 无 | 获取当前GrowingIO SDK 版本号 | 2.0.0 |
| :--- | :--- | :--- | :--- |


| setEnableLog | YES | 调试日志开关，enableLog == YES 时，会输出调试日志 |  |
| :--- | :--- | :--- | :--- |


| getEnableLog | 无 | 获取调试日志开关的当前状态 |  |
| :--- | :--- | :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>setDeviceIDModeTo</p>
        <p>CustomBlock</p>
      </th>
      <th style="text-align:left">无</th>
      <th style="text-align:left">
        <p>用户自定义ID（即 u 值）,会覆盖原来</p>
        <p>的 u 值</p>
      </th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody></tbody>
</table>| setTrackerHost | 无 | 设置数据收集平台服务器地址 |  |
| :--- | :--- | :--- | :--- |


| setReportHost | 无 | 设置设备报活服务器地址 |  |
| :--- | :--- | :--- | :--- |


| setDataHost | 无 | 设置数据查看平台服务器地址 |  |
| :--- | :--- | :--- | :--- |


| setGtaHost | 无 | 设置数据后台服务器地址 |  |
| :--- | :--- | :--- | :--- |


| setWsHost | 无 | 设置数据后台服务器地址 |  |
| :--- | :--- | :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>setHybridJSSDK</p>
        <p>UrlPrefix</p>
      </th>
      <th style="text-align:left">无</th>
      <th style="text-align:left">设置数据后台服务器地址</th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody></tbody>
</table>| setZone | 无 | 设置 zone 信息，即时区信息 |  |
| :--- | :--- | :--- | :--- |


| getDeviceId | 无 | 获取当前设备 id |  |
| :--- | :--- | :--- | :--- |


| getVisitUserId | 无 | 获取当前 uid |  |
| :--- | :--- | :--- | :--- |


| getSessionId | 无 | 获取当前访问 id |  |
| :--- | :--- | :--- | :--- |


## 数据采集发送 API

| 数据相关API | 默认值 | 说明 |
| :--- | :--- | :--- |


| setAspectMode | 无 | 设置数据采集模式，有 GrowingAspectModeSubClass 和 GrowingAspectModeDynamicSwizzling 两种 |
| :--- | :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left">setEnableDiagnose</th>
      <th style="text-align:left">enable</th>
      <th style="text-align:left">
        <p>是否允许发送基本性能诊断信息，默认为开。</p>
        <p>基本性能指发送成功、失败、timeout等信息</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>| disable | 无 | 全局不发送统计信息 |
| :--- | :--- | :--- |


| enableAllWebViews | enable | 设置是否采集 UIWebView / WKWebView 信息 |
| :--- | :--- | :--- |


| enableHybridHashTag | enable | 是否启用 HashTag |
| :--- | :--- | :--- |


| isTrackingWebView | true | 是否启用 trackingWebView |
| :--- | :--- | :--- |


| setImp | true | 设置是否发送元素的展现次数（浏览量、曝光量） |
| :--- | :--- | :--- |


| setFlushInterval | 10s | 设置、获取发送数据的时间间隔，默认值为10秒 |
| :--- | :--- | :--- |


| setDailyDataLimit | 5M | 设置每天使用数据网络（2G、3G、4G）上传的数据量的上限（单位是 KB），默认值为 3 MB |
| :--- | :--- | :--- |


| getDailyDataLimit | 无 | 获取每天使用数据网络（2G、3G、4G）上传的数据量的上限（单位是 KB），默认值为3 MB |
| :--- | :--- | :--- |


| disableDataCollect | 无 | 设置 GDPR 生效 |
| :--- | :--- | :--- |


| enableDataCollect | 无 | 设置 GDPR 失效 |
| :--- | :--- | :--- |


| disablePushTrack | Yes | 设置是否采集push推送点击，默认不采集 |
| :--- | :--- | :--- |


在 IOS SDK 文档中描述的更详细，请[点击查看](https://docs.growingio.com/docs/sdk-integration/ios-sdk#zi-ding-yi-shi-jian-he-bian-liang-api)。

| API函数 | 说明 | 最低版本 |
| :--- | :--- | :--- |
| track | 发送自定义事件，对应cstm事件 | 2.0.0 |
| setPageVariable | 发送页面级变量，对应pvar事件 | 2.0.0 |
| setEvar | 发送转化变量，对应evar事件 | 2.0.0 |
| setPeopleVariable | 发送用户变量，对应ppl事件 | 2.0.0 |
| setUserId | 置登录用户ID，对应cs1字段 | 2.0.0 |
| clearUserId | 清除登录用户ID | 2.0.0 |
| setVisitor | 设置访问用户变量，对应vstr事件 | 2.4.0 |

## 2.X 动态添加属性说明

### （1）UIView 增加属性

```text
// 手动标识该view不要追踪
@property (nonatomic, assign) BOOL growingAttributesDonotTrack; 

// 手动标识该view不要追踪它的值，默认是NO，特别的UITextView，UITextField，
//UISearchBar默认是YES
@property (nonatomic, assign) BOOL growingAttributesDonotTrackValue; 

//手动标识该view的取值  比如banner广告条的id 可以放在banner按钮的任意view上
@property (nonatomic, copy)   NSString *growingAttributesValue; 

// 手动标识SDCycleScrollView组件的bannerIds  如若使用,请在创建SDCycleScrollView实例对象后,
//立即赋值;(如果不进行手动设置,SDK默认会采集banner的imageName或者imageURL)
@property (nonatomic, strong)  NSArray<NSString *> *growingSDCycleBannerIds;

 // 手动标识该view的附加属性  该值可被子节点继承
@property (nonatomic, copy)   NSString* growingAttributesInfo;
```

### （2）UIViewController 增加属性

```text
// 手动标识该vc的附加属性  该值可被子节点继承
@property (nonatomic, copy)   NSString* growingAttributesInfo; 

// 手动标识该页面的标题，必须在该UIViewController显示之前设置
@property (nonatomic, copy)   NSString* growingAttributesPageName;
```

