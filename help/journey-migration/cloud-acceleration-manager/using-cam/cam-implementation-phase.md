---
title: Cloud Acceleration Manager中的实施阶段
description: 本页概述Cloud Acceleration Manager中的实施阶段。
exl-id: e6ac88f0-4b3f-43a1-98bc-8c6608713784
source-git-commit: 24331b974ded34ef949cc3d6fb157b124c145dee
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 4%

---

# Cloud Acceleration Manager中的实施阶段 {#implementation-phase-cam}

实施阶段包括：

* [本地开发](#local-development)
* [代码重构](#code-refactoring)
* [AEMas a Cloud Service部署](#aem-as-a-cloud-service-deployment)
* [内容传输](#content-transfer)


单击您的项目卡片以打开项目登录页面，然后导航到 **实施** 部分，如下图所示。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>请参阅 [在Cloud Acceleration Manager中创建和管理项目](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en#create-project) 以了解更多。


## 使用本地开发卡 {#local-development}

当您开始迁移历程的“实施”阶段时，“本地开发”卡会提供所有相关内容，以帮助您设置本地AEM开发环境。

请按照以下部分，浏览本地开发活动卡：

1. 单击 **查看** 按钮 **地方发展** 卡。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-2.png)

1. 内容轮播显示迁移历程的这一阶段的相关信息。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-3.png)


## 使用代码重构卡 {#code-refactoring}

“代码重构”活动卡提供了所有相关信息，并突出显示了在移动到AEMas a Cloud Service时需要查看和解析的代码重构区域。

请按照以下部分来浏览代码重构活动卡：

1. 单击 **审阅** 按钮 **代码重构** 活动卡片。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-4.png)

1. 该页面显示按严重性级别组织的代码重构活动列表。 您可以通过单击两个高亮显示的图标了解更多信息。

   该页面在三个不同的选项卡中显示代码重构注意事项：

   * 概述
   * Dispatcher
   * 测试

>[!NOTE]
>请查看这些选项卡中的内容，以了解最佳实践分析器未涵盖的其他一些区域。

的 **Dispatcher** 选项卡提供了有关如何构建AEMas a Cloud ServiceApache和Dispatcher配置的信息，以及如何在部署到云环境之前在本地验证和运行该配置。 此外，还介绍了如何在云环境中进行调试。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-2.png)

的 **测试** 选项卡提供了有关功能、体验审核和UI测试的信息。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/coderefactoring-3.png)


## 使用AEMas a Cloud Service部署卡 {#aem-as-a-cloud-service-deployment}

AEMas a Cloud Service部署卡提供了所有相关内容，可帮助您将代码部署到AEMas a Cloud Service。

请按照以下部分浏览AEMas a Cloud Service部署卡活动卡：

1. 单击 **查看** 按钮 **AEMas a Cloud Service部署** 活动卡片。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/implementation-6.png)

1. 内容轮播显示迁移历程的这一阶段的相关信息。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/aem-deployment-card.png)


## 使用内容传输卡 {#content-transfer}

内容传输卡允许您启动和管理从当前AEM实例到AEMas a Cloud Service的内容传输。

请按照以下部分来浏览内容传输活动卡：

1. 单击 **审阅** 按钮 **内容传输** 活动卡片。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-1.png)

1. 要开始内容传输，您需要创建迁移集。 单击 **创建迁移集**. 迁移集允许内容传输到AEMas a Cloud Service。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-2.png)

   >[!NOTE]
   >请查看 [先决条件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en) 和 [最佳实践和准则](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en) 使用内容传输工具之前，请执行以下操作：

1. 您需要下载并安装内容传输工具以填充迁移集，并完成内容传输的提取阶段。 审阅 [内容传输工具快速入门](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/getting-started-content-transfer-tool.html?lang=zh-Hans) 了解如何使用内容传输工具。

1. 要将内容从迁移集摄取到AEMas a Cloud Service的环境中，您需要开始摄取。 导航到 **摄取作业** 单击 **新摄取**. 审阅 [将内容摄取到目标](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/content-transfer-tool/ingesting-content.html?lang=en) 了解如何完成内容传输的摄取阶段。

   ![图像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-3.png)

### 估计内容传输时间 {#calculating}

提供了内容传输工具计算器，用于估算完成内容传输活动可能需要多长时间。 您可以使用内容存储库大小滑块选择适用于您的项目的大小。 对于提取和摄取阶段，传输时间会有所不同。

![图像](/help/journey-migration/cloud-acceleration-manager/assets/contenttransfer-4.png)

>[!NOTE]
>这些时间只是估计。 这些估计中没有考虑网络速度和扩展实例的时间等因素。

要估计AEM存储库的大小，可以在 `http://HOST:PORT/etc/reports/diskusage.html`.

您还可以使用 `path` 参数，例如， `http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`.

## 下一步 {#whats-next}

了解如何登录Cloud Acceleration Manager以及如何利用实施阶段后，您现在便可以继续查看 [上线阶段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=en).
