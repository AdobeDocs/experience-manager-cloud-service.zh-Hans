---
title: HTML5表单的最佳实践
description: 优化基于XFA的HTML5 Forms以获得最佳性能。
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
content-type: reference
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 62ff6306-9989-43b0-abaf-b0a811f0a6a4
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '1386'
ht-degree: 0%

---

# HTML5表单的最佳实践{#best-practices-for-html-forms}

<span class="preview"> HTML5 Forms功能作为提前访问计划的一部分提供。 要请求访问，请将您的官方（工作）电子邮件ID通过电子邮件发送到aem-forms-ea@adobe.com。
</span>

## 概述 {#overview}

AEM Forms具有一个名为HTML5 forms的组件。 它有助于以HTML5格式呈现现有的基于XFA的PDF forms （XDP文件）。 本文档提供了减少加载时间并提高HTML5表单在移动设备上的性能的指导和建议。

大多数移动设备的处理能力和内存功能有限。 它有助于提高移动设备的待机时间。 在移动设备上运行的Web浏览器可以访问有限的资源（有限的内存和处理能力）。 达到限制后，浏览器行为将变得缓慢。 本文档提供了保持HTML5表单大小可控的建议。 较小的形式不会破坏设备的内存和处理能力限制，并提供流畅的体验。

虽然本文中讨论的建议面向HTML5表单，但这些建议同样适用于基于XFA的PDF forms。 这些最佳实践共同为HTML5表单的整体性能做出贡献。 它需要认真规划，以发展高效和富有成效的形式。 让我们开始吧：

## 节点是HTML5表单的货币，明智地使用它们 {#nodes-are-currency-of-html-forms-spend-them-wisely}

通常，XFA表单有多个元素。 例如，表格、文本字段和图像。 每个元素都有几个属性来控制元素的行为和外观。 以HTML5格式呈现XFA表单时，所有XFA元素和相应的属性都会转换为模型或HTML DOM节点。 这些节点会增加DOM的大小和复杂性。 降低HTML5表单的呈现速度。

浏览器渲染更精简的DOM会更容易。 因此，您可以对XFA表单执行以下优化来减少节点数。 因此，生成精简DOM结构：

* 使用caption属性向字段添加标签。 不要使用单独的文本元素添加标签。 这有助于减轻重量，提高性能。 它还有助于避免布局问题。
* 将表单上Draw文本元素的数目保持为最小值。 绘制元素有助于提高可读性和外观，但没有任何信息存储功能。 建议将多个Draw文本元素合并为一个Draw文本元素。 不要翻开石头，让表单更精简。

## Lite表单的性能更好，可保持资源得到压缩 {#lite-forms-perform-better-keep-the-resources-compressed}

HTML5表单可包含多个外部资源，如图像、JavaScript和CSS文件。 每次浏览器请求表单时，都会通过网络发送外部资源。 通过网络传输所需的时间与文件大小成正比。

因此，减小外部资源的规模并仅使用绝对需要的资源是提高表单性能的首选方法。 您可以对XFA表单执行以下优化，以减小表单的外部资源大小：

