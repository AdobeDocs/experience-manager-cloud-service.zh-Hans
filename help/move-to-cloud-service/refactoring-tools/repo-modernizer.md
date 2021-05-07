---
title: 存储库Modernizer
description: 存储库Modernizer
exl-id: b89156a8-3d7d-4d36-89a2-beeda35bbc01
translation-type: tm+mt
source-git-commit: 0ed18aad48f33fb0504d59a5f583b5a3dbea59f6
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 4%

---

# 存储库Modernizer {#repo-modernizer}

Repository Modernizer是一个实用程序，它通过将内容和代码分离为离散的包来重构现有项目包，以与为Adobe Experience Manager定义的项目结构(作为Cloud Service)兼容。

## 简介 {#introduction}

Adobe Experience Manager作为一名Cloud Service，为您的AEM项目带来了许多新增功能和可能性。 但是，Adobe Experience Manager Maven项目需要进行一些更改，才能与AEM Cloud Service兼容。 在高级别上，AEM要求将&#x200B;**内容**&#x200B;和&#x200B;**代码**&#x200B;分离为离散子包，以尊重可变内容和不可变内容之间的分离。 请参阅[AEM项目结构](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)，了解有关用于Cloud Service的新AEM项目结构的详细信息。

存储库现代化器通过创建以下部署结构创建一个兼容的AEM Cloud Service项目结构：

* `ui.apps` 包部署到 `/apps` 并包含所有代码

* `ui.content` 包部署到运行时可写区域(例如 `/content`、 `/conf`、 `/home`或任何非 `/apps`)，并包含所有内容和配置。

* `all` package是包含子包和的容器 `ui.apps` 包 `ui.content`。

>[!NOTE]
>项目结构基于&#x200B;*Archetype 24*，用于包及其`pom.xml/filter.xml files`。 有关更多详细信息，请参阅[Archetype 24](https://github.com/adobe/aem-project-archetype)。

## 使用存储库Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* 通过Adobe I/O CLI :建议通过`aio-cli-plugin-aem-cloud-service-migration`使用Repository Modernizer(AEM作为Adobe I/O CLI的Cloud Service代码重构插件)。

   请参阅&#x200B;**[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**&#x200B;了解如何安装和使用插件。

* 作为独立的实用程序：Repository Modernizer也可以作为独立实用程序执行。

   请参阅&#x200B;**[Git资源：存储库Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)**&#x200B;了解如何使用此工具。

   >[!NOTE]
   >
   >存储库Modernizer是使用NodeJS开发的。 建议安装NodeJS 10.0+。
