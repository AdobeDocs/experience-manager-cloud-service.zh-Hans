---
title: Cloud Acceleration Manager中的就绪阶段
description: 本页概述了Cloud Acceleration Manager中的就绪阶段。
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 5%

---

# Cloud Acceleration Manager中的就绪阶段 {#readiness-phase-cam}

在Cloud Acceleration Manager中创建项目后，您现在可以在准备阶段开始评估当前AEM实施。

准备阶段包括：

* [最佳实践分析](#best-practices-analysis)
* [规划和设置](#planning-setup)

按照以下步骤导航到就绪阶段：

1. 单击项目信息卡以打开项目登陆页面。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. 导航到 **就绪性** 部分，如下图所示。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >请参阅在Cloud Acceleration Manager中创建和管理项目，以了解更多信息。

## 使用最佳实践分析卡 {#best-practices-analysis}

请按照以下步骤使用Best Practices Analysis卡：

1. 单击 **审核** 按钮来自 **最佳实践分析** 信息卡。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. 按照以下步骤下载Best Practices Analyzer (BPA)。

   >[!NOTE]
   >为避免对业务关键型实例产生影响，建议您在自定义、配置、内容和用户应用程序方面尽可能接近生产环境的创作环境中运行BPA。 或者，也可以在克隆的生产“创作”环境中运行。

   1. 导航到 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 门户，并将最佳实践分析器下载为zip文件。

      >[!NOTE]
      >审核 [使用最佳实践分析器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) 学习如何运行BPA。

   1. 以CSV格式导出报表

1. 单击 **上传新报告** 在CAM中上传BPA报告。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3.png)

   >[!IMPORTANT]
   >如果您处于浏览器的无痕模式，则无法上传报告。

1. 上传新报告后，您将看到最佳实践分析报告。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

1. 查看并探索CAM中的最佳实践分析仪表板。 请参阅以下部分 [审核最佳实践分析报告](#analysis-report) 了解更多详细信息。

   >[!NOTE]
   >上传新报告会重置所有评估。

### 使用打印预览 {#print-preview-cam}

您可以在Cloud Acceleration Manager中选择打印预览选项，以便预览报告的可打印内容，也可以将报告打印为PDF格式，以便轻松共享。

应遵循以下步骤：

1. 单击 **打印预览** 图标，如下所示。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1.png)

1. 单击 **打印预览** 打开一个新选项卡，报告显示在可打印的预览中。 单击 **打印** 将报表打印为PDF格式。

   >[!IMPORTANT]
   >* 选项 **另存为PDF** 建议并支持上述功能。
   >* 如果使用浏览器的打印按钮，它将只打印一页。


   ![图像](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### 使用视图趋势线 {#trendline-view-cam}

在项目中上传多个Best Practices Analyzer (BPA)报告时，您可以选择 **查看趋势线** 用于查看和比较历史BPA报表结果的选项。

按照以下步骤从趋势线选项查看报表：

>[!NOTE]
>在项目中上传多个BPA报告时，您将看到 **...** 图标。

1. 导航到您的项目并单击 **审核** 从 **最佳实践分析** 中的信息卡 **就绪性** 阶段。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 单击 **...** 图标，以显示下拉列表。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

   >[!IMPORTANT]
   >显示的报表始终是具有最新报表日期的报告。

1. 单击 **查看趋势线**，如下图所示。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. 单击 **查看趋势线** 打开报告的趋势线视图，如下图所示。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >趋势线报告以图形形式显示历史BPA报告的结果。
   >
   >您将看到两个显示以下趋势的图形：
   >1. **报告调查结果趋势**
   >1. **自定义组件和模板趋势**

   >
   >您可以通过下拉列表添加或更改图形视图，如下图所示：
   >![图像](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### 审核最佳实践分析报告 {#analysis-report}

探索最佳实践分析报告页面中可用的以下信息卡：

![图像](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> 利用每张卡，您能够：
>* 单击每张信息卡以打开其关联的选项卡
>* 将所有报表选项卡（包括筛选）加入书签，以便共享或将来检索
>* 使用详细信息图标可查看每个报告查找结果的详细信息


#### 报表属性 {#report-properties}

此 **报表属性** 信息卡提供有关报表属性的信息，例如报表日期、持续时间、过滤器、上传日期和Adobe Experience Manager (AEM)详细信息。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### 报表概述 {#report-overview}

此 **报表概述** 信息卡提供在评估迁移到AEMas a Cloud Service的准备情况时使用的报告发现结果和严重性级别，如下图所示。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

单击此报告将打开 **报告** 选项卡。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

您可以根据重要性、子类型或计数筛选报表。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>请参阅 [解释Best Practices Analyzer报告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) 了解调查结果类别和重要性级别。

#### 最佳实践评估 {#best-practices-assessment}

“最佳实践评估”选项可对您当前的AEM实例进行评估，并为采用AEM最佳实践的后续步骤提供指导。 您可以从此选项卡中查看以下信息：

* AEM实例概述
* 自定义组件和模板
* 其他调查结果
* 较慢查询
* 维护任务

#### 迁移复杂性评估 {#migration-complexity-assessment}

“迁移复杂性评估”选项可评估将现有AEM实施迁移到AEMas a Cloud Service的复杂性。

您可以从此选项卡中查看以下信息：

* AEM实例概述
* 评估
* 内容迁移注意事项

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## 使用Planning and Setup卡 {#planning-setup}

阅读本节内容，了解“规划和设置”活动信息卡。

1. 单击 **视图** 按钮来自 **规划和设置** 信息卡。 此信息卡提供所有相关内容，将帮助您规划和设置AEM迁移。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. 内容轮播会显示迁移历程的此阶段的所有相关信息。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### 删除最佳实践分析报告 {#delete-trendline}

按照以下步骤从趋势线视图中删除报告：

>[!IMPORTANT]
>仅当在一个项目中上传了多个报告时，才能删除报告。

1. 导航到您的项目并单击 **审核** 从 **最佳实践分析** 中的信息卡 **就绪性** 阶段。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 单击 **...** 图标，以显示下拉列表。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. 单击 **查看趋势线**，如下图所示。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view2.png)

1. 单击删除图标，该图标位于 **趋势线报告** 屏幕。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. 单击 **删除** 以确认删除。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## 后续内容 {#whats-next}

了解如何登录Cloud Acceleration Manager以及如何创建项目后，您现在可以继续查看中的下一步 [实施阶段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en).
