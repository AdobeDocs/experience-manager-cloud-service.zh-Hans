---
title: RemotePage 组件
description: RemotePage元件是自訂頁面元件，用於在AEM內編輯遠端React SPA。
exl-id: d3465592-0392-49b0-b49d-de93983c1d6e
source-git-commit: d213dd0788e66015237d241caf0f3b5737ce725c
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%

---

# RemotePage 组件 {#remote-page-component}

決定時 [哪一個層級的整合](/help/implementing/developing/headful-headless.md) 您想要在外部SPA和AEM之間使用，通常很明顯您需要能夠在AEM中檢視和編輯SPA。 RemotePage元件是僅供此目的使用的自訂頁面元件。

## 概述 {#overview}

RemotePage元件會從應用程式產生的擷取所有必要的資產 `asset-manifest.json` 和用來在AEM中轉譯SPA。

* RemotePage可讓您將SPA的指令碼和樣式表插入AEM Page元件的內文中。
* 虛擬前端元件允許在AEM SPA編輯器中將區段標示為可編輯。
* 將託管在不同網域上的SPA放在一起，即可在AEM中編輯。

請參閱文章 [在AEM內編輯外部SPA](editing-external-spa.md) 以進一步瞭解AEM中可編輯的外部SPA。

## 要求 {#requirements}

* 在開發中啟用CORS
* 在頁面屬性中設定遠端URL
* 在AEM中轉譯SPA
* Web應用程式必須使用類似下列其中一種的套件組合資產資訊清單，並公開 `asset-manifest.json` 位於網域根目錄的檔案，該檔案會列在 `entrypoints property` 所有要載入的CSS和JS檔案：
   * https://github.com/shellscape/webpack-manifest-plugin
   * https://github.com/webdeveric/webpack-assets-manifest
   * https://github.com/mugi-uno/parcel-plugin-bundle-manifest
      ![entrypoints屬性範例](assets/asset-manifest-entrypoints.png)
* 應用程式必須能夠在中初始化 `<div id="root"></div>` 底下 `body` 元素。 如果應用程式需要不同的標籤才能具現化，則必須在具有的Proxy元件的HTL指令碼中據以調整 `sling:resourceSuperType="spa-project-core/components/remotepage`.

## 限制 {#limitations}

* RemotePage元件預期實作會提供如下的資產資訊清單 [可在此處找到。](https://github.com/shellscape/webpack-manifest-plugin) 不過，RemotePage元件僅經過測試，可用於React架構（以及透過remote-page-next元件的Next.js），因此不支援從其他架構(例如Angular)遠端載入應用程式。
* 在AEM中執行遠端轉譯時，應用程式的根HTML檔案中定義的內部CSS以及根DOM節點上的內嵌CSS將不可用。

## 技术详细信息 {#technical-details}

如同其他的AEM SPA專案，RemotePage元件是開放原始碼。 如需RemotePage元件的完整技術詳細資訊， [請參閱GitHub存放庫。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
