---
title: 存储库Modernizer
description: 存储库Modernizer
translation-type: tm+mt
source-git-commit: fd70f5b6a17666d411a64a8fb3961555a42a5430
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 3%

---


# 存储库Modernizer {#repo-modernizer}

Repository Modernizer是一个实用程序，它通过将内容和代码分离成离散的包来重组现有项目包，以与为Adobe Experience Manager定义为Cloud Service的项目结构兼容。

## 简介 {#introduction}

Adobe Experience Manager作为Cloud Service，为您的AEM项目带来许多新功能和可能性。 但是，Adobe Experience ManagerMaven项目需要进行一些更改，才能与AEMCloud Service兼容。 在高级别上，AEM要求将内容和 **代码分** 离 **成离散的** 子包，以尊重可变内容和不可变内容之间的拆分。 有关新AEM项 [目结构的更](https://docs.adobe.com/content/help/zh-Hans/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 多详细信息，请参阅AEM项目结构以进行Cloud Service。

存储库现代化器通过创建以下部署结构创建兼容的AEMCloud Service项目结构：

* `ui.apps` 包部署到并 `/apps` 包含所有代码

* `ui.content` 包部署到运行时可写区域(例如， `/content`、 `/conf`、 `/home`或任何非 `/apps`内容)，并包含所有内容和配置。

* `all` 包是包含子包和的容器 `ui.apps` 包 `ui.content`。

## 使用存储库Modernizer {#using-repo-modernizer}

* 通过AdobeI/O CLI :建议通过(AEM作为AdobeI/O `aio-cli-plugin-aem-cloud-service-migration` CLI的Cloud Service代码重构插件)使用存储库Modernizer。

   请参阅 **[Git资源：aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** ，了解如何安装和使用插件。

* 作为独立实用程序：存储库Modernizer也可以作为独立实用程序执行。

   请参阅 **[Git资源：Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** ，了解如何使用此工具。
