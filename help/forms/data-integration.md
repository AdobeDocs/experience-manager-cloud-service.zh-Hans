---
title: 如何將資料庫連線至 [!DNL AEM Forms] as a Cloud Service？
seo-title: AEM Forms Data Integration
description: 您可以從以下位置擷取資料並儲存至RESTful Web服務、以SOAP為基礎的Web服務和OData服務 [!DNL AEM Forms] as a Cloud Service。 此服務提供專用的工具，可擷取、測試、驗證資料並將其傳送至各種型別的資料來源。
exl-id: 9d146275-de0a-4861-b060-d205ed6305f3
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 1%

---

# 将数据源连接到 Cloud Service {#aem-forms-data-integration}

![資料整合](do-not-localize/data-integeration.png)

企業基礎架構包括不同的後端系統或資料來源，例如資料庫、網站服務、REST服務、OData服務和CRM解決方案。 他們共同組成資訊系統，為企業應用程式提供資料，以執行日常業務。 另一方面，應用程式會擷取資料，並將其傳回以更新資料來源。

[!DNL AEM Forms] Adaptive Forms和互動式通訊等應用程式需要與資料來源整合，以便在呈現表單和建立互動式通訊時擷取客戶資料。 在某些情況下，系統會根據最適化Forms中的使用者輸入，從資料來源擷取資料。 此外，提交的最適化表單資料可以回寫以更新各自的資料來源。

雖然分散式模組化系統有其自身的優點，但難題在於跨資料來源整合及建立資料關聯。 資料整合是功能強大且效率優異的企業基礎建設的關鍵所在，企業基礎建設擁有各種不同的資料來源，可連線應用程式以交換業務資料。

## 資料整合概觀 {#data-integration-overview}

![aem-forms-data-integration](assets/aem-forms-data-integeration.png)

[!DNL AEM Forms] 資料整合可讓您設定不同的資料來源，並透過將其連線 [!DNL AEM Forms]. 它提供直覺式使用者介面，可跨連線的資料來源建立商業實體和服務的統一資料呈現結構描述。 此統一表示法稱為表單資料模型，是JSON結構描述的擴充功能。 表單資料模型中的圖元稱為資料模型物件。 表單資料模型可讓您：

* 從連線的資料來源存取資料模型物件、屬性和服務。
* 建立自訂資料模型物件和屬性
* 在資料來源內和資料來源之間的資料模型物件之間建立關聯。
* 叫用資料模型物件服務來查詢或寫入資料到資料來源或從資料來源寫入資料。

建立表單資料模型後，您就可以將其用於各種最適化表單和互動式通訊工作流程，例如：

* 根據表單資料模型建立最適化Forms和互動式通訊
* 從已設定的資料來源預先填入最適化Forms和互動式通訊
* 使用最適化表單規則叫用資料來源服務/作業
* 將提交的最適化表單資料寫入資料來源

## 開始使用資料整合 {#get-started-with-data-integration}

實作資料整合的第一步是識別並設定資料來源，以儲存您要在Adaptive Forms和互動式通訊使用案例中運用的資訊。 接下來，您會建立表單資料模型，此模型會使用來自一或多個資料來源的資料模型物件、屬性及服務。 您可以根據表單資料模型建立最適化Forms和互動式通訊，其中互動式通訊中的最適化表單欄位或預留位置會繫結至各自的資料來源屬性。

[!DNL AEM Forms] 也可讓您建立獨立於資料來源的表單資料模型，並在稍後將表單資料模型中的資料模型物件和屬性與資料來源建立關聯或繫結。 當您處理表單資料模型時，它可消除對資料來源的任何相依性。

請參閱下列內容，以開始使用、瞭解並實作資料整合。

* [配置数据源](configure-data-sources.md)
* [建立表單資料模型](create-form-data-models.md)
* [使用表單資料模型](work-with-form-data-model.md)
* [使用表單資料模型](using-form-data-model.md)

>[!NOTE]
>
>[!UICONTROL Experience Manager Forms] 不支援關聯式資料庫。
