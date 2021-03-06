# Android SDK 常见问题

## GrowingIO 对于页面的定义

**Android 常见的应用场景是一个**`Activity`**中嵌套多个**`Fragment`**，那么我们是怎么定义页面的呢？**

APP进入一个页面之后，无论其中有多少层`Fragment`嵌套，200ms 内最后一个初始化完成的`Fragment`即认为当前的页面。在用户可见的界面上，有事件操作的归因都会这个`Fragment`上。您在埋点的时候一定要确认当前的页面，并在当前的页面埋点是最稳定可靠的。

确认当前页面方法有三种：

1.[圈选](../../data-definition/circle/app.md)，查看圈选页面为当前页面![](https://docs.growingio.com/.gitbook/assets/-LGNxeGABUADKiTWTaEM-LI58sGTg1USJzrnTVZD-LI5KdIC78J2Y7tfdBp2image.png)

2.[查看日志](./#setdebugmode)，进入页面发送的`page`的`p`为当前的页面

3.使用[`Mobile Debugger`](../growingio-debugger/#growingio-mobile-debugger)查看`page`事件的`p`

## 点击事件采集逻辑

设置以下点击事件的控件会被采集点击事件，如果您自定义了点击事件，不在下方列举之内，将无法采集点击事件，影响数据分析。

```java
onCheckedChanged(android/widget/CompoundButton)
onCheckedChanged(android/widget/RadioGroup)
onClick(android/content/DialogInterface)
onClick(android/view/View)
onItemClick(android/widget/AdapterView;android/view/View)
onItemSelected(android/widget/AdapterView;android/view/View)
onNewIntent(android/content/Intent)
onRatingChanged(android/widget/RatingBar)
onStopTrackingTouch(android/widget/SeekBar)
onFocusChange(android/view/View)
onMenuItemClick(android/view/MenuItem)
onOptionsItemSelected(android/view/MenuItem)
onGroupClick(android/widget/ExpandableListView;android/view/View)
onChildClick(android/widget/ExpandableListView;android/view/View)
```

如果您自定义了 Click 事件， 但是希望 SDK 采集。 可以放置一个 `onClickListener` 作为代理。这种方案及时随着我们的 SDK 升级也会被兼容。

```java
public void onCustomClick(View view){
    // 您的业务
    ...

    // 为了 GrowingIO 能够采集自定义点击事件，调用 android.view.OnClickListener
    new View.OnClickListener() {
        @Override
        public void onClick(View v) {}
    }.onClick(view);
}
```

{% hint style="danger" %}
如果您还未采集到点击事件， 并且使用了 lambda 表达式，请看 [lambda 配置](./#5-lambda-biao-da-shi-zhi-chi-pei-zhi-xiang)。
{% endhint %}

## SDK 编译时性能和消耗时间

GrowingIO Android SDK 的编译时耗时取决于您的项目大小，我们的原理是字节码插桩\(使用Transform API\)。  
从clean项目， 执行assembleDebug， 如果添加了GrowingIO的SDK， 会大约增加50%的时间， 如果执行assembleRelease， 添加GrowingIO SDK 大约会增加30%的时间。  
可以看出GrowingIO确实会影响您的编译时长，尤其是在项目比较大的情况。  
如果您感觉到明显的编译耗时长，我们提供了一个在开发期间 GrowingIO 不参与编译的配置，如下：

1.在 Project 项目中，gradle.properties 文件内添加

```text
# true GrowingIO 参与编译，false 不参与编译
gioenable = true
```

2.在 Module 级别的 build.gradle 文件中增加配置

```groovy
android {
    defaultConfig {
        resValue("string", "growingio_project_id", "您的项目ID")
        resValue("string", "growingio_url_scheme", "您的URL Scheme")
        // 增加 gioenable 的配置
        resValue("string", "growingio_enable", project.gioenable)
    }
}
```

{% hint style="danger" %}
**上线时，一定要将 gradle.properties 文件中的 gioenable 改为 true 。否则我们将无法采集数据。**
{% endhint %}

{% hint style="info" %}
SDK 暂时不支持 Instant Run , 请开发者开发期间配置 gioenable = false ，即可使用 Instant Run。
{% endhint %}

