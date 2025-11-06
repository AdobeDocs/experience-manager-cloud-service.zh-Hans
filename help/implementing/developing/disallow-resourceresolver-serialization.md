---
title: 禁止通过 Sling 模型导出器序列化 ResourceResolver
description: 禁止通过 Sling 模型导出器序列化 ResourceResolver
exl-id: 63972c1e-04bd-4eae-bb65-73361b676687
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 5%

---

# 禁止通过 Sling 模型导出器序列化 ResourceResolver {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

Sling模型导出器功能允许将Sling模型对象序列化为JSON格式。 此功能被广泛使用，因为它使SPA（单页应用程序）能够轻松地从AEM访问数据。 在实施方面，使用Jackson Databind库来序列化这些对象。

序列化是递归操作。 从“根对象”开始，递归遍历所有符合条件的对象并将其及其子对象序列化。 您可以在文章[Jackson - Decision What Fields Get Serialized/Deserialized](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not)中找到有关哪些字段已序列化的说明。

此方法将所有类型的对象序列化为JSON。 当然，如果序列化规则涵盖Sling `ResourceResolver`对象，它也可以将其序列化。 这是有问题的，因为`ResourceResolver`服务（因此也是代表它的服务对象）包含不应公开的潜在敏感信息。 例如：

* 用户ID
* 用于解析相对路径的搜索路径
* `propertyMap`

特别敏感的是`propertyMap`（请参阅[`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--)的API文档），因为它是内部数据结构，可用于多种用途，例如缓存与`ResourceResolver`共享相同生命周期的对象。 序列化这些内容可能会泄露实施详细信息，并可能会产生安全影响，因为数据会泄露，而最终用户应该无法读取和访问。 因此，不应将`ResourceResolvers`序列化为JSON。

Adobe计划以两步方式禁用`ResourceResolvers`的序列化：

1. 从AEM as a Cloud Service发行14697本开始，每当序列化`ResourceResolver`时，AEM都将记录一条警告消息。 我们鼓励所有客户检查其应用程序日志以获取这些日志语句，并相应地调整其代码库。
1. 稍后，Adobe将禁用`ResourceResolver`作为JSON的序列化。

## 实施 {#implementation}

警告消息同时记录在AEM as a Cloud Service实例和本地AEM SDK实例中，如下所示：

```text
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

此日志消息表示在将`/content/…/page`序列化为JSON的过程中，`ResourceResolver`已经序列化。 通过请求`/content/../page.model.json`，您可以检查`ResourceResolver`的字段的确切显示位置，并使用该位置来识别实际触发此行为的Sling模型类。


>[!NOTE]
>
>已验证[AEM核心组件](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-core-components/using/introduction)不受此问题的影响。

## 请求的操作 {#requested-action}

Adobe要求所有客户检查其应用程序日志和代码库，以查看他们是否受此问题影响，并在必要时更改自定义应用程序，以便此警告消息不再显示在日志中。

假定在大多数情况下，这些必需的改变是直接的。 JSON输出中完全不需要`ResourceResolver`对象，因为前端应用程序通常不需要其中包含的信息，这意味着在大多数情况下，它应足以排除Jackson不考虑`ResourceResolver`对象（请参阅[规则](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not)）。

如果Sling模型受到此问题影响但未发生更改，则显式禁用`ResourceResolver`对象的序列化(作为第二步由Adobe执行)将强制对JSON输出进行更改。
