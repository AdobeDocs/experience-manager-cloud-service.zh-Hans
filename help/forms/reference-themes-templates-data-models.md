---
title: 如何获取AEM表单的参考主题和模板？
description: AEM Forms提供了示例自适应表单主题、模板和表单数据模型，以帮助您快速创建表单。
exl-id: 81588759-22da-4123-92fe-5ca97e97f1e4
source-git-commit: 046ffed13569ca3f9c104fb4525d28361873277a
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 23%

---

# 参考主题、模板和表单数据模型 {#reference-themes-templates-and-data-models}


| 应用到 | 文章链接 |
| -------- | ---------------------------- |
| 基于核心组件的自适应表单 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) |
| 基于Foundation组件的自适应表单 | 本文 |

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/creating-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

AEM Formsas a Cloud Service提供了多个参考主题、模板和表单数据模型，可帮助您快速开始创建自适应Forms。 您可以下载 [来自软件分发门户的引用内容包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) 并使用 [包管理器](/help/implementing/developing/tools/package-manager.md) 安装 [参考内容包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) 在生产、开发或本地开发环境中，将这些参考资产引入您的环境。

参考内容包中包含的主题、模板和表单数据模型包括：


| 主题 | 模板 | 表单数据模型 |
---------|----------|---------
| Canvas 3.0 | 基本 | Microsoft Dynamics 365 |
| 宁静 | 空白 | Salesforce |
| 城镇 |   |  |
| 超海洋 |  |  |
| 贝里尔 |  |  |
| 医疗保健 |  |   |
| FSI |   |   |

## 参考主题 {#reference-themes}

[主题](/help/forms/themes.md) 让您能够在对CSS没有深入了解的情况下为表单设置样式。 通过安装 [参考内容包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip)：

* 贝里尔
* Canvas 3.0
* 宁静
* 城镇
* 超海洋
* 医疗保健
* FSI（金融服务和保险）

每个主题都包含独特而优雅的样式，可用于为用户创建令人愉悦的自适应表单。 它包含面板、文本框、数字框、单选按钮、表格和开关等选择器的独特样式。 这些主题中的样式是根据需求而定的。 例如，在特定场景中，您需要使用简洁字体的最小主题。 自由主题可让您获得这样的外观。

![参考主题](assets/ref-themes.png)

此包中包含的主题是响应式的，这些主题中的样式是为移动和桌面显示定义的。 各种设备上的大多数现代浏览器都可以轻松渲染应用了这些主题之一的表单。

有关安装软件包的更多信息，请参阅 [如何使用包](/help/implementing/developing/tools/package-manager.md).

## 贝里尔 {#beryl}

Beryl主题强调使用背景图像、透明度和大平面图标。 在下面的屏幕截图中，您可以看到贝里尔主题的外观，以及它如何增强表单的样式。

![柏瑞尔主题](assets/beryl.png)

## Canvas 3.0 {#canvas}

Canvas 3.0是自适应Forms的默认主题，它强调使用基本颜色、透明度和平面图标。 在下面的屏幕截图中，您可以看到画布3.0主题的外观。

![柏瑞尔主题](assets/canvas.png)


## 宁静 {#tranquil}

宁静主题提供宁静颜色方案的浅色和深色，以突出显示表单的不同组件。 例如，单选按钮、面板和选项卡具有不同的绿色阴影。

![宁静的主题](assets/tranquil.png)


## 城镇 {#urbane}

都市化主题强调您的外表应具有极简和功能性的风格。 将Urbane主题应用于表单时，您可以看到组件是平面的。 这些面板具有细的外框，可创建现代外观。

![城市主题](assets/urbane.png)


## 超海洋 {#ultramarine}

Ultraminary主题使用深蓝色阴影突出显示选项卡、面板、文本框和按钮等组件。

![超海洋主题](assets/ultramarine.png)

## 医疗保健 {#healthcare}

医疗保健主题使用深绿色阴影突出显示选项卡、面板、文本框和按钮等组件。

![FSI主题](assets/healthcare.png)


## FSI（金融服务和保险）

FSI主题强调您的表单的极简和功能外观。 将FSI主题应用于表单时，可以看到面板组件为黄色。

![FSI主题](assets/fsi.png)

## 参考模板 {#reference-templates}


[模板](/help/forms/themes.md) 允许您为表单定义初始表单结构、内容和操作。 通过安装 [参考内容包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip)：

* 基本
* 空白

基本模板可帮助您快速创建注册表单。 您还可以使用它来预览自适应Forms基础组件的功能。 它提供了用于逐部分呈现数据的向导版面。使用空白模板在空白画布上开始创建自适应表单。


## 参考表单数据模型 {#reference-models}

然后，自适应Forms可以与Microsoft Dynamics 365和Salesforce服务器交互以启用业务工作流。 例如：

* 将数据写入Microsoft Dynamics 365和Salesforce on Adaptive Form提交。
* 通过表单数据模型中定义的自定义实体在Microsoft Dynamics 365和Salesforce中写入数据，反之亦然。
* 查询Microsoft Dynamics 365和Salesforce服务器以获取数据并预填充自适应Forms。
* 从Microsoft Dynamics 365和Salesforce服务器读取数据。

您可以通过安装[参考内容包](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip)来获取以下表单数据模型：

* Microsoft® Dynamics 365
* Salesforce

有关使用这些模型的信息，请参阅 [配置Microsoft Dynamics 365和Salesforce云服务](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=en#configure-dynamics-cloud-service)


## 另请参阅 {#see-also}

{{see-also}}