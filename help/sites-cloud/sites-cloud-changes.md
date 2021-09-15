---
title: 对 AEM 云服务中 AEM Sites 的显著更改
description: 对 AEM 云服务中 AEM Sites 的显著更改
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
source-git-commit: ab81bca96bcf06b06357f900464e999163bb1bb2
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 18%

---

# 对 AEM Sites as a Cloud Service 的显著更改 {#notable-changes}

AEM Sites as aCloud Service作为云原生AEM as aCloud Service平台的一部分，提供体验管理功能。 除了AEM as a Sites的核心优势（如云原生可扩展性、正常运行时间以及始终保持最新）之外，AEM Sites as a Analytics还提供了许多特定于Sites的更改和增补。

>[!NOTE]
>本文档重点介绍对AEM Sites的显着更改。 有关AEM as a Cloud Service和其他模块的常规更改，请参阅：
>
>* [Adobe Experience Manager as a Cloud Service 简介](/help/overview/introduction.md)
>* [AEM as a Cloud Service 概述 - 新增功能和改进功能](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a Cloud Service[架构](/help/overview/architecture.md)
>* [对 AEM as a Cloud Service 的显著更改（发行说明）](/help/release-notes/aem-cloud-changes.md)
>* [对 AEM Assets as a Cloud Service 的显著更改](/help/assets/assets-cloud-changes.md)
>* [将AEM Assets作为Cloud Service介绍](/help/assets/overview.md)
>* [Adobe Experience Manager as a Cloud Service 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html)


AEM Sites作为Cloud Service的更改和添加如下：

* [异步页面操作](#asynchronous-page-operations)
* [新的参考站点和教程](#new-reference-site-and-tutorial)

## 异步页面操作 {#asynchronous-page-operations}

在AEM Cloud服务中，传统上阻止UI的操作已被划分为在后台运行的较小任务。

* 移动页面
* 转出页面

此类操作的发起者可以在位于`/mnt/overlay/dam/gui/content/asyncjobs.html`的新UI中检查其状态。

>[!NOTE]
>
>系统用户无需更改即可使用此新功能。 此处仅将其作为与AEM先前内部部署版本相比的行为更改进行说明。

## 新的参考站点和教程 {#new-reference-site-and-tutorial}

[更新并发布了新的AEM参考网站WKND](https://wknd.site/)，以反映使用AEM构建网站的最佳实践，以及AEM中提供的一整套功能、组件和部署模型。新的引用站点和随附的[教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)涵盖了一些基本主题，如项目设置、核心组件、可编辑的模板、客户端库以及使用Adobe Experience Manager Sites进行组件开发。

以前，We.Retail默认与AEM一起安装（生产模式下启动时除外）。  现在，以后默认情况下不会安装引用站点。  相反，提供了随附教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)的[git repo](https://github.com/adobe/aem-guides-wknd/)和[，以及更新的WKND引用站点代码。

## 运行时无法使用的功能 {#capabilities-not-available-at-runtime}

AEM as aCloud Service始终处于开启状态，并且始终处于最新状态。 要实现此目的，需要将AEM存储库分离到不可变和可变内容中，并在运行时禁止访问不可变内容。 有关可变内容和不可变内容的更多详细信息，请参阅[存储库的可变区域和不可变区域](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable)。

由于不可变内容在运行时无法访问，因此在运行时无法使用以下AEM Sites操作：

* i18n词典翻译
* AEM Sites页面编辑器中的开发人员模式

这些功能可以通过AEM as a Cloud Service的本地独立开发人员实例来使用，用于将AEM作为Cloud ServiceGIT存储库中的内容和代码更新，但不能在托管的运行时实例中使用。
