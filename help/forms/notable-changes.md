---
title: AEM 6.5 Forms與AEM Cloud Services之間的差異
description: 您是Experience Manager Forms使用者，且想要升級至Adobe Experience Manager Formsas a Cloud Service嗎？ 比較AEM 6.5 Forms和AEM Cloud Services，並在升級或移轉至Cloud Service之前瞭解最顯著的變更。
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
contentOwner: khsingh
source-git-commit: 54a1ae1cc030030e44612b502b70c9b567144538
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 2%

---

# 現有Adobe Experience Manager 6.5 Forms使用者的重大變更  {#notable-changes-for-existing-AEM-Forms-users}

與Adobe Experience Manager Forms On-Premise和Adobe Experience Manager Forms相比，as a Cloud Service對現有功能進行了一些重大變更。 [!DNL Adobe-Managed Service] 環境。 主要差異列示如下：

## 雲端原生功能

* 此服務採用雲端原生架構，可根據負載自動縮放、升級時無需停機時間、經常推出新功能和更新後使用，以及最佳化的拓撲，以發揮最大彈性和效率。

* 此服務不包含將資料儲存至Adobe Experience ManagerCloud Service執行個體的提交動作，因此超級安全。 透過表單擷取的資料會直接傳送至已設定的資料存放區。

* 此外，還提供免費的CDN （內容傳遞網路），協助您以更快的速度傳遞和轉譯表單。


## 更新開發流程

* 此服務會提供SDK，在將自訂程式碼部署至Cloud Service之前，可在本機環境（本機電腦）中開發和測試自訂程式碼。 開發人員在本機電腦上使用SDK來開發和測試自訂元件、主題、工作流程應用程式、設定、範本等。 在其本機開發環境中測試自訂程式碼後，他們將自訂程式碼部署到 [Forms CS環境開發或預備環境](/help/implementing/cloud-manager/deploy-code.md) 以供進一步測試，然後再提升至生產環境。

* 開發人員會維護共同的Cloud Service和本機開發環境程式碼 [Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/cloud-manager-repositories.html). 建立AEMas a Cloud Service程式時，會自動建立以AEM原型為基礎的Git存放庫。

   ![](/help/forms/assets/git-repo-local-and-forms-cs.png)

* Formsas a Cloud Service的開發流程會與AEM Cloud Service的AEM Archetype一致。 不過，Adobe Experience Manager Maven專案必須進行一些變更，才能與AEM Cloud Service相容。 在高層面上，AEM需要將內容和程式碼分離為離散的子套件，以遵循可變和不可變內容之間的分割。 使用 [Repository Modernizer工具](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) 將內容和程式碼分割為獨立套件，以與Adobe Experience Manager as a Cloud Service定義的專案結構相容，藉此重組現有的專案套件。

* 在Formsas a Cloud Service中使用客戶套件組合之前，請先使用最新版adobe-aemfd-docmanager重新編譯自訂程式碼。

* 使用 [AEM Formsas a Cloud Service移轉公用程式](/help/forms/migrate-to-forms-as-a-cloud-service.md) 準備和移轉最適化Forms、主題、範本和雲端設定，從 <!-- AEM 6.3 Forms--> OSGi上的AEM 6.4 Forms和OSGi上的AEM 6.5 Forms至 [!DNL AEM] as a Cloud Service。 使用 [您程式的Git存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) 以匯入現有的最適化表單範本。

* 電子郵件預設僅支援HTTP和HTTP通訊協定。 [聯絡支援團隊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) 啟用傳送電子郵件的連線埠，並為您的環境啟用SMTP通訊協定。

## 本地化

* 本地化的最適化Forms的URL慣例現在支援在URL中指定地區設定。 新的URL慣例可在Dispatcher或CDN上快取本地化的表單。 在Cloud Service環境中，使用URL格式 `http://host:port/content/forms/af/<afName>.<locale>.html` 請求最適化表單的當地語系化版本，而非 `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`.

* Adobe建議使用Dispatcher或CDN快取。 它有助於提高預填表單的呈現速度。


## 自适应表单

