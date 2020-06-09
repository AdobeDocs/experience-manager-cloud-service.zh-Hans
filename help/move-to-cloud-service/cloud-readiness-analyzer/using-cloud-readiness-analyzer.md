---
title: 使用云就绪性分析器
description: 使用云就绪性分析器
translation-type: tm+mt
source-git-commit: 317dd08600df9c7127cf8502341f93758ac8ce0b
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# 使用云就绪性分析器 {#using-cloud-readiness-analyzer}

## 使用云就绪性分析器的重要注意事项 {#imp-considerations}

请按照以下部分了解运行云就绪性分析器(CRA)时的重要注意事项：

* CRA支持在版本6.1及更高版本的源AEM实例上。
* CRA可以在任何环境上运行。 但是，为了提高检测率并避免业务关键型实例出现任何慢速情况，建议在源作者临时环境上运行它，该临时在自定义、配置、内容和用户应用程序方面尽可能接近生产实例。 或者，也可以在发布环境的克隆上运行它。

## 可用性 {#availability}

云就绪性分析器(CRA)可从软件分发门户下载为zip文件。 您可以通过源Adobe Experience Manager(AEM)实例上的包管理器安装该包。

>[!NOTE]
>从待定位置下载云就绪性分析器(CRA)。

## 运行云就绪性分析器 {#running-tool}

请按照本节学习如何运行云就绪性分析器：

1. 选择Adobe Experience Manager并导航到工具->操 **作** -> **云就绪性分析器**。

### 查看结果 {#viewing-the-results}

视图CRA产出有两种方法：

1. 使用有组织的报告（在AEM 6.3及更高版本上提供）请参阅CRA文档规划和状态，以在报告中描述重要性级别

要视图CRA的输出（可与AEM 6.1及更高版本一起使用）:

1. 通过浏览至，导航到AEM Web Console。

1. 选择状态——云就绪性分析器，如下图所示。