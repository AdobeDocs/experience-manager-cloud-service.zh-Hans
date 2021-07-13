---
title: Cloud Acceleration Manager中的就绪阶段
description: 本页概述Cloud Acceleration Manager中的就绪阶段。
source-git-commit: 177e24d20bc97e4a7f2be749771463d7e79005c4
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 5%

---


# Cloud Acceleration Manager中的就绪阶段 {#readiness-phase-cam}

在Cloud Acceleration Manager中创建项目后，您现在可以在准备阶段开始评估当前的AEM实施。

准备阶段包括：

* [最佳实践分析](#best-practices-analysis)
* [计划和设置](#planning-setup)

请按照以下步骤导航到准备阶段：

1. 单击您的项目卡片上的以打开项目登录页面。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-landing1.png)

1. 导航到&#x200B;**Readiness**&#x200B;部分，如下图所示。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >请参阅在Cloud Acceleration Manager中创建和管理项目，以了解更多信息。

## 使用最佳实践分析卡 {#best-practices-analysis}

请按照以下步骤使用“最佳实践分析”信息卡：

1. 单击&#x200B;**Best Practices Analysis**&#x200B;卡中的&#x200B;**Review**&#x200B;按钮。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-2.png)

1. 请按照以下步骤下载Best Practices Analyzer(BPA)。

   >[!NOTE]
   >为避免对业务关键型实例产生影响，建议您在自定义、配置、内容和用户应用程序方面尽可能接近生产环境的创作环境中运行BPA。 或者，也可以在克隆的生产“创作”环境中运行。

   1. 导航到[Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)门户，并以zip文件形式下载Best Practices Analyzer。

      >[!NOTE]
      >查看[使用最佳实践分析器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations)以了解如何运行BPA。

   1. 以CSV格式导出报表

1. 单击&#x200B;**上传新报表**&#x200B;以在CAM中上传BPA报表。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-3.png)

1. 上传新报表后，您将看到“最佳实践分析”报表。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

1. 查看并浏览CAM中的“最佳实践分析”功能板。 有关更多详细信息，请参阅下面的[查看最佳实践分析报表](#analysis-report)一节。

   >[!NOTE]
   >上传新报表会重置所有评估。

### 查看最佳实践分析报表 {#analysis-report}

浏览“最佳实践分析报表”页面中提供的以下信息卡：

![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> 通过每张卡，您能够：
>* 单击每个卡片以打开其关联选项卡
>* 将所有报表选项卡（包括过滤）加入书签，以便共享或将来检索
>* 使用“详细信息”图标查看每个报表查找结果的详细信息


#### 报表属性 {#report-properties}

**报表属性**&#x200B;卡片提供有关报表属性的信息，例如报表日期、持续时间、过滤器、上传日期和Adobe Experience Manager(AEM)详细信息。

![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-properties.png)

#### 报表概述 {#report-overview}

此&#x200B;**报告概述**&#x200B;信息卡提供在评估是否准备将作为Cloud Service移动到AEM时适用的报告发现结果和严重性级别，如下图所示。

![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview.png)

单击此报表会打开&#x200B;**Report**&#x200B;选项卡。

![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview2.png)

您可以根据重要性、子类型或计数来过滤报表。

![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>请参阅[解释最佳实践分析器报告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) ，以了解发现结果类别和重要性级别。

#### 最佳实践评估 {#best-practices-assessment}

“最佳实践评估”选项对您当前的AEM实例进行评估，并就采用AEM最佳实践的后续步骤提供指导。 您可以从此选项卡中查看以下信息：

* AEM实例概述
* 自定义组件和模板
* 其他发现
* 较慢查询
* 维护任务

#### 迁移复杂性评估 {#migration-complexity-assessment}

“迁移复杂性评估”选项可评估将现有AEM实施作为Cloud Service迁移到AEM的复杂性。

您可以从此选项卡中查看以下信息：

* AEM实例概述
* 评估
* 内容迁移注意事项

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/migration-complexity-1.png)

## 使用计划和设置卡 {#planning-setup}

请按照此部分来浏览“计划和设置”活动卡。

1. 单击&#x200B;**Planning And Setup**&#x200B;卡中的&#x200B;**View**&#x200B;按钮。 此卡提供所有相关内容，可帮助您规划和设置AEM迁移。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-view.png)

1. 内容轮播显示迁移历程这一阶段的所有相关信息。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5-planning.png)

## 下一步 {#whats-next}

了解如何登录Cloud Acceleration Manager以及如何创建项目后，您现在可以继续查看[实施阶段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en)中的下一步。
