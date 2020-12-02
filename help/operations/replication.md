---
title: 复制
description: 分发 和复制故障排除。
translation-type: tm+mt
source-git-commit: abb45225e880f3d08b9d26c29e243037564acef0
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 2%

---


# 复制 {#replication}

Adobe Experience Manager作为Cloud Service使用[Sling内容分发](https://sling.apache.org/documentation/bundles/content-distribution.html)功能将内容移动到运行在AEM运行时以外的Adobe I/O上的管道服务上进行复制。

>[!NOTE]
>
>有关详细信息，请阅读[分发](/help/core-concepts/architecture.md#content-distribution)。

## 发布内容的方法{#methods-of-publishing-content}

### 快速取消／发布——计划取消／发布{#publish-unpublish}

作者的这些标准AEM功能不会因AEMCloud Service而改变。

### 开启和关闭时间——触发器配置{#on-and-off-times-trigger-configuration}

在页面属性](/help/sites-cloud/authoring/fundamentals/page-properties.md#basic)的[基本选项卡中，可以找到&#x200B;**开始时间**&#x200B;和&#x200B;**结束时间**&#x200B;的其他可能性。

要实现自动复制，您需要在[OSGi配置](/help/implementing/deploying/configuring-osgi.md) **开关触发器配置**&#x200B;中启用&#x200B;**自动复制**:

![OSGi On Off触发器配置](/help/operations/assets/replication-on-off-trigger.png)

### 树激活{#tree-activation}

要执行树激活:

1. 从AEM开始菜单，导航到&#x200B;**工具>部署>分发**
2. 选择卡&#x200B;**forwardPublisher**
3. 进入forwardPublisher Web控制台UI后，**选择“分发”**

   ![分发](assets/distribute.png "分发")
4. 在路径浏览器中选择路径，根据需要选择添加节点、树或删除，然后选择&#x200B;**提交**

## 疑难解答 {#troubleshooting}

要排除复制故障，请导航到AEM作者服务Web UI中的复制队列：

1. 从AEM开始菜单，导航到&#x200B;**工具>部署>分发**
2. 选择卡&#x200B;**forwardPublisher**
   ![状](assets/status.png "态")
3. 检查应为绿色的队列状态
4. 可以测试与复制服务的连接
5. 选择&#x200B;**日志**&#x200B;选项卡，其中显示内容发布的历史记录

![日](assets/logs.png "志")

如果内容无法发布，则将从AEM发布服务恢复整个发布。
在这种情况下，应检查队列，以确定哪些项目导致取消发布。 通过单击显示红色状态的队列，将显示包含待处理项目的队列，如果需要，可以从中清除单个或所有项目。
