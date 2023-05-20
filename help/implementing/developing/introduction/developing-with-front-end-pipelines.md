---
title: 使用前端管道开发站点
description: 有了前端管道，前端開發人員可獲得更多獨立性，且開發流程可獲得大幅度的速度。 本檔案說明應予說明的前端建置流程的一些特定考量事項。
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
source-git-commit: a6b228023d7bd2a40e4db3a1d2c3900a5c24031c
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 1%

---


# 使用前端管道开发站点 {#developing-site-with-front-end-pipeline}

[透過前端管道，](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end) 前端開發人員可獲得更多獨立性，且開發流程可獲得大幅度的速度。 本檔案說明此程式的運作方式，以及一些需要注意的事項，以便充分發揮此程式的潛力。

>[!TIP]
>
>如果您還不熟悉如何使用前端管道及其帶來的好處，請檢視 [快速網站建立歷程](/help/journey-sites/quick-site/overview.md) 有關如何快速部署新網站並完全獨立於後端開發來自訂其主題的範例。

## 前端建置合約 {#front-end-build-contract}

類似於 [完整棧疊組建環境，](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) 前端管道有其自己的環境。 只要遵循以下前端建置合約，開發人員就可以在此管道中擁有一些彈性。

前端管道需要前端Node.js專案使用 `build` 指令碼指示詞，用於產生將由前端管道部署的建置。 即Cloud Manager使用命令 `npm run build` 將可部署的專案產生至 `dist` 資料夾。

的內容 `dist` 資料夾是最終部署到AEM的內容，與Cloud Manager管道as a Cloud Service。

### 節點版本 {#node-versions}

預設情況下，前端管道使用節點14，但也可以使用12和16。

您可以使用 `CM_CUSTOM_VAR_NODE_VERSION` 環境變數來設定所需的版本。

## 單一信任來源 {#single-source-of-truth}

一般良好做法是維護部署至AEM的單一信任來源。 Cloud Manager的目標是讓該單一真實來源變得顯而易見。 但是，由於前端管道允許分離部分代碼的位置，因此前端管道的正確設定有一些額外的責任。 必須注意不要建立多個前端管道來部署到相同環境中的相同站點。

因此，特別是當建立了幾個前端管道時，建議保持如以下的系統化命名慣例：

* 前端模組的名稱，由 `name` 的屬性 `package.json` 檔案中，應包含套用到的網站名稱。 例如，對於位於 `/content/wknd`，前端模組的名稱會類似於 `wknd-theme`.
* 當前端模組與其他模組共用相同的Git存放庫時，其資料夾名稱應等於或包含前端模組的相同名稱。 例如，如果前端模組命名為 `wknd-theme`，則封入資料夾名稱類似於 `wknd-theme-sources`.
* Cloud Manager前端管道的名稱也應包含前端模組的名稱，並新增其部署到的環境（生產或開發）。 例如，對於前端模組命名為 `wknd-theme`，此管道的名稱可能如下 `wknd-theme-prod`.

此慣例應有效防止下列部署錯誤：

* 將前端模組套用至錯誤的網站
* 建立多個套用相同網站的前端模組，這會相互覆寫
* 為相同來源建立多個前端管道，這可能會導致競爭條件，無法保證部署順序

## 分离关注点 {#separation-of-concerns}

適用於任何疑慮分離的另一個良好做法，是特別注意分離疑慮的合約如何設計和管理。 在前端管道中，將該程式碼與其餘程式碼分開的合約是網站呈現的HTML和JSON。 如果該HTML和JSON保持穩定，則前端管道會讓前端團隊完全獨立，以實現其最大價值。

目前沒有與前端管道同步執行完整棧疊管道的特定功能。 因此，當將前端開發從完整棧疊管道分離時，必須在分離這兩個關注領域的合約中格外小心。 該合約通常是Experience Manager轉譯的HTML和/或JSON。 因此，該合約的變更必須在操作不同管道的團隊之間精心規劃，以便他們同意如何排列對應變更的順序。

當需要對HTML和/或JSON輸出執行會影響這兩個關注領域的變更時，通常建議採取以下步驟。

1. 後端團隊會先使用新HTML和/或JSON輸出設定開發環境。
   1. 透過完整棧疊管道，他們部署轉譯所需新HTML和/或JSON輸出所需的程式碼。
   1. 如果這屬於前端團隊之前無權存取的環境，則必須執行以下步驟。
      1. URL：前端團隊必須知道該開發環境的URL。
      1. ACL：必須為前端團隊指派具有類似「貢獻者」許可權的本機AEM使用者。
      1. Git：前端團隊必須為明確針對該開發環境的前端模組提供單獨的Git位置。
         * 通常的做法是建立 `dev` 分支，如此一來針對開發環境所做的變更，便可輕鬆合併回 `main` 要部署到生產環境的分支。
      1. 管道：前端團隊必須具有部署到開發環境的前端管道。 該管道將部署通常位於以下位置的前端模組： `dev` 分支，如上一個點所述。
1. 前端團隊接著會讓CSS和JS程式碼同時使用舊輸出和新輸出。
   1. 如往常一樣，若要在本機開發：
      1. 此 `npx aem-site-theme-builder proxy` 在前端模組內執行的命令會啟動向AEM環境請求內容的Proxy伺服器，同時將前端模組的CSS和JS檔案替換為來自本機的檔案 `dist` 資料夾。
      1. 設定 `AEM_URL` 變數 `.env` 檔案可控制本機Proxy伺服器使用內容的AEM環境。
      1. 變更此專案的值 `AEM_URL` 因此，允許在生產環境和開發環境之間切換，以便調整CSS和JS，使其適合這兩個環境。
      1. 它必須與呈現新輸出的開發環境以及呈現舊輸出的生產環境搭配使用。
   1. 前端工作是在更新的前端模組適用於兩個環境時完成，並部署至兩個環境。
1. 然後，後端團隊可以透過部署程式碼來更新生產環境，該程式碼會透過完整棧疊管道來呈現新HTML和/或JSON輸出。
1. 然後，前端團隊可以清理其CSS和JS，並移除僅需要舊輸出的內容，透過前端管道將最後一次更新部署到生產環境。

## 其他资源 {#additional-resources}

* [網站主題](/help/sites-cloud/administering/site-creation/site-themes.md)  — 瞭解如何使用AEM網站主題來自訂網站的樣式和設計。
* [AEM網站主題產生器](https://github.com/adobe/aem-site-theme-builder) -Adobe提供AEM網站主題產生器，作為一組用於建立新網站主題的指令碼。
