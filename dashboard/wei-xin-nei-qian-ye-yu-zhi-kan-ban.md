# 微信内嵌页预置看板

## 预置看板简介

当成功通过了微信内嵌页SDK的集成流程后，在 GrowingIO 的首页里面会自动出现针对微信内嵌页的预置看板，您可以直接得到常见的流量分析报告，和页面分析报告，通过监测基础数据来获得洞察。

微信内嵌页预置看板提供默认2个场景的数据：

1. 增长指标
2. 落地页和浏览页分析

对于进阶分析需求，比如转化分析、自定义事件、更多维度拆分等，可以点击图表，拆分后另存为您自己的单图和看板来分析，并且可以添加到首页“自定义看板”做日常监测。

![&#x589E;&#x957F;&#x6307;&#x6807;&#x6570;&#x636E;-&#xFF08;&#x6D4B;&#x8BD5;&#x6570;&#x636E;&#xFF09;](../.gitbook/assets/image-120.png)

![&#x7528;&#x6237;&#x6765;&#x6E90;&#x63CF;&#x8FF0;&#xFF08;&#x6D4B;&#x8BD5;&#x6570;&#x636E;&#xFF09;](../.gitbook/assets/image-44.png)

整体描述你的微信内嵌页的流量表现，主要分成两部分信息：

1. 整体流量指标：在选定**时间段**内的访问量和PV总量，并统计去重的访问用户量和登录用户量（登录用户量即上传注册用户ID后统计的用户量）。数字图中同时会展示日的趋势图。
2. 用户来源情况描述：描述访问用户和新访问用户打开微信内嵌页的页面来源；其中具体的访问来源请见[下文描述](wei-xin-nei-qian-ye-yu-zhi-kan-ban.md#11-1)
3. 用户来源的地区，通过识别用户访问内嵌页的时候所在的GPS以及IP地址来解析；优先使用GPS，没有采集到时，根据IP所在的地址解析；部分情况下解析不到IP所在地址，会显示“未知”。
4. 用户来源的广告来源，采用UTM进行追踪，详情请见[UTM简介](../ads-tracking/utm-parameters.md)。

**右上角“自定义”可以支持选择自定义的时间。当选择“今日”时，趋势图会自动切换为今日小时颗粒度的数据。**

## 微信内嵌页的访问来源

内嵌页的流量来源，可以是微信中的各种可识别到的来源，如下，也可能因为部分技术原因采集不到直接的访问来源，即会被识别成“直接访问”；如果非被归集到一下的解释的分类中，识别了访问来源，会直接展示访问来源的域名。

访问来源中微信类来源:，GrowingIO 识别了几种微信环境访问 H5 的分类，常见的用例有这样几种：

| 访问来源值 | 场景 | 解释 |
| :---: | :--- | :--- |
| 微信-其他 | 扫描二维码在微信中打开H5页面查看 | 如果不使用GrowingIO生成具体的追踪链接，仅可以识别微信环境打开；如果想要识别具体的二维码的信息，例如那篇文章的，哪个公众号等，详情可以了解广告监测-web链接的相关功能。 |
| 微信-其他 | 打开分享到朋友圈、群聊、单聊消息中的URL链接 | 如果仅是URL，只会追踪具体的URL，但可以识别在微信环境中打开。 |
| 微信-其他 | 公众号直接给文字/图片链接，用户打开 | 如果不使用GrowingIO生成具体的追踪链接，仅可以识别微信环境打开；如果想要识别具体的二维码的信息，例如那篇文章的，哪个公众号等，详情可以了解广告监测链接的相关功能。 |
| 微信-公众号 | 公众号中查看图文消息-点击“阅读原文” | GroiwngIO会识别到微信的环境，微信会返回“公众号”访问来源链接（例如mp.weixinbridge.com\)，即可以判断出公众号的来源。 |
| 微信-朋友圈 | 朋友圈里查看分享的页面类链接 | GroiwngIO会识别到微信的环境，同时微信会给出相应的技术参数，即可以判断为朋友圈打开。 |
| 微信-群聊 | 查看分享给群组的页面链接 | GroiwngIO会识别到微信的环境，同时微信会给出相应的技术参数，即可以判断为群组信息中打开。 |
| 微信-单聊 | 查看分享给单个好友的页面链接 | GroiwngIO会识别到微信的环境，同时微信会给出相应的技术参数，即可以判断为好友信息中打开。 |
|  |  |  |

## 其他指标解释

### \*访问用户数  <a id="fang-wen-yong-hu-shu"></a>

GrowingIO默认使用cookie作为识别访问用户的标识；访问用户数即为去重的独立cookie数量。

### \*新访问用户数  <a id="xin-fang-wen-yong-hu-shu"></a>

新访问用户是指在同一个项目ID中接入GrowingIO SDK后，第一次统计到的cookie。

