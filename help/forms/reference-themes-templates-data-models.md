---
title: 参考主题、模板和表单数据模型
seo-title: Reference Themes, Templates, and Form Data models
description: AEM Forms提供自适应表单主题、模板和表单数据模型，您可以从Software Distribution获取这些主题、模板和表单数据模型
seo-description: AEM Forms provides adaptive forms themes, templates, and form data models that you can get from Software Distribution
source-git-commit: 196a2f221c637d58ea6642177f530f158888efe0
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# 参考主题、模板和表单数据模型 {#reference-themes-templates-and-data-models}

AEM Forms as a Cloud Service提供了多个参考主题、模板和表单数据模型，以帮助您快速开始创建自适应Forms。 您可以下载 [从software distribution门户中引用内容包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) 并使用 [包管理器](/help/implementing/developing/tools/package-manager.md) 安装 [引用内容包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) 在生产、开发或本地开发环境中获取这些参考资产。

参考内容包中包含的主题、模板和表单数据模型包括：


| 主题 | 模板 | 表单数据模型 |
---------|----------|---------
| 画布3.0 | 基本 | Microsoft Dynamics 365 |
| 宁静 | 空白 | Salesforce |
| 厄巴纳 |  |  |
| 超海洋 |  |  |
| 柏利 |  |  |
| 医疗保健 |  |  |
| FSI |  |  |

## 参考主题 {#reference-themes}

[主题](/help/forms/themes.md) 允许您在不深入了解CSS的情况下设置表单样式。 您可以通过安装 [引用内容包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* 柏利
* 画布3.0
* 宁静
* 厄巴纳
* 超海洋
* 医疗保健
* FSI（金融服务与保险）

每个主题都包含独特而优雅的风格，您可以使用这些风格为用户创建有趣的自适应表单。 它包含选择器的唯一样式，例如面板、文本框、数字框、单选按钮、表和开关。 这些主题中的样式是基于要求的。 例如，在特定情景中，您需要具有简洁字体的极简主义主题。 自由主题让你能够达到这种效果。

![参考主题](assets/ref-themes.png)

此包中包含的主题是响应式的，并且为移动设备和桌面显示屏定义了这些主题中的样式。 各种设备上的大多数现代浏览器都可以轻松渲染使用其中一个主题应用的表单。

有关安装包的更多信息，请参阅 [如何使用包](/help/implementing/developing/tools/package-manager.md).

## 柏利 {#beryl}

Beryl主题强调背景图像、透明度和大型平面图标的使用。 在下面的屏幕截图中，您可以看到Beryl主题的外观，以及它如何增强表单的样式。

![柏力主题](assets/beryl.png)

## 画布3.0 {#canvas}

Canvas 3.0是自适应Forms的默认主题，强调使用基本颜色、透明度和平面图标。 在下面的屏幕截图中，您可以看到Canvas 3.0主题的外观。

![柏力主题](assets/canvas.png)


## 宁静 {#tranquil}

宁静的主题提供宁静色彩方案的浅色和深色色调，以突出表单的不同组成部分。 例如，单选按钮、面板和选项卡的绿色阴影不同。

![宁静的主题](assets/tranquil.png)


## 厄巴纳 {#urbane}

都市主题强调您的形式极简而实用。 将城市主题应用于表单时，您可以看到组件是平的。 这些面板具有细轮廓以创造现代外观。

![城市主题](assets/urbane.png)


## 超海洋 {#ultramarine}

Ultramarine主题使用深蓝色阴影来突出显示组件，如选项卡、面板、文本框和按钮。

![超海洋主题](assets/ultramarine.png)

## 医疗保健 {#healthcare}

医疗保健主题使用深绿色阴影来突出显示组件，如选项卡、面板、文本框和按钮。

![FSI主题](assets/healthcare.png)


## FSI（金融服务与保险）

FSI主题强调您表单的极简主义和功能性外观。 将FSI主题应用于表单时，您可以看到面板组件为黄色。

![FSI主题](assets/fsi.png)

## 参考模板 {#reference-templates}


[模板](/help/forms/themes.md) 允许您为表单定义初始表单结构、内容和操作。 您可以通过安装 [引用内容包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* 基本
* 空白

基本模板可帮助您快速创建注册表单。 您还可以使用它来预览自适应Forms基础组件的功能。 它为逐段呈现数据提供了向导布局。 使用空白模板在空白画布上开始创建自适应表单。


## 引用表单数据模型 {#reference-models}

随后，自适应Forms可以与Microsoft Dynamics 365和Salesforce服务器进行交互，以启用业务工作流。 例如：

* 在自适应表单提交时，将数据写入Microsoft Dynamics 365和Salesforce。
* 通过在表单数据模型中定义的自定义实体在Microsoft Dynamics 365和Salesforce中写入数据，反之亦然。
* 查询Microsoft Dynamics 365和Salesforce服务器以获取数据并预填充自适应Forms。
* 从Microsoft Dynamics 365和Salesforce服务器中读取数据。

您可以通过安装 [引用内容包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip):

* Microsoft® Dynamics 365
* Salesforce

有关使用这些模型的信息，请参阅 [配置Microsoft Dynamics 365和Salesforce云服务](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=en#configure-dynamics-cloud-service)






