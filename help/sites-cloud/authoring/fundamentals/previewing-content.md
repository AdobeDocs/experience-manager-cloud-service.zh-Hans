---
title: 预览内容
description: 了解如何在上线之前使用AEM预览服务预览内容。
exl-id: 6b4b57f6-2e66-4c83-94d9-bc1e0daab0f3
source-git-commit: 78c5649c6b9c04cb459f5730161affeb452c916c
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# 预览内容 {#previewing-content}

>[!NOTE]
>
>要在2021年8月3日之前创建的环境中启用预览功能，请确保该环境为AEM版本2021.05.5368.20210529T101701Z或更高版本，然后执行客户启动的管道。

AEM提供了“站点预览”服务，旨在让开发人员和内容作者在网站到达发布环境之前预览网站的最终体验并公开提供。

它有助于预览在创作环境中不可见的页面体验，如页面过渡和其他仅发布端内容。

另请阅读有关访问预览服务](/help/implementing/cloud-manager/manage-environments.md#access-preview-service)的信息。[

## 将内容发布到预览 {#publishing-content-to-preview}

您可以使用管理的发布UI将内容发布到预览服务，如下所示：

1. 选择要在站点控制台中进行预览的一个或多个页面，然后单击&#x200B;**管理发布**&#x200B;按钮
1. 在下面的向导中，选择&#x200B;**预览**&#x200B;作为目标

   ![托管出版物](/help/sites-cloud/authoring/assets/previewmanagedpublication.png)

1. 单击&#x200B;**Next**，然后单击&#x200B;**Publish**&#x200B;以确认。

1. 将显示一个对话框，用于在“预览”环境中访问内容的URL。

   或者，要查看预览内容，您还可以将&#x200B;**preview**&#x200B;附加到生产实例的发布URL。

   URL的构建方式如下：

   ```
   https://preview-p[programID]-e[environmentID].adobeaemcloud.com/pathtopage.html
   ```

有关如何获取环境URL的更多信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md)。

也可以通过以下方法发布内容：使用[发布内容树工作流程](/help/operations/replication.md#publish-content-tree-workflow)（将agentId参数设置为预览），或者使用[复制API](/help/operations/replication.md#replication-api)（配置了AgentFilter进行预览）。

## 为预览层配置OSGi设置 {#configuring-osgi-settings-for-the-preview-tier}

预览层的OSGI属性值继承自发布层，但可以使用特定于环境的值将服务参数设置为值“preview”，从发布层中区分预览层值。 以下OSGI属性为例，该属性可确定集成端点的URL:

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

有关更多信息，请参阅OSGi配置文档的[此部分](/help/implementing/deploying/configuring-osgi.md#author-vs-publish-configuration)。

## 使用开发人员控制台调试预览 {#debugging-preview-using-the-developer-console}

要使用开发人员控制台调试预览层，请按照以下步骤操作：

* 在[开发人员控制台](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools)中，选择&#x200B;**— All Preview —**&#x200B;或名称中包含&#x200B;**prev**&#x200B;的生产环境
* 为预览实例生成相关信息
有关如何获取环境URL的更多信息，请参阅[管理环境](/help/implementing/cloud-manager/manage-environments.md)。
