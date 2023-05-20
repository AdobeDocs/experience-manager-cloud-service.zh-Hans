---
title: Commerce Integration Framework (CIF)附加元件的重大變更
description: Commerce Integration Framework (CIF)與舊CIF版本相比有重大變更。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: 6c9a44940ea9e52bd27a233c7aa24e320a24076c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 3%

---

# Commerce Integration Framework (CIF)附加元件的重大變更{#notable-changes}

Adobe Experience Manager as a Cloud Service提供許多管理AEM專案的新功能，並帶來許多可能性。 若要進一步瞭解這些功能，請瀏覽以下連結瞭解 [Experience Manageras a Cloud Service的變更](/help/release-notes/aem-cloud-changes.md).

本檔案著重說明Commerce Integration Framework (CIF)附加元件和舊版CIF之間的重要差異，後者稱為CIF Classic (Quickstart)和CIF Open-source。

## 安裝與更新

AEM CIF附加元件會透過Cloud Manager安裝。 安裝需要CIF點數，但沙箱除外，因為可以安裝CIF而不需要點數。 您會透過在AEM合約中布建CIF附加元件來自動接收積分。

此附加元件會隨著一般AEMas a Cloud Service更新而自動更新。

**舊版CIF**

* CIF Classic：不需要安裝，CIF是Quickstart的一部分。 CIF更新是定期AEM或Service Pack更新的一部分
* AEM內部部署的CIF開放原始碼：透過GitHub安裝。 更新是手動更新/維護工作的一部分。
* AEM Adobe Managed Services的CIF開放原始碼：透過Adobe帳戶團隊安裝。 更新是手動更新/維護工作的一部分。

## 端點設定

端點會透過Cloud Manager UI或其CLI進行設定和更新。

**舊版CIF**

* CIF Classic：透過AEM中的OSGi設定
* CIF開放原始碼：透過CIF設定瀏覽器

## 部署CIF Venia專案

中可用的專案 [Cloud Manager Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/integrating-with-git.html) 並透過以下方式完成部署： [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html)

**舊版CIF**

* CIF Classic：透過AEM套件安裝
* cif開放原始碼：透過 [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)

## 產品目錄資料

透過對支援必要GraphQL API的外部端點的即時呼叫，可隨選要求產品目錄資料。 這些API支援在任何指定日期存取即時或分段資料。 不需要復寫。

**舊版CIF**

* CIF Classic：透過完整或差異產品匯入，即時和分階段產品資料匯入並儲存在AEM Author上的JCR中。 即時產品資料會複製到AEM Publish。

## 具有AEM轉譯的產品目錄體驗

AEM會使用已指派給產品和類別的AEM目錄範本，即時呈現產品目錄體驗。 不需要復寫。

**舊版CIF**

* CIF Classic： AEM作者會使用目錄Blueprint工具，為每個類別/產品建立AEM頁面。 這些頁面會復寫到AEM Publish。

>[!NOTE]
>
>如需如何搭配AEM Managed Service或AEM On-premise使用CIF的其他檔案，請參閱 [Commerce整合框架](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
