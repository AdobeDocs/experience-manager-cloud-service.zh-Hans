---
title: 添加CDN配置
description: 了解如何为Edge Delivery站点或Cloud Manager环境添加CDN配置。
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: e57a6ceb2482e61acabe928da0f539d26989985c
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 8%

---


# 添加CDN配置 {#add-cdn}

必须完成添加CDN配置才能使用SSL配置域。

>
>
>对于由Adobe管理的CDN，在使用DV证书时，只允许使用ACME验证的站点。

**添加CDN配置：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登录 Cloud Manager 并选择适当的组织。

1. 单击&#x200B;**CDN配置**。

1. 在“CDN配置”页面的右上角附近，单击&#x200B;**添加**。

   ![配置CDN对话框](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

1. 在&#x200B;**配置CDN**&#x200B;对话框中，提供必要的信息。

   * 从&#x200B;**Origin**&#x200B;下拉列表中，执行以下操作之一：
      * **站点：**&#x200B;选择Edge Delivery Services站点。
      * **环境：**&#x200B;选择Cloud Service环境。
         * **层：**&#x200B;为所选环境选择&#x200B;**Publish**&#x200B;或&#x200B;**预览** Web层。
   * 选择您的CDN类型： **托管CDN** Adobe或&#x200B;**其他CDN提供商**。
   * 选择域。
   * 选择SSL证书。 仅当选择&#x200B;**Adobe托管CDN**&#x200B;作为您的CDN类型时才需要。

1. 单击&#x200B;**保存**。




