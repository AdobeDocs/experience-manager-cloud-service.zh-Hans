---
title: 智能成像
description: “了解智能图像处理如何应用每个用户的独特查看特性，自动提供为其体验优化的正确图像，从而提高性能和参与度。”
feature: 资产管理，演绎版
topic: 商务从业人员
role: Business Practitioner
exl-id: 863784d9-0c91-4deb-8edd-1354a21581c3
translation-type: tm+mt
source-git-commit: e1ca8c3a26fae6e421a087ade03cfeddc7a94a0e
workflow-type: tm+mt
source-wordcount: '1926'
ht-degree: 2%

---

# 智能成像 {#smart-imaging}

## 什么是“智能成像”？{#what-is-smart-imaging}

Smart Imaging技术应用Adobe Sensei AI功能并与现有“图像预设”配合使用。 它根据客户端浏览器功能自动优化图像格式、大小和质量，从而增强图像投放性能。

>[!NOTE]
>
>此功能要求您使用与Adobe Experience Manager Dynamic Media捆绑的现成CDN(内容投放网络)。 此功能不支持任何其他自定义CDN。

Smart Imaging还得益于与Adobe一流的高级CDN(内容投放网络)服务完全集成所带来的性能提升。 此服务可找到服务器、网络和对点之间的最佳Internet路由。 它找到的路由具有最低的延迟和最低的数据包丢失率，而不是使用Internet上的默认路由。

以下图像资产示例描述了添加的智能成像优化：

