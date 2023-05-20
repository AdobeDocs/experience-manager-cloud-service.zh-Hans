---
title: Formsas a Cloud Service常見問題
description: Formsas a Cloud Service常見問題
contentOwner: khsingh
exl-id: 0b14b680-7da5-4e0b-bd6a-c379d148f9d7
index: false
source-git-commit: 93e7c4b31ea3037c98b64790ffdee11f94cc6134
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 3%

---

# 常见问题 {#frequently-asked-questions}

* **我可以使用程式碼編輯器建立規則嗎？**
您可以使用視覺化編輯器來建立規則。 程式碼編輯器無法用於 [!DNL Forms] as a Cloud Service。 如果您的最適化表單使用使用程式碼編輯器開發的規則指令碼，請使用 [移轉公用程式](migrate-to-forms-as-a-cloud-service.md) 將程式碼指令碼轉換為自訂函式。 您可以透過視覺化編輯器使用自訂函式，繼續取得透過程式碼編輯器取得的結果。

* **我可以在Cloud Service執行個體上建立XFA型最適化表單嗎？**
可以，您可以在Cloud Service執行個體上建立XFA型最適化表單。 不過，AEM Formsas a Cloud ServiceSDK （本機開發環境）不支援XFA型最適化Forms。 如果您打算搭配AEM Formsas a Cloud ServiceSDK使用XFA型最適化Forms，請聯絡Adobe支援，提供您使用案例的詳細資訊和特定需求。

<!-- * **Can I use an XDP as a Document of Record (DoR) template? Is Forms Designer included in AEM Forms as a Cloud Service license?** 

  Yes, you can use an XDP as a Document of Record template on Cloud Service instances. However, support to use XDP as a Document of Record template is not available for AEM Forms as a Cloud Service SDK (Local development environment). -->

* **我可以將內容從內部部署移轉或 [!DNL Adobe-Managed Services] 環境至 [!DNL Forms] as a Cloud Service環境？**
是，您可以從內部部署移轉自訂程式碼、內容和資產，或 [!DNL Adobe-Managed Services] 環境至 [!DNL Forms] as a Cloud Service環境。 如需詳細指示，請參閱 [移轉至Formsas a Cloud Service](migrate-to-forms-as-a-cloud-service.md).

