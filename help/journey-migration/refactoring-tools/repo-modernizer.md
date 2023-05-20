---
title: 存储库现代化器
description: 存储库现代化器
exl-id: cd9d212e-e720-4209-8b5a-659883cc1d95
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 6%

---

# 存储库现代化器 {#repo-modernizer}

Repository Modernizer是一個公用程式，開發目的是將內容和程式碼分割為獨立套件，以與Adobe Experience Manager as a Cloud Service定義的專案結構相容，藉此重組現有的專案套件。

## 简介 {#introduction}

Adobe Experience Manager as a Cloud Service為您的AEM專案提供許多新功能和可能性。 不過，Adobe Experience Manager Maven專案必須進行一些變更，才能與AEM Cloud Service相容。 概略來說，AEM需要分隔 **內容** 和 **程式碼** 分成離散的子套件，以遵循可變和不可變內容之間的分割。 請參閱 [AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 以進一步瞭解Cloud Service的新AEM專案結構。

Repository Modernizer會建立下列部署結構，以建立相容的AEM Cloud Service專案結構：

* `ui.apps` 套件部署至 `/apps` 並包含所有程式碼

* `ui.content` 套件部署到執行階段可寫入的區域(例如， `/content`， `/conf`， `/home`，或不存在的任何專案 `/apps`)並包含所有內容和設定。

* `all` 封裝是包含子封裝的容器封裝 `ui.apps` 和 `ui.content`.

>[!NOTE]
>專案結構是根據 *原型24* 適用於套件及其 `pom.xml/filter.xml files`. 請參閱 [原型24](https://github.com/adobe/aem-project-archetype) 以取得更多詳細資料。

## 使用Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

* 透過Adobe I/OCLI ：建議透過以下方式使用Repository Modernizer： `aio-cli-plugin-aem-cloud-service-migration` (Adobe I/OCLI的AEMas a Cloud Service程式碼重構外掛程式)。

   請參閱 **[Git資源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 瞭解如何安裝及使用外掛程式。

* 作為獨立公用程式： Repository Modernizer也可以作為獨立公用程式執行。

   請參閱 **[Git資源： Repository Modernizer](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer)** 以瞭解如何使用此工具。

   >[!NOTE]
   >
   >Repository Modernizer是使用NodeJS開發。 建議安裝NodeJS 10.0+。
