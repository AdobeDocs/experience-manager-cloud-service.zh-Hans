---
title: 内容服务的JSON导出程序
description: AEM Content Services设计为在AEM关注网页之外对内容进行投放和描述。 它们使用标准化方法向非传统AEM网页的渠道提供内容投放，这些方法可供任何客户使用。
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 7%

---


# 内容服务的JSON导出程序 {#json-exporter-for-content-services}

AEM Content Services设计为将内容的描述和投放从AEM扩展到网页焦点之外。

它们使用标准化方法向非传统AEM网页的渠道提供内容投放，这些方法可供任何客户使用。 这些渠道可以包括：

* 单页应用程序
* 本机移动应用程序
* AEM外部的其他渠道和接触点

对于使用结构化内容的内容片段，您可以通过使用JSON导出器以JSON数据模型格式交付AEM页的内容来提供内容服务。 然后，您自己的应用程序可以使用它。

## 包含内容片段核心组件的JSON导出程序 {#json-exporter-with-content-fragment-core-components}

使用AEM JSON导出器，您可以以JSON数据模型格式提供(y)AEM页面的内容。 然后，您自己的应用程序可以使用它。

在AEM中，投放是使用选择器和扩 `model` 展来 `.json` 实现的。

`.model.json`

1. 例如，URL，如：

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. 将提供以下内容：

   ![WKND内容的JSON模型](assets/json-model-wknd.png)

您也可以通过专门定位结构化内容片段来提供其内容。

这是使用片段的整个路径(通过 `jcr:content`);例如，带有后缀（如）。

`.../jcr:content/root/container/container/contentfragment.model.json`

您的页面可以包含单个内容片段或多种类型的组件。 您还可以使用列表组件等机制自动搜索相关内容。

* 例如，URL，如：

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
   ```

* 将提供以下内容：

   ![WKND内容片段的JSON模型](assets/json-model-wknd-content-fragment.png)

   >[!NOTE]
   >
   >您可以 [调整自己的组件](enabling-json-exporter.md) ，以访问和使用这些数据。

   >[!NOTE]
   >
   >虽然不是标准实现， [但支持多个选择器](enabling-json-exporter.md#multiple-selectors) , `model` 但必须是第一个选择器。

### 更多信息 {#further-information}

另请参阅：

* 资产 HTTP API
   * [资产 HTTP API](/help/assets/developer-reference-material-apis.md)
* Sling Models:
   * [Sling模型——自130年起将模型类与资源类型关联](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM with JSON:
   * [为组件启用JSON导出](enabling-json-exporter.md)

## 相关文档 {#related-documentation}

有关更多详细信息，请参阅：

* [资产用户指南中的内容片段](/help/assets/content-fragments/content-fragments.md)
* [内容片段模型](/help/assets/content-fragments/content-fragments-models.md)
* [使用内容片段进行创作](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [核心组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/introduction.html) 和内容 [片段组件](https://docs.adobe.com/content/help/zh-Hans/experience-manager-core-components/using/components/content-fragment-component.html)
