---
title: 为组件启用 JSON 导出
description: 组件可以适应为基于建模器框架生成其内容的JSON导出。
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 07327f80b23e1e6fdbb3fb49d861221877724d39
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 6%

---

# 为组件启用 JSON 导出 {#enabling-json-export-for-a-component}

组件可以适应为基于建模器框架生成其内容的JSON导出。

## 概述 {#overview}

JSON导出基于[Sling模型](https://sling.apache.org/documentation/bundles/models.html)和[Sling模型导出程序](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130)框架（它本身依赖于[Jackson注释](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)）。

这意味着组件必须具有Sling模型（如果它必须导出JSON）。 因此，请按照以下两个步骤对任何组件启用JSON导出。

* [为组件定义Sling模型](#define-a-sling-model-for-the-component)
* [在Sling模型界面中添加批注](#annotate-the-sling-model-interface)

## 为组件定义Sling模型 {#define-a-sling-model-for-the-component}

首先，必须为元件定义Sling模型。

>[!NOTE]
>
>有关使用Sling模型的示例，请参阅文章[在AEM中开发Sling模型导出程序](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=zh-hans)。

Sling模型实现类必须使用以下内容进行注释：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

这将确保可以使用`.model`选择器和`.json`扩展自行导出组件。

此外，这会指定Sling模型类可以调整到`ComponentExporter`接口中。

>[!NOTE]
>
>Jackson注释通常不是在Sling模型类级别指定的，而是在Model接口级别指定的。 这是为了确保将JSON导出视为组件API的一部分。

>[!NOTE]
>
>`ExporterConstants`和`ComponentExporter`类来自`com.adobe.cq.export.json`捆绑包。

### 使用多个选择器 {#multiple-selectors}

虽然这不是标准用例，但除了`model`选择器之外，还可以配置多个选择器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

但是，在这种情况下，`model`选择器必须是第一个选择器，扩展名必须为`.json`。

## 在Sling模型界面中添加批注 {#annotate-the-sling-model-interface}

要由JSON导出程序框架考虑，模型接口应实现`ComponentExporter`接口（如果是容器组件，则为`ContainerExporter`）。

随后将使用[Jackson注释](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)对相应的Sling模型接口(`MyComponent`)进行注释，以定义应如何导出（序列化）。

必须正确注释模型接口以定义应序列化的方法。 默认情况下，所有遵守getter的常规命名约定的方法都将进行序列化，并且将从getter名称自然派生其JSON属性名称。 可使用`@JsonIgnore`或`@JsonProperty`来阻止或覆盖此项以重命名JSON属性。

## 示例 {#example}

[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)支持JSON导出，可用作参考。

有关示例，请参阅图像核心组件的Sling模型实施及其注释的界面。

## 相关文档 {#related-documentation}

* [内容片段](/help/sites-cloud/administering/content-fragments/overview.md)
* [内容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
* [使用内容片段创作](/help/sites-cloud/authoring/fragments/content-fragments.md)
* [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=zh-hans)和[内容片段组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans)
