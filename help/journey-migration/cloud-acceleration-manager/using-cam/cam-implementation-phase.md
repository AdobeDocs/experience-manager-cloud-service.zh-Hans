---
title: Cloud Acceleration Manager中的实施阶段
description: 本页概述了Cloud Acceleration Manager中的实施阶段。
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 6%

---

# Cloud Acceleration Manager中的实施阶段 {#implementation-phase-cam}

实施阶段包括：

* [本地开发](#local-development)
* [代码重构](#code-refactoring)
* [AEMas a Cloud Service部署](#aem-as-a-cloud-service-deployment)
* [内容传输](#content-transfer)


单击项目信息卡，以打开项目登陆页面并导航到 **实现** 部分，如下图所示。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>参见 [在Cloud Acceleration Manager中创建和管理项目](getting-started-cam.md#create-project) 了解更多信息。


## 使用本地开发卡 {#local-development}

“本地开发”卡提供所有相关内容，可帮助您在迁移历程的实施阶段开始时设置本地AEM开发环境。

阅读本节内容，以便您能够探索本地开发活动信息卡：

1. 单击 **视图** 从 **本地开发** 信息卡。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. 内容轮播会显示此阶段迁移历程的相关信息。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## 使用代码重构卡 {#code-refactoring}

“代码重构”活动卡提供所有相关信息，并突出显示迁移到AEMas a Cloud Service时要查看和解决的代码重构区域。

请阅读本节内容，以便您能够浏览“代码重构”活动信息卡：

1. 单击 **审核** 从 **代码重构** 活动信息卡。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. 该页面将显示按严重性级别组织的代码重构活动列表。 您可以通过单击两个突出显示的图标了解更多信息。

   该页面在三个不同的选项卡中显示代码重构注意事项：

   * 概述
   * Dispatcher
   * 测试

>[!NOTE]
>查看这些选项卡中的内容，了解Best Practices Analyzer未涵盖的一些其他区域。

此 **调度程序** 选项卡提供有关如何构建AEMas a Cloud ServiceApache和Dispatcher配置的信息，以及如何在部署到云环境之前在本地验证和运行该配置的信息。 它还介绍了在云环境中进行调试。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

此 **测试** 选项卡提供有关功能、体验审核和UI测试的信息。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## 使用AEMas a Cloud Service部署卡 {#aem-as-a-cloud-service-deployment}

AEMas a Cloud Service部署卡提供所有相关内容，可帮助您将代码部署到AEMas a Cloud Service。

阅读本节内容，以便您能够探索AEMas a Cloud Service部署卡活动信息卡：

1. 单击 **视图** 从 **AEMas a Cloud Service部署** 活动信息卡。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. 内容轮播会显示此阶段迁移历程的相关信息。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## 使用内容传输卡 {#content-transfer}

内容传输卡允许您启动和管理从当前AEM实例到AEMas a Cloud Service的内容传输。

阅读本节内容，以便您能够探索内容传输活动信息卡：

1. 单击 **审核** 从 **内容传输** 活动信息卡。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. 要开始内容传输，您必须创建一个迁移集。 单击 **创建迁移集**. 迁移集允许将内容传输到AEMas a Cloud Service。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >迁移集在长时间不活动后过期。 参见 [迁移集到期](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/overview-content-transfer-tool.md#migration-set-expiry) 了解详细信息。

   >[!NOTE]
   >参见 [先决条件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=zh-Hans) 和 [最佳实践和准则](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) ，然后再使用内容传输工具。

1. 下载并安装内容传输工具以填充迁移集并完成内容传输的提取阶段。 审核 [内容传输工具快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hans) 以了解如何使用内容传输工具。

1. 要将内容从迁移集摄取到AEMas a Cloud Service上的环境中，您必须开始摄取。 导航到 **引入作业** 并单击 **新引入**. 审核 [将内容引入目标](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html) 这样您就可以了解如何完成内容传输的摄取阶段。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

<!--### Estimating Content Transfer Time {#calculating}

A Content Transfer Tool calculator has been provided to estimate how long it could take to complete the content transfer activity. You can use the content repository size slider to select the size that applies to your project. The transfer times vary for the extraction and ingestion phases. 

   ![image](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

   >[!NOTE]
   >These times are estimates only. Factor such as network speeds and time to scale up instances have not been accounted for in these estimates.

To estimate the size of the AEM Repository, you can run the Disk Usage report under `http://HOST:PORT/etc/reports/diskusage.html`. 

You can also estimate the size of specific repository paths by using the `path` parameter, for example, `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`. -->

## 后续内容 {#whats-next}

在了解如何登录Cloud Acceleration Manager以及如何使用实施阶段后，您便可以继续查看中的下一步 [上线阶段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-golive-phase.html).
