---
title: Repository Modernizer
description: Repository Modernizer
exl-id: b89156a8-3d7d-4d36-89a2-beeda35bbc01
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# Repository Modernizer {#repo-modernizer}

Repository Modernizer是一个实用程序，旨在通过将内容和代码分离为离散的包来重构现有项目包，以与为Adobe Experience Manager(作为Cloud Service)定义的项目结构兼容。

## 简介 {#introduction}

Adobe Experience Manager as aCloud Service为您的AEM项目提供了许多新功能和可能性。 但是，Adobe Experience Manager Maven项目需要进行一些更改才能与AEMCloud Service兼容。 在高级别上， AEM要求将&#x200B;**内容**&#x200B;和&#x200B;**代码**&#x200B;分离为离散的子包，以考虑在可变内容和不可变内容之间进行拆分。 有关新的AEM项目结构以进行Cloud Service的更多详细信息，请参阅[AEM项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html)。

Repository Modernizer通过创建以下部署结构创建兼容的AEMCloud Service项目结构：

* `ui.apps` 包部署到并 `/apps` 包含所有代码

* `ui.content` 包部署到运行时可写区域(例如， `/content`、  `/conf`、  `/home`或任何非 `/apps`的内容)并包含所有内容和配置。

* `all` 包是包含子包和的容器 `ui.apps` 包 `ui.content`。

>[!NOTE]
>项目结构基于&#x200B;*包及其`pom.xml/filter.xml files`的Archetype 24*。 有关更多详细信息，请参阅[Archetype 24](https://github.com/adobe/aem-project-archetype)。

## 使用Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* 通过Adobe I/OCLI :建议通过`aio-cli-plugin-aem-cloud-service-migration`使用Repository Modernizer(AEM作为Adobe I/OCLI的Cloud Service代码重构插件)。

   请参阅&#x200B;**[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** ，以了解如何安装和使用插件。

* 作为独立实用程序：Repository Modernizer也可以作为独立实用程序执行。

   请参阅&#x200B;**[Git资源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)**&#x200B;以了解如何使用此工具。

   >[!NOTE]
   >
   >Repository Modernizer是使用NodeJS开发的。 建议安装NodeJS 10.0+。
