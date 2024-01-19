---
title: 不允许通过Sling模型导出器序列化资源解析器
description: 不允许通过Sling模型导出器序列化资源解析器
source-git-commit: 4543a4646719f8433df7589b21344433c43ab432
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# 不允许通过Sling模型导出器序列化资源解析器 {#disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter}

Sling模型导出器功能允许将Sling模型对象序列化为JSON格式。 此功能之所以得到广泛应用，是因为它使SPA（单页应用程序）能够轻松从AEM访问数据。 在实施端，使用Jacson Databind库来序列化这些对象。

序列化是递归操作。 从“根对象”开始，递归遍历所有符合条件的对象并将其及其子对象序列化。 您可以查找在其中序列化了哪些字段的描述 [本文](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not).

这种方法将所有类型的对象序列化为JSON，自然地它也可以序列化Sling `ResourceResolver` 对象（如果序列化规则涵盖该对象）。 这是有问题的，因为 `ResourceResolver` 服务（因此也是代表它的服务对象）包含潜在的敏感信息，这些信息不应公开。 例如：

* 用户ID
* 用于解析相对路径的搜索路径
* 此 `propertyMap`.

特别敏感的是 `propertyMap` （请参阅的API文档） [`getPropertyMap`](https://sling.apache.org/apidocs/sling12/org/apache/sling/api/resource/ResourceResolver.html#getPropertyMap--))，因为这是一种内部数据结构，可用于多种用途，例如缓存与共享相同生命周期的对象。 `ResourceResolver`. 序列化这些内容可能会泄露实施详细信息，并可能会产生安全影响，因为数据会被公开，最终用户应该无法读取和访问。 出于这个原因 `ResourceResolvers` 不应序列化为JSON。

Adobe计划禁用序列化 `ResourceResolvers` 分两步执行：

1. 从AEMas a Cloud Service发行14697本开始，每当收到 `ResourceResolver` 序列化AEM将记录警告消息。 我们鼓励所有客户检查其应用程序日志以获取这些日志语句，并相应地调整其代码库。
1. 稍后，Adobe将禁用将ResourceResolvers序列化为JSON。

## 实施 {#implementation}

WARN消息同时记录在AEMas a Cloud Service和本地AEM SDK实例中，如下所示：

```
[127.0.0.1 [1705061734620] GET /content/../page.model.json HTTP/1.1] org.apache.sling.models.jacksonexporter.impl.JacksonExporter A ResourceResolver is serialized with all its private fields containing implementation details you should not disclose. Please review your Sling Model implementation(s) and remove all public accessors to a ResourceResolver.
```

此日志消息表示在序列化过程中 `/content/…/page` 转换为JSON a `ResourceResolver` 已序列化。 通过请求 `/content/../page.model.json` 您可以检查 `ResourceResolver` 会显示，并使用它来识别实际触发此行为的Sling模型类。


>[!NOTE]
>
>经验证，AEM核心组件不会受到此问题的影响。

## 请求的操作 {#requested-action}

Adobe要求所有客户检查其应用程序日志和代码库，以查看他们是否受此问题影响，并在必要时更改自定义应用程序，以便不再显示此警告消息。

假设在大多数情况下，这些必需的更改是直接的，因为 `ResourceResolver` 对象完全不需要JSON输出，因为前端应用程序通常不需要其中包含的信息。 这意味着，在大多数情况下，应足以排除 `ResourceResolver` Jackson考虑的对象(请参见 [规则](https://www.baeldung.com/jackson-field-serializable-deserializable-or-not))。

如果Sling模型受此问题影响但未发生更改，则会显式禁用的 `ResourceResolver` 对象(在第2步中由Adobe执行)将强制JSON输出中的更改。



