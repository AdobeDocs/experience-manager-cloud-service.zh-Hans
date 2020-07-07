---
title: 复制
description: 分发 和复制故障排除。
translation-type: tm+mt
source-git-commit: 23349f3350631f61f80b54b69104e5a19841272f
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%

---


# 复制 {#replication}

Adobe Experience Manager作为Cloud Service使 [用Sling Content](https://sling.apache.org/documentation/bundles/content-distribution.html) Distribution功能将内容移动以复制到运行于AEM运行时以外的Adobe I/O上的管道服务。

>[!NOTE]
>
>阅读 [分发](/help/core-concepts/architecture.md#content-distribution) ，了解更多信息。

## 发布内容的方法 {#methods-of-publishing-content}

### 快速取消／发布——计划取消／发布 {#publish-unpublish}

作者的这些标准AEM功能在AEMCloud Service中不会更改。

### 树激活 {#tree-activation}

要执行树激活:

1. 从AEM开始菜单中，导航到工 **具>部署>分发**
2. 选择卡转发发 **布者**
3. 进入转发发布者Web控制台UI后，选 **择分发**
   ![分发](assets/distribute.png "分发")
4. 在路径浏览器中选择路径，根据需要选择添加节点、树或删除，然后选择提交 **。**

## 疑难解答 {#troubleshooting}

要排除复制故障，请导航到AEM Author服务Web UI中的复制队列：

1. 从AEM开始菜单中，导航到工 **具>部署>分发**
2. 选择卡转发发 **布者**
   ![状](assets/status.png "态")
3. 检查应为绿色的队列状态
4. 可以测试与复制服务的连接
5. 选择“ **日志** ”选项卡，其中显示内容发布的历史记录

![日](assets/logs.png "志")

如果内容无法发布，则将从AEM Publish服务恢复整个发布。
在这种情况下，应检查队列，以确定哪些项目导致取消发布。 通过单击显示红色状态的队列，将显示包含待处理项目的队列，如果需要，可以从中清除单个或所有项目。
