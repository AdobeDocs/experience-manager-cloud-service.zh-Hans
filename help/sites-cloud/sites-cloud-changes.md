---
title: 对 AEM Cloud Service 中的 AEM Sites 的重要更改
description: 对 AEM Cloud Service 中的 AEM Sites 的重要更改
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
source-git-commit: ab81bca96bcf06b06357f900464e999163bb1bb2
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 21%

---

# 对 AEM Sites as a Cloud Service 的显著更改 {#notable-changes}

AEM Sitesas a Cloud Service作为云原生AEMas a Cloud Service平台的一部分提供了体验管理功能。 除了AEMas a Cloud Service的核心优势（如云原生可扩展性、正常运行时间以及始终处于最新状态）之外，AEM Sitesas a Cloud Service还提供了许多特定于站点的更改和增补。

>[!NOTE]
>本文档重点介绍对AEM Sites的显着更改。 有关AEMas a Cloud Service和其他模块的常规更改，请参阅：
>
>* [Adobe Experience Manager as a Cloud Service 简介](/help/overview/introduction.md)
>* [AEM as a Cloud Service 概述 - 新增功能和改进功能](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a Cloud Service 的[架构](/help/overview/architecture.md)
>* [对 AEM as a Cloud Service 的显著更改（发行说明）](/help/release-notes/aem-cloud-changes.md)
>* [对 AEM Assets as a Cloud Service 的显著更改](/help/assets/assets-cloud-changes.md)
>* [AEM Assets as a Cloud Service 简介](/help/assets/overview.md)
>* [Adobe Experience Manager as a Cloud Service 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=zh-Hans)


AEM Sitesas a Cloud Service中的更改和添加如下：

* [异步页面操作](#asynchronous-page-operations)
* [新的参考站点和教程](#new-reference-site-and-tutorial)

## 异步页面操作 {#asynchronous-page-operations}

在AEM Cloud服务中，传统上阻止UI的操作已被划分为在后台运行的较小任务。

* 移动页面
* 转出页面

此类操作的启动者可以在新UI中检查其状态，具体位于 `/mnt/overlay/dam/gui/content/asyncjobs.html`.

>[!NOTE]
>
>系统用户无需更改即可使用此新功能。 此处仅将其作为与AEM先前内部部署版本相比的行为更改进行说明。

## 新的参考站点和教程 {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/)，一个新的AEM参考网站，已更新和发布，以反映使用AEM构建网站的最佳实践，以及AEM中提供的一整套功能、组件和部署模型。 新的参考站点和 [随附教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans) 涵盖基本主题，如项目设置、核心组件、可编辑模板、客户端库以及使用Adobe Experience Manager Sites进行组件开发。

以前，We.Retail默认与AEM一起安装（生产模式下启动时除外）。  现在，以后默认情况下不会安装引用站点。  而是 [git存储库](https://github.com/adobe/aem-guides-wknd/) 和 [随附教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) 提供了更新的WKND引用站点代码。

## 运行时无法使用的功能 {#capabilities-not-available-at-runtime}

AEMas a Cloud Service始终处于开启状态，并且始终处于最新状态。 要实现此目的，需要将AEM存储库分离到不可变和可变内容中，并在运行时禁止访问不可变内容。 有关可变内容和不可变内容的更多详细信息，请参阅 [存储库的可变区域与不可变区域](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable).

由于不可变内容在运行时无法访问，因此在运行时无法使用以下AEM Sites操作：

* i18n词典翻译
* AEM Sites页面编辑器中的开发人员模式

这些功能可以通过AEMas a Cloud Service的本地独立开发人员实例来使用，用于更新AEMas a Cloud ServiceGIT存储库中的内容和代码，但不能用于托管的运行时实例。
