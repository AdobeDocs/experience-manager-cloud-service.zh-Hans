---
title: 对 AEM Cloud Service 中的 AEM Sites 的重要更改
description: 对 AEM Cloud Service 中的 AEM Sites 的重要更改
exl-id: 60b1aec4-75a0-459f-bf77-8d8c1af757ce
source-git-commit: ab81bca96bcf06b06357f900464e999163bb1bb2
workflow-type: ht
source-wordcount: '532'
ht-degree: 100%

---

# 对 AEM Sites as a Cloud Service 的重要更改 {#notable-changes}

AEM Sites as a Cloud Service 提供了体验管理功能作为云原生 AEM as a Cloud Service 平台的一部分。除了 AEM as a Cloud Service 的核心优势（例如云原生可扩展性、正常运行时间和始终保持最新）之外，AEM Sites as a Cloud Service 还提供了许多特定于站点的更改和补充。

>[!NOTE]
>本文档重点介绍了对 AEM Sites 的重要更改。有关对 AEM as a Cloud Service 和其他模块的一般更改，请参阅：
>
>* [Adobe Experience Manager as a Cloud Service 简介](/help/overview/introduction.md)
>* [AEM as a Cloud Service 概述 – 新增功能和改进功能](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a Cloud Service 的[架构](/help/overview/architecture.md)
>* [对 AEM as a Cloud Service 的重要更改（发行说明）](/help/release-notes/aem-cloud-changes.md)
>* [对 AEM Assets as a Cloud Service 的重要更改](/help/assets/assets-cloud-changes.md)
>* [AEM Assets as a Cloud Service 简介](/help/assets/overview.md)
>* [Adobe Experience Manager as a Cloud Service 教程](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/overview.html?lang=zh-Hans)


AEM Sites as a Cloud Service 中的更改和补充如下所示：

* [异步页面操作](#asynchronous-page-operations)
* [新引用站点和教程](#new-reference-site-and-tutorial)

## 异步页面操作 {#asynchronous-page-operations}

在 AEM Cloud Service 中，传统上阻止 UI 的操作已分解成后台运行的多个小型任务。

* 移动页面
* 转出页面

此类操作的发起者可以在 `/mnt/overlay/dam/gui/content/asyncjobs.html` 上的新 UI 中检查其状态。

>[!NOTE]
>
>系统用户无需进行更改即可使用此新功能。此处仅将它记录为以前的 AEM 本地版本的行为变化。

## 新引用站点和教程 {#new-reference-site-and-tutorial}

[WKND](https://wknd.site/)（新的 AEM 引用站点）已进行更新和发布，以反映使用 AEM 构建网站的最佳实践，以及 AEM 中提供的一整套功能、组件和部署模型。新的引用站点和[随附教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans)涵盖了项目设置、核心组件、可编辑模板、客户端库和使用 Adobe Experience Manager Sites 进行组件开发等基本主题。

以前，We.Retail 默认与 AEM 一起安装（在生产模式下启动时除外）。现在，默认情况下将不会安装引用站点。而是将提供 [Git 存储库](https://github.com/adobe/aem-guides-wknd/)和[随附教程](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hans)以及更新后的 WKND 引用站点代码。

## 运行时不可用的功能 {#capabilities-not-available-at-runtime}

AEM as a Cloud Service 始终处于开启状态并保持最新。要实现这一点，需要将 AEM 存储库分为不可变内容和可变内容，并禁止在运行时访问不可变内容。有关可变内容与不可变内容的更多详细信息，请参阅[存储库的可变与不可变区域](/help/implementing/developing/introduction/aem-project-content-package-structure.md#mutable-vs-immutable)。

由于在运行时无法访问不可变内容，因此，以下 AEM Sites 操作在运行时不可用：

* i18n 词典翻译
* AEM Sites 页面编辑器中的开发人员模式

可以通过 AEM as a Cloud Service 的本地独立开发人员实例使用这些功能来更新 AEM as a Cloud Service GIT 存储库中的内容和代码，但不能在托管的运行时实例中使用。