<!-- You can use package manager or Experience Manager UI to [export and import Forms and related assets](import-export-forms-templates.md), use the migration utility to make your existing assets compatible with [!DNL Forms] as a Cloud Service, use the [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#best-practices-analyzer) tool to find the features and APIs that require changes and updated before migration, and use the [Content Transfer Tools](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/moving/home.html) to move your custom code without refactoring it. -->

* **我可以在哪裡取得AEM [!DNL Forms] as a Cloud Service [!DNL Java™] API參考檔案？**
您可以下載Java™ API參考檔案，網址為 [!DNL Maven Central Repository]. 若要下載：
   1. 转到 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. 找到並開啟包含最新版本的最新頁面 [!DNL Experience Manager Forms] SDK.
   1. 按一下「檢視全部」選項以檢視所有檔案。
   1. 下載並解壓縮 `aem-forms-sdk-api-<version>-javadocs`.jar.
   1. 開啟index.html檔案以檢視API參考檔案。

* **我可以在哪裡取得 [!DNL JavaScript™] 最適化Forms的API參考資料？**
您可以下載 [!DNL JavaScript™] API參考檔案來自[!DNL  Maven Central Repository]. 若要下載：
   1. 打开 [[!DNL Maven Central Repository]](https://mvnrepository.com/artifact/com.adobe.aem/aem-forms-sdk-api).
   1. 找到並開啟包含最新版本的最新頁面 [!DNL Experience Manager Forms] SDK.
   1. 按一下「檢視全部」選項以檢視所有檔案。
   1. 下載並解壓縮 `aem-forms-sdk-api-<version>-jsdoc.jar`.
   1. 開啟index.html檔案以檢視API參考檔案。

* **我可以繼續使用現有主題和範本嗎？**
是，使用AEM 6.4 Forms和AEM 6.5 Forms後，您就可以繼續使用隨著 [移轉公用程式](migrate-to-forms-as-a-cloud-service.md) 以將其移至 [!DNL AEM Forms] as a Cloud Service。

   您也可以根據以下專案建立專案： [!DNL AEM Forms] as a Cloud Service [原型](setup-local-development-environment.md#forms-cloud-service-local-development-environment) 並使用包含的範例主題和範本。

* **我可以產生符合結構描述的資料嗎？**
可以，您可以建立最適化Forms以產生符合結構描述的資料。

<!-- * **Can I pass custom parameters to the prefill service?**
Custom parameters are planned for an upcoming release. -->

* **我可以快取安全內容嗎？**
預設會停用快取安全內容功能。 若要啟用此功能，您可以執行以下提供的指示： [快取安全內容](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=zh-Hans).

* **我有當地語系化的最適化表單；它不是呈現當地語系化版本嗎？ 原因可能是什麼，以及如何解決此問題？**

   本地化的最適化Forms的URL慣例現在支援在URL中指定地區設定。 新的URL慣例可在Dispatcher或CDN上快取本地化的表單。 在Cloud Service環境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 請求最適化表單的當地語系化版本，而非 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe建議使用Dispatcher或CDN快取。 它有助於提高預填表單的呈現速度。

* **我已更新最適化表單；客戶無法使用更新的版本？**
根據預設，CDN會在每5分鐘重新整理快取，等待5分鐘，然後檢查更新的版本。

* **我可以在最適化表單中使用簽名步驟來建立瀏覽器內簽名體驗嗎？**
否，簽名步驟不可用於 [!DNL Forms] as a Cloud Service。 移除最適化Forms中的簽名步驟。 請讓使用者在提交後簽署最適化表單，而不是簽名步驟。 這可協助您繼續提供瀏覽器內簽名體驗。

* **我可以在最適化表單中使用驗證步驟嗎？**
否，驗證步驟不可用於 [!DNL Forms] as a Cloud Service。 將最適化Forms移至Cloud Service環境之前，請從現有的最適化表單移除驗證步驟。

* **我可以將圖表新增至最適化表單嗎？**
可以，您可以將圖表新增至最適化Forms。 Adaptive Forms提供圖表元件。 您可以使用它來將圖表新增至最適化表單。

* **我可以將「表單資料模型」連線至關聯式資料庫模型嗎？**
您可以將表單資料模型連線至 [!DNL RESTful web services]， [!DNL SOAP-based web services]， [!DNL OData services]，並將使用者設定檔Experience Manager為資料來源。 不支援將表單資料模型與關聯式資料庫連線。

* **我可以在表單資料模型中使用自訂憑證來進行驗證嗎？**
表單資料模型未提供使用自訂憑證進行驗證的方法。 因此，不支援自訂憑證，例如x509和雙向SSL。

* **我可以使用Forms Portal提交動作Adaptive Forms嗎？**

   您可以修改現有的最適化Forms以使用 [提交至REST端點](configuring-submit-actions.md#submit-to-rest-endpoint)， [傳送電子郵件](configuring-submit-actions.md#send-email)， [使用表單資料模型提交](configuring-submit-actions.md#submit-using-form-data-model)、和 [叫用AEM工作流程](configuring-submit-actions.md#invoke-an-aem-workflow) 提交動作。 Forms Portal和Forms Portal提交動作還無法使用。 請留意功能是否可用的每月發行說明。

* **我可以使用 [!DNL AEM Forms] 應用程式搭配 [!DNL AEM Forms] as a Cloud Service？**

   自适应表单提供了响应式设计。这些表单会根据底层设备更改外观、设计和交互性。您可以繼續在行動裝置上使用最適化Forms，同時保留每月發行說明的監看資訊，以瞭解功能是否可用。

* **初始GA發行版本未包含哪些功能？**
Forms入口網站， [!DNL AEM Forms] 應用程式、與Adobe Analytics的整合以及與Adobe Target的整合不屬於初始GA發行的一部分。 請檢視每月發行說明，以瞭解新功能的相關資訊。

* **我已設計 [用於建立最適化表單的JSON結構描述](adaptive-form-json-schema-form-model.md). JSON結構描述會為適用性表單的某些元件定義事件。 AEM Formsas a Cloud Service是否支援事件？**
在Experience Manager6.5 Forms環境中根據JSON結構描述建立調適型表單，並使用 [移轉公用程式](migrate-to-forms-as-a-cloud-service.md) 將此類最適化Forms移轉至AEM Formsas a Cloud Service。 公用程式會將這類事件轉換為使用者端程式庫，而且您可以繼續在Cloud Service環境中搭配使用Adaptive Forms事件。

<!-- 

* **Is there any AEM Forms as a Cloud Service connector for Microsoft Power Automate?**

  Yes, Adobe provides an Adobe Experience Manager connector to access [Adobe Experience Manager Forms - Communication capabilities](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html) through Microsoft Power Automate. You can create a PDF document that is based on a form design and XML form data or create PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) and other Printer Definition Language documents. 

  You can get started with Adobe Experience Manager easily with just a few steps:

  1. Generate the Service credentials: Use Adobe Experience Manager Developer Console to [generate](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html?#generate-service-credentials) the service credentials.  
  
  1. Setup your connection: Add your service credentials to the Adobe Experience Manager Connector. You can get crdential from service credential JSON and copy these credential details to your one-time connection setup:

    * AEM Server
    * Organization ID 
    * Client ID
    * Client Secret
    * Technical Account ID
    * Meta Scopes
    * Private Key - base64 encoded keys are accepted
    * Adobe IMS Host URL

    <br> 
    
    ![Use your Service Credential JSON for credential details](assets/forms-aem-pa-connector-connection.png)

    A sample Service Credential JSON file fields mapped to Adobe Experience Manager connector for Microsoft Power Automate.

    -->


