---
title: 如何從AEM 6.5 Forms和AEM 6.4 Forms移轉至 [!DNL AEM Forms] as a Cloud Service環境？
description: 從移轉 [!DNL AEM Forms] （內部部署和AMS環境）至 [!DNL AEM Forms] as a Cloud Service環境
contentOwner: khsingh
feature: Adaptive Forms
role: User, Developer
level: Intermediate
topic: Migration
exl-id: 090e77ff-62ec-40cb-8263-58720f3b7558
source-git-commit: d9c19d0b567a9a97973c4c4e25e64722da109dbb
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 5%

---

# 從移轉 [!DNL AEM Forms] （內部部署和AMS環境）至 [!DNL AEM Forms] as a Cloud Service  {#Harden-your-AEM-Forms-as-a-Cloud-Service-environment}

您可以移轉最適化Forms、主題、範本和雲端設定，從 <!-- AEM 6.3 Forms--> OSGi上的AEM 6.4 Forms和OSGi上的AEM 6.5 Forms至 [!DNL AEM] as a Cloud Service。 在移轉這些資產之前，請使用移轉公用程式，將舊版使用的格式轉換為中使用的格式 [!DNL AEM] as a Cloud Service。 當您執行Migration Utility時，會更新下列資產：

* 最適化Forms的自訂元件
* 最適化Forms範本和主題
* 雲端設定
* 程式碼編輯器指令碼會轉換為可重複使用的函式，並套用至視覺規則。

## 注意事项 {#consideration}

* 此服務僅協助移轉內容 [!DNL AEM Forms] 在OSGi環境中。 內容移轉來源 [!DNL AEM Forms] 不支援在JEE上移至Cloud Service環境。

* (僅適用於AEM 6.3 Forms或已升級至AEM 6.4 Forms或AEM 6.5 Forms的舊版環境)不支援以AEM 6.3 Forms或舊版中提供的現成可用範本和主題為基礎的最適化Forms [!DNL AEM Forms] as a Cloud Service。

* 與Adobe Experience Manager 6.5 Forms (內部部署和Adobe代管服務)環境相比，Adobe Experience Manager Formsas a Cloud Service對現有功能進行了一些重大變更。 在繼續移轉至服務之前， [瞭解這些值得注意的變更](notable-changes.md) 和 [功能層級的差異](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report) 以根據貴組織所需的功能來決定移轉。




<!-- 
## Difference with AEM 6.5 Forms 

