---
title: 存储库现代化器
description: 存储库现代化器
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 6%

---

# 存储库现代化器 {#repo-modernizer}

Repository Modernizer是一个实用程序，旨在通过将内容和代码分离为离散的包来重构现有项目包，以便与为Adobe Experience Manager as a Cloud Service定义的项目结构兼容。

## 简介 {#introduction}

Adobe Experience Manager as a Cloud Service为您的AEM项目提供了许多新功能和可能性。 但是，Adobe Experience Manager Maven项目需要进行一些更改才能与AEM Cloud Service兼容。 在高级别，AEM要求将 **内容** 和 **代码** 分离子包，以遵循可变内容和不可变内容之间的拆分。 请参阅 [AEM项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 有关用于Cloud Service的新AEM项目结构的更多详细信息。

Repository Modernizer通过创建以下部署结构创建兼容的AEM Cloud Service项目结构：

* `ui.apps` 包部署到 `/apps` 和包含所有代码

* `ui.content` 包部署到运行时可写区域(例如， `/content`, `/conf`, `/home`，或任何其他非 `/apps`)并包含所有内容和配置。

* `all` 包是包含子包的容器包 `ui.apps` 和 `ui.content`.

>[!NOTE]
>项目结构基于 *原型24* 包及其 `pom.xml/filter.xml files`. 请参阅 [原型24](https://github.com/adobe/aem-project-archetype) 以了解更多详细信息。

## 使用Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* 通过Adobe I/OCLI :建议通过 `aio-cli-plugin-aem-cloud-service-migration` (AEMas a Cloud Service代码重构插件，用于Adobe I/OCLI)。

   请参阅 **[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 了解如何安装和使用插件。

* 作为独立实用程序：Repository Modernizer也可以作为独立实用程序执行。

   请参阅 **[Git资源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** 了解如何使用此工具。

   >[!NOTE]
   >
   >Repository Modernizer是使用NodeJS开发的。 建议安装NodeJS 10.0+。
