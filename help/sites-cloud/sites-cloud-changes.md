---
title: 对 AEM 云服务中 AEM Sites 的显著更改
description: '对 AEM 云服务中 AEM Sites 的显著更改 '
translation-type: tm+mt
source-git-commit: e381807d7c199113689304e9481dfe2022ee5f93
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 21%

---


# 对 AEM Sites as a Cloud Service 的显著更改 {#notable-changes}

AEM Sites作为Cloud Service，作为云本地AEM的一个Cloud Service平台的一部分，提供体验管理功能。 除了AEM作为Cloud Service的核心优势（如云本机可伸缩性、正常运行时间以及始终处于最新状态）外，AEM Sites作为Cloud Service还提供了许多特定于站点的更改和添加。

>[!NOTE]
>这一文档突显了AEM Sites的显着变化。 有关AEM作为Cloud Service和其他模块的常规更改，请参阅：
>
>* [Adobe Experience Manager as a Cloud Service 简介](/help/overview/introduction.md)
>* [AEM as a Cloud Service 概述 - 新增功能和改进功能](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a Cloud Service[架构](/help/core-concepts/architecture.md)
>* [对 AEM as a Cloud Service 的显著更改（发行说明）](/help/release-notes/aem-cloud-changes.md)
>* [对 AEM Assets as a Cloud Service 的显著更改](/help/assets/assets-cloud-changes.md)
>* [将AEM Assets作为Cloud Service](/help/assets/overview.md)
>* [Adobe Experience Manager as a Cloud Service 教程](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/overview.html)


AEM Sites作为Cloud Service的变动和增补如下：

* [异步页面操作](#asynchronous-page-operations)
* [新参考站点和教程](#new-reference-site-and-tutorial)

## 异步页面操作 {#asynchronous-page-operations}

在AEM Cloud服务中，传统上阻止UI的操作已细分为在后台运行的较小任务。

* 移动页面
* 滚出页面

此类操作的发起者可以在新的UI中检查其状态 `/mnt/overlay/dam/gui/content/asyncjobs.html`。

>[!NOTE]
>
>系统用户无需更改即可利用此新功能。 此处仅指出它与AEM的先前内部部署版本相比的行为发生了变化。

## 新参考站点和教程 {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/)是一个新的AEM参考站点，它已更新并发布，以反映构建包含AEM的网站以及AEM提供的一整套功能、组件和部署模型的最佳做法。 新的参考站点和随附 [的教程](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) ，涵盖基本主题，如项目设置、核心组件、可编辑模板、客户端库以及与Adobe Experience Manager Sites的组件开发。

以前，We.Retail默认安装在AEM中（在生产模式下启动时除外）。  现在，默认情况下，以后将不会安装引用站点。  而是提 [供了git](https://github.com/adobe/aem-guides-wknd/) repo [以及随附的教程](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) ，以及更新的WKND参考站点代码。

## 运行时不提供的功能 {#capabilities-not-available-at-runtime}

AEM作为Cloud Service始终处于开启状态并始终保持最新状态。 要实现这一点，需要将AEM存储库分离在不可变和可变内容中，并在运行时禁止访问不可变内容。 有关可变内容与不可变内容的更多详细 [信息，请参阅存储库的可变区与不可变区域](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable)。

由于不可变的内容在运行时无法访问，以下AEM Sites操作在运行时不可用：

* i18n词典翻译
* AEM Sites页面编辑器中的开发者模式

这些功能可以通过AEM的本地独立开发人员实例作为Cloud Service使用，用于将AEM中的内容和代码作为Cloud ServiceGIT存储库进行更新，但不能在托管运行时实例中使用。
