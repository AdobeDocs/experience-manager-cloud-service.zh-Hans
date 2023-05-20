---
title: 内容服务的 JSON 导出器
description: AEM 内容服务旨在概括 AEM 中/来自 AEM 的内容的描述和投放，而不只是关注网页。它们使用可供任何客户使用的标准化方法，将内容投放到非传统 AEM 网页的渠道。
exl-id: d3ddffb7-cef9-4c86-aa31-175f13f9b4a5
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 31%

---

# 内容服务的 JSON 导出器 {#json-exporter-for-content-services}

AEM Content Services旨在概括AEM中/來自Web網頁以外內容的說明和傳遞。

它们使用可供任何客户使用的标准化方法，将内容投放到非传统 AEM 网页的渠道。 这些渠道可以包括：

* 单页面应用程序
* 本机移动设备应用程序
* AEM外部的其他管道和接觸點

對於使用結構化內容的內容片段，您可以使用JSON匯出工具以JSON資料模型格式傳送AEM頁面的內容，以提供內容服務。 然後，您自己的應用程式便可使用它。

## 具有內容片段核心元件的JSON匯出工具 {#json-exporter-with-content-fragment-core-components}

您可以使用AEM JSON匯出工具，以JSON資料模型格式傳送AEM頁面的內容。 然後，您自己的應用程式便可使用它。

在AEM中，傳遞是使用選擇器達成 `model` 和 `.json` 副檔名。

`.model.json`

1. 例如，URL，例如：

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. 將傳送下列內容：

   ![WKND內容的JSON模型](assets/json-model-wknd.png)

或者，您可以透過特別定位來傳送結構化內容片段的內容。

這是使用片段的整個路徑來完成的(透過 `jcr:content`)；例如尾碼為。

`.../jcr:content/root/container/container/contentfragment.model.json`

您的頁面可包含單一內容片段或多個不同型別的元件。 您也可以使用清單元件等機制來自動搜尋相關內容。

* 例如，URL，例如：

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
   ```

* 將傳送下列內容：

   ![WKND內容片段的JSON模型](assets/json-model-wknd-content-fragment.png)

   >[!NOTE]
   >
   >您可以 [調整您自己的元件](enabling-json-exporter.md) 以存取及使用此資料。

   >[!NOTE]
   >
   >雖然不是標準實作， [支援多個選擇器，](enabling-json-exporter.md#multiple-selectors) 但是 `model` 必須為第一個。

### 更多信息 {#further-information}

另请参阅：

* Assets HTTP API
   * [Assets HTTP API](/help/assets/developer-reference-material-apis.md)
* Sling 模型:
   * [Sling模型 — 自130起將模型類別與資源型別建立關聯](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* 使用JSON的AEM：
   * [为组件启用 JSON 导出](enabling-json-exporter.md)

## 相關檔案 {#related-documentation}

如需詳細資訊，請參閱：

* [内容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)
* [内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)
* [使用內容片段編寫](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 和 [內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans)
