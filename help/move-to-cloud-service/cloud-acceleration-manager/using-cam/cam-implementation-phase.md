---
title: Cloud Acceleration Manager中的实施阶段
description: 本页概述Cloud Acceleration Manager中的实施阶段。
source-git-commit: 83da3b647e47022a41160f2007d90dc7b23db671
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 2%

---


# Cloud Acceleration Manager中的实施阶段 {#implementation-phase-cam}

实施阶段包括：

* [地方发展](#local-development)
* [代码重构](#code-refactoring)
* [AEM as a Cloud Service部署](#aem-as-a-cloud-service-deployment)
* [内容传输](#content-transfer)


单击项目卡以打开项目登录页面，然后导航到&#x200B;**实施**&#x200B;部分，如下图所示。

![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-1.png)

>[!NOTE]
>请参阅[在Cloud Acceleration Manager中创建和管理项目](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/getting-started-cam.html?lang=en#create-project)以了解更多信息。


## 使用本地开发卡 {#local-development}

当您开始迁移历程的“实施”阶段时，本地开发卡会提供所有相关内容，以帮助您设置本地AEM开发环境。

请按照以下部分，浏览本地开发活动卡：

1. 单击&#x200B;**Local Development**&#x200B;卡中的&#x200B;**View**&#x200B;按钮。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-2.png)

1. 内容轮播显示迁移历程的这一阶段的相关信息。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-3.png)


## 使用代码重构卡 {#code-refactoring}

“代码重构”活动卡片提供了所有相关信息，并突出显示了在移动到AEM as a Cloud Service时需要查看和解析的代码重构区域。

请按照以下部分来浏览代码重构活动卡：

1. 单击&#x200B;**代码重构**&#x200B;活动卡中的&#x200B;**Review**&#x200B;按钮。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-4.png)

1. 该页面显示按严重性级别组织的代码重构活动列表。 您可以通过单击两个高亮显示的图标了解更多信息。

   该页面在三个不同的选项卡中显示代码重构注意事项。

   * 概述:
   * Dispatcher
   * 测试

   **概述**&#x200B;选项卡显示代码重构活动的列表。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/coderefactoring-1.png)

   **Dispatcher**&#x200B;选项卡提供了有关如何将AEM构建为Apache和DispatcherCloud Service配置的信息，以及如何在部署到云环境之前在本地验证和运行该配置。 此外，还介绍了如何在云环境中进行调试。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/coderefactoring-2.png)

   **Testing**&#x200B;选项卡提供了有关功能、体验审核和UI测试的信息。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/coderefactoring-3.png)


   >[!NOTE]
   >此外，请查看页面选项卡中的内容，以了解最佳实践分析器未涵盖的其他一些区域。


## 将AEM用作Cloud Service部署卡 {#aem-as-a-cloud-service-deployment}

AEM as a Cloud Service部署卡提供了所有相关内容，可帮助您将代码作为Cloud Service部署到AEM。

请按照以下部分来浏览AEM as a Cloud Service部署卡活动卡：

1. 单击&#x200B;**AEM as a Cloud Service部署**&#x200B;活动卡中的&#x200B;**查看**&#x200B;按钮。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-6.png)

1. 内容轮播显示迁移历程的这一阶段的相关信息。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/aem-deployment-card.png)


## 使用内容传输卡 {#content-transfer}

内容传输活动卡提供了相关指导和注意事项，在使用内容传输工具将内容从当前AEM实例移动到AEM作为Cloud Service时，应该对这些内容进行审核。

请按照以下部分来浏览内容传输活动卡：

1. 单击&#x200B;**内容传输**&#x200B;活动卡中的&#x200B;**查看**&#x200B;按钮。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/implementation-8.png)

1. 内容轮播显示迁移历程的这一阶段的相关信息。

   ![图像](/help/move-to-cloud-service/cloud-acceleration-manager/assets/content-transfertool-card.png)

   >[!NOTE]
   >在使用内容传输工具之前，请查看[先决条件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/prerequisites-content-transfer-tool.html?lang=en)和[最佳实践和准则](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang=en)。

### 估计内容传输时间 {#calculating}

提供了新的内容传输工具计算器，用于估算完成内容传输活动可能需要多长时间。 您可以使用内容存储库大小滑块选择适用于您的项目的大小。 对于提取和摄取阶段，传输时间会有所不同。

>[!NOTE]
>这些时间只是估计。 这些估计中没有考虑网络速度和扩展实例的时间等因素。

要估计AEM存储库的大小，可以在`http://HOST:PORT/etc/reports/diskusage.html`下运行“Disk Usage（磁盘使用情况）”报告。

您还可以使用`path`参数（例如`http://HOST:PORT/etc/reports/diskusage.html?path=/content/dam`）来估计特定存储库路径的大小。

## 下一步 {#whats-next}

了解如何登录Cloud Acceleration Manager以及如何利用实施阶段后，您现在可以继续查看[上线阶段](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-golive-phase.html?lang=en)中的下一步。
