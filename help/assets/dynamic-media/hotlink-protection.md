---
title: 在 Dynamic Media 中激活热链接保护
description: 了解如何在Dynamic Media中激活热链接保护。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: b37ff72dbcf85e5558eb3421b5168dc48e063b47
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 9%

---

# 在 Dynamic Media 中激活热链接保护 {#activating-hotlink-protection-in-dynamic-media}

热链接是指第三方网站使用HTML代码显示您网站中的图像的情况。 每次请求图片时，他们都会使用您的带宽，因为访客的浏览器会直接从您的服务器访问图片。 热链接 *保护* 是一种阻止其他网站直接链接到您网页上的图片、CSS或JavaScript的方法。 这种屏蔽有助于减少Dynamic Media帐户下不必要的带宽使用。

[Adobe客户支持](https://experienceleague.adobe.com/?support-solution=Experience+Manager#home) 可以在CDN级别配置反向链接过滤器。 这样做可以确保Dynamic Media内容仅提供给域中允许网站列表中的网站。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager Dynamic Media捆绑在一起的现成CDN。 此功能不支持任何其他自定义CDN。 要激活热链接保护，管理员必须创建支持工单以请求对您的Dynamic Media帐户进行配置更改。 激活热链接保护无需额外付费。
