---
title: Cloud Acceleration Manager中的准备阶段
description: 本页概述了Cloud Acceleration Manager中的就绪阶段。
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 9%

---

# Cloud Acceleration Manager中的准备阶段 {#readiness-phase-cam}

在Cloud Acceleration Manager (CAM)中创建项目后，您现在可以在准备阶段开始评估当前Adobe Experience Manager (AEM)实施。

准备阶段包括：

* [最佳实践分析](#best-practices-analysis)
* [规划和设置](#planning-setup)

执行以下步骤以导航到准备阶段：

1. 单击项目信息卡。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. 在项目登陆页面上，导航到 **准备就绪** 部分，如下图所示。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >请参阅在Cloud Acceleration Manager中创建和管理项目以了解更多信息。

## 使用最佳实践分析卡 {#best-practices-analysis}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa"
>title="最佳实践分析报告"
>abstract="可以将 BPA 报告上传到 CAM，以针对迁移到 AEM as a Cloud Service。"
>additional-url="https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer" text="使用 Best Practices Analyzer"

1. 单击 **审核** 从 **最佳实践分析** 卡片。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. 下载最佳实践分析器(BPA)。

   >[!NOTE]
   >为避免对业务关键实例产生影响，Adobe建议您在创作环境中运行BPA。 在自定义、配置、内容和用户应用程序方面，环境应尽可能接近生产环境。 或者，也可以在克隆的生产“创作”环境中运行。

   1. 导航至 [Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=best*) 门户，并以zip文件形式下载最佳实践分析器。

      >[!NOTE]
      >审核 [使用最佳实践分析器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html#imp-considerations) 学习如何运行BPA。

1. 在CAM中，单击 **获取上传密钥**，因此您可以获得用于配置系统的密钥，以将BPA报表自动直接上传到CAM。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3b.png)

   >[!IMPORTANT]
   >报告仍可以手动上传，但使用上传密钥可简化操作。 请注意，如果您处于浏览器的无痕模式，则无法手动上传报告。

1. 上传新报告后，您可以在CAM中看到“最佳实践分析”报告。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

   >[!NOTE]
   >如果上载了多个不同的报告，则详细显示的报告始终是具有最新创建日期（而非上载日期）的报告。

1. 查看并探索CAM中的“最佳实践分析”仪表板。 请参阅 [审核最佳实践分析报告](#analysis-report) 以了解更多详细信息。

   >[!NOTE]
   >如果上传新报告比之前加载的报告更新，则上传新报告会重置所有评估。

### 使用打印预览 {#print-preview-cam}

您可以在Cloud Acceleration Manager中选择打印预览选项，以便打印报告预览或按PDF格式打印报告以便轻松共享。

应遵循以下步骤：

1. 单击 **打印预览** 操作。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1b.png)

1. 在可打印预览中显示报告的新选项卡上，单击 **打印** 将报表打印为PDF格式。

   >[!IMPORTANT]
   >
   >* 选项 **另存为PDF** 建议并支持上述功能。
   >* 如果使用浏览器的打印按钮，则仅打印一页。

   ![图像](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### 使用查看趋势线 {#trendline-view-cam}

在项目中上传多个不同的最佳实践分析器(BPA)报告时，您可以选择 **查看趋势线** 用于查看和比较历史BPA报表结果的选项。

请按照以下步骤从趋势线选项查看报表：

>[!NOTE]
>在项目中上传多个不同的BPA报告时，您会看到 **...** 图标。 如果报告的主机和创建时间相同，则将其视为相同（非不同）。

1. 导航到您的项目并单击 **审核** 从 **最佳实践分析** 中的卡 **准备就绪** 阶段。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 从 **视图** 下拉列表，单击 **趋势线报告**，如下图所示。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. 点击 **趋势线报告** 打开报告的趋势线视图。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >趋势线报告以图形形式显示历史BPA报告的结果。
   >
   >您会看到两个显示以下趋势的图表：
   > 
   >1. **报告调查结果趋势**
   >1. **自定义组件和模板趋势**
   >
   >您可以通过下拉菜单添加或更改图形视图，如下图所示：
   >![图像](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### 审核最佳实践分析报告 {#analysis-report}

探索最佳实践分析报告页面中提供的以下信息卡：

![图像](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> 使用每张卡，您可以：
>
>* 打开其关联的选项卡
>* 将所有报表选项卡（包括筛选）加入书签以便共享或将来检索
>* 使用详细信息图标可查看每个报告查找结果的详细信息

#### 报告属性 {#report-properties}

此 **报表属性** 信息卡提供有关报表属性的信息，例如报表日期、持续时间、过滤器、上传日期和Adobe Experience Manager (AEM)详细信息。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### 报告概述 {#report-overview}

此 **报表概述** 信息卡提供在评估迁移到AEMas a Cloud Service的准备情况时使用的报告查找结果和严重性级别，如下图所示。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

单击此报告将打开 **报表** 选项卡。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

您可以根据重要性、子类型或计数筛选报表。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>请参阅 [解释Best Practices Analyzer报告](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html) 了解调查结果的类别和重要性级别。

#### 最佳实践评估 {#best-practices-assessment}

最佳实践评估选项可对您当前的AEM实例进行评估，并为采用AEM最佳实践的后续步骤提供指导。 您可以从此选项卡中查看以下信息：

* AEM 实例概述
* 自定义组件和模板
* 其他调查结果
* 查询速度较慢
* 维护任务

#### 迁移复杂度评估 {#migration-complexity-assessment}

“迁移复杂性评估”选项可评估将现有AEM实施迁移到AEMas a Cloud Service的复杂性。

您可以从此选项卡中查看以下信息：

* AEM 实例概述
* 评估
* 内容迁移注意事项

  ![图像](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## 使用规划和设置卡 {#planning-setup}

1. 单击 **视图** 从 **规划和设置** 卡片。 此信息卡提供所有相关内容，帮助您规划和设置AEM迁移。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. 内容轮播会显示迁移历程的此阶段的所有相关信息。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### 从趋势线视图删除最佳实践分析报告 {#delete-trendline}

>[!IMPORTANT]
>仅当在一个项目中上传了多个报告时，才能删除报告。

1. 导航到您的项目并单击 **审核** 从 **最佳实践分析** 中的卡 **准备就绪** 阶段。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. 单击 **...**.

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. 在下拉列表中，单击 **查看趋势线**，如下图所示。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. 单击中的“删除”图标 **趋势线报告** 屏幕。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. 单击 **删除** 以确认删除。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## 后续内容 {#whats-next}

在了解如何登录Cloud Acceleration Manager以及如何创建项目后，您现在可以继续查看中的下一步 [实施阶段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html).
