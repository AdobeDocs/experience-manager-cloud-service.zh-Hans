---
title: AEM Formsas a Cloud Service — 通訊
description: 自动将数据与 XDP 和 PDF 模板合并，或以 PCL、ZPL 和 PostScript 格式生成输出
exl-id: 9fa9959e-b4f2-43ac-9015-07f57485699f
source-git-commit: 33e59ce272223e081710294a2e2508edb92eba52
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 7%

---


# 使用同步處理 {#sync-processing-introduction}

Formsas a Cloud Service- Communications API可讓您建立、彙編及提供品牌導向和個人化的通訊，例如商業往來函、檔案、報表、索賠處理信函、利益通知、索賠處理信函、每月帳單和歡迎套件。 您可以使用Communications API將範本(XFA或PDF)與客戶資料結合，以產生PDF、PS、PCL、DPL、IPL和ZPL格式的檔案。

假設您有一或多個範本，且每個範本有多個XML資料記錄。 您可以使用Communications API為每筆記錄產生列印檔案。 <!-- You can also combine the records into a single document. --> 結果會產生非互動式PDF檔案。 非互動式PDF檔案不允許使用者在其欄位中輸入資料。

Formsas a Cloud Service — 通訊功能提供隨選和批次API （非同步API），用於產生排程檔案：

* 同步API適用於隨選、低延遲和單一記錄檔案產生使用案例。 这些 API 更适用于基于用户操作的用例。例如，在使用者填寫表單後產生檔案。

* 批次API （非同步API）適用於排程的高輸送量多檔案產生使用案例。 这些 API 会批量生成文档。例如，每月生成的电话帐单、信用卡对帐单和收益对帐单。

## 使用同步作業 {#batch-operations}

同步作業是以線性方式產生檔案的程式。 這些API分類為單一租使用者API和多租使用者API：

### 單一租使用者API

* 檔案產生API
* 檔案操作API

<!-- 
### Multi-tenant APIs

* Document utility APIs -->


### 驗證單一租使用者API

單一租使用者API操作支援兩種型別的驗證：

* **基本驗證**：基本驗證是內建在HTTP通訊協定中的簡單驗證配置。 使用者端傳送的HTTP要求具有Authorization標頭，其中包含字詞Basic，後跟空格和base64編碼的字串username：password。 例如，若要以管理員/管理員身分授權，使用者端會傳送「基本」 [base64編碼字串使用者名稱]： [base64編碼字串密碼].

