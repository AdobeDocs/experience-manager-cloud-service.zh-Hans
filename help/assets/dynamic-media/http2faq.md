---
title: HTTP2 内容交付常见问题解答
description: 了解HTTP2内容投放。
translation-type: tm+mt
source-git-commit: d9673296208831e68c5f776e0a9b142f348efc95
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 3%

---


# HTTP2 内容交付常见问题解答{#http-delivery-of-content-faq}

Adobe很高兴地宣布推出HTTP/2投放内容。 使用HTTP/2时，您会注意到整体性能有所提高。

## 什么是HTTP/2?{#what-is-http}

HTTP/2改进了浏览器和服务器的通信方式，允许更快地传输信息，同时降低所需的处理能力。

以下网站简要而简单地描述了HTTP/2及其优点：

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## 转向HTTP/2进行内容投放有哪些主要优势？{#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

性能改进因网站代码、Dynamic Media的使用方式、消费者设备、屏幕和位置等因素而异。

Adobe自己的测试得出以下结果：

* 对于图像，响应时间根据设备和浏览器而提高了7%-28%。 在iOS设备上，性能提高最显着。
* 对于查看器，加载时间性能提高了15%。

以下演示说明了HTTP/1与HTTP/2加载之间的区别：

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## 我是否有资格切换到HTTP/2?{#am-i-eligible-to-switch-over-to-http}

要使用HTTP/2，必须满足以下要求：

* 为您的富媒体请求使用安全HTTPS。
* 将Adobe捆绑的CDN(内容投放网络)作为Dynamic Media经典许可证的一部分。
* 使用专用域（即`images.company.com`或`mycompany.scene7.com`），而不使用通用的Dynamic Media域（即`s7d1.scene7.com`、`s7d2.scene7.com`或`s7d13.scene7.com`）。

   要查找您的域，请[登录每个公司帐户的Dynamic Media经典](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)实例。

   单击&#x200B;**[!UICONTROL 设置 > 应用程序设置 > 常规设置]**。查找标有&#x200B;**发布服务器名称**&#x200B;的字段。 如果您当前使用的是通用的Dynamic Media域，则可以请求移至您自己的自定义域作为此过渡的一部分。

## 为我的Dynamic Media帐户启用HTTP/2的过程是什么？{#what-is-the-process-for-enabling-http-for-my-dm-account}

必须[使用Admin Console创建支持案例](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)并请求切换到HTTP/2;它不会自动为您完成。

1. 在您的支持案例中提供以下信息：

   * 主要联系人姓名、电子邮件和电话号码。
   * 要过渡到HTTP2的所有域。 即`images.company.com`或`mycompany.scene7.com`。

   要查找您的域，请[登录每个公司帐户的Dynamic Media经典](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)实例。

   单击&#x200B;**[!UICONTROL 设置 > 应用程序设置 > 常规设置]**。查找标有&#x200B;**[!UICONTROL 发布服务器名称]**&#x200B;的字段。

   * 验证是否对多媒体请求使用安全HTTPS。
   * 验证您是否通过Adobe使用CDN，而不是通过直接关系进行管理。
   * 验证您使用的是专用域。 即`images.company.com`或`mycompany.scene7.com`，不是通用的Dynamic Media域，如`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com`。

   要查找您的域，请[登录每个公司帐户的Dynamic Media经典](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)实例。

   单击&#x200B;**[!UICONTROL 设置 > 应用程序设置 > 常规设置]**。查找标有&#x200B;**[!UICONTROL 发布服务器名称]**&#x200B;的字段。 如果您当前使用的是通用的Dynamic Media域，则可以请求移至您自己的自定义域作为此过渡的一部分。

   1. 技术支持根据请求的提交顺序将您添加到HTTP/2客户等候名单。
   1. 当Adobe准备好处理您的请求时，支持部门将与您联系以协调过渡并设置目标日期。
   1. 完成后将通知您，并可验证是否成功过渡到HTTP2。



## 我何时可以过渡到HTTP/2?{#when-can-i-expect-to-be-transitioned-over-to-http}

请求的处理顺序由技术支持部门接收。

>[!NOTE]
>
>由于HTTP/2的过渡涉及清除缓存，因此可能会有很长的提前期。 因此，一次只能处理少数客户过渡。

## 转向HTTP/2有哪些风险？{#what-are-the-risks-with-moving-to-http}

HTTP/2过渡将清除CDN中的缓存，因为它涉及到移到新的CDN配置。

未缓存的内容会直接点击Adobe的来源服务器，直到重新构建缓存。 因此，Adobe计划一次处理几个客户过渡，以便在从来源处理请求时保持可接受的性能。

## 如何验证URL或网站是否已通过HTTP/2激活？{#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

您需要下载外部才能与Web浏览器一起使用。 对于Firefox和Chrome，有一个名为&#x200B;**[!UICONTROL HTTP/2和SPDY Indicator]**&#x200B;的扩展。 浏览器仅安全地支持HTTP/2，因此有必要使用HTTPS调用URL进行验证。 如果支持HTTP/2，则此扩展以蓝色Flash符号和标题“X-Firefox-Spdy”表示：“h2”。
