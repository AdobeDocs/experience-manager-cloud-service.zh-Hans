---
title: HTML5表单简介
description: HTML5 forms是Adobe Experience Manager 6.0 (AEM 6.0)软件中的一项新功能，可渲染HTML5格式的XFA表单模板。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 0facca18-ffa1-420c-859a-6f1f2c449d71
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# HTML5表单简介{#introduction-to-html-forms}

<span class="preview"> HTML5 Forms功能作为提前访问计划的一部分提供。 要请求访问，请将您的官方（工作）电子邮件ID通过电子邮件发送到aem-forms-ea@adobe.com。
</span>

HTML5 forms是Adobe Experience Manager 6.0 (AEM 6.0)软件中的一项新功能，可渲染HTML5格式的XFA表单模板。 凭借此功能，可以在那些不支持基于XFA的PDF的移动设备和桌面浏览器上渲染表单。 HTML5 forms不仅支持XFA表单模板的现有功能，还增加了适用于移动设备的新功能，如涂写签名。

HTML5 forms基于标准HTML5构造生成文档。 您可以在支持HTML5的所有新式浏览器中查看HTML5表单。 它不需要为浏览器安装任何其他浏览器插件。 有关支持的浏览器的详细信息，请参阅[支持的客户端平台](https://adobe.com/go/learn_aemforms_supportedplatforms_63)。

![HTML5表单预览](assets/mobile_form_on_an_ipad_date_14.png)

## HTML5 Forms的关键功能 {#key-capabilities-of-html-forms-br}

* 在所有兼容的浏览器上支持HTML5中呈现现有的XFA表单。
* 利用标准XFA表单设计功能来针对移动设备定位表单。
* 在HTML5格式中使用动态XFA功能。
* 使用高度准确的SVG文本布局(SVG 1.1)以匹配PDF文本布局。
* 支持JavaScript和FormCalc。
* 根据数据驱动事件或用户输入，动态地将片段组合到交互式表单中。
* 支持自定义CSS，以根据您的企业标准匹配表单的外观。
* 支持自定义构件，以提供丰富的数据捕获体验。
* 提供与Web应用程序集成的支持。

### 多渠道发布 {#multichannel-publishing}

表单开发人员可以使用XFA模板渲染PDF和HTML5格式的表单。 当您具有大量XFA表单集，并且需要最少的更改来适应HTML5表单设计实践时，此功能非常有用。 您可以将现有XFA表单渲染到HTML5，以定位尚未支持基于XFA的PDF的各种设备。

## 管理HTML5表单 {#manage-html-forms}

AEM还为使用AEM Forms UI列出和管理所有表单模板提供了一个统一的视图。 您可以激活、取消激活、发布和预览表单。<!--For more information, see [Introduction to managing forms](../../forms/using/introduction-managing-forms.md).-->

### Forms自定义 {#forms-customization}

HTML5表单使用标准HTML5结构呈现表单模板。 这使得使用Web技术(主要是CSS和JavaScript)以HTML5格式自定义和扩展表单变得简单。 您可以轻松自定义现有构件的外观，创建自己的自定义构件，或在表单中使用自定义样式。 有关创建自定义构件和自定义现有构件的更多信息，请参阅[使用HTML5表单插入自定义构件](/help/forms/custom-widgets.md)。
