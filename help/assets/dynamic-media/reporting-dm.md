---
title: Dynamic Media中的报表
description: 了解如何为Dynamic Media交付失败的URL请求错误报告。
contentOwner: Rick Brough
feature: Asset Management
role: User
hide: true
hidefromtoc: true
exl-id: 2488f813-df15-4dbb-8747-f827ee5925e1
source-git-commit: aa7429d9ca9f67979303c0b85c9dbd5b8c74c05c
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# 为失败的Dynamic Media投放URL请求错误报告

您可以请求错误报告，以标识在交付时失败的Dynamic Media URL。 此报表是最多五天的数据汇总，并以CSV格式提供。 错误报告包含以下信息：

* 失败的Dynamic Media投放URL — 失败的URL是Dynamic Media生成的URL，无法在投放时生成任何内容。
* 反向链接URL — 从中调用失败投放URL的反向链接URL。
* 失败计数 — 导致失败的投放URL的加载次数。

当您请求错误报表时，AdobeDynamic Media团队会以CSV格式向您发送该报表。 申请从提出请求之日起算起，有效期为五天。

您可以每月为给定公司请求一次错误报告。

**为失败的Dynamic Media投放URL请求错误报告：**

1. [向reports-dynamic-media@adobe.com](mailto:reports-dynamic-media@adobe.com)发送一封电子邮件，其中包含与您的Dynamic Media帐户关联的公司名称。

   如果您不知道公司名称，请在&#x200B;**[!UICONTROL Dynamic Media]** > **[!UICONTROL Cloud Service]** > **[!UICONTROL 工具]** > **[!UICONTROL Dynamic Media配置]**&#x200B;中查看[Adobe Experience Manager配置](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html?lang=zh-Hans#configuring-dynamic-media-cloud-services)页面。 在“Dynamic Media配置浏览器”页面上，单击&#x200B;**[!UICONTROL 全局]**，选中&#x200B;*[Dynamic_Media_folder_icon]*&#x200B;复选框，然后选择&#x200B;**[!UICONTROL 编辑]**。 您必须在AEM中拥有管理员权限才能访问Dynamic Media配置页面。

   ![访问Dynamic Media配置页面。](/help/assets/dynamic-media/assets/reporting-accessdmconfig.png)
