---
title: Cloud Acceleration Manager中的实施阶段
description: 本页概述了Cloud Acceleration Manager中的实施阶段。
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: c8739388ac21dd40d6757815af6f2732991d216b
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 7%

---

# Cloud Acceleration Manager中的实施阶段 {#implementation-phase-cam}

实施阶段包括：

* [本地开发](#local-development)
* [代码重构](#code-refactoring)
* [AEMas a Cloud Service部署](#aem-as-a-cloud-service-deployment)
* [内容传输](#content-transfer)


单击项目信息卡，以打开项目登陆页并导航到 **实现** 部分，如下图所示。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>请参阅 [在Cloud Acceleration Manager中创建和管理项目](getting-started-cam.md#create-project) 了解更多信息。


## 使用本地开发卡 {#local-development}

本地开发卡提供所有相关内容，可帮助您在迁移历程的实施阶段开始时设置本地AEM开发环境。

阅读本节内容，以便您可以探索本地开发活动信息卡：

1. 单击 **视图** 从 **本地开发** 卡片。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. 内容轮播会显示迁移历程的此阶段的相关信息。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## 使用代码重构卡片 {#code-refactoring}

“代码重构”活动卡提供了所有相关信息，并突出显示要在迁移到AEMas a Cloud Service时查看和解决的代码重构区域。

请阅读本节内容，以便您能够浏览“代码重构”活动信息卡：

1. 单击 **审核** 从 **代码重构** 活动信息卡。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. 此页显示按严重性级别组织的代码重构活动的列表。 您可以通过单击两个突出显示的图标了解更多信息。

   该页面在三个不同的选项卡中显示代码重构注意事项：

   * 概述
   * Dispatcher
   * 测试

>[!NOTE]
>查看这些选项卡中的内容，了解Best Practices Analyzer未涵盖的一些其他区域。

此 **Dispatcher** 选项卡提供了有关以下内容的信息：如何构建AEMas a Cloud Service的Apache和Dispatcher配置，以及如何在部署到云环境之前在本地验证和运行该配置。 它还介绍了在云环境中进行调试的情况。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

此 **测试** 选项卡提供有关功能、体验审核和UI测试的信息。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## 使用AEMas a Cloud Service部署卡 {#aem-as-a-cloud-service-deployment}

AEMas a Cloud Service部署信息卡提供所有相关内容，帮助您将代码部署到AEMas a Cloud Service。

请参阅此部分，以便您可以浏览AEMas a Cloud Service部署卡活动信息卡：

1. 单击 **视图** 从 **AEMas a Cloud Service部署** 活动信息卡。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. 内容轮播会显示迁移历程的此阶段的相关信息。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## 使用内容传输卡 {#content-transfer}

内容传输卡允许您启动和管理从当前AEM实例到AEMas a Cloud Service的内容传输。

请阅读以下章节，以便浏览内容传输活动信息卡：

1. 单击 **审核** 从 **内容传输** 活动信息卡。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. 要开始内容传输，您必须创建一个迁移集。 单击 **创建迁移集**. 迁移集允许将内容传输到AEMas a Cloud Service。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >迁移集在长时间不活动后过期。 请参阅 [迁移集到期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 以了解详细信息。

   >[!NOTE]
   >请参阅 [先决条件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=zh-Hans) 和 [最佳实践和指南](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) ，然后再使用内容传输工具。

1. 下载并安装内容传输工具以填充迁移集并完成内容传输的提取阶段。 审核 [内容传输工具快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hans) 以了解如何使用内容传输工具。

1. 要将内容从迁移集摄取到AEMas a Cloud Service上的环境中，您必须开始摄取。 导航到 **引入作业** 并单击 **新建引入**. 审核 [将内容提取到目标](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/ingesting-content.md) 这样您就可以了解如何完成内容传输的摄取阶段。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![image](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## 后续内容 {#whats-next}

在了解如何登录Cloud Acceleration Manager以及如何使用实施阶段后，您便可以继续阅读中的下一步 [上线阶段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-golive-phase.html).