* 使用[压缩图像](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)。 它减少了呈现表单所需的网络活动和内存量。 因此，成形加载时间显着减少。
* 使用AEM Configuration Manager (Day CQ HTML Library Manager)中的“缩小”选项压缩JavaScript和CSS文件。 有关详细信息，请参阅[OSGi配置设置](/help/implementing/deploying/configuring-osgi.md)。
* 启用Web压缩。 它减小了源自表单的请求和响应的大小。 有关详细信息，请参阅[AEM Forms服务器的性能优化](https://helpx.adobe.com/cn/aem-forms/6-3/performance-tuning-aem-forms.html)。

## 保持兴趣状态，仅显示必填字段  {#keep-the-interest-alive-show-only-required-fields}

HTML5表单可能会占用数百页。 包含大量字段的表单在浏览器中加载缓慢。 您可以对XFA表单执行以下优化，以优化具有大量字段和页面的表单：

* 评估是否将大型表单拆分为多个表单。 您还可以使用表单集将所有较小的表单组合在一起，并将它们作为单个单元呈现。 表单集仅加载所需的表单。 此外，在表单集中，您可以配置不同表单中的常用字段以共享数据绑定。 数据绑定可帮助用户仅填写一次常用信息；这些信息会在后续表单中自动填写，从而显着提升性能。 有关表单集的更多详细信息，请参阅AEM表单中的[表单集](https://helpx.adobe.com/cn/aem-forms/6-3/formset-in-aem-forms.html)。
* 请考虑拆分截面并将每个截面移动到不同的页面。 HTML5 forms会在页面滚动请求时动态加载每个页面。 内存中只存储滚动的页面（正在显示的页面以及它之前的页面）；其余的页面将按需加载。 因此，在其自身的页面上拆分和移动区域可缩短加载表单所需的时间。 您还可以将表单的第一页用作登陆页面。 它类似于一本书的目录(TOC)。 表单的登陆页面仅包含指向表单其他部分的链接。 它显着缩短了表单第一页的加载时间，从而改善了用户体验。
* 默认情况下，将条件部分保持隐藏。 使这些部分仅在满足特定条件时可见。 它有助于将DOM的大小保持在最小。 也可使用选项卡式导航一次只显示一个截面。

## 越少越好，请减少页数 {#less-is-more-reduce-the-number-of-pages}

HTML5表单可包含数据驱动字段（表格和子表单）。 这些字段可在运行时扩展表单的大小。 例如，HTML5表单中的数据驱动表可以跨越数千行。 此类表可能会导致布局和性能下降。 下面建议的优化可以帮助您缩短使用数据驱动字段的HTML5表单的加载时间：

* 使用XFA脚本实现分页导航以显示数据驱动字段（表和子表单）。 在分页导航中，页面上仅显示特定数据。 它限制浏览器每次只对显示的字段进行绘画操作，并使表单更容易导航。 此外，移动设备上的用户只对数据的子集感兴趣。 它可帮助您提供卓越的用户体验，并减少加载所需数据所需的时间。 你得到两个解决方案，而价格只有一个。  另请注意，分页导航不可开箱即用。 您可以使用XFA脚本来开发分页导航。

* 评估将多个只读列合并到单个列的情况。 它减少了显示表单所需的内存。 此外，避免显示不需要用户输入任何内容的列。
* 如果上述建议没有产生很多改进，请评估将数据驱动表单拆分为[表单集](https://helpx.adobe.com/cn/aem-forms/6-3/formset-in-aem-forms.html)。 例如，如果表的行数超过1000，则每隔100行移至另一个表单。 这有助于改善表单的加载时间和性能。  另请注意，表单集为所有表单生成合并的提交XML。 要区分每个表单的数据，请使用不同的数据根。 有关详细信息，请参阅AEM Forms中的[表单集](https://helpx.adobe.com/cn/aem-forms/6-3/formset-in-aem-forms.html)。

## 记录文档(DOR)的二次幂 {#power-of-two-for-document-of-record-dor}

XFA表单可以具有大量专门用于记录文档(DOR)的节。 为了减少节点数并提高此类表单的性能，您可以维护表单的不同副本 — 一个副本用于填写表单，另一个副本用于在服务器上生成记录文档。 在要填写XFA表单的副本中显示仅捕获数据所需的字段。 在从生成记录文档XFA中，仅在表单的打印输出中保留必填字段。 在选择建议的方法之前，先评估性能增益和维护开销。

## 推荐阅读  {#recommended-reads}

Adobe Experience Manager (AEM)表单可帮助您将复杂的交易转换为简单、愉快的数字体验。 然而，它需要作出协调一致的努力，以发展高效率和富有成效的形式。 除了HTML5 Forms之外，下面是一些一般AEM最佳实践的推荐阅读：


<!--

* Best practices for Deploying and maintaining AEM
* Best practices for Authoring content
* [Best practices for Administering AEM](/help/sites-administering/administer-best-practices.md)
* [Best practices for Developing solutions](/help/sites-developing/best-practices.md)
* [Best practices for working with adaptive forms](/help/forms/using/adaptive-forms-best-practices.md)
* [AEM Forms server does not embed fonts to a Dynamic PDF form](https://helpx.adobe.com/aem-forms/kb/aem-forms-server-does-not-embed-fonts-to-dynamic-pdf-form.html)

-->

## 快速参考卡 {#quick-reference-card}

您可以打印以下卡（单击卡可下载高分辨率版本），并将其放在您的办公桌上以供快速参考：
[![HTML5 Forms最佳实践快速参考卡](assets/best-practices_reference_card.png)](assets/html5_forms_best_practices_reference_card.pdf)
