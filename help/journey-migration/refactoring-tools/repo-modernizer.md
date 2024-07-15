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

Adobe Experience Manager as a Cloud Service为您的AEM项目提供了许多新功能和可能性。 但是，需要对Adobe Experience Manager Maven项目进行一些更改才能与AEM Cloud Service兼容。 在高级别，AEM要求将&#x200B;**内容**&#x200B;和&#x200B;**代码**&#x200B;分离为离散的子包，以遵循可变和不可变内容之间的拆分。 有关用于Cloud Service的新AEM项目结构的更多详细信息，请参阅[AEM项目结构](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html)。

Repository Modernizer通过创建以下部署结构来创建兼容的AEM Cloud Service项目结构：

* `ui.apps`包部署到`/apps`并包含所有代码

* `ui.content`包部署到运行时可写区域（例如，`/content`、`/conf`、`/home`或非`/apps`的任何区域）并包含所有内容和配置。

* `all`包是包含子包`ui.apps`和`ui.content`的容器包。

>[!NOTE]
>项目结构基于包及其`pom.xml/filter.xml files`的&#x200B;*原型24*。 有关详细信息，请参阅[原型24](https://github.com/adobe/aem-project-archetype)。

## 使用存储库现代化器 {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* 通过Adobe I/OCLI ：Adobe建议通过`aio-cli-plugin-aem-cloud-service-migration` (用于Adobe I/OCLI的AEM as a Cloud Service代码重构插件)使用Repository Modernizer。

  请参阅&#x200B;**[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**，以便您了解如何安装和使用插件。

* 作为独立实用程序：Repository Modernizer也可以作为独立实用程序执行。

  请参阅&#x200B;**[Git资源：存储库现代化器](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)**，以便您了解如何使用此工具。

  >[!NOTE]
  >
  >Repository Modernizer是使用NodeJS开发的。 建议安装NodeJS 10.0+。
