---
title: 使用云就绪性分析器
description: 使用云就绪性分析器
translation-type: tm+mt
source-git-commit: 1739f81d4894f3e04cc4119f344a3bea5bd042d8
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 1%

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

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-1.png)

1. 单击“云就绪 **性分析器**”后，生成报告的工具开始在几分钟后AEM实例中会显示摘要报告。

   >[!NOTE]
   >您必须向下滚动页面以视图完整报告。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-2.png)

### 查看摘要报告中的结果 {#viewing-the-results}

>[!IMPORTANT]
>从云就绪性分析器生成的报告基于模式检测器。 有关更多 [详细信息](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/pattern-detector.html) ，请参阅图案检测器。

向下滚动页面以视图完整的摘要报告后，您可以看到报告中突出显示的每个类别的以下信息：

1. **重要性级别**

   下表描述了各种模式检测器和云就绪性分析器重要性级别的含义。

   | 重要性级别 | 描述 |
   |--- |--- |
   | INFO/0 | 此查找结果仅供参考。 |
   | 建议/1 | 此发现可能是升级问题。 建议进一步调查。 |
   | MAJOR/2 | 这一发现可能是一个应解决的升级问题。 |
   | 关键/3 | 这一发现很可能是一个必须解决的升级问题，以防止功能或性能丢失。 |

1. **说明**&#x200B;说明提供有关报告类别的信息。

1. **文档URL**&#x200B;文档URL允许您视图关联类型的技术文档。

1. **消息**&#x200B;单个消息中查找结果的描述。

### 以CSV格式查看结果 {#viewing-the-results-csv}

摘要报告可在AEM用户界面中找到。 您可以以逗号分隔值(CSV)格式下载完整报告，这在重构过程中非常有用。

请按照以下步骤生成摘要报告的CSV格式：

1. 
   1. 选择Adobe Experience Manager并导航到工具->操 **作** -> **云就绪性分析器**。

1. 报告可用后，单击 **CSV** ，以逗号分隔值(CSV)格式下载完整的摘要报告，如下图所示。

![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-3.png)


#### 在AEM 6.1实例中查看报表 {#aem-instances-report}

请按照以下步骤下载Adobe Experience Manager(AEM)6.1的CSV报告：

1.使用导 **航到Adobe Experience Manager Web Console配置**`https://serveraddress:serverport/system/console/configMgr`。

1. 选择 **状态** 选项卡，并从下 **拉列表中** 搜索模式检测器，如下图所示。

   ![图像](/help/move-to-cloud-service/cloud-readiness-analyzer/assets/cra-4.png)

1. 您可以以zip文件夹或JSON格式下载摘要报告。


