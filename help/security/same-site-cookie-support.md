---
title: 与Adobe Experience ManagerCloud Service支持相同的网站Cookie
description: 与Adobe Experience ManagerCloud Service支持相同的网站Cookie
exl-id: 2cec7202-4450-456f-8e62-b7ed3791505c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---

# 对Adobe Experience Manager与Cloud Service{#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}的相同站点Cookie支持

自版本80、Chrome及更高版本的Safari以来，为Cookie安全引入了新模型。 此模式旨在通过名为`SameSite`的设置，对Cookie的可用性引入安全控制。 有关更多详细信息，请参阅此[文章](https://web.dev/samesite-cookies-explained/)。

此设置的默认值(`SameSite=Lax`)可能会导致AEM实例或服务之间的身份验证无法工作。 这是因为这些服务的域或URL结构可能不受此Cookie策略的约束。

为了解决此问题，您需要将登录令牌的SameSite Cookie属性设置为`None`。

您可以按照以下步骤执行操作：

1. 在本地安装AEM SDK快速启动版本
1. 转到位于`http://serveraddress:serverport/system/console/configMgr`的Web控制台
1. 搜索并单击&#x200B;**AdobeGranite令牌身份验证处理程序**
1. 将登录令牌Cookie **的** SameSite属性设置为`None`，如下图所示
   ![samesite](/help/security/assets/samesite1.png)
1. 单击Save
1. 按照[使用AEM SDK快速入门生成OSGi配置](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)中所述的步骤，为此特定设置生成JSON格式配置
1. 按照[Cloud Manager API格式中的步骤来应用设置，以设置属性](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGi文档。

更新此设置后，用户将注销并再次登录， `login-token` Cookie将设置`None`属性，并将包含在跨站点请求中。
