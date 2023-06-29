---
title: 配置预览层的 OSGi 设置
description: 了解如何配置 AEM 预览服务在内容上线前进行预览。
exl-id: 1200bb17-8a3c-4e41-85f4-ed2334b61f69
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 95%

---

# 配置预览层的 OSGi 设置 {#configure-osgi-preview-tier}

AEM 提供站点预览服务，让开发人员和内容作者可以在网站到达发布环境并公开使用之前预览网站的最终体验。

它有助于预览在创作环境中不可见的各类体验。例如，页面转换、体验片段和其他仅发布端的内容。

预览层的 OSGi 属性值继承自发布层。不过，可以通过将 `service` 参数设置为 `preview` 值来使预览层的值与发布层的值不同。

>[!NOTE]
>
>有关预览环境的更多详细信息，请参阅 [管理环境](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

## 配置预览层的 OSGi 设置 {#configuring-osgi-settings-for-the-preview-tier}

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
