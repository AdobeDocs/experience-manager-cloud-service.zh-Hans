---
title: 为组件启用 JSON 导出
description: 元件可調整為根據模型程式框架產生其內容的JSON匯出。
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 12%

---

# 为组件启用 JSON 导出 {#enabling-json-export-for-a-component}

元件可調整為根據模型程式框架產生其內容的JSON匯出。

## 概述 {#overview}

JSON匯出是根據 [Sling模型](https://sling.apache.org/documentation/bundles/models.html)，並在上 [Sling模型匯出工具](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 框架(本身需仰賴 [Jackson附註](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations))。

這表示元件在需要匯出JSON時必須具有Sling模型。 因此，您需要遵循這兩個步驟，才能在任何元件上啟用JSON匯出。

* [為元件定義Sling模型](#define-a-sling-model-for-the-component)
* [為Sling模型介面加上註釋](#annotate-the-sling-model-interface)

## 為元件定義Sling模型 {#define-a-sling-model-for-the-component}

首先，必須為元件定義Sling模型。

>[!NOTE]
>
>如需使用Sling模型的範例，請參閱文章 [在AEM中開發Sling模型匯出工具](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=zh-Hans).

Sling模型實作類別必須使用下列專案註釋：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

這可確保您的元件可自行匯出，使用 `.model` 選擇器和 `.json` 副檔名。

此外，這會指定Sling模型類別可以改編為 `ComponentExporter` 介面。

>[!NOTE]
>
>Jackson註解通常不會在Sling模型類別層級指定，而是在Model介面層級指定。 這是為了確保將JSON匯出視為元件API的一部分。

>[!NOTE]
>
>此 `ExporterConstants` 和 `ComponentExporter` 類別來自 `com.adobe.cq.export.json` 套件組合。

### 使用多个选择器 {#multiple-selectors}

雖然這不是標準使用案例，但除了以下設定外，您也可以設定多個選取器： `model` 選擇器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

但在這種情況下， `model` 選擇器必須是第一個選擇器，而擴充功能必須是 `.json`.

## 註釋Sling模型介面 {#annotate-the-sling-model-interface}

若要JSON匯出工具架構列入考量，模型介面應實作 `ComponentExporter` 介面(或 `ContainerExporter`（若為容器元件）。

對應的Sling模型介面(`MyComponent`)之後會使用進行註解 [Jackson附註](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) 以定義應如何匯出（序列化）。

需要正確註解模型介面，以定義應序列化哪些方法。 依預設，所有遵守getter一般命名慣例的方法都將序列化，並且從getter名稱自然衍生出其JSON屬性名稱。 這可以使用防止或覆寫 `@JsonIgnore` 或 `@JsonProperty` 重新命名JSON屬性。

## 示例 {#example}

[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 支援JSON匯出，可作為參考使用。

如需範例，請參閱影像核心元件的Sling模型實作及其附註介面。

## 相關檔案 {#related-documentation}

如需詳細資訊，請參閱：

* [内容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)
* [内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)
* [使用內容片段編寫](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 和 [內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans)
