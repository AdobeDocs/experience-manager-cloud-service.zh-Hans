---
title: AEM Commerceas a Cloud Service快速入門
description: 瞭解如何將具有Commerce功能的AEM專案部署至執行中的AEM as a Cloud Service環境。 使用Adobe Cloud Manager和CI/CD管道的功能，建立執行環境的Venia參考店面。
topics: Commerce
feature: Commerce Integration Framework, Cloud Manager
version: Cloud Service
doc-type: tutorial
kt: 4947
thumbnail: 37843.jpg
exl-id: 73ba707e-5e2d-459a-8cc8-846d1a5f2fd7
source-git-commit: aa7b9daba4242965baf20a77af356952cd7bc279
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 3%

---

# AEM Commerceas a Cloud Service快速入門 {#start}

若要開始使用AEM Commerceas a Cloud Service，您的Experience Manager Cloud Service需要布建Commerce Integration Framework (CIF)附加元件。 CIF附加元件是此附加元件之前的另一個模組 [AEM Sitesas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/home.html).

## 入门培训 {#onboarding}

AEM Commerceas a Cloud Service入門有兩個步驟：

1. 啟用AEM Commerceas a Cloud Service並布建CIF附加元件
2. 將AEM Commerceas a Cloud Service與您的商務解決方案連線

第一個入門步驟透過Adobe完成。 如需定價和布建的詳細資訊，請洽詢您的銷售代表。

布建CIF附加元件後，它會套用至任何現有的Cloud Manager方案。 如果您沒有Cloud Manager計畫，則需要建立一個新計畫。 如需詳細資訊，請參閱 [設定您的程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html).

第二步是每個AEMas a Cloud Service環境的自助服務。 在初始布建CIF附加元件後，您需要進行一些其他設定。

## 將AEM與商務解決方案連線 {#solution}

