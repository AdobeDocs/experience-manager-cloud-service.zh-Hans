---
title: Adobe Experience Manager与Cloud Service支持相同的站点Cookie
description: 将Adobe Experience Manager作为Cloud Service支持ISame站点Cookie
translation-type: tm+mt
source-git-commit: d9a7836034134fac91529a1996c8f05a48a5f4fd
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# 对Adobe Experience Manager的站点Cookie支持与Cloud Service{#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}相同

自版本80、Chrome和更高版本的Safari推出了Cookie安全的新模型。 此模式旨在通过名为`SameSite`的设置对Cookie向第三方站点的可用性引入安全控制。 有关详细信息，请参阅此[文章](https://web.dev/samesite-cookies-explained/)。

此设置(`SameSite=Lax`)的默认值可能导致AEM实例或服务之间的身份验证不工作。 这是因为这些服务的域或URL结构可能不受此Cookie策略的约束。

为了避免这种情况，您需要将登录令牌的SameSite cookieattribue设置为`None`。

您可以按照以下步骤操作：

1. 在本地安装AEM SDK Quickstart的版本
1. 转到位于`http://serveraddress:serverport/system/console/configMgr`的Web控制台
1. 搜索并单击&#x200B;**AdobeGranite令牌身份验证处理程序**
1. 如下图所示，将登录令牌cookie **的** SameSite属性设置为`None`
   ![samesite](/help/security/assets/samesite1.png)
1. 单击“保存”
1. 按照使用AEM SDK Quickstart](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configuratuions-using-the-aem-sdk-quickstart)生成OSGi配置中所述的步骤，为此特定设置生成JSON格式配置[
1. 按照[Cloud Manager API Format for Setting Properties](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGi文档中的步骤应用设置。
