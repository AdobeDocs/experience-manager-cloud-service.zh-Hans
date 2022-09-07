---
title: 预览内容
description: 了解如何使用 AEM 预览服务在内容上线前进行预览。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 5a804895013e19592f918341bbc7921261b26945
workflow-type: ht
source-wordcount: '407'
ht-degree: 100%

---


# 预览内容 {#previewing-content}

AEM 提供站点预览服务，让开发人员和内容作者可以在网站到达发布环境并公开使用之前预览网站的最终体验。

它有助于预览在创作环境中不可见的页面体验，例如页面过渡和其他仅发布方内容。

有关预览环境的更多详细信息，请参阅文档[管理环境](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)。

>[!NOTE]
>
>将体验片段发布到预览基本上遵循与页面相同的过程，不过是从体验片段控制台或编辑器中发布。

## 将内容发布到预览 {#publishing-content-to-preview}

您可以使用&#x200B;**托管发布** UI 将内容发布到预览服务。

1. 在站点控制台中，选择要发送到预览的一个或多个页面，并单击&#x200B;**管理发布**&#x200B;按钮
1. 在以下向导中，选择&#x200B;**预览**&#x200B;作为目标

   ![托管发布](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 单击&#x200B;**下一步**，然后单击&#x200B;**发布**&#x200B;以进行确认。

1. 一个对话框随即出现，其中显示用于在预览环境中访问内容的 URL。


除了使用向导中显示的 URL 查看预览内容之外，您还可以将 `preview-` 添加到生产实例的发布 URL。

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

有关如何为您的环境检索 URL 的更多信息，请参阅文档[管理环境](/help/implementing/cloud-manager/manage-environments.md)。

也可以使用[发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow)并将 `agentId` 参数设置为 `preview` 或使用[复制 API](/help/operations/replication.md#replication-api) 并为预览配置 `AgentFilter` 来将内容发布到预览。

## 从预览中取消发布内容 {#unpublishing-content-from-preview}

从&#x200B;**预览**&#x200B;环境中取消发布内容与从&#x200B;**发布**&#x200B;环境中[取消发布页面](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#unpublishing-pages)的过程基本相同。

唯一的区别是您可以选择&#x200B;**目标**&#x200B;为&#x200B;**预览**。

## 配置预览层的 OSGi 设置 {#configuring-osgi-settings-for-the-preview-tier}

预览层的 OSGi 属性值继承自发布层。不过，可以通过将 `service` 参数设置为 `preview` 值来使预览层的值与发布层的值不同。以下 OSGi 属性示例确定集成端点的 URL。

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
