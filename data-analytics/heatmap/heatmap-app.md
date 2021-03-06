# App 热图

* [1.简介](heatmap-app.md#1-jian-jie)
* [2.使用步骤](heatmap-app.md#2-shi-yong-bu-zhou)
* [3.常见问题](heatmap-app.md#3-chang-jian-wen-ti)

## 1.简介

与网页端的圈选不同，移动端的圈选需要在移动端上完成。前提是您需要将已经集成 GrowingIO SDK 的 App 安装到您的手机.**使用移动端热图，需要更新Android SDK 到 0.9.101版本以上， iOS SDK 到 0.9.45版本以上。**

## 2.使用步骤

**开启热图：热图功能需要在App圈选模式下开启。**

**Step 1：**通过现有的方式（在Web首页→选择圈选→扫描二维码）唤醒在App内圈选；  
**Step 2：**在圈选模式下点击小红点；  
**Step 3：**设置中点击开启热图功能。

![](https://docs.growingio.com/.gitbook/assets/aeb2f5d7-9217-4ab6-b491-d844ea36c980.png)

![](https://docs.growingio.com/.gitbook/assets/caac45df-d10b-464d-ab41-bdaf4c7524a7.png)

## 3.常见问题

1. 移动端热图显示的是可点击元素的点击热度;
2. 移动端热图暂不支持更改时间段,目前显示的最近72小时\(3天\)的点击数据;
3. 热图数据来自于 GIO 的全量采集,如果您已经拥有集成了 SDK 的线上版本,只需要集成带有热图的 SDK,不用重新发版即可查看热图。

