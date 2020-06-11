---
title: 使用云就绪性分析器
description: 使用云就绪性分析器
translation-type: tm+mt
source-git-commit: 47773a56f8bb24342281068a8c4d03d6edfb9277
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# 使用云就绪性分析器 {#using-cloud-readiness-analyzer}

## 使用云就绪性分析器的重要注意事项 {#imp-considerations}

请按照以下部分了解运行云就绪性分析器(CRA)时的重要注意事项：

* CRA支持6.1及更高版本的源AEM实例
* CRA可以在任何环境上运行(最 *好是* Stage环境)

   >[!NOTE]
   >为了提高检测率并避免业务关键型实例出现任何慢速情况，建议在源作者临时环境上运行CRA，这些临时在自定义、配置、内容和用户应用程序方面尽可能接近生产实例。 或者，它也可以在发布环境的克隆上 *运行* 。

## 可用性 {#availability}

Cloud Readiness Analyzer可从软件分发门户以zip文件的形式下载。 您可以通过源Adobe Experience Manager(AEM)实例上的包管理器安装该包。

>[!NOTE]
>正在从软件分发门户下载云就绪性分析 *器*。

## 运行云就绪性分析器 {#running-tool}

请按照本节学习如何运行云就绪性分析器：

1. 选择Adobe Experience Manager并导航到工具->操 **作** -> **云就绪性分析器**。

### 查看结果 {#viewing-the-results}

>[!IMPORTANT]
>从云就绪性分析器生成的报告基于模式检测器。 有关更多 [详细信息](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) ，请参阅图案检测器。

有两种方法可视图来自云就绪性分析器的输出：

1. **使用有组织的报表**

   >[!NOTE]
   >AEM版本6.3及更高版本提供有组织的报告。

   或者，

1. **查看CRA的输出**

   请按照以下步骤视图来自云就绪性分析器的输出：

   >[!NOTE]
   >以下步骤适用于AEM 6.1及更高版本。

   1. 使用导 **航到AEM Web** Console `https://serveraddress:serverport/system/console/configMgr`。

   1. 选择 **状态——图案检测器** ，如下图所示。

#### 在AEM 6.1实例中查看报表 {#aem-instances-report}

您可以下载AEM 6.1的csv报告。此报告处于挂起状态。

#### 了解报表中的重要性级别 {#importance-levels}

下表描述了各种模式检测器和云就绪性分析器重要性级别的含义。

| 重要性级别 | 描述 |
|--- |--- |
| INFO/0 | 此查找结果仅供参考。 |
| 建议/1 | 此发现可能是升级问题。 建议进一步调查。 |
| MAJOR/2 | 这一发现可能是一个应解决的升级问题。 |
| 关键/3 | 这一发现很可能是一个必须解决的升级问题，以防止功能或性能丢失。 |