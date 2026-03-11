---
title: 在AEM Sites主题中嵌入自适应Forms主题
description: 了解如何将自适应Forms主题（例如，画布）集成到AEM Sites主题中，以便Sites页面和嵌入的自适应Forms共享一个统一的主题和部署。
keywords: 自适应表单主题，站点主题， AEM Sites主题，表单主题集成，前端管道，主题嵌入
feature: Adaptive Forms, Core Components
role: Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="适用于AEM Forms)。"
exl-id: 0607e11c-84d2-42cb-be9f-acd7c328a342
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 1%

---

# 在AEM Sites主题中嵌入自适应Forms主题

您可以将自适应Forms主题(如[AEM Forms画布主题](https://github.com/adobe/aem-forms-theme-canvas))嵌入到AEM Sites主题中。 这样，单个主题即可同时驱动您的站点页面和嵌入在这些页面上的任何自适应Forms，并通过[AEM前端管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html)生成一个内部版本和一个部署。

本文适用于维护或自定义标准（或自定义）AEM Sites主题，并且希望包含自适应表单样式而不管理单独的Forms主题部署的开发人员。

## 先决条件 {#prerequisites}

在开始之前，请确保您已：

* 为站点主题配置了前端管道&#x200B;**的** AEM as a Cloud Service[](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html)。
* **站点主题源** — 例如，[标准站点模板主题](https://github.com/adobe/aem-site-template-standard)（包含带有`theme/`、`src/theme.scss`等的`src/components/`的存储库）。
* **Forms主题源** - [AEM Forms画布主题](https://github.com/adobe/aem-forms-theme-canvas)&#x200B;(或其他兼容的自适应Forms主题)已克隆或下载到本地。
* **Node.js和npm** — 构建站点主题（有关支持的版本，请参阅主题自述文件）。
* **Maven** — 如果您生成完整的站点模板包（对于仅主题工作可选）。

## 第1步：创建自适应表单组件文件夹 {#step-1-create-folder}

在您的站点主题存储库中，创建将存放Forms主题的文件夹：

```text
theme/src/components/adaptiveform/
```

所有Forms主题资产将位于此文件夹下，因此它们与现有站点组件分开。

## 步骤2：复制Forms主题组件和图像 {#step-2-copy-components-and-images}

使用您的&#x200B;**Forms主题**（例如，`aem-forms-theme-canvas`）和&#x200B;**站点主题**&#x200B;路径：

1. **复制组件文件夹**\
   从Forms主题中，将`src/components/`的整个内容复制到站点主题中，如下所示：

   ```text
   theme/src/components/adaptiveform/
   ```

   所以你会得到这样的路径：

   ```text
   theme/src/components/adaptiveform/button/
   theme/src/components/adaptiveform/checkbox/
   theme/src/components/adaptiveform/container/
   … (one folder per component)
   ```

   ![添加自适应表单组件](/help/forms/assets/theme-add-adaptiveform-component.png)

2. **复制映像**\
   将Forms主题图像复制到站点主题中：

   ```text
   Forms theme:  src/resources/images/*
   Site theme:   theme/src/components/adaptiveform/resources/images/
   ```

   创建`theme/src/components/adaptiveform/resources/images/`（如果它不存在），然后复制所有图像资产（例如`question.svg`、`Chevron-Left.svg`、`busy-state.gif`等）。

   ![添加图像](/help/forms/assets/theme-add-images.png)

## 步骤3：复制变量和mixin {#step-3-copy-variables-and-mixins}

Forms主题在`src/site/`下使用共享变量和mixin。 仅将这两个文件复制到&#x200B;**的**&#x200B;根`adaptiveform/`（不在`site`子文件夹中）：

| Source(Forms主题) | 目标（站点主题） |
|---------------------------|---------------------------------------------------|
| `src/site/_variables.scss` | `theme/src/components/adaptiveform/_variables.scss` |
| `src/site/_mixin.scss` | `theme/src/components/adaptiveform/_mixin.scss` |

请&#x200B;**不**&#x200B;复制Forms主题的`src/site/`文件夹的其余部分；嵌入的表单样式只需要这两个文件。

![添加变量和mixin](/help/forms/assets/theme-add-mixin-variable.png)

## 步骤4：在SCSS中修复图像路径 {#step-4-fix-image-paths}

在Forms主题中，组件SCSS文件通常引用路径为`./resources/`或`url(resources/`的图像。 复制到站点主题后，这些路径必须指向`theme/src/components/adaptiveform/resources/images/`。

**标准站点模板主题**&#x200B;使用从`url()`解析出`theme/src/`个路径的Parcel。 因此，当图像位于`theme/src/components/adaptiveform/resources/images/`中时，请使用路径&#x200B;**`components/adaptiveform/resources/images/`**（相对于`theme/src/`）。

在&#x200B;**下的每**&#x200B;中`.scss`查找并替换`theme/src/components/adaptiveform/`：

| 查找 | 替换为 |
|------|------------------|
| `./resources/` | `components/adaptiveform/resources/` |
| `url(resources/` | `url(components/adaptiveform/resources/` |
| `url('resources/` | `url('components/adaptiveform/resources/` |
| `url(../resources/` | `url(components/adaptiveform/resources/` |

**示例** — 之前(Forms主题)：

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(./resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

**在**&#x200B;之后（站点主题，`adaptiveform/resources/images/`中的图像）：

```scss
.cmp-adaptiveform-button__questionmark {
  background: url(components/adaptiveform/resources/images/question.svg) center center / cover no-repeat, #969696;
}
```

![更改图像URL](/help/forms/assets/theme-change-url.png)

对`adaptiveform/`下引用图像（按钮、可折叠项、向导、容器、涂写等）的每个SCSS文件重复此操作。 建议在IDE中查找/替换`theme/src/components/adaptiveform/`以上的项目。

## 步骤5：创建自适应表单入口点SCSS {#step-5-create-adaptiveform-scss}

在站点主题中创建&#x200B;**`theme/src/components/adaptiveform/_adaptiveform.scss`**。 此文件必须：

1. 导入共享变量和mixin。
2. 导入每个自适应表单组件的主SCSS文件。

使用以下内容作为完整入口点（与所有基于核心组件的表单组件的标准集成匹配）：

```scss
//== Adaptive Form components (forms theme integration)
// Variables and mixins for adaptive form components
@import 'variables';
@import 'mixin';

//== Core adaptive form components
@import './button/_button.scss';
@import './checkboxgroup/_checkboxgroup.scss';
@import './container/_container.scss';
@import './datepicker/_datepicker.scss';
@import './dropdown/_dropdown.scss';
@import './fileinput/_fileinput.scss';
@import './footer/_footer.scss';
@import './image/_image.scss';
@import './numberinput/_numberinput.scss';
@import './panelcontainer/_panelcontainer.scss';
@import './radiobutton/_radiobutton.scss';
@import './text/_text.scss';
@import './textinput/_textinput.scss';
@import './accordion/_accordion.scss';
@import './tabsontop/_tabsontop.scss';
@import './pageheader/_pageheader.scss';
@import './wizard/_wizard.scss';
@import './title/_title.scss';
@import './telephoneinput/_telephoneinput.scss';
@import './emailinput/_emailinput.scss';
@import './recaptcha/_recaptcha.scss';
@import './verticaltabs/_verticaltabs.scss';
@import './checkbox/_checkbox.scss';
@import './termsandconditions/_termsandconditions.scss';
@import './switch/_switch.scss';
@import './hcaptcha/_hcaptcha.scss';
@import './turnstile/_turnstile.scss';
@import './review/_review.scss';
@import './scribble/_scribble.scss';
@import './datetime/_datetime.scss';
```

![自适应表单scss](/help/forms/assets/theme-adaptive-form-scss.png)

如果您的Forms主题省略了一些组件（例如，没有涂写或验证码），请移除或注释掉相应的`@import`行以避免生成错误。 上述列表与[画布主题](https://github.com/adobe/aem-forms-theme-canvas)结构匹配。

## 步骤6：导入站点主题中的自适应表单主题 {#step-6-import-in-theme-scss}

在&#x200B;**`theme/src/theme.scss`**&#x200B;中，在文件的&#x200B;**end**&#x200B;处添加单个导入（在其他组件导入之后）：

```scss
//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

**示例** - `theme.scss`结束：

```scss
// ... existing site component imports ...
@import './components/embed/_embed.scss';
@import './components/pdfviewer/_pdfviewer.scss';
@import './components/socialmediasharing/_social_media_sharing.scss';

//== Adaptive Form components (forms theme)
@import './components/adaptiveform/_adaptiveform.scss';
```

![添加自适应表单scss](/help/forms/assets/theme-add-adaptive-form-scss-theme.png)

这是现有站点主题结构中唯一需要的更改；所有特定于表单的代码都保留在`src/components/adaptiveform/`下。

## 步骤7：生成和部署 {#step-7-build-and-deploy}

1. 从主题根构建站点主题：

   ```bash
   cd theme
   npm install
   npm run build
   ```

   ![运行生成](/help/forms/assets/theme-mpm-run-build.png)

2. 通过现有[前端管道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html)部署。 部署后，相同主题CSS将应用于站点页面和嵌入的自适应Forms。

## 疑难解答 {#troubleshooting}

| 问题 | 检查内容 |
|-------|-------------------------------|
| 生成失败：图像的“找不到文件” | 确保所有表单图像都在`theme/src/components/adaptiveform/resources/images/`中。 在`.scss`下的每个`adaptiveform/`中，使用`url(components/adaptiveform/resources/images/...)`，以便路径从`theme/src/`解析（使用Parcel的标准站点主题生成所必需的）。 不要单独使用`../resources/`或`resources/`，除非您的捆绑包为每个文件解析路径；然后使用与您的图像文件夹匹配的路径。 |
| 生成失败：`_variables.scss`或`_mixin.scss`的“找不到文件” | 将这两个文件从Forms主题`src/site/`复制到`theme/src/components/adaptiveform/` （自适应表单根），而不是复制到`site`子文件夹中。 |
| 生成失败：组件（例如`_scribble.scss`）的“找不到文件” | 您的Forms主题可能不包括该组件。 在`theme/src/components/adaptiveform/_adaptiveform.scss`中，移除或注释掉该组件的`@import`行。 |
| 表单会渲染，但没有样式 | 确认页面使用了包含已构建主题CSS的客户端库，并且`theme.scss`包含`@import './components/adaptiveform/_adaptiveform.scss';`行并且已重新生成和部署主题。 |
| 站点组件与表单组件之间的样式冲突 | 表单组件类已命名（如`cmp-adaptiveform-button`）。 如果看到冲突，请检查自定义站点CSS是否覆盖这些类，并调整特殊性或顺序。 |

## 另请参阅 {#see-also}

* [使用主题为基于核心组件的自适应Forms设置样式](/help/forms/using-themes-in-core-components.md)
* [使用前端管道开发](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines.html)
