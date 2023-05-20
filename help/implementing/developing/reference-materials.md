---
title: API 参考材料
description: AEM具有廣泛且強大的API，您可將這些API用於數位體驗專案。
exl-id: d4ef3040-5a0a-4149-9e99-09eda9605038
source-git-commit: cc6565121a76f70b958aa9050485e0553371f3a3
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 9%

---

# API 参考材料 {#api-reference-materials}

Adobe Experience Manager (AEM)提供許多API來開發應用程式和擴充AEM。 AEM是以許多開放原始碼技術為基礎所建置，這也可供運用。

## AEM Core API {#core-aem-apis}

以下API是AEM的核心。

| API | 描述 |
|---|---|
| [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | 產品抽象概念，例如頁面、資產、工作流程等。 |
| [Granite UI](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html#) | Adobe的Open Web棧疊，提供各種基本元件（請注意，6.5 Granite材料適用於AEMaaCS） |
| [Coral UI](https://opensource.adobe.com/coral-spectrum/documentation/) | Adobe的雲端UI視覺樣式，旨在提供一致的使用者體驗 |

<!---
|Editor core JavaScript API reference|Provides all the base objects and concepts to support authoring of content resources|
--->

## 其他框架 {#additional-apis}

AEM需仰賴許多其他開放原始碼API。

| API | 描述 |
|---|---|
| [Apache Sling](https://sling.apache.org/apidocs/sling11/) | 使用Java Content Repository (JCR)儲存和管理內容的Web架構 |
| [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 實作可擴充的高效能階層Java內容存放庫(JCR)，以作為現代世界級網站的基礎 |
| [Java內容存放庫](https://www.adobe.io/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) | JCR 2.0版的規格 |
| [Apache Felix](https://felix.apache.org) | 實作Open Services Gateway Initiative (OSGi)架構和服務平台 |

## API偏好設定准則 {#guidelines}

AEM是以下列四個主要Java API集為基礎建立，依偏好設定由上往下排序。

| 优先级 | API | 描述 |
|---|---|---|
| 1 | [Adobe Experience Manager as a Cloud Service](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/index.html) | 產品抽象概念，例如頁面、資產、工作流程等。 |
| 2 | [Apache Sling](https://sling.apache.org/apidocs/sling11/) | REST和以資源為基礎的抽象化，例如資源、值對映和HTTP請求。 |
| 3 | [Apache Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/oak_api/overview.html) | 節點、屬性和工作階段等資料和內容抽象概念。 |
| 4 | [Apache Felix](https://felix.apache.org/) | OSGi應用程式容器抽象概念，例如服務和(OSGi)元件。 |

如果API是由AEM所提供，則偏好使用API而非Sling、JCR和OSGi。 如果AEM不提供API，則偏好使用Sling而非JCR和OSGi。

>[!TIP]
>
>如需這些指引的詳細資訊，請參閱檔案 [瞭解Java API最佳實務。](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

## AEM傳遞與內容管理服務與API {#delivery-apis}

AEM提供可自訂的元件和內容傳送選項。

| 专题 | 描述 |
|---|---|
| [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) | 適用於AEM的標準化網頁內容管理(WCM)元件，可加快開發時間並降低網站的維護成本 |
| [JSON匯出工具](/help/implementing/developing/components/json-exporter.md) | 以JSON資料模型格式傳遞任何AEM頁面的內容 |
| [为组件启用 JSON 导出](/help/implementing/developing/components/enabling-json-exporter.md) | 根據模型程式框架產生元件內容的JSON匯出 |
| [Assets API](/help/assets/mac-api-assets.md) | 允許對資產執行建立 — 讀取 — 更新 — 刪除(CRUD)操作，包括二進位、中繼資料、轉譯和註解。 請參閱AEM Assets HTTP API |
| [內容片段HTTP API](/help/assets/content-fragments/assets-api-content-fragments.md) | 透過CRUD作業，直接透過HTTP API存取內容片段內容 |
| [內容片段GraphQL API](/help/headless/graphql-api/content-fragments.md) | 在Headless CMS實作中有效率地將內容片段傳送至JavaScript使用者端 |
| [內容片段資產HTTP API](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/admin/mac-api-assets.html) | 支援的HTTP資產請求的確切格式 |

## SPA專屬的API {#spa-apis}

AEM單頁應用程式(SPA)編輯器SDK架構提供特定的JavaScript API參考。

| API | 描述 |
|---|---|
| [元件對應](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping) | 提供單頁應用程式將前端元件對應至Adobe Experience Manager資源型別(AEM元件)的方法 |
| [頁面模型管理員](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager) | Adobe Experience Manager編輯器和Adobe Experience Manager單頁應用程式(SPA)編輯器之間的解譯 |
| [React可編輯元件](https://www.npmjs.com/package/@adobe/aem-react-editable-components) | 提供React元件和整合層，讓您開始使用Adobe Experience Manager網站編輯器 |
| [angular可編輯元件](https://www.npmjs.com/package/@adobe/aem-angular-editable-components) | 提供Angular元件和整合層，讓您開始使用Adobe Experience Manager網站編輯器 |

>[!TIP]
>
>檢視 [SPA簡介和逐步解說](/help/implementing/developing/hybrid/introduction.md) 以取得單頁應用程式的詳細資訊。
