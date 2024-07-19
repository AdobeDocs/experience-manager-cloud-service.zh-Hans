---
title: 导航到 Screens Services Provider
description: 本页介绍如何导航到Screens服务提供商。
exl-id: 9eff6fe8-41d4-4cf3-b412-847850c4e09c
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f91166ca0349636386aa8721ded5b3bbda1cdb51
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 4%

---

# 导航到 Screens Services Provider {#setup-screens-services-provider}

## 简介 {#introduction}

**Screens Services Provider**&#x200B;允许内容作者、开发人员和管理员在将内容添加到渠道后管理内容播放的显示器和播放器。 授予用户访问AEM Cloud Service的权限后，他们应该能够登录Screens服务提供商。

本节介绍如何设置Screens服务提供商。


## 目标 {#objective}

以下部分介绍了如何配置和设置Screens服务提供商。

## 设置Screens服务提供商的步骤 {#screens-services-provider}

请按照以下步骤设置Screens服务提供商：

1. 从[此处](https://experience.adobe.com/screens)导航到Screens服务提供商。

   >[!CAUTION]
   >如果您有权访问多个组织，请确保您已登录到正确的组织。 要更改您的组织，请单击屏幕右上角的组织名称，然后选择您需要访问的所需组织。

1. 单击项目旁边的齿轮图标（左上角）

   ![图像](/help/screens-cloud/assets/configure/configure-screens0.png)

1. 在“编辑设置”对话框中输入以下详细信息。
   * **Publish Url** - AEM发布URL（例如，`https://publish-p12345-e12345.adobeaemcloud.com`）
   * **作者URL** - AEM作者URL（例如，`https://author-p12345-e12345.adobeaemcloud.com`）

   >[!NOTE]
   >在Screens服务提供商下配置AEM之前，请确保创建并发布至少一个AEM屏幕渠道。 要创建渠道，请在您的内容提供商中导航到/screens.html 。

   ![图像](/help/screens-cloud/assets/configure/configure-screens4.png)

1. 单击&#x200B;**保存**&#x200B;以连接到Screens内容提供程序。

1. 如果您已将AEM发布实例配置为仅允许Cloud Manager的IP 允许列表功能访问受信任的IP地址，则需要在“设置”对话框中配置具有键值的标头，如下所示。
需要列入白名单的IP还需要移动到配置文件，并需要从Cloud Manager设置中[取消应用](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list)。

   ![图像](/help/screens-cloud/assets/configure/configure-screens20.png)

需要在AEM CDN配置中配置相同的密钥。  建议不要将标头值直接放入GITHub中，并且使用[机密引用](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-credentials-authentication#rotating-secrets)。
下面提供了[CDN配置](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf)示例：

列入允许列表     kind： &quot;CDN&quot;
    version： &quot;1&quot;
    metadata：
    envTypes： [&quot;dev&quot;， &quot;stage&quot;， &quot;prod&quot;]
    data：
    trafficFilters：
    规则：
     — 名称： &quot;block-request-from-not-allowed-ips&quot;
    条件：
    allOf：
    - reqProperty： clientIp
    notIn： [&quot;101.41.112.0/24&quot;]
    - reqProperty： tier
    equequequals： publish
     4}操作： block
     — 名称： &quot;allow-requests-with-header&quot;
    when：
    allOf：
    - reqProperty： tier
    equals： publish
    - reqProperty： path
    equals： /screens/channels.json
    - reqHeader： x-screens-key
    equals： ${\
    {CDN_HEADER_KEY}
    操作：
    类型： allow

1. 从左侧导航栏中选择&#x200B;**渠道**，然后单击&#x200B;**在内容提供程序中打开**。

   ![图像](/help/screens-cloud/assets/configure/configure-screens1.png)

1. Screens内容提供程序将在另一个选项卡中打开，通过该选项卡可创建内容。

   ![图像](/help/screens-cloud/assets/configure/configure-screens2.png)

## 后续内容 {#whats-next}

了解如何设置Screens服务提供程序后，请导航到[使用Screens内容提供程序](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html#screens-content-provider)以了解更多详细信息。
