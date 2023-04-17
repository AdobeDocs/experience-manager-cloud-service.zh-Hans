---
title: 配置预览层的 OSGi 设置
description: 了解如何在上线之前将AEM预览服务配置为预览内容。
source-git-commit: 7b56bb05e31d7a61d7a8fb13e2bd0ff6e4fb301d
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 64%

---


# 配置预览层的 OSGi 设置 {#configure-osgi-preview-tier}

AEM提供了“站点”预览服务，允许开发人员和内容作者在网站到达发布环境并公开可用之前，预览网站的最终体验。

它有助于预览一系列在创作环境中不可见的体验。 例如，页面过渡、体验片段和其他仅发布端内容。

预览层的 OSGi 属性值继承自发布层。不过，可以通过将 `service` 参数设置为 `preview` 值来使预览层的值与发布层的值不同。

>[!NOTE]
>
>有关预览环境的更多详细信息，请参阅文档[管理环境](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)。

## 为预览层配置OSGi设置 {#configuring-osgi-settings-for-the-preview-tier}

以下 OSGi 属性示例确定集成端点的 URL。

```
[
{
"name":"INTEGRATION_URL",
"type":"string",
"value":"http://s2.integrationvendor.com",
"service": "preview"
}
]
```

有关更多信息，请参阅 OSGi 配置文档的[此部分](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration)。

## 使用 Developer Console 调试预览 {#debugging-preview-using-the-developer-console}

请使用 Developer Console 执行以下步骤来调试预览层：

* 在 [Developer Console](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools) 中，选择 **-- 所有预览 --** 或其名称包含 **prev** 的生产环境
* 生成预览实例的相关信息
有关如何获取环境 URL 的更多信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md)。
