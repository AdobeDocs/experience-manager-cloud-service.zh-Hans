---
title: 在 Dynamic Media 中激活热链接保护
description: 了解如何在Dynamic Media中激活热链接保护。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 0198b3a3-173e-46ca-a845-3f58f8eab769
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 6%

---

# 在 Dynamic Media 中激活热链接保护 {#activating-hotlink-protection-in-dynamic-media}

热链接是指第三方网站使用HTML代码显示您网站中的图像的情况。 每次请求图片时，他们都会使用您的带宽，因为访客的浏览器会直接从您的服务器访问图片。 热链接&#x200B;*保护*&#x200B;是一种方法，可阻止其他网站直接链接到您网页上的图片、CSS或JavaScript。 这种屏蔽有助于减少Dynamic Media帐户下不必要的带宽使用量。

[Adobe客户支持](https://experienceleague.adobe.com/?support-solution=Experience+Manager#home)可以在CDN级别配置反向链接筛选器。 这样做可确保仅将Dynamic Media内容提供给域中允许网站列表中的网站。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager Dynamic Media捆绑在一起的现成CDN。 此功能不支持任何其他自定义CDN。 要激活热链接保护，管理员必须创建支持票证以请求对您的Dynamic Media帐户进行配置更改。 激活热链接保护不需要额外付费。
