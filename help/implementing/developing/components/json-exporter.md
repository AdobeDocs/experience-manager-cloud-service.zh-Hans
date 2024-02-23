---
title: 内容服务的 JSON 导出器
description: AEM Content Services旨在概括AEM中/来自AEM的内容的描述和交付，而不只是关注网页。 它们使用可供任何客户使用的标准化方法，将内容投放到非传统AEM网页的渠道。
exl-id: d3ddffb7-cef9-4c86-aa31-175f13f9b4a5
source-git-commit: 89f23a590338561b4cfeb10b54a260a135ec2f08
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 17%

---

# 内容服务的 JSON 导出器 {#json-exporter-for-content-services}

AEM Content Services旨在概括AEM中/来自Web页面的内容的描述和交付，而不只是网页的焦点。

它们使用可供任何客户使用的标准化方法，将内容投放到非传统 AEM 网页的渠道。这些渠道可以包括：

* 单页面应用程序
* 本机移动设备应用程序
* AEM外部的其他渠道和接触点

对于使用结构化内容的内容片段，您可以通过使用JSON导出程序以JSON数据模型格式交付AEM页面的内容来提供内容服务。 然后，这可以由您自己的应用程序使用。

## 包含内容片段核心组件的JSON导出器 {#json-exporter-with-content-fragment-core-components}

使用AEM JSON导出程序，您可以以JSON数据模型格式交付AEM页面的内容。 然后，这可以由您自己的应用程序使用。

在AEM中，使用选择器实现投放 `model` 和 `.json` 扩展。

`.model.json`

1. 例如，URL，例如：

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. 将投放如下内容：

   ![WKND内容的JSON模型](assets/json-model-wknd.png)

或者，您可以通过专门定向结构化内容片段来投放其内容。

这是使用片段的整个路径完成的(通过 `jcr:content`)；例如，后缀为。

`.../jcr:content/root/container/container/contentfragment.model.json`

您的页面可以包含单个内容片段，也可以包含多种类型的多个组件。 您还可以使用列表组件等机制来自动搜索相关内容。

* 例如，URL，例如：

  ```shell
  http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
  ```

* 将投放如下内容：

  ![WKND内容片段的JSON模型](assets/json-model-wknd-content-fragment.png)

  >[!NOTE]
  >
  >您可以 [调整您自己的组件](enabling-json-exporter.md) 以访问和使用此数据。

  >[!NOTE]
  >
  >虽然不是标准实施， [支持多个选择器，](enabling-json-exporter.md#multiple-selectors) 但是 `model` 必须是第一个。

### 更多信息 {#further-information}

* Assets HTTP API
   * [Assets HTTP API](/help/assets/developer-reference-material-apis.md)
* Sling模型：
   * [Sling模型 — 自130年起将模型类与资源类型相关联](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* 带有JSON的AEM：
   * [为组件启用 JSON 导出](enabling-json-exporter.md)

## 相关文档 {#related-documentation}

* [内容片段](/help/sites-cloud/administering/content-fragments/overview.md)
* [内容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
* [使用内容片段创作](/help/sites-cloud/authoring/fragments/content-fragments.md)
* [核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 和 [内容片段组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=zh-Hans)
