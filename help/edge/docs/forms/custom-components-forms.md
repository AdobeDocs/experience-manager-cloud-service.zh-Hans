---
title: 为 EDS Form 创建自定义组件
description: 为 EDS Form 创建自定义组件
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 77e90657-38db-4a49-9aac-3f3774b62624
role: Admin, Architect, Developer
source-git-commit: 4a8153ffbdbc4da401089ca0a6ef608dc2c53b22
workflow-type: ht
source-wordcount: '665'
ht-degree: 100%

---

# 创建自定义组件

适用于 AEM Forms 的 Edge Delivery Services 允许您自定义 [原生 HTML 表单组件](/help/edge/docs/forms/form-components.md) 并创建用户友好且交互式的表单。它使您能够使用预定义标记来修改表单组件，如 [表单字段的样式](/help/edge/docs/forms/style-theme-forms.md) 中所述，使用自定义 CSS（层叠样式表）和自定义代码来装饰组件，从而增强自适应表单块中表单字段的外观。

![自定义组件](/help/edge/assets/custom-component-image.png)

本文档概述了通过设置原生 HTML 表单组件的样式来创建自定义组件的步骤，以改善用户体验并增加表单的视觉吸引力。

让我们以 `range` 在表单上显示的组件 `Estimated trip cost` 为例。 `range` 组件显示为一条直线，不显示任何值，如最小值、最大值或选定值。

![Native Range 组件](/help/edge/assets/native-range-component.png)

让我们开始自定义 `range` 字段，通过使用 CSS 添加样式并添加自定义函数来装饰组件，以显示行上的最小值、最大值和选定值。

![Custom Range 组件](/help/edge/assets/custom-range-component.png)

在本文结束时，您将学会通过在 CSS 文件和自定义函数中添加样式来创建自定义组件。

## 先决条件

在开始创建自定义组件之前，您应该：

* 掌握 [原生 HTML 组件](/help/edge/docs/forms/form-components.md)的基本知识。
* 了解如何 [使用 CSS 选择器根据字段类型设置表单字段的样式](/help/edge/docs/forms/style-theme-forms.md)


## 创建自定义组件


![创建自定义组件的步骤](/help/edge/docs/forms/assets/steps-to-create-custom-component.png)

现在让我们详细了解每个步骤。

请参阅 [询价电子表格](/help/edge/docs/forms/assets/enquiry.xlsx) 来自定义 `range` 组件，具体步骤如下。

### 添加自定义函数来装饰组件

`[../Form Block/components]` 中添加的自定义函数包括：

* **函数声明**：定义函数名称及其参数。
* **逻辑实施**：编写为组件添加自定义行为的逻辑。
* **函数导出**：使该函数在 `[Form Block]`中可访问。

让我们创建一个名为 `range.js` 的 JavaScript 文件来设置范围组件的样式。要添加自定义函数：

1. 转到 Google Drive 或 SharePoint 上的 AEM 项目文件夹。
1. 导航到 `[../Form Block/components]`。
1. 添加一个名为 `range.js`的新文件。
1. 添加以下代码行：

   ```javascript
   function updateBubble(input, element) {
   const step = input.step || 1;
   const max = input.max || 0;
   const min = input.min || 1;
   const value = input.value || 1;
   const current = Math.ceil((value - min) / step);
   const total = Math.ceil((max - min) / step);
   const bubble = element.querySelector('.range-bubble');
   // during initial render the width is 0. Hence using a default here.
   const bubbleWidth = bubble.getBoundingClientRect().width || 31;
   const left = `${(current / total) * 100}% - ${(current / total) * bubbleWidth}px`;
   bubble.innerText = `${value}`;
   const steps = {
   '--total-steps': Math.ceil((max - min) /    step),
   '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   // eslint-disable-next-line no-unused-vars
   export default function decorateRange(fieldDiv, field) {
   loadCSS('/blocks/form/components/range/range.css');
   const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 1;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper';
   input.after(div);
   const hover = document.createElement('span');
   hover.className = 'range-bubble';
   const rangeMinEl = document.createElement('span');
   rangeMinEl.className = 'range-min';
   const rangeMaxEl = document.createElement('span');
   rangeMaxEl.className = 'range-max';
   rangeMinEl.innerText = `${input.min || 1}`;
   rangeMaxEl.innerText = `${input.max}`;
   div.appendChild(hover);
   // move the input element within the wrapper div
   div.appendChild(input);
   div.appendChild(rangeMinEl);
   div.appendChild(rangeMaxEl);
   input.addEventListener('input', (e) => {
       updateBubble(e.target, div);
   });
   updateBubble(input, div);
   // as a best practice add a custom css class to apply custom styling
   fieldDiv.classList.add('decorated');
   return fieldDiv;    
   }
   ```

1. 保存更改。

### 在表单块中注入装饰器

 `[Form Block]` 使用语义 HTML 来呈现表单字段，包括输入字段、标签和帮助文本，并具有标准属性以实现可访问性。要让 `[Form Block]` 为指定组件使用自定义装饰器，请在 `mappings.js` 文件中定义它。 `mappings.js` 文件导入了一个函数，该函数返回负责装饰特定组件的模块。该函数采用字段属性并返回表单字段的装饰器函数。

在我们的例子中，该函数检查字段的 `fieldType` 属性，并从 `range.js` 中存在的文件 `[../Form Block/components]`返回自定义范围装饰器。

在表单块中注入装饰器：

1. 前往 `[../Form Block/]` 并打开 `mapping.js`。
1. 添加以下代码行：

   ```javascript
   export default async function componentDecorator(fd) {
   const { ':type': type = '', fieldType } = fd;
   .... existing code ....
   if (fieldType === 'range') {
   const module = await import('./components/range.js');
   return module.default;
   }
    return null; // null should be returned to use the original markup
   }
   ```

1. 保存更改。

### 在 CSS 文件中为组件添加样式

您将会学习到如何使用 CSS 选择器根据字段类型和字段名称更改表单字段的样式，从而根据需求实现一致或独特的样式。要设置组件的样式，请在 `form.css` 文件中添加代码来修改表单组件的外观。

要自定义 `range` 组件的样式，请在表单中包含一个 CSS 代码片段，用于设置 `range` 输入元素及其相关组件的样式。这假设一个结构化的 HTML 布局，其中包含诸如`.form` 和 `.range-wrapper`。

要在 CSS 文件中添加组件样式：
1. 前往 `[../Form Block/]` 并打开 `form.css`。
1. 添加以下代码行：

   ```javascript
       /** styling for range */
   main .form .range-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, var(--button-primary-color) calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #fff;
   border: 3px solid var(--button-primary-color);
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: var(--button-primary-color);
   }
   
   .range-wrapper.decorated .range-bubble {
   color: #17252e;
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   }
   
   .range-wrapper.decorated .range-min,
   .range-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-wrapper.decorated .range-max {
   float: right;
   }
   ```
1. 保存更改。

### 部署文件并构建项目

将更新后的`range.js`、`mapping.css`和`form.css` 文件部署到您的 GitHub 项目并验证是否成功构建。

### 使用 AEM Sidekick 预览表单

使用 [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) 通过新实现的`range`组件样式函数来预览您的表单。

![自定义组件表单](/help/edge/assets/custom-componet-form.png)

`range` 组件的新样式通过使用 CSS 和包含组件装饰器的自定义函数添加样式来显示线上的最小值、最大值和选定值。


## 另请参阅

{{see-more-forms-eds}}



