---
title: 使用云就绪性分析器
description: 使用云就绪性分析器
translation-type: tm+mt
source-git-commit: 3d818278c53f3d3b4c5b53aa5b78d06d876bf05f
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# 使用云就绪性分析器 {#using-cloud-readiness-analyzer}

## 使用云就绪性分析器的重要注意事项 {#imp-considerations}

请按照以下部分了解运行云就绪性分析器(CRA)时的重要注意事项：

* CRA支持在版本6.1及更高版本的源AEM实例上。
* CRA可以在任何环境上运行。

   >[!NOTE]
   >为了提高检测率并避免业务关键型实例出现任何慢速情况，建议在源作者临时环境上运行CRA，这些临时在自定义、配置、内容和用户应用程序方面尽可能接近生产实例。 或者，也可以在发布环境的克隆上运行它。

## 可用性 {#availability}

云就绪性分析器(CRA)可从软件分发门户下载为zip文件。 您可以通过源Adobe Experience Manager(AEM)实例上的包管理器安装该包。

>[!NOTE]
>从待定位置下载云就绪性分析器( *CRA)*。

## 运行云就绪性分析器 {#running-tool}

请按照本节学习如何运行云就绪性分析器：

1. 选择Adobe Experience Manager并导航到工具->操 **作** -> **云就绪性分析器**。

### 查看结果 {#viewing-the-results}

视图CRA产出有两种方法：

1. 使用有组织的报告

   >[!NOTE]
   >AEM版本6.3及更高版本提供有组织的报告。

请参阅CRA文档规划和状态，在报告中描述重要性级别

1. 查看CRA的输出（可与AEM 6.1及更高版本一起使用）:

   1. 通过浏览至，导航到AEM Web Console。

   1. 选择状态——云就绪性分析器，如下图所示。

#### 了解报表中的重要性级别 {#importance-levels}

下表描述了各种模式检测器和云就绪性分析器重要性级别的含义。

| 重要性级别 | 描述 |
|--- |--- |
| INFO/0 | 此查找结果仅供参考。 |
| 建议/1 | 此发现可能是升级问题。 建议进一步调查。 |
| MAJOR/2 | 这一发现可能是一个应解决的升级问题。 |
| 关键/3 | 这一发现很可能是一个必须解决的升级问题，以防止功能或性能丢失。 |