* **權杖型驗證：** 權杖型驗證使用存取權杖（持有者驗證權杖）來向as a Cloud ServiceExperience Manager發出請求。 AEM Formsas a Cloud Service提供API來安全地擷取存取Token。 若要擷取並使用權杖來驗證請求：

   1. [從開發人員控制檯擷取Experience Manageras a Cloud Service認證](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. [在您的環境中安裝Experience Manageras a Cloud Service認證](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html). (應用程式伺服器、Web伺服器或其他非AEM伺服器)設定為傳送要求給（進行呼叫）雲端服務。
   1. [產生JWT權杖並與Adobe IMS API交換存取權杖](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).
   1. 以存取權杖作為持有者驗證權杖執行Experience ManagerAPI。
   1. [在Experience Manager環境中為技術帳戶使用者設定適當的許可權](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?lang=en#configure-access-in-aem).

   >[!NOTE]
   >
   >Adobe建議在生產環境中使用權杖型驗證。

<!-- 

### Authenticate a multi-tenant API

#### Authentication Headers

Every inbound HTTP API call to the multi-tenant API must contain these three headers:


* `x-api-key`
* `x-gw-ims-org-id`
* `Authorization`

The values which should be sent in the `x-api-key` and `x-gw-ims-org-id` headers are provided in the Credentials details screen in the [Adobe Developer Console](https://developer.adobe.com/console). The value of the `x-api-key` header is the Client ID and the value for the `x-gw-ims-org-id` header is the Organization ID.

#### Configure Adobe Developer console to generate an access token

To set up authentication APIs, create a project in Adobe Developer Console and add Communication APIs to the project on Adobe Developer Console. The integration generates API Key, Client Secret, Payload (JWT):

1. Contact you Adobe Developer Console administrator. Ask the administrator to add as a developer.
1. Log in to `https://developer.adobe.com/console/`. Use your developer account that your administrator has provisioned to log in to Adobe Developer Console.
1. Select your organization from the top-right corner. If you do not know your organization, contact your administrator.
1. Tap **[!UICONTROL Create new project]**. A screen to get started with your new project appears. Tap **[!UICONTROL Add API]**. A screen with list of all the APIs enabled for your account appears.
1. Select **[!UICONTROL AEM Forms - Communications]** and tap **[!UICONTROL Next]**. A screen to configure the API appears.
1. Select **[!UICONTROL OPTION 1 Generate a key pair]** and tap **[!UICONTROL Generate keypair]**. It creates and downloads the configuration file. The downloaded configuration file contains all your app settings, along with the only copy of your private key. Adobe does not record your private key, make sure to securely store the downloaded file. Tap **[!UICONTROL Next]**.
1. Select **[!UICONTROL Integrations - Cloud Service]** and tap **[!UICONTROL Save configured API]**. Tap **[!UICONTROL Service Account (JWT)]** to view the API Key, Client Secret, and other information required to access the APIs. You set to use the token to access the APIs.

#### Programmatically generate and use an access token

To programmatically generate an access token, generate a JSON Web Token (JWT) and exchange it with the Adobe Identity Management Service (IMS) for an access token.

Use the following keys, referred to as claims, to construct JWT JSON object:


* `exp`- the requested expiration of the access token, expressed as a number of seconds since January 1, 1970 GMT. For most use cases, this is a relatively small value. For example, 5 minutes, for five minutes from now, this value should be 1670923791.
* `iss` - the Organization ID from the Adobe Developer Console project, in the format org_ident@AdobeOrg.
* `sub` - the Technical Account ID from the Adobe Developer Console integration, in the format: id@techacct.adobe.com.
* `aud` - the Client ID from the Adobe Developer Console integration prepended with `https://ims-na1.adobelogin.com/c/`.
* `https://ims-na1-stg1.adobelogin.com/s/ent_aemforms_docprocessing` - set to the literal value `true`

This JSON object must be then base64 encoded and signed using the private key for the project. Finally, the encoded value is sent in the body of a POST request to `https://ims-na1.adobelogin.com/ims/exchange/jwt` along with the Client ID and Client Secret for the project.

##### Example

```JSON

    ========================= REQUEST ==========================
    POST https://ims-na1.adobelogin.com/ims/exchange/jwt
    -------------------------- body ----------------------------
    client_id={myClientId}&client_secret={myClientSecret}&jwt_token={myJSONWebToken}
    ------------------------- headers --------------------------
    Content-Type: application/x-www-form-urlencoded
    Cache-Control: no-cache

```

#### Language Support for JWT

While it is possible to do the entire JWT generation and exchange process in custom code, it is more common to use a higher-level library to do so. A number of such libraries are listed on the [Adobe I/O JWT Documentation](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/).

-->

### （僅適用於Document Generation API）設定資產和許可權

若要使用同步API，需具備下列條件：

* 具有Experience Manager管理員許可權的使用者
* 將範本和其他資產上傳至您的Experience Manager FormsCloud Service執行個體

### （僅適用於Document Generation API）上傳範本和其他資產至您的Experience Manager執行個體

組織通常有多個範本。 例如，信用卡對帳單、福利對帳單及索賠申請各一個範本。 將所有此類XDP和PDF範本上傳到您的Experience Manager執行個體。 若要上傳範本：

1. 開啟您的Experience Manager執行個體。
1. 前往「Forms > Forms和檔案」
1. 按一下「建立>資料夾」並建立資料夾。 開啟資料夾。
1. 按一下「建立>檔案上傳」並上傳範本。

### 叫用API

此 [API參考檔案](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) 提供API所提供的所有引數、驗證方法及其他各種服務的詳細資訊。 API參考檔案也提供.yaml格式的API定義檔案。 您可以下載.yaml檔案並將其上傳到 [Postman](https://www.postman.com/) 檢查API的功能。

>[!VIDEO](https://video.tv.adobe.com/v/335771)

>[!NOTE]
>
>只有Forms-users群組的成員可以存取Communications API。
