---
title: 预览内容
description: 了解如何在上线之前使用AEM预览服务预览内容。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 66bc262b35f69b7877e4a01df9ab26395afd604d
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 1%

---


# 预览内容 {#previewing-content}

AEM提供了“站点”预览服务，允许开发人员和内容作者在网站到达发布环境并公开可用之前，预览网站的最终体验。

它有助于预览在创作环境中不可见的页面体验，如页面过渡和其他仅发布端内容。

有关预览环境的更多详细信息，请参阅此文档 [管理环境。](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).

>[!NOTE]
>
>将体验片段发布到预览基本上遵循与页面相同的过程，不过是从体验片段控制台或编辑器中发布。

## 将内容发布到预览 {#publishing-content-to-preview}

您可以使用 **托管发布** UI。

1. 在站点控制台中，选择要发送以进行预览的一个或多个页面，然后单击 **管理发布** 按钮
1. 在以下向导中，选择 **预览** 作为目标

   ![托管出版物](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 单击 **下一个**，然后 **发布** 确认。

1. 将显示一个对话框，用于显示用于访问预览环境中内容的URL。


或者，您也可以使用向导中显示的URL来查看预览内容，并在 `preview-` 到生产实例的发布URL。

```
https://preview-p<programID>-e>environmentID>.adobeaemcloud.com/<pathtopage>.html
```

查看文档 [管理环境](/help/implementing/cloud-manager/manage-environments.md) 有关如何检索环境URL的更多信息。

也可以使用 [发布内容树工作流](/help/operations/replication.md#publish-content-tree-workflow) 和 `agentId` 参数设置为 `preview` 或使用 [复制API](/help/operations/replication.md#replication-api) 带 `AgentFilter` 配置了预览。

## 为预览层配置OSGi设置 {#configuring-osgi-settings-for-the-preview-tier}

预览层的OSGi属性值继承自发布层。 但是，通过设置 `service` 参数到值 `preview`. OSGi属性的以下示例确定集成端点的URL。

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

有关更多信息，请参阅 [此部分](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration) OSGi配置文档中的。

## 使用开发人员控制台调试预览 {#debugging-preview-using-the-developer-console}

要使用开发人员控制台调试预览层，请按照以下步骤操作：

* 在 [开发人员控制台](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)，选择 **— 全部预览 —** 或包含 **prev** 在
* 生成预览实例的相关信息请参阅 [管理环境](/help/implementing/cloud-manager/manage-environments.md) 有关如何获取环境URL的更多信息。