* **規則編輯器：** AEM Formsas a Cloud Service提供強化的功能， [規則編輯器](rule-editor.md#visual-rule-editor). Formsas a Cloud Service上沒有程式碼編輯器。

   此 [移轉公用程式](/help/forms/migrate-to-forms-as-a-cloud-service.md) 可協助您移轉具有自訂規則（在程式碼編輯器中建立）的表單。 公用程式會將這些規則轉換為Formsas a Cloud Service支援的自訂函式。 您可以将可重用的函数与 规则编辑器结合使用，以继续获取通过规则脚本获取的结果。此 `onSubmitError` 或 `onSubmitSuccess` 函式現在可作為規則編輯器中的動作。

* **預填服務：** 預設情況下，預填服務會在使用者端將資料與最適化表單合併，而不是在AEM 6.5 Forms中合併伺服器上的資料。 此功能有助於改善預填最適化表單所需的時間。 您一律可以設定為在Adobe Experience Manager Forms伺服器上執行合併動作。

* **提交動作：** 此 **電子郵件** 提交動作提供傳送附件和將記錄檔案(DoR)附加於電子郵件的選項。 您可以使用它來取代 **以PDF形式傳送電子郵件** AEM 6.5 Forms中可用的動作。

* **automated forms conversion服務**：服務未提供Automated forms conversion服務的中繼模型。 您可以 [從Automated forms conversion服務檔案下載](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/extending-the-default-meta-model.html?lang=en#default-meta-model).

* **XSD式最適化Forms：** 您可以使用XDP範本來設計記錄檔案的範本。 此服務不支援XFA型最適化Forms

* **元件**：您可以使用 [Adaptive Forms Core-Components](/help/forms/creating-adaptive-form-core-components.md) 以設計您的表單。 這些元件以WCM核心元件為基礎，遵循BEM標準，並可輕鬆自訂。 此服務不支援表單內簽名體驗，也不包含最適化表單的「摘要」和「驗證」元件

## Forms Portal

* 您可以使用Forms Portal的搜尋與清單製作程式、草稿與提交和連結元件，為登入的使用者列出表單。 未提供開箱即用(OOTB)的Forms入口網站匿名使用支援。 您可以自訂Forms入口網站，以啟用為非登入使用者顯示表格。

* 此服務不會保留草稿和已提交的最適化Forms的中繼資料。

## 文档服务:

Formsas a Cloud Service提供Document Generation和Document Manipulation RESTful API。 您可以視需要使用這些API來依需求或批次產生或操控檔案：

* **Document Services： Document Generation API （輸出服務）**：在單一API呼叫或批次中，您只能使用含有多個DATA XML檔案的範本。 不支援在單一API呼叫中對多個資料檔案使用多個範本。

* **Document Manipulation API （組合器服務）**：

   * 依賴檔案服務或應用程式的作業無法使用。 例如，不支援Microsoft Word至PDF、Microsoft Excel至PDF、HTML至PDF、PostScript (PS)至PDF、XDP至PDF forms。 這些作業分別依賴Microsoft Office、Adobe Acrobat、Adobe Distiller、Forms Document Service。

   * 在搭配Communications Document Manipulation API使用非PDF格式的檔案之前，請先將其轉換為PDF格式。 例如，如果您的檔案是Microsoft Office、HTML、PostScript (PS)、XDP格式，請先將這些檔案轉換為PDF格式，然後再將這些檔案與PDF檔案一起使用。 您可以使用 [ConvertPDF](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-document-services/using-convertpdf-service.html) 轉換服務。

* 您可以使用AEM 6.5 Forms環境進行數位簽名、加密、Reader延伸、傳送至印表機、轉換PDF和條碼Forms服務。


## 資料整合（表單資料模型）

* 此服務也支援JDBC聯結器、Microsoft Dynamics、SalesForce、以SOAP為基礎的Web服務，以及支援OData的服務。

* 您也可以連線AEM使用者設定檔，以擷取和更新使用者資訊。

* Forms資料模型僅支援HTTP和HTTPS端點來提交資料。 此服務不支援REST聯結器的雙向SSL，也不支援SOAP資料來源的x509憑證式驗證。

* Formsas a Cloud Service允許使用Microsoft Azure Blob、Microsoft Sharepoint、Microsoft OneDrive以及支援一般CRUD （建立、讀取、更新和刪除）作業的服務作為資料存放區，同時支援Open API規格2.0和Open API 3.0規格。


## 電子簽章

* 此服務提供與Adobe Sign的OOTB整合，並支援電子簽章的DocuSign。

* 此服務也支援Adobe Sign角色。 您可以在最適化Forms編輯器中為商業使用者設定角色，以輕鬆設定簽署工作流程。


## HTML5 表单

* 您可以使用AEM 6.5 Forms環境來：

   * 將您的XDP型表單轉譯為HTML5 Forms。 此服務不支援HTML5 Forms (Mobile Forms)。

   * 離線擷取資料，並在下次您回到線上時使用 [AEM Forms工作區](https://experienceleague.adobe.com/docs/experience-manager-65/forms/use-aem-forms-workspace/introduction-html-workspace.html) 應用程式。

## 交互式通信

* 您可以使用Communications API來隨選或在Formsas a Cloud Service上批次產生個人化檔案。 您可以使用AEM 6.5 Forms環境進行互動式通訊和代理程式UI使用案例。


