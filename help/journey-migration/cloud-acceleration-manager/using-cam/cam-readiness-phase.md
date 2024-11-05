---
title: Cloud Acceleration Manager中的准备阶段
description: 本页概述了Cloud Acceleration Manager中的就绪阶段。
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
feature: Migration
role: Admin
source-git-commit: f86d681c8f8cb6d602058ef30b648c53ff7bad69
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 7%

---

# Cloud Acceleration Manager中的准备阶段 {#readiness-phase-cam}

在Cloud Acceleration Manager (CAM)中创建项目后，您现在可以在准备阶段开始评估当前Adobe Experience Manager (AEM)实施。

准备阶段包括：

* [最佳实践分析](#best-practices-analysis)
* [计划和设置](#planning-setup)

执行以下步骤以导航到准备阶段：

1. 单击项目信息卡。

   ![项目信息卡](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. 在项目登录页面上，导航到&#x200B;**准备就绪**&#x200B;部分，如下图所示。

   ![准备就绪](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >请参阅在Cloud Acceleration Manager中创建和管理项目以了解更多信息。

## 使用最佳实践分析卡 {#best-practices-analysis}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa"
>title="最佳实践分析报告"
>abstract="可以将 BPA 报告上传到 CAM，以针对迁移到 AEM as a Cloud Service。"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer" text="使用 Best Practices Analyzer"

1. 从&#x200B;**最佳实践分析**&#x200B;卡中单击&#x200B;**审阅**。

   ![最佳实践分析 — 审核](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. 下载最佳实践分析器(BPA)。

   >[!NOTE]
   >为避免对业务关键实例产生影响，Adobe建议您在创作环境中运行BPA。 在自定义、配置、内容和用户应用程序方面，环境应尽可能接近生产环境。 或者，也可以在克隆的生产“创作”环境中运行。

   1. 导航到[软件分发](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=best*)门户，并将最佳实践分析器下载为zip文件。

      >[!NOTE]
      >查看[使用最佳实践分析器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html#imp-considerations)以了解如何运行BPA。

1. 在CAM中，单击&#x200B;**获取上传密钥**，以便获取用于配置系统以将BPA报告自动直接上传到CAM的密钥。

   ![获取上载密钥](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3b.png)

   >[!IMPORTANT]
   >报告仍可以手动上传，但使用上传密钥可简化操作。 请注意，如果您处于浏览器的无痕模式，则无法手动上传报告。

1. 上传新报告后，您可以在CAM中看到“最佳实践分析”报告。

   ![最佳实践分析报告](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

   >[!NOTE]
   >如果上载了多个不同的报告，则详细显示的报告始终是具有最新创建日期（而非上载日期）的报告。

1. 查看并探索CAM中的“最佳实践分析”仪表板。 有关更多详细信息，请参阅[查看最佳实践分析报告](#analysis-report)。

   >[!NOTE]
   >如果上传新报告比之前加载的报告更新，则上传新报告会重置所有评估。

### 使用打印预览 {#print-preview-cam}

您可以在Cloud Acceleration Manager中选择打印预览选项，以便预览报表的可打印内容，或者将报表打印为PDF格式以便轻松共享。

应遵循以下步骤：

1. 单击&#x200B;**打印预览**&#x200B;操作。

   ![打印预览](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1b.png)

1. 在可打印预览中显示报告的新选项卡上，单击&#x200B;**打印**&#x200B;以将报告打印为PDF格式。

   >[!IMPORTANT]
   >
   >* 上述功能推荐并支持选项&#x200B;**另存为PDF**。
   >* 如果使用浏览器的打印按钮，则仅打印一页。

   ![打印](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### 使用查看趋势线 {#trendline-view-cam}

在项目中上传多个不同的最佳实践分析器(BPA)报告时，您可以选择&#x200B;**查看趋势线**&#x200B;选项以查看和比较历史BPA报告的结果。

请按照以下步骤从趋势线选项查看报表：

>[!NOTE]
>在项目中上传多个不同的BPA报告时，您会看到&#x200B;**...**&#x200B;图标。 如果报告的主机和创建时间相同，则将其视为相同（非不同）。

1. 导航到您的项目，然后在&#x200B;**准备工作**&#x200B;阶段的&#x200B;**最佳实践分析**&#x200B;卡中单击&#x200B;**审核**。

   ![最佳实践分析 — 审核](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 从&#x200B;**视图**&#x200B;下拉列表中，单击&#x200B;**趋势线报告**，如下图所示。

   ![趋势线报告](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. 单击&#x200B;**趋势线报告**&#x200B;将打开该报告的趋势线视图。

   ![趋势线视图](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >趋势线报告以图形形式显示历史BPA报告的结果。
   >
   >您会看到两个显示以下趋势的图表：
   > 
   >1. **报告调查结果趋势**
   >1. **自定义组件和模板趋势**
   >
   >您可以通过下拉菜单添加或更改图形视图，如下图所示：
   >![选择图形视图](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### 审核最佳实践分析报告 {#analysis-report}

探索最佳实践分析报告页面中提供的以下信息卡：

![最佳实践分析报告](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> 使用每张卡，您可以：
>
>* 打开其关联的选项卡
>* 将所有报表选项卡（包括筛选）加入书签以便共享或将来检索
>* 使用详细信息图标可查看每个报告查找结果的详细信息

#### 报告属性 {#report-properties}

**报告属性**&#x200B;卡提供有关报告属性的信息，如报告日期、持续时间、筛选器、上传日期和Adobe Experience Manager (AEM)详细信息。

![报告属性](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### 报告概述 {#report-overview}

此&#x200B;**报告概述**&#x200B;信息卡提供在评估迁移到AEM as a Cloud Service的准备情况时适用的报告发现和严重性级别，如下图所示。

![报告概述](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

单击此报表可打开&#x200B;**报表**&#x200B;选项卡。

![报告选项卡](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

您可以根据重要性、子类型或计数筛选报表。

![报告筛选器](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>请参阅[解释Best Practices Analyzer报告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html)以了解调查结果类别和重要性级别。

#### 最佳实践评估 {#best-practices-assessment}

最佳实践评估选项可对您当前的AEM实例进行评估，并为采用AEM最佳实践的后续步骤提供指导。 您可以从此选项卡中查看以下信息：

* AEM 实例概述
* 自定义组件和模板
* 其他调查结果
* 查询速度较慢
* 维护任务

#### 迁移复杂度评估 {#migration-complexity-assessment}

“迁移复杂性评估”选项可评估将现有AEM实施迁移到AEM as a Cloud Service的复杂性。

您可以从此选项卡中查看以下信息：

* AEM 实例概述
* 评估
* 内容迁移注意事项

  ![迁移复杂性评估](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## 使用规划和设置卡 {#planning-setup}

1. 从&#x200B;**计划和设置**&#x200B;卡中单击&#x200B;**查看**。 此信息卡提供所有相关内容，帮助您规划和设置AEM迁移。

   ![规划和设置 — 视图](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. 内容轮播会显示迁移历程的此阶段的所有相关信息。

   ![计划和设置轮播](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### 从趋势线视图删除最佳实践分析报告 {#delete-trendline}

>[!IMPORTANT]
>仅当在一个项目中上传了多个报告时，才能删除报告。

1. 导航到您的项目，然后在&#x200B;**准备工作**&#x200B;阶段的&#x200B;**最佳实践分析**&#x200B;卡中单击&#x200B;**审核**。

   ![最佳实践分析 — 审核](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 单击&#x200B;**...**。

   ![椭圆](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. 在下拉列表中，单击&#x200B;**查看趋势线**，如下图所示。

   ![查看趋势线](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. 单击&#x200B;**趋势线报告**&#x200B;屏幕中的删除图标。

   ![趋势线报告 — 删除](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. 单击&#x200B;**删除**&#x200B;以确认删除。

   ![删除](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## 后续内容 {#whats-next}

在了解如何登录Cloud Acceleration Manager以及如何创建项目后，您现在已准备好继续查看[实施阶段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html)的下一步。
