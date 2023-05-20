---
title: 移轉至AEM Commerce Integration Framework (CIF)附加元件
description: 如何從舊版本移轉至AEM Commerce Integration Framework (CIF)附加元件
exl-id: 0db03a05-f527-4853-b52f-f113bce929cf
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 28%

---

# Experience Manager Cloud Service移轉指南 {#cif-migration}

本指南帮助确定您需要为 Experience Manager Cloud Service 迁移而更新的领域。

## CIF附加元件

对于 Experience Manager as a Cloud Service，CIF 加载项是 Adobe Commerce 和第三方 Commerce 唯一支持的 Commerce 集成解决方案。CIF 加载项自动为 Experience Manager as a Cloud Service 上的客户部署，无需手动部署。请参阅 [AEM Commerce as a Cloud Service 快速入门](getting-started.md)。

若要支援部署CIFAdobe的專案，請提供 [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components).

CIF 加载项可用于 AEM 6.5 以及通过[软件分发门户](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html)使用。它是兼容的，提供了与 Experience Manager as a Cloud Service 的 CIF 加载项相同的功能，无需调整。

Classic CIF 及其依赖项不再可用。依賴此CIF版本的程式碼，使用 `com.adobe.cq.commerce.api` Java API必須調整為CIF附加元件及其原則。

無法再安裝先前可用的CIF聯結器。 依賴此聯結器的程式碼需要調整為CIF附加元件及其原則。

## 專案結構

瞭解 [AEM專案結構](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) 以及AEMas a Cloud Service的特性。 將專案設定調整為AEMas a Cloud Service版面。
與AEM 6.5部署相比，以下有兩個主要差異：

* GraphQL使用者端OSGI套件組合 **不得** 會透過CIF附加元件部署AEM專案
* GraphQL使用者端和Graphql資料服務的OSGI設定 **不得** 已包含在AEM專案中

>[!TIP]
>
>檢視 [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia) GitHub專案。 此專案為AEMas a Cloud Service和內部部署提供Maven設定檔，這些設定檔會考慮不同的框架條件。

## 產品目錄

不再支援匯入產品目錄資料。 使用CIF附加元件主參與者產品和目錄請求是透過對外部商務解決方案的即時呼叫隨選的。 前往整合一章，進一步瞭解整合商務解決方案。

>[!TIP]
>
>如果沒有可用的即時API，則應使用具有API的外部產品快取進行整合。 範例 [Magento開放原始碼](https://business.adobe.com/products/magento/open-source.html).

## 具有AEM轉譯的產品目錄體驗

如果您使用包含Classic CIF的目錄Blueprint，則需要更新產品目錄工作流程。 CIF附加元件現在會使用AEM目錄範本即時轉譯產品目錄體驗。 不再需要複製產品資料或產品頁面。

## 無法快取的資料和購物互動

不可快取資料和互動的使用者端請求（例如加入購物車、搜尋）應透過CDN / Dispatcher直接前往商務端點（商務解決方案或整合層）。 移除AEM只是Proxy的任何呼叫。
