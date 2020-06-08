---
title: 对 AEM 云服务中 AEM Sites 的显著更改
description: '对 AEM 云服务中 AEM Sites 的显著更改 '
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 11%

---


# 对 AEM Sites 云服务的显著更改 {#notable-changes}

AEM Sites作为云服务平台，作为云本机AEM的一部分，提供体验管理功能。 除了AEM作为云服务的核心优势（如云本机可伸缩性、正常运行时间以及始终处于最新状态）外，AEM Sites作为云服务还提供了许多特定于站点的更改和添加。

>[!NOTE]
>此文档重点介绍对AEM Sites的显着更改。 有关云中AEM的常规更改，请参阅：
>
>* [对 Adobe Experience Manager (AEM) 云服务的显著更改](/help/release-notes/aem-cloud-changes.md)


AEM Sites作为云服务的更改和添加内容如下：

* [异步页面操作](#asynchronous-page-operations)
* [新参考站点和教程](#new-reference-site-and-tutorial)

## 异步页面操作 {#asynchronous-page-operations}

在AEM Cloud服务中，传统上阻止UI的操作已细分为在后台运行的较小任务。

* 移动页面
* 滚出页面

此类操作的发起者可以在新的UI中检查其状态 `/mnt/overlay/dam/gui/content/asyncjobs.html`。

>[!NOTE]
>
>系统用户无需更改即可利用此新功能。 此处仅指出它是与AEM的先前内部部署版本相比的行为变化。

## 新参考站点和教程 {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/)是一个新的AEM参考站点，它已更新并发布，以反映使用AEM构建网站的最佳实践以及AEM中提供的一整套功能、组件和部署模型。 新的参考站点和随附 [的教程](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) ，涵盖基本主题，如项目设置、核心组件、可编辑模板、客户端库以及使用Adobe Experience Manager Sites进行组件开发。

以前，We.Retail是默认随AEM一起安装的（在生产模式下启动时除外）。  现在，默认情况下，以后将不会安装引用站点。  而是提 [供了git](https://github.com/adobe/aem-guides-wknd/) repo [以及随附的教程](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) ，以及更新的WKND参考站点代码。

## 运行时不提供的功能 {#capabilities-not-available-at-runtime}

AEM作为云服务始终处于最新状态。 要实现这一点，需要将AEM存储库分离在不可变和可变内容中，并在运行时禁止访问不可变内容。 有关可变内容与不可变内容的更多详细 [信息，请参阅存储库的可变区与不可变区域](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable)。

由于不可变内容在运行时不可访问，因此以下AEM站点操作在运行时不可用：

* i18n词典翻译
* AEM站点页面编辑器中的开发人员模式

这些功能可通过AEM的本地独立开发人员实例（作为云服务）使用，以作为云服务GIT存储库更新AEM中的内容和代码，但不能在托管运行时实例中使用。
