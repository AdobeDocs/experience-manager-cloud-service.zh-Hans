---
title: 为组件启用 JSON 导出
description: 组件可以基于建模器框架进行修改，以生成其内容的JSON导出。
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 11%

---

# 为组件启用 JSON 导出 {#enabling-json-export-for-a-component}

组件可以基于建模器框架进行修改，以生成其内容的JSON导出。

## 概述 {#overview}

JSON导出基于 [Sling模型](https://sling.apache.org/documentation/bundles/models.html)、和 [Sling模型导出程序](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 框架(它本身依赖 [Jackson批注](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations))。

这意味着如果组件需要导出JSON，则必须具有Sling模型。 因此，您需要按照以下两个步骤在任何组件上启用JSON导出。

* [为组件定义Sling模型](#define-a-sling-model-for-the-component)
* [在Sling模型界面中添加批注](#annotate-the-sling-model-interface)

## 为组件定义Sling模型 {#define-a-sling-model-for-the-component}

首先，必须为组件定义Sling模型。

>[!NOTE]
>
>有关使用Sling模型的示例，请参阅文章 [在AEM中开发Sling模型导出程序](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html).

Sling模型实施类必须使用以下内容添加注释：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

这可确保您的组件可以使用 `.model` 选择器和 `.json` 扩展。

此外，这还指定Sling Model类可以适应于 `ComponentExporter` 界面。

>[!NOTE]
>
>Jackson批注通常不是在Sling模型类级别指定，而是在模型界面级别指定。 这是为了确保将JSON导出视为组件API的一部分。

>[!NOTE]
>
>的 `ExporterConstants` 和 `ComponentExporter` 课程来自 `com.adobe.cq.export.json` 捆绑。

### 使用多个选择器 {#multiple-selectors}

除了 `model` 选择器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

但是，在这种情况下， `model` 选择器必须是第一个选择器，并且扩展必须是 `.json`.

## 在Sling模型界面中添加批注 {#annotate-the-sling-model-interface}

要由JSON导出程序框架考虑，模型界面应实施 `ComponentExporter` 界面(或 `ContainerExporter`，对于容器组件)。

相应的Sling模型界面(`MyComponent`)，则将使用 [Jackson批注](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) 定义应如何导出（序列化）。

需要对“模型”(Model)界面进行适当的注释，以定义应序列化哪些方法。 默认情况下，所有遵循getter通用命名约定的方法都将进行序列化，并将从getter名称中自然派生其JSON属性名称。 可以使用阻止或覆盖此功能 `@JsonIgnore` 或 `@JsonProperty` 重命名JSON属性。

## 示例 {#example}

[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-Hans) 支持JSON导出，可用作引用。

有关示例，请参阅图像核心组件及其注释界面的Sling模型实施。

## 相关文档 {#related-documentation}

有关更多详细信息，请参阅：

* [内容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)
* [内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)
* [使用内容片段创作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [内容片段组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans)