| Feature         | Difference with AEM 6.5 Forms    |
|--------------|-----------|
| HTML5 Forms (Mobile Forms)     | The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. |
| Adaptive Forms     | <li><b>XSD-Based Adaptive Forms:</b> The service does not support HTML5 Forms (Mobile Forms). If you render your XDP-based forms as HTML5 Forms, you can continue using the feature on AEM 6.5 Forms. </li> <li><b> Adaptive Form templates:</b> Use build pipeline and corresponding Git repository of your program to import existing Adaptive Form templates. </li><li><b>Rule editor:</b> AEM Forms as a Cloud Service provides a hardened [Rule editor](rule-editor.md#visual-rule-editor). The code editor is not available on Forms as a Cloud Service. The migration utility helps you migrate your forms that have custom rules (created in code editor). The utility converts such rules into custom functions supported on Forms as a Cloud Service. You can use the reusable functions with Rule editor to continue obtaining results obtained with rule scripts  The `onSubmitError` or `onSubmitSuccess` functions are now available as actions the Rule Editor. </li> <li><b>Drafts and submissions:</b> The service does not retain metadata for drafts and submitted Adaptive Forms. </li> <li><b> Prefill Service:</b> By default, the prefill service merges data with an Adaptive Form at client as opposed to merging data on Server in AEM 6.5 Forms. The feature helps improve the time required to prefill an Adaptive Form. You can always configure to run the merge action on the Adobe Experience Manager Forms Server. </li><li><b>Submit actions:</b> The **Email as PDF** action is not available. The **Email** submit action provide options to send attachments and attach Document of Record (DoR) with email. </li>|
| Form Data Model | <li>Forms data model supports only HTTP and HTTPs endpoints to submit data. </li><li>Forms as a Cloud Service allows to use Microsoft Azure Blob, Microsoft Sharepoint, Microsoft OneDrive, and services supporting general CRUD (Create, Read, Update, and Delete) operations as data stores. The service does not support JDBC connector, Mutual SSL for Rest connector, and x509 certificate-based authentication for SOAP data sources. </li>|
| Automated Forms Conversion Service     | The service does not provide meta-model for Automated Forms Conversion Service. You can [download it from Automated Forms Conversion Service documentation](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).|
|Configurations|<li>Email support only HTTP and HTTPs protocols, by default. [Contact the support team](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) to enable ports for sending emails and to enable SMTP protocol for your environment. </li> <li>If you use custom bundles, recompile your code with latest version of adobe-aemfd-docmanager before using these bundles with Forms as a Cloud Service.</li> |
| Document Manipulation APIs (Assembler Service)| The service does not support operations dependent on other services or applications: <li>Conversion of documents in a non-PDF format to a PDF format is not supported. For example, Microsoft Word to PDF, Microsoft Excel to PDF, and HTML to PDF are not supported</li><li>Adobe Distiller-based conversions are not supported. For example, PostScript(PS) to PDF</li><li>Forms Service-based conversions are not supported. For example, XDP to PDF Forms.</li><li>The service does not support converting a Signed PDF or Transparent PDF to another PDF format.</li>| -->

## 前提条件 {#prerequisites}

* [啟用Forms — 數位註冊](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/setting-up-program.html?#editing-program) 為您的FormsCloud Service計畫和 [執行管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html).

   ![练习结果](assets/enable-add-on.png)

* 在Cloud Service環境中，移轉公用程式可搭配使用者對應工具和內容轉移工具運作。 移轉公用程式可讓 [!DNL AEM Forms] 與Cloud Service相容的資產，而內容轉移工具會將內容從您的 [!DNL AEM Forms] 環境至 [!DNL AEM] as a Cloud Service環境。 在使用移轉公用程式之前，請先瞭解以下步驟 [移至AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/home.html). 此程式有兩個工具：
   * [使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration)：使用者對應工具可協助您將使用者與對應的Adobe IMS使用者帳戶對應。
   * [內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration)：內容轉移工具可幫助您準備內容並將內容從現有環境轉移到Cloud Service環境。
* 具有管理員許可權的帳號 [!DNL AEM Forms] as a Cloud Service與您的本機 [!DNL AEM Forms] 環境。
* 下載並安裝Best Practice Analyzer、內容轉移工具和 [!DNL AEM Forms] 移轉公用程式 [軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)

* 執行 [Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html?lang=en#cloud-migration) 工具並修正回報的問題。 如需從Adobe Experience Manager Forms移轉至Adobe Experience Manager Formsas a Cloud Service的相關可能問題，請參閱 [Formsas a Cloud Service的AEM模式偵測](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#viewing-report).


<!-- * Download the latest [compatibility package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en#aem-65-forms-releases) for your [!DNL AEM Forms] version. -->

## 移轉 [!DNL AEM Forms] 資產  {#use-the-migration-utility}

執行以下步驟，讓 [!DNL AEM Forms] 與Cloud Service相容的資產，並將其轉移至 [!DNL AEM] as a Cloud Service環境。

1. 建立 [原地複製](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/correct-method-to-clone-the-aem-environment/qaq-p/363487) 您現有的 [!DNL AEM Forms] 環境。

   請一律使用複製的環境來執行內容轉移工具和移轉公用程式。 內容轉移工具和移轉公用程式會對內容和資產進行一些變更。 因此，請勿在生產環境中執行內容轉移工具和移轉公用程式。

1. 以管理許可權登入您的複製環境。

1. 執行 [使用者對應工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html?lang=en#cloud-migration) 將您的使用者與對應的Adobe IMS使用者帳戶對應。 您需要Adobe IMS使用者帳戶才能登入 [!DNL AEM Forms] as a Cloud Service執行個體。

1. 下載並安裝 [內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) 和 [!DNL AEM Forms] as a Cloud Service移轉公用程式，從 [軟體發佈入口網站](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html) 在複製的環境上。 您可以使用AEM Package Manager來安裝工具與公用程式。

1. 導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 內容移轉]**.

1. 開啟 **[!UICONTROL 準備Forms進行移轉]** 卡片。 瀏覽器會顯示五個選項：
   * **[!UICONTROL AEM Forms 资产迁移]**
   * **[!UICONTROL 最適化Forms自訂元件移轉]**
   * **[!UICONTROL 最適化Forms範本移轉]**
   * **[!UICONTROL AEM Forms 云配置迁移]**
   * **[!UICONTROL 程式碼編輯器指令碼移轉]**

1. 逐一使用選項來製作您的 [!DNL AEM Forms] 資產相容於 [!DNL AEM] as a Cloud Service：

   1. 點選 **[!UICONTROL AEM Forms資產移轉]**，然後在下一個畫面中，點選 **[!UICONTROL 開始移轉]**. 它讓您瞭解最適化Forms和主題 [!DNL AEM Forms] 環境相容於 [!DNL AEM] as a Cloud Service。

   1. 點選 **[!UICONTROL 最適化Forms自訂元件移轉]** 並在「自訂元件移轉」頁面中，點選 **[!UICONTROL 開始移轉]**. 它讓您為最適化Forms開發的任何自訂元件，以及在上的元件覆蓋 [!DNL AEM Forms] 環境相容於 [!DNL AEM] as a Cloud Service。

   1. 點選 **[!UICONTROL 最適化Forms範本移轉]** 並在「自訂元件移轉」頁面中，點選 **[!UICONTROL 開始移轉]**. 這會使/apps或/conf處並使用AEM範本編輯器建立的最適化表單範本相容於 [!DNL AEM] as a Cloud Service。

   1. 點選 **[!UICONTROL AEM Forms雲端設定移轉]** 然後在「設定移轉」頁面上，點選「 」 **[!UICONTROL 開始移轉]**. 它會更新下列Cloud Services並將其移動到新位置：

      * 表單資料模型Cloud Service
      * Google reCAPTCHACloud Service
      * [!DNL Adobe Sign] 云服务
      * Adobe FontsCloud Service
   1. 點選 **[!UICONTROL 程式碼編輯器指令碼移轉]**，指定儲存可重複使用函式的位置，然後點選**[!UICONTROL 開始移轉].

   Cloud Service不支援規則編輯器指令碼。 此 **[!UICONTROL 程式碼編輯器指令碼移轉]** tool會將您環境上的所有規則指令碼轉換為可重複使用的函式，並將可重複使用的函式套用至適當位置的視覺化編輯器。 這些可重複使用的功能會以使用者端程式庫形式儲存，並協助您保持現有功能不變。 此工具會自動將產生的可重複使用函式套用至對應的Adaptive Forms。

   使用 [封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html?lang=en#contentmanagement) 將可重複使用的函式（使用者端程式庫）匯出至套件。

1. [部署](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#deploying-content-packages-via-cloud-manager-and-package-manager) 可重複使用的函式（使用者端程式庫）套件， [自訂程式碼、元件、設定](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/devops/deploy-code.html#cloud-manager)，自訂地區設定專屬程式庫 [!DNL AEM] as a Cloud Service環境。

   <!-- 1. Install the latest [Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration) to your cloned [!DNL AEM Forms] environment. -->

1. 執行 [內容轉移工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?#cloud-migration). 在上指定引數時 **[!UICONTROL 建立移轉集]** 畫面，指定最適化Forms、主題、範本、表單資料模型、Cloud Services、自訂元件和其他AEM Forms特定資產的路徑， **[!UICONTROL 要包含的路徑]** 選項。 它新增指定的 [!DNL AEM Forms] 資產移轉至移轉集。

## 各種AEM Forms專屬資產的路徑

* **最適化Forms**：您可在以下網址找到最適化表單： `/content/dam/formsanddocuments/`和/content/forms/af。 例如，對於標題為WKND註冊的最適化表單，請新增路徑 `/content/dam/formsanddocuments/wknd-registration` 和 `/content/forms/af/wknd-registration`.
* **表單資料模式**：您可以在以下位置找到所有表單資料模型： `/content/dam/formsanddocuments-fdm`. 例如：`/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`。

* **使用者端資料庫**：使用者端資料庫的預設路徑為 `/etc/clientlibs/fd/theme`.

* **最適化表單範本**：範本的預設路徑為 `/conf/<template folder>`. 例如，對於標題為基本新增路徑的範本 `/conf/ReferenceEditableTemplates/settings/wcm/templates/basic`.

* **最適化表單主題和使用者端資料庫**：主題的預設路徑為 ` /content/dam/formsanddocuments-themes/` 而使用者端程式庫的預設路徑為 `/etc/clientlibs/fd/theme`. 例如，對於名為WKND佈景主題的新增路徑範本 ` /content/dam/formsanddocuments-themes/wkndtheme` 主題的使用者端資料庫 `/etc/clientlibs/reference-themes/wkndtheme-3-0`. 您也可以在其他自訂路徑上擁有主題和使用者端資料庫。

* **雲端設定**：您可以在下列位置找到雲端設定： `/conf/`. 例如，表單資料模型雲端設定位於 `/conf/global/settings/cloudconfigs/fdm`.

* **工作流程模型**：您可以在下列位置找到AEM工作流程模型： `/conf/global/settings/workflow/models/`. 例如，對於標題為WKND註冊的工作流程模型，新增路徑 `/conf/global/settings/workflow/models/wknd-registration`

您可以新增下列最上層資料夾路徑或特定資料夾路徑，如下所述。 它可讓您一次移轉特定資產及所有資產和表單。

* /content/dam/formsanddocuments-fdm
* /content/dam/formsanddocuments/themes
* /content/forms/af
* /etc/clientlibs/fd/theme

若要移轉AEM Workflow模型，請指定下列路徑：

* /conf/global/settings/workflow/models/
* /conf/global/settings/workflow/launcher
* /var/workflow/model
