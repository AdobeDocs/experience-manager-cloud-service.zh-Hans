---
title: 存储库现代化器
description: 了解如何重构现有项目包，使其与为Adobe Experience Manager as a Cloud Service定义的项目结构兼容。
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 2%

---

# 存储库现代化器 {#repo-modernizer}

Repository Modernizer是一个实用程序，开发用于通过将内容和代码分隔到单独的软件包来重构现有项目软件包，以便与为Adobe Experience Manager as a Cloud Service定义的项目结构兼容。

## 简介 {#introduction}

Adobe Experience Manager as a Cloud Service为您的AEM项目提供了许多新功能和可能性。 但是，需要对Adobe Experience Manager Maven项目进行一些更改才能与AEM Cloud Service兼容。 从较高层面看，AEM要求将 **内容** 和 **代码** 分为离散的子包，以遵循可变和不可变内容之间的拆分。 请参阅 [AEM项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html) 以了解有关用于Cloud Service的新AEM项目结构的更多详细信息。

Repository Modernizer通过创建以下部署结构来创建兼容的AEM Cloud Service项目结构：

* `ui.apps` 包部署到 `/apps` 并包含所有代码

* `ui.content` 软件包部署到运行时可写区域(例如， `/content`， `/conf`， `/home`，或任何其他非项目 `/apps`)并包含所有内容和配置。

* `all` 包是包含子包的容器包 `ui.apps` 和 `ui.content`.

>[!NOTE]
>项目结构基于 *24原型* 程序包及其 `pom.xml/filter.xml files`. 请参阅 [24原型](https://github.com/adobe/aem-project-archetype) 以了解更多详细信息。

## 使用存储库现代化器 {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* 通过Adobe I/OCLI ：Adobe建议通过以下方式使用Repository Modernizer `aio-cli-plugin-aem-cloud-service-migration` (用于Adobe I/OCLI的AEMas a Cloud Service代码重构插件)。

  请参阅 **[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 这样您就可以了解如何安装和使用插件。

* 作为独立实用程序：Repository Modernizer也可以作为独立实用程序执行。

  请参阅 **[Git资源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** 这样您就可以了解如何使用此工具。

  >[!NOTE]
  >
  >Repository Modernizer是使用NodeJS开发的。 建议安装NodeJS 10.0+。
