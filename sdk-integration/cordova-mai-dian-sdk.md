---
description: GrowingIO 埋点 SDK 仅自动采集设备信息和您埋点内容数据。
---

# Cordova 埋点 SDK

GitHub Demo ：[https://github.com/growingio/Cordova-Demo](https://github.com/growingio/Cordova-Demo) 。

## 支持版本

支持 Cordova 5.0.0 以上，暂不支持低版本。

## 安装 Cordova 插件

在你项目主目录中执行以下操作：

```bash
cordova plugin add cordova-growingio-plugin
```

## Android 集成

### 1. 添加 Android 埋点 SDK 依赖

* 建议使用 Android Studio 打开项目中， `platforms`文件夹中的`android` 文件夹
* Cordova 埋点 SDK 是在 Android 原生 SDK 上的扩展，参照[ Android 埋点 SDK](android-sdk/android-mai-dian-sdk.md#ji-cheng-mai-dian-sdk)，集成步骤的 1~4，操作步骤完全一致。

### 2. 重要配置

和 Android 埋点 SDK 一致，[传送门](android-sdk/android-mai-dian-sdk.md#zhong-yao-pei-zhi)。

## iOS 集成

### 1. **添加 iOS 埋点 SDK 依赖**

Cordova 埋点 SDK 是在 iOS 原生 SDK 上的扩展，请参照 [iOS 埋点 SDK 集成步骤 1~3 ](ios-sdk/mai-dian-sdk-ji-cheng.md#mai-dian-sdk-ji-cheng)，操作完全一致。

### **2.重要配置**

与原生混合开发的开发者可详细查看[ iOS 无埋点 重要配置](ios-sdk/#zhong-yao-pei-zhi)文档，如果原生控件使用不多，只需关注如下配置即可：

* \*\*\*\*[**App Store 提交应用注意事项**](ios-sdk/#zai-app-store-ti-jiao-ying-yong)\*\*\*\*

## 自定义事件和变量API

对于用户行为，比如搜索、添加到购物车、购买等，我们可以很很容易的通过一行代码采集到这些事件，比如：

```javascript
gio.track("purchase", 456, { item: '123' }, onSucc, onFail)
```

### 采集自定义事件

```javascript
track(eventId, number, eventLevelVariable, onSuccess, onFail)
```

采集自定义事件 `eventId`，该事件的属性信息属于事件级变量。

在添加所需要发送的事件代码之前，需要在打点管理用户界面配置事件以及事件级变量`eventLevelVariable`。

**参数说明：**

| 参数名称 | 参数类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |


| `eventId` | String | 是 | 事件标识符 |
| :--- | :--- | :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left"><code>number</code>
      </th>
      <th style="text-align:left">Number</th>
      <th style="text-align:left">否</th>
      <th style="text-align:left">
        <p>事件的数值，没有number参数时，事件默认加一；</p>
        <p>当出现number参数时，事件自增number的数值</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>| `eventLevelVariable` | Object | 否 | 事件发生时所伴随的维度信息 |
| :--- | :--- | :--- | :--- |


| `onSucc` | Function | 否 | 发送成功后触发的回调函数 |
| :--- | :--- | :--- | :--- |


| `onFail` | Function | 否 | 发送失败后触发的回调函数 |
| :--- | :--- | :--- | :--- |


参数违反以下条件将不发送数据，调用后请验证数据是否发送，事件类型`t`为`cstm`。

| 参数名称 | 限制条件 |
| :--- | :--- |


| `eventId` | 非空，长度限制小于等于50； |
| :--- | :--- |


|  `number` | 非空。 |
| :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left"><code>eventLevelVariable</code>
      </th>
      <th style="text-align:left">
        <p>非空，长度限制小于等于100（<code>eventLevelVariable.length()&lt;=100</code>）；</p>
        <p><code>eventLevelVariable</code> 内部不允许嵌套 Object；</p>
        <p><code>eventLevelVariable</code>Object 中的 <code>key</code>长度限制小于等于50，<code>value</code>长度限制小等于1000。</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>```java
var gio = window.cordova.require('cordova-plugin-growingio.GrowingIO');

var onSucc = function(msg) {
    alert(msg);
};
var onFail = function(msg) {
    alert(msg);
};

// track API调用示例一
gio.track("registerSuccess",onSucc,onFail);
// track API调用示例二
gio.track("registerSuccess",{ 'item': '123' },onSucc,onFail);
// track API调用示例三
gio.track("loanAmount", 80000, 
            { "gender":"male","age":"21" },onSucc,onFail);
```

**检验数据发送日志示例：**

注意 `t` 等于 `cstm` 字段，表示自定义事件发送成功，只需注意 `var`、`n` 、`num`字段，其它字段无需仔细验证**。**

```javascript
//展示 track 接口调用示例三日志内容
{
    "s":"31e3aa14-5241-490c-821c-a741e9bf0f87",
    // t 为事件类型， track 接口调用发送的事件类型为 cstm
    "t":"cstm",
    "tm":1532085495251,
    "d":"com.growingio.android.test",
    // n 为 eventId 参数携带的值
    "n":"loanAmount",
    // var 为 eventLevelVariable 参数携带的值
    "var":{
        "gender":"male",
        "age":"21"
    },
    "ptm":0,
    // num 为 number 参数携带的值
    "num":80000,
    "gesid":18,
    "esid":0,
    "u":"b6247b01-a31a-3bc6-a391-4c456888c1ee"
}
```

{% hint style="info" %}
#### 推荐您使用MobileDebugger，我们为您列举了应用场景和验证示例，请移步查看：[cstm 事件验证](growingio-debugger/best-practice.md#cstm-shi-jian-yi-ji-guan-lian-de-shi-jian-ji-bian-liang-shi-jian)。
{% endhint %}

### 设置转化变量

```javascript
setEvar(conversionVariables, onSuccess, onFail)
```

发送一个转化信息用于高级归因分析，在添加代码之前必须在打点管理界面上声明转化变量。

转化变量是一种非常强大的变量类型，主要是为了归因而用，比如访问渠道、站外搜索关键词、站内搜索关键词等等。在 GrowingIO 里面可以定制变量的归因方式和持久性范围。

**参数说明：**

| 参数名 | 类型 | 是否必填 | 描述 |
| :--- | :--- | :--- | :--- |
| conversionVariables | Object | 是 | 转化级属性 |
| onSuccess | Function | 否 | 设置成功后触发的回调函数 |
| onFail | Function | 否 | 设置失败后触发的回调函数 |

**参数限制条件：**

| 参数名称 | 限制条件 |
| :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left">conversionVariables</th>
      <th style="text-align:left">
        <p>非空，键值对个数小于等于100；</p>
        <p><code>conversionVariables</code> 内部不允许含有<code>Object</code> 嵌套；</p>
        <p><code>conversionVariables</code>Object 中的 <code>key</code>长度限制小于等于50，<code>value</code>长度限制小等于1000。</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>```java
gio.setEvar({ "evarTest":111,
        "campaignId":"1234567890",
        "campaignOwner":"Li Si" },onSucc,onFail);
```

**检验数据发送日志示例：**

注意 `t` 等于`evar`字段，表示自定义事件发送成功，只需注意 `var` 字段，其它字段无需仔细验证**。**

```javascript
{
    "s":"e1c48845-dd60-4cf2-b1a5-a8e529d2188d",
    // t 为事件类型， evar 为转化事件
    "t":"evar",
    "tm":1532338526083,
    "d":"com.growingio.android.test",
    "cs1":"GrowingIO",
    // 转化变量
    "var":{
        "evarTest":111,
        "campaignId":"1234567890",
        "campaignOwner":"Li Si"
    },
    "gesid":300,
    "esid":22
}
```

{% hint style="info" %}
#### 推荐您使用 MobileDebugger，我们为您列举了应用场景和验证示例，请移步查看：[ evar 事件验证](growingio-debugger/best-practice.md#evar-zhuan-hua-bian-liang-shi-jian)
{% endhint %}

### 设置用户级变量

```javascript
setPeopleVariable(peopleVariables, onSuccess, onFail)
```

设置用户自身属性相关的属性信息，比如用户姓名、邮件地址、信用等级等。

在添加代码之前必须在打点管理界面上声明用户变量。

**参数说明：**

| 参数名 | 类型 | 是否必填 | 描述 |
| :--- | :--- | :--- | :--- |
| peopleVariables | Object | 是 | 用户属性 |
| onSuccess | Function | 否 | 设置成功后触发的回调函数 |
| onFail | Function | 否 | 设置失败后触发的回调函数 |

**参数限制条件：**

| 参数名称 | 限制条件 |
| :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left">peopleVariables</th>
      <th style="text-align:left">
        <p>非空，长度限制小于等于100（<code>peopleVariables.length()&lt;=100</code>）；</p>
        <p><code>peopleVariables</code> 内部不允许含有<code>JSONObject</code>或者；</p>
        <p><code>peopleVariables</code>Object 中的 <code>key</code>长度限制小于等于50，<code>value</code>长度限制小等于1000。</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>```java
gio.setPeopleVariable({ 'name': '玎玎', 'email': 'dingding@growingio.com' })
```

**检验数据发送日志示例：**

注意 `t` 等于`ppl`字段，表示用户变量发送成功，只需注意 `var`字段，其它字段无需仔细验证。

```javascript
{
    "s":"a35872af-13df-4479-90bc-25558d12328e",
    // t 为事件类型， pvar 为发送用户变量事件
    "t":"ppl",
    "tm":1532339208991,
    "d":"com.growingio.android.test",
    "cs1":"GrowingIO",
    // 用户变量
    "var":{
        'name': '玎玎', 
        'email': 'dingding@growingio.com'
    },
    "gesid":311,
    "esid":0
}
```

{% hint style="info" %}
#### 推荐您使用 MobileDebugger，我们为您列举了应用场景和验证示例，请移步查看：[ ppl 事件验证](growingio-debugger/best-practice.md#ppl-yong-hu-bian-liang-shi-jian)
{% endhint %}

### 关联注册用户

```javascript
setUserId(userId, onSuccess, onFail)
```

把 GrowingIO 识别的访问用户跟应用自身的注册用户做关联，用以登录用户行为分析。

**参数说明：**

| 参数名称 | 参数类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left">userId</th>
      <th style="text-align:left">String</th>
      <th style="text-align:left">是</th>
      <th style="text-align:left">
        <p>登录用户Id，长度限制小于等于1000；</p>
        <p>如果值为空则清空了登录用户变量，不建议这么用，</p>
        <p>请使用 clearUserId 清除登录用户变量。</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>```java
gio.setUserId('xiaoming');
```

注：您的 App 每次用户升级版本时无需重新登录的话，建议在用户每次升级App 版本后初次访问时重新调用上述 setUserId 方法。

{% hint style="info" %}
#### 推荐您使用 MobileDebugger，我们为您列举了应用场景和验证示例，请移步查看：[ 用户变量](growingio-debugger/best-practice.md#chang-jing-yi-yong-hu-bian-liang-zhi-deng-lu-yong-hu-id)
{% endhint %}

### 解除关联注册用户

```javascript
clearUserId(onSuccess, onFail)
```

当访问用户跟注册用户关联后，之后触发的行为会绑定到该注册用户上。如果有需要解除绑定，比如用户退出登录后，可以通过该函数解决绑定。

**参数说明**

| 参数名 | 类型 | 是否必填 | 描述 |
| :--- | :--- | :--- | :--- |
| onSuccess | Function | 否 | 关联成功后触发的回调函数 |
| onFail | Function | 否 | 关联失败后触发的回调函数 |

**示例**

```javascript
gio.clearUserId();
```

### 设置访问用户变量

当用户未登录时，定义用户属性变量，也可用于A/B测试上传标签。

```java
setVisitor(visitorVar,onSucc,onFail)
```

**参数说明：**

| 参数名称 | 参数类型 | 必填 | 说明 |
| :--- | :--- | :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left"><code>visitorVar</code>
      </th>
      <th style="text-align:left">Object</th>
      <th style="text-align:left">是</th>
      <th style="text-align:left">
        <p>不可使用嵌套的<code>JSONObject</code>对象，即为JSONObject中不可以放入<code>JSONObject</code>或者<code>JSONArray</code>；</p>
        <p>key 长度限制小于等于50，value长度限制小等于1000，值不能为空串，也就是""。</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>| `onSucc` | Function | 否 | 设置成功后触发的回调函数 |
| :--- | :--- | :--- | :--- |


| `onFail` | Function | 否 | 设置失败后触发的回调函数 |
| :--- | :--- | :--- | :--- |


```java
gio.setVisitor({"gender":"male","age":21});
```

**检验数据发送日志示例：**

注意 `t` 等于`vstr`字段，表示访问用户变量发送成功，其它字段无需仔细验证。

```javascript
{
    "s":"d334b4a1-57eb-4bf4-b426-64c1cce5a5c0",
    // t 为事件类型， vstr 为发送访问用户变量事件
    "t":"vstr",
    "tm":1532341259134,
    "d":"com.growingio.android.test",
    "cs1":"GrowingIO",
    //访问用户变量
    "var":{
        "gender":"male",
        "age":21
    },
    "gesid":322,
    "esid":0
}
```

## 验证 SDK 是否正常采集

#### 验证内容：

1. 验证打点事件是否发送

#### 验证工具：

1. [Mobile Debugger](growingio-debugger/)
2. Android [查看日志： ](android-sdk/#she-zhi-debug-mo-shi)设置 TestMode  和 Debug Mode ：

```java
GrowingIO.startWithConfiguration(this,new Configuration()
    //BuildConfig.DEBUG 这样配置就不会上线忘记关闭
    .setDebugMode(BuildConfig.DEBUG)
    .setTestMode(true)
    ...
    );
```

1. iOS 查看日志：iOS 在 AppDelegate 文件中配置：

```objectivec
[Growing setEnableLog:YES];
```