若要連線CIF附加元件和 [AEM CIF Core Components](https://github.com/adobe/aem-core-cif-components) 使用商務解決方案時，您需要透過Cloud Manager環境變數提供GraphQL端點URL。 變數名稱為 `COMMERCE_ENDPOINT`. 必須設定透過HTTPS的安全連線。

此環境變數用於兩個位置：

- GraphQL會透過AEM CIF核心元件和客戶專案元件使用的一些常見可共用GraphQl使用者端，從AEM呼叫商務後端。
- 在設定變數的每個AEM環境中設定GraphQL Proxy URL，網址為 `/api/graphql`. AEM Commerce編寫工具（CIF附加元件）和CIF使用者端元件會使用此專案。

不同的GraphQL端點URL可用於每個AEMas a Cloud Service環境。 如此一來，專案可將AEM中繼環境與商務中繼系統和AEM生產環境連線到商務生產系統。 GraphQL端點必須是公開可用的，不支援私人VPN或本機連線。 可選擇性地提供驗證標頭，以使用需要驗證的其他CIF功能。

CIF附加元件僅適用於Adobe Commerce Enterprise/Cloud，選擇性支援為AEM作者使用分階段目錄資料。 這需要設定授權標頭。 基於安全理由，此標頭僅適用於AEM編寫執行個體。 AEM發佈執行個體無法顯示分段資料。

有兩個選項可設定端點：

### 透過Cloud Manager UI （預設） {#cm-ui}

>[!VIDEO](https://video.tv.adobe.com/v/37843?quality=12&learn=on)

這可以使用「環境詳細資訊」頁面上的對話方塊來完成。 檢視已啟用Commerce的程式的此頁面時，如果目前未設定端點，則會顯示按鈕：

![CM環境資訊](/help/commerce-cloud/assets/commerce-cmui.png)

按一下此按鈕會開啟一個對話方塊：

![CM商務端點](/help/commerce-cloud/assets/commerce-cm-endpoint.png)

在設定分段目錄支援的端點及選擇性授權標頭後，端點將顯示在詳細資訊頁面上。 按一下「編輯」圖示會開啟相同的對話方塊，您可視需要在此修改端點。

![CM環境資訊](/help/commerce-cloud/assets/commerce-cmui-done.png)

### 透過Adobe I/OCLI  {#adobe-cli}

若要透過Adobe I/OCLI連線AEM與商務解決方案，請遵循下列步驟：

1. 使用Cloud Manager外掛程式取得Adobe I/OCLI

   檢查 [AdobeCloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hans) 下載、設定及使用 [ADOBE I/OCLI](https://github.com/adobe/aio-cli) 使用 [Cloud Manager CLI外掛程式](https://github.com/adobe/aio-cli-plugin-cloudmanager).

2. 使用AEMas a Cloud Service程式驗證Adobe I/OCLI

3. 設定 `COMMERCE_ENDPOINT` Cloud Manager中的變數

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable COMMERCE_ENDPOINT "<Magento GraphQL endpoint URL>"
   ```

   另請參閱 [CLI檔案](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) 以取得詳細資訊。

   商務GraphQL端點URL必須指向商務的GraphQl服務，並使用安全的HTTPS連線。 例如：`https://<yourcommercesystem>/graphql`。

4. 啟用需要驗證的階段式目錄功能（選擇性）

   >[!NOTE]
   >
   >此功能僅適用於Adobe Commerce Enterprise或Cloud Edition。 另請參閱 [權杖型驗證](https://devdocs.magento.com/guides/v2.4/get-started/authentication/gs-authentication-token.html#integration-tokens) 以取得詳細資訊。

   設定 `COMMERCE_AUTH_HEADER` Cloud Manager中的密碼變數：

   ```bash
   aio cloudmanager:set-environment-variables ENVIRONMENT_ID --secret COMMERCE_AUTH_HEADER "Authorization: Bearer <Access Token>"
   ```

>[!TIP]
>
>您可以使用以下命令列出所有Cloud Manager變數來仔細檢查： `aio cloudmanager:list-environment-variables ENVIRONMENT_ID`

有了它，您就可以使用AEM Commerceas a Cloud Service，並且可以透過Cloud Manager部署您的專案。

## 設定存放區和目錄 {#catalog}

CIF附加元件和 [CIF Core Components](https://github.com/adobe/aem-core-cif-components) 可用於連線至不同商業商店（或商店檢視等）的多個AEM網站結構。依預設，CIF附加元件會以連線至Adobe Commerce預設商店和目錄的預設設定部署。

您可以按照以下步驟，透過CIFCloud Service設定來針對專案調整此設定：

1. 在AEM中前往「工具 — >Cloud Services-> CIF設定」

2. 選取您要變更的商務設定

3. 透過動作列開啟設定屬性

![CIFCloud Services設定](/help/commerce-cloud/assets/cif-cloud-service-config.png)

可設定下列屬性：

- GraphQL使用者端 — 選取已設定的GraphQL使用者端以進行商務後端通訊。 這通常應該保持在預設值。
- 存放區檢視 — 存放區檢視識別碼。 如果為空，則使用預設存放區檢視。
- GraphQL Proxy路徑 — AEM中的GraphQL Proxy用來將請求代理至商務後端GraphQL端點的URL路徑。
   >[!NOTE]
   >
   > 在大多數設定中，預設值 `/api/graphql` 不可變更。 只有不使用所提供的GraphQL Proxy的進階設定才應變更此設定。
- 啟用目錄UID支援 — 在商務後端GraphQL呼叫中啟用UID而非ID支援。
   >[!NOTE]
   >
   > Adobe Commerce 2.4.2匯入UID支援。只有在您的Commerce後端支援2.4.2版或更新版本的GraphQL結構描述時，才會啟用此功能。
- 目錄根類別識別碼 — 商店目錄根的識別碼（UID或ID）
   >[!CAUTION]
   >
   > 從CIF Core Components 2.0.0版開始，支援 `id` 已移除並取代為 `uid`. 如果您的專案使用CIF核心元件2.0.0版，您必須啟用目錄UID支援，並使用有效的類別UID作為「目錄根類別識別碼」。

以上所示的設定僅供參考。 專案應提供自己的設定。

如需使用多個AEM網站結構與不同商業目錄結合的更複雜設定，請參閱 [Commerce多商店設定](configuring/multi-store-setup.md) 教學課程。

## 其他资源 {#additional-resources}

- [AEM 项目原型](https://github.com/adobe/aem-project-archetype)
- [AEM Venia參考存放區](https://github.com/adobe/aem-cif-guides-venia)
- [Commerce多商店設定](configuring/multi-store-setup.md)
- [多商务系统设置](configuring/multiple-commerce-systems-setup.md)

