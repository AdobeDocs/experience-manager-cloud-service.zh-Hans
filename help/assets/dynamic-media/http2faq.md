---
title: HTTP2 内容交付常见问题解答
description: 了解HTTP2内容交付。
role: Admin,User
exl-id: 0a8a5fd8-a341-4e7f-84a5-409e2de97efe
source-git-commit: 49302452b9544b9414ec49ce2862d9913fbfc6a6
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# HTTP2 内容交付常见问题解答{#http-delivery-of-content-faq}

Adobe很兴奋地宣布推出HTTP/2内容交付。 使用HTTP/2时，整体性能会有所提高。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager - Dynamic Media捆绑在一起的现成内容交付网络。 此功能不支持任何其他自定义内容交付网络。

## 什么是HTTP/2? {#what-is-http}

HTTP/2改进了浏览器和服务器的通信方式，允许更快地传输信息，同时降低所需的处理能力。

网站文章[您必须了解的关于HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)的内容以简短而简单的方式介绍了HTTP/2及其好处。

## 迁移到HTTP/2进行内容交付有哪些主要优势？ {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

性能改进因各种因素而异。 例如，您网站的代码、使用Dynamic Media的方式、消费者的设备、屏幕和位置。

Adobe自己的测试产生了以下结果：

* 对于图像，响应时间缩短了7%-28%，具体取决于设备和浏览器。 性能提升最显着的是iOS设备。
* 对于查看器，加载时间性能提高了15%。

以下演示说明了HTTP/1加载与HTTP/2加载之间的区别：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否有资格切换到HTTP/2? {#am-i-eligible-to-switch-over-to-http}

要使用HTTP/2，您必须满足以下要求：

* 对富媒体请求使用安全HTTPS。
* 将Adobe捆绑的CDN（内容交付网络）用作Dynamic Media Classic许可证的一部分。
* 使用专用域（即`images.company.com`或`mycompany.scene7.com`），而不使用通用的Dynamic Media域（即`s7d1.scene7.com`、`s7d2.scene7.com`或`s7d13.scene7.com`）。

   要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   转到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**。 查找标有&#x200B;**Published Server Name**&#x200B;的字段。 如果您当前使用的是通用Dynamic Media域，则可以在此过渡中请求移至您自己的自定义域。

## 为我的Dynamic Media帐户启用HTTP/2的过程是什么？ {#what-is-the-process-for-enabling-http-for-my-dm-account}

[使用Admin Console创建支持案](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) 例，并请求切换到HTTP/2;它不会自动为您完成。

1. 在支持案例中提供以下信息：

   * 主要联系人姓名、电子邮件和电话号码。
   * 要过渡到HTTP2的所有域。 即`images.company.com`或`mycompany.scene7.com`。

   要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   转到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**。 查找标有&#x200B;**[!UICONTROL Published Server Name]**&#x200B;的字段。

   * 确认您对富媒体请求使用安全HTTPS。
   * 验证您是否通过Adobe使用CDN，以及是否通过直接关系进行管理。
   * 验证您使用的是专用域。 即`images.company.com`或`mycompany.scene7.com`，而不是通用的Dynamic Media域，如`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com`。

   要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的帐户。

   转到&#x200B;**[!UICONTROL 设置]** > **[!UICONTROL 应用程序设置]** > **[!UICONTROL 常规设置]**。 查找标有&#x200B;**[!UICONTROL Published Server Name]**&#x200B;的字段。 如果您当前使用的是通用Dynamic Media域，则可以在此过渡中请求移至您自己的自定义域。

   1. 客户支持将您根据请求提交的顺序添加到HTTP/2客户等待列表。
   1. 当Adobe准备好处理您的请求时，客户支持团队会联系您以协调过渡并设置目标日期。
   1. 完成后，系统会通知您，并可以验证是否成功过渡到HTTP2。



## 我何时可以转换到HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

请求的处理顺序是客户支持部门接收请求的顺序。

>[!NOTE]
>
>提前时间较长，因为过渡到HTTP/2涉及清除缓存。 因此，一次只能处理少数客户过渡。

## 迁移到HTTP/2有哪些风险？ {#what-are-the-risks-with-moving-to-http}

过渡到HTTP/2会清除CDN中的缓存，因为它涉及到迁移到新的CDN配置。

非缓存内容会直接点击Adobe的源服务器，直到再次重建缓存为止。 由于采取了这项措施，Adobe计划一次处理一些客户过渡。 此方法可确保在从源中提取请求时保持可接受的性能。

## 如何验证URL或网站是否已通过HTTP/2激活？ {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

下载要与Web浏览器一起使用的扩展。 对于Firefox和Chrome，有一个名为&#x200B;**[!UICONTROL HTTP/2和SPDY Indicator]**&#x200B;的扩展。 浏览器仅安全支持HTTP/2，因此需要通过HTTPS调用URL进行验证。 如果支持HTTP/2，则扩展将以蓝色Flash符号和标题“X-Firefox-Spdy”的形式指示：&quot;h2&quot;。
