---
title: 为 EDS Form 创建自定义组件
description: 为 EDS Form 创建自定义组件
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 77e90657-38db-4a49-9aac-3f3774b62624
role: Admin, Architect, Developer
source-git-commit: 4356fcc73a9c33a11365b1eb3f2ebee5c9de24f0
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 4%

---

# 创建自定义组件

AEM FormsEdge Delivery Services允许您自定义[本机HTML表单组件](/help/edge/docs/forms/form-components.md)并创建用户友好的交互式表单。 使用该功能，您可以使用预定义的标记来修改表单组件，如表单字段[样式](/help/edge/docs/forms/style-theme-forms.md)中所述，使用自定义CSS（层叠样式表）和自定义代码来装饰该组件，从而增强自适应Forms块中表单字段的外观。

![自定义组件](/help/edge/assets/custom-component-image.png)

本文档概述了通过设置本机HTML表单组件的样式来创建自定义组件的步骤，以便改善用户体验并提高表单的视觉吸引力。

让我们举一个在表单上显示`Estimated trip cost`的`range`组件的示例。 `range`组件显示为直线，不显示任何值，如最小值、最大值或选定值。

![本机范围组件](/help/edge/assets/native-range-component.png)

让我们开始自定义`range`字段以显示行上的最小、最大和选定值，方法是使用CSS添加样式并添加自定义函数来装饰组件。

![自定义范围组件](/help/edge/assets/custom-range-component.png)

在本文的最后，您将了解如何通过在CSS文件和自定义函数中添加样式来创建自定义组件。

## 先决条件

在开始创建自定义组件之前，您应：

* 具有[本机HTML组件](/help/edge/docs/forms/form-components.md)的基础知识。
* 了解如何使用CSS选择器根据字段类型[样式表单字段](/help/edge/docs/forms/style-theme-forms.md)


## 创建自定义组件


创建自定义组件的![步骤](/help/edge/docs/forms/assets/steps-to-create-custom-component.png)

现在，让我们详细了解每个步骤。

请参考[查询电子表格](/help/edge/docs/forms/assets/enquiry.xlsx)以自定义`range`组件，具体步骤如下所示。

### 添加自定义函数以装饰组件

在`[../Form Block/components]`中添加的自定义函数包括：

* **函数声明**：定义函数名及其参数。
* **逻辑实施**：编写逻辑以添加组件的自定义行为。
* **函数导出**：使函数可在`[Form Block]`中访问。

让我们创建一个名为`range.js`的JavaScript文件来设置范围组件的样式。 要添加自定义函数，请执行以下操作：

1. 转到Google Drive或SharePoint上的AEM项目文件夹。
1. 导航到`[../Form Block/components]`。
1. 添加名为`range.js`的新文件。
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

### 在表单块中插入修饰符

`[Form Block]`使用语义HTML呈现表单字段，包括输入字段、标签和帮助文本，以及可访问性的标准属性。 要让`[Form Block]`为指定的组件使用自定义修饰符，请在`mappings.js`文件中定义它。 `mappings.js`文件导入一个函数，该函数返回负责装饰特定组件的模块。 该函数接受字段属性并返回表单字段的修饰符函数。

在本例中，该函数检查字段的`fieldType`属性，并从`[../Form Block/components]`中存在的`range.js`文件中返回自定义范围修饰符。

要在表单块中插入修饰符，请执行以下操作：

1. 转到`[../Form Block/]`并打开`mapping.js`。
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

### 在CSS文件中添加组件的样式

您可以使用CSS选择器根据字段类型和字段名称更改表单字段的外观，从而根据要求允许一致或唯一的样式。 要设置组件的样式，请在`form.css`文件中添加代码以修改表单组件的外观。

要自定义`range`组件的样式，请包含一个CSS代码片段，该代码片段在表单中为`range`输入元素及其关联的组件设置样式。 这假定具有类（如`.form`和`.range-wrapper`）的结构化HTML布局。

要在CSS文件中为组件添加样式，请执行以下操作：
1. 转到`[../Form Block/]`并打开`form.css`。
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

### 部署文件并生成项目

将更新的`range.js`、`mapping.css`和`form.css`文件部署到GitHub项目，并验证生成是否成功。

### 使用AEM Sidekick预览表单

使用[AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content)预览新实现的函数，该函数为`range`组件设置样式。

![自定义组件表单](/help/edge/assets/custom-componet-form.png)

`range`组件的新样式通过添加使用CSS的样式以及包含该组件的修饰器的自定义函数来显示行上的最小值、最大值以及选定的值。


## 另请参阅

{{see-more-forms-eds}}



