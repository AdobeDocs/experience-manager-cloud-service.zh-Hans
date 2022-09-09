---
title: 面向 Adobe Experience Manager as a Cloud Service 的相同网站 Cookie 支持
description: 面向 Adobe Experience Manager as a Cloud Service 的相同网站 Cookie 支持
exl-id: 2cec7202-4450-456f-8e62-b7ed3791505c
source-git-commit: e1234e90e276a6274fc4dc9de0ae577219669ecf
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 100%

---

# 面向 Adobe Experience Manager as a Cloud Service 的相同网站 Cookie 支持 {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

从 80 版开始，Chrome 和后来的 Safari 都引入了一种新的 Cookie 安全模型。此模式旨在通过名为 `SameSite` 的设置向第三方站点引入有关 Cookie 可用性的安全控制措施。有关更多详细信息，请参阅[本文](https://web.dev/samesite-cookies-explained/)。

此设置的默认值 (`SameSite=Lax`) 可能会导致 AEM 实例或服务之间的身份验证不起作用。这是因为这些服务的域或 URL 结构可能不受此 Cookie 策略的约束。

要解决此问题，您需要将登录令牌的 SameSite Cookie 属性设置为 `None`。

>[!CAUTION]
>
>`SameSite=None` 设置仅在协议安全 (HTTPS) 时应用。
>
>如果协议不安全 (HTTP)，则将忽略该设置，服务器将显示以下警告消息：
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

您可以按照以下步骤添加设置：

1. 在本地安装 AEM SDK 快速入门版本
1. 转至位于 `http://serveraddress:serverport/system/console/configMgr` 的 Web 控制台
1. 搜索找到 **Adobe Granite Token Authentication Handler** 并单击它
1. 将&#x200B;**登录令牌 Cookie 的 SameSite 属性**&#x200B;设置为 `None`，如下图所示
   ![samesite](/help/security/assets/samesite1.png)
1. 单击“保存”
1. 执行[使用 AEM SDK 快速入门生成 OSGi 配置](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)中概述的步骤，为此特定设置生成 JSON 格式配置
1. 按照[用于设置属性的 Cloud Manager API 格式](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) OSGi 文档中的步骤来应用设置。

在更新此设置且用户注销并再次登录后，`login-token` Cookie 将具有 `None` 属性集，并且将包含在跨站点请求中。
