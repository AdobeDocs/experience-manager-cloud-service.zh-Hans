---
title: 为组件启用 JSON 导出
description: 组件可以适用于基于建模器框架生成其内容的JSON导出。
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 12%

---

# 为组件启用 JSON 导出 {#enabling-json-export-for-a-component}

组件可以适用于基于建模器框架生成其内容的JSON导出。

## 概述 {#overview}

JSON导出基于 [Sling模型](https://sling.apache.org/documentation/bundles/models.html)，并且位于 [Sling模型导出程序](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) 框架(它本身依赖于 [Jackson注释](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations))。

这意味着组件在需要导出JSON时必须具有Sling模型。 因此，您需要执行这两个步骤才能对任何组件启用JSON导出。

* [为组件定义Sling模型](#define-a-sling-model-for-the-component)
* [在Sling模型界面中添加批注](#annotate-the-sling-model-interface)

## 为组件定义Sling模型 {#define-a-sling-model-for-the-component}

首先，必须为组件定义Sling模型。

>[!NOTE]
>
>有关使用Sling模型的示例，请参阅文章 [在AEM中开发Sling模型导出程序](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=zh-Hans).

Sling模型实现类必须使用以下内容进行注释：

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

这可确保可以使用单独导出组件 `.model` 选择器和 `.json` 扩展。

此外，这会指定Sling模型类可以调整到 `ComponentExporter` 界面。

>[!NOTE]
>
>Jackson注释通常不是在Sling模型类级别指定的，而是在Model接口级别指定的。 这是为了确保将JSON导出视为组件API的一部分。

>[!NOTE]
>
>此 `ExporterConstants` 和 `ComponentExporter` 课程来自 `com.adobe.cq.export.json` 捆绑。

### 使用多个选择器 {#multiple-selectors}

虽然这不是标准用例，但除了标准用例之外，还可以配置多个选择器 `model` 选择器。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

然而，在此情况下， `model` 选择器必须是第一个选择器，扩展必须是 `.json`.

## 在Sling模型界面中添加批注 {#annotate-the-sling-model-interface}

要供JSON导出程序框架考虑，模型接口应实现 `ComponentExporter` 界面(或 `ContainerExporter`（对于容器组件）。

相应的Sling模型界面(`MyComponent`)，然后使用进行注释 [Jackson注释](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) 以定义应如何导出（序列化）。

需要对模型接口进行正确注释以定义应序列化的方法。 默认情况下，将序列化所有遵守getter的常规命名约定的方法，并将从getter名称中自然派生其JSON属性名称。 可以使用阻止或覆盖此项 `@JsonIgnore` 或 `@JsonProperty` 以重命名JSON属性。

## 示例 {#example}

[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 支持JSON导出，可用作参考。

有关示例，请参阅图像核心组件的Sling模型实施及其注释界面。

## 相关文档 {#related-documentation}

有关更多详细信息，请参阅：

* [内容片段](/help/sites-cloud/administering/content-fragments/content-fragments.md)
* [内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)
* [使用内容片段创作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [内容片段组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans)