| 图像<br>(URL) | 缩略图 | 大小<br>(JPEG) | 大小(WebP)<br>（使用智能成像） | 减少 |
|---|---|---|---|---|
| [图1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [图2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [图3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [图4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | 平均= 51% |

与上述内容类似，Adobe还对来自实时客户站点的7009个URL运行测试。 他们平均可以进一步优化JPEG文件大小38%。 对于采用WebP格式的PNG，他们平均可以进一步优化31%的文件大小。 这种优化是可能的，因为智能成像的能力。

## 最新的Smart Imaging有哪些主要优势？{#what-are-the-key-benefits-of-smart-imaging}

图像构成页面的大部分加载时间。 因此，任何性能改进都会对更高的转化率、网站逗留时间和更低的网站跳出率产生深远影响。

最新版Smart Imaging中的增强功能：

* 利用最新的Smart Imaging改进了网页的Google SEO排名。
* 立即提供优化内容（在运行时）。
* 使用Adobe Sensei技术根据图像请求中指定的质量(qlt)进行转换。
* 可以使用“bfc”URL参数关闭智能成像。
* TTL（生存时间）独立。 以前，“智能成像”必须至少使用12小时的TTL才能正常工作。
* 以前，原始图像和派生图像都被缓存，使缓存失效是一个两步过程。 在最新的智能成像中，只缓存衍生项，从而允许单步缓存失效过程。
* 使用其规则集中自定义标题的客户。 例如，[向图像响应添加自定义标头值|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html)中建议的“允许来源计时”、“X-Robot”可从最新的智能成像中受益。 这些标头不会被阻止，这与以前版本的智能成像不同。

## 是否存在与智能成像相关的许可成本？{#are-there-any-licensing-costs-associated-with-smart-imaging}

否. 您的现有许可证包含Smart Imaging。 此规则适用于Dynamic Media Classic或Experience Manager Dynamic Media(On-prem、AMS和Experience Manager作为Cloud Service)。

>[!NOTE]
>
>Smart Imaging不适用于Dynamic Media — 混合型客户。

## 智能图像处理是如何工作的？{#how-does-smart-imaging-work}

当消费者请求图像时，Smart Imaging会检查用户特征，并根据使用中的浏览器转换为适当的图像格式。 以不会降低视觉保真度的方式执行这些格式转换。 智能成像功能会按以下方式根据浏览器功能自动将图像转换为不同格式。

<!--   * Safari 14.0 +
    * Safari 14 only with iOS 14.0 and above and macOS BigSur and above -->

* 自动转换为以下浏览器的WebP:
   * 铬黄
   * Firefox
   * Microsoft® Edge
   * Safari（跨iOS、macOS、iPadOS），提供了浏览器和操作系统版本支持WebP
   * Android™
   * Opera
* 对以下内容的传统浏览器支持：

   | 浏览器 | 浏览器/操作系统版本 | 格式 |
   | --- | --- | --- |
   | Safari | 早于iOS/iPad 14.0或macOS BigSur | JPEG2000 |
   | Edge | 早于18 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* 对于不支持这些格式的浏览器，将提供最初请求的图像格式。

如果原始图像大小小于智能成像生成的图像大小，则会提供原始图像。

## 支持哪些图像格式？{#what-image-formats-are-supported}

Smart Imaging支持以下图像格式：

* JPEG
* PNG

<!-- For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## 智能成像如何处理您现有的已使用图像预设？{#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

Smart Imaging可与您现有的“图像预设”配合使用。 如果请求的文件格式为JPEG或PNG，它将观察除质量(`qlt`)和格式(`fmt`)外的所有图像设置。 对于格式转换，“智能成像”可保持图像预设设置所定义的完全视觉保真度，但文件大小较小。 如果原始图像大小小于智能成像生成的图像大小，则会提供原始图像。

<!-- In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## 我是否必须更改任何URL、图像预设，或在我的网站上部署任何用于智能成像的新代码？{#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

如果您在现有自定义域上配置Smart Imaging，Smart Imaging可无缝地与您的现有图像URL和图像预设配合使用。 此外，智能成像不要求您在网站上添加任何代码以检测用户的浏览器。 它都是自动处理的。

如果必须配置新的自定义域才能使用智能成像，则必须更新URL以反映此自定义域。

要了解智能成像的先决条件，请参阅[我是否有资格使用智能成像？](#am-i-eligible-to-use-smart-imaging)

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## Smart Imaging是否可以与HTTPS一起使用？ HTTP/2如何？{#does-smart-imaging-working-with-https-how-about-http}

Smart Imaging可处理通过HTTP或HTTPS传送的图像。 此外，它还适用于HTTP/2。

## 我是否有资格使用智能成像？{#am-i-eligible-to-use-smart-imaging}

要使用智能成像，您公司的Dynamic Media Classic或Experience Manager帐户上的Dynamic Media必须满足以下要求：

* 将Adobe捆绑的CDN(内容投放网络)作为许可的一部分。
* 使用专用域（例如`images.company.com`或`mycompany.scene7.com`），而不使用通用域（例如`s7d1.scene7.com`、`s7d2.scene7.com`或`s7d13.scene7.com`）。

要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

点按&#x200B;**[!UICONTROL 设置>应用程序设置>常规设置]**。 查找标有&#x200B;**[!UICONTROL 发布服务器名称]**&#x200B;的字段。 如果您当前使用的是通用域，则可以请求移至您自己的自定义域。 在您提交技术支持票证时发出此过渡请求。

您的第一个自定义域无需支付Dynamic Media许可证的额外费用。

## 为我的帐户启用智能成像的过程是什么？{#what-is-the-process-for-enabling-smart-imaging-for-my-account}

请求使用智能成像；它不会自动启用。

1. [使用Admin Console创建支持案例。](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)
1. 在您的支持案例中提供以下信息：

   1. 主要联系人姓名、电子邮件、电话。
   1. 要启用智能成像的所有域（即`images.company.com`或`mycompany.scene7.com`）。

      要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

      单击&#x200B;**[!UICONTROL 设置 > 应用程序设置 > 常规设置]**。

      查找标有&#x200B;**[!UICONTROL 发布服务器名称]**&#x200B;的字段。
   1. 验证您是否通过Adobe使用CDN，而不是通过直接关系进行管理。
   1. 验证您使用的是专用域（如`images.company.com`或`mycompany.scene7.com`），而不是通用域（如`s7d1.scene7.com`、`s7d2.scene7.com`、`s7d13.scene7.com`）。

      要查找您的域，请打开[Dynamic Media Classic桌面应用程序](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started)，然后登录到您的公司帐户或帐户。

      单击&#x200B;**[!UICONTROL 设置 > 应用程序设置 > 常规设置]**。

      查找标有&#x200B;**[!UICONTROL 发布服务器名称]**&#x200B;的字段。 如果您当前使用的是通用Dynamic Media经典域，则可以请求移至您自己的自定义域作为此过渡的一部分。
   1. 指示是否希望它通过HTTP/2使用。

1. Adobe客户关怀根据请求的提交顺序将您添加到智能图像处理客户等待列表。
1. 当Adobe准备好处理您的请求时，客户关怀部门会联系您以协调和设置目标日期。
1. **可选**:在Adobe将新功能推向生产之前，您可以选择在暂存中测试智能成像。
1. 完成后，客户服务将通知您。
1. 为最大限度地提高智能成像的性能，Adobe建议将“生存时间(TTL)”设置为24小时或更长。 TTL定义CDN缓存资源的时间。 要更改此设置：

   1. 如果您使用Dynamic Media Classic，请单击&#x200B;**[!UICONTROL 设置>应用程序设置>发布设置>图像服务器]**。 将“**[!UICONTROL 默认客户端缓存时间”值设置为“Live]**”值24或更长。
   1. 如果使用Dynamic Media，请按照[这些说明](config-dm.md)操作。 将&#x200B;**[!UICONTROL Expiration]**&#x200B;值设置为24小时或更长。

## 我预计我的帐户何时启用智能成像？{#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

请求将按照客户关怀部门接收请求的顺序进行处理，这取决于等待列表。

>[!NOTE]
>
>可能会有很长的提前期，因为启用智能成像涉及Adobe清除缓存。 因此，在任何给定时间只能处理少数客户过渡。

## 改用Smart Imaging有哪些风险？{#what-are-the-risks-with-switching-over-to-use-smart-imaging}

客户网页不存在风险。 但是，智能成像的过渡确实会清除您的CDN缓存。 此操作涉及在Experience Manager上切换到Dynamic Media Classic或Dynamic Media的新配置。

在初始过渡期间，非缓存图像直接点击Adobe的来源服务器，直到再次重建缓存。 因此，Adobe计划一次处理几个客户过渡，以便在从来源中提出请求时保持可接受的性能。 对于大多数客户而言，在CDN中在1-2天内重新完全建立缓存。

## 如何验证智能成像是否按预期工作？{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. 在您的帐户配置了智能图像后，请在浏览器上加载Dynamic Media Classic或Adobe Experience Manager - Dynamic Media图像URL。
1. 在浏览器中单击&#x200B;**[!UICONTROL “视图”>“开发人员”>“开发人员工具”]**，打开Chrome开发人员窗格。 或者，选择您选择的任何浏览器开发者工具。

1. 确保在开发人员工具打开时禁用缓存。

   * 在Windows®上，导航到开发人员工具窗格中的设置，然后选中&#x200B;**[!UICONTROL 禁用缓存（当devtools打开时）]**&#x200B;复选框。
   * 在macOS上，在开发人员窗格的&#x200B;**[!UICONTROL Network]**&#x200B;选项卡下，选择&#x200B;**[!UICONTROL 禁用缓存]**。

1. 观察内容类型将转换为适当的格式。 以下屏幕截图显示了在Chrome上将动态转换为WebP的PNG图像。
1. 在不同的浏览器和用户条件上重复此测试。

>[!NOTE]
>
>并非所有图像都已转换。 Smart Imaging决定转换能否提高性能。 有时，如果没有预期的性能增益，或者格式不是JPEG或PNG，则不会转换图像。

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## 是否可以关闭任何请求的智能映像？{#turning-off-smart-imaging}

是. 可以通过向URL添加修饰符`bfc=off`来关闭智能成像。

## 提供哪些“调整”？ 是否可以定义任何设置或行为？ (#tuning-settings)

当前，您可以选择启用或禁用智能成像。 没有其他调整可用。

## 如果“智能成像”管理质量设置，我是否可以设置最小值和最大值？ 例如，是否可以设置“不低于60”和“不大于80品质”？ (#minimum-maximum)

当前智能映像中没有此类设置功能。

## 有时，JPEG图像会返回到Chrome而不是WebP图像。 为什么会发生这种变化？ (#jpeg-webp)

“智能成像”可确定转换是否有益。 仅当转换导致文件大小更小且质量相当时，才会返回新图像。
