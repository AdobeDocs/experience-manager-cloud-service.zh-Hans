---
title: 管理分阶段的产品目录体验
description: 瞭解如何管理分階段產品目錄體驗。
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 10%

---

# 构建分阶段的产品目录体验 {#building-experiences}

瞭解如何管理分階段產品目錄體驗。

## 迄今为止的故事 {#story-so-far}

在AEM Content and Commerce歷程的上一個檔案中， [管理產品目錄頁面和範本](catalog-templates.md)，您已瞭解如何根據範本管理和建立產品目錄體驗。

本文基於這些基礎之上。

## 目标 {#objective}

本檔案可協助您瞭解如何根據分階段產品資料和AEM啟動來管理產品目錄體驗。 許多時候，作者必須同時準備即將推出的產品（例如新的服裝系列）。 這需要存取階段性產品資料（尚未上線）和準備內容的能力。 此新內容將在產品上市時上線。

    >[！NOTE]
    >
    >此功能僅適用於Adobe Commerce或Cloud Edition，以及支援權杖式驗證的第三方聯結器。 如需詳細資訊，請參閱[快速入門](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html)。

首先，讓我們看看作者如何使用CIF存取分階段產品資料。

## 使用階段產品資料 {#staged-product-data}

存取分階段產品資料的一種方法是使用產品駕駛艙。 按一下AEM主功能表中的Commerce圖示，開啟產品目錄。 這可讓您存取即時產品資料。 開啟左側的篩選標籤並展開 **暫存目錄**. 您現在可以使用預覽資料存取任何時間點的階段產品資料。 階段資料包括新的類別、產品或更新的欄位，例如價格。

![中繼駕駛艙](assets/staged-cockpit.png)

您可以使用時間扭曲檢視來預覽包含分段資料的店面。 開啟編輯器並將模式切換為時間扭曲。 選取任何未來的日期。 請注意編輯器頂端的資訊，表示您正在檢視特定日期的頁面。

![階段時間扭曲](assets/staged-timewarp.png)

您現在可以瀏覽包含分段資料的目錄。 如果您開啟階段類別或產品頁面，編輯器將顯示視覺指示器。

![階段計畫](assets/staged-plp.png)

    >[！NOTE]
    >
    >Omnisearch沒有內容，因此只會傳回即時產品目錄資料

## AEM 启动项 {#launches}

AEM Launches可讓您建立分段產品資料的內容。 如果您不熟悉Launch，請依照 [其他資源區段](#additional-resources). 然後會使用「啟動日期」來存取階段產品資料。

![中繼啟動](assets/staged-launch.png)

請注意，選擇器會遵循啟動日期，並在右側加上分段指示器。

![階段選取器](assets/staged-picker.png)

## 后续内容 {#what-is-next}

現在您已完成歷程的這一部分，您應：

* 透過Launch瞭解分階段產品目錄和內容的概念
* 能夠透過產品駕駛艙和編輯器存取分階段產品目錄資料

您現在已準備好管理 [產品體驗](product-experience-management.md). 不過，AEM Content and Commerce有許多其他可用選項。 查看[“其他资源”部分](#additional-resources)中的一些其他资源，详细了解您在此历程中看到的功能。

## 其他资源 {#additional-resources}

* [产品 Cockpit](/help/commerce-cloud/authoring/product-cockpit.md)
* [快速入门](/help/commerce-cloud/getting-started.md)
* [启动项](/help/sites-cloud/authoring/launches/overview.md)
