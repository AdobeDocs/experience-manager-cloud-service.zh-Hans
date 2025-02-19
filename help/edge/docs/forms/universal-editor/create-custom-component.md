---
title: 为 EDS Form 创建自定义组件
description: 为 EDS Form 创建自定义组件
feature: Edge Delivery Services
hide: true
hidefromtoc: true
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 76301ca614ae2256f5f8b00c41399298c761ee33
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 5%

---

# 在WYSIWYG创作中创建自定义组件

Edge Delivery Services Forms提供自定义功能，允许前端开发人员构建量身定制的表单组件。 这些自定义组件无缝集成到WYSIWYG创作体验中，使表单作者能够在表单编辑器中轻松添加、配置和管理它们。 通过自定义组件，作者可以增强功能，同时确保创作过程顺畅而直观。

本文档概述了通过设置原生 HTML 表单组件的样式来创建自定义组件的步骤，以改善用户体验并增加表单的视觉吸引力。

## 先决条件

在开始创建自定义组件之前，您应该：

* 掌握 [原生 HTML 组件](/help/edge/docs/forms/form-components.md)的基本知识。
* 了解如何 [使用 CSS 选择器根据字段类型设置表单字段的样式](/help/edge/docs/forms/style-theme-forms.md)

## 创建自定义组件

在通用编辑器中添加自定义组件意味着，表单作者可以在设计表单时使用新的组件。 这包括注册组件、定义其属性并配置可在何处使用它。 创建自定义组件的步骤如下：

[1. 正在为新自定义组件添加结构](#1-adding-structure-for-new-custom-component)
[2。 定义用于创作](#2-defining-the-properties-of-your-custom-component-for-authoring)的自定义组件的属性
[3。  使您的自定义组件在WYSIWYG组件列表](#3-making-your-custom-component-visible-in-the-wysiwyg-component-list)中可见
[4。 正在注册您的自定义组件](#4-registering-your-custom-component)
[5。 正在添加自定义组件](#5-adding-the-runtime-behaviour-for-your-custom-component)的运行时行为

让我们以创建一个名为&#x200B;**range**&#x200B;的新自定义组件为例。 范围组件显示为一条直线，并显示最小值、最大值或选定值等值。

![范围组件样式](/help/edge/docs/forms/universal-editor/assets/custom-component-range-style.png)

在本文的最后，您将了解如何从头开始创建自定义组件。

### 1.为新自定义组件添加结构

必须先注册自定义组件，以便通用编辑器将该组件识别为可用选项，然后才能使用自定义组件。 这是通过组件定义实现的，该定义包括唯一标识符、默认属性和组件结构。执行以下步骤，使自定义组件可用于表单创作：

1. **添加新文件夹和文件**
在AEM项目中为新自定义组件添加新文件夹和文件。
   1. 打开您的AEM项目并导航到`../blocks/form/components/`。
   1. 在`../blocks/form/components/<component_name>`为自定义组件添加新文件夹。 在此示例中，我们创建了一个名为`range`的文件夹。
   1. 导航到`../blocks/form/components/<component_name>`处新创建的文件夹。 例如，导航到`../blocks/form/components/range`，然后添加以下文件：
      * `/blocks/form/components/range/_range.json`：包含自定义组件的定义。
      * `../blocks/form/components/range/range.css`：定义自定义组件的样式。
      * `../blocks/form/components/range/range.js`：在运行时自定义自定义组件。

        ![添加用于创作的自定义组件](/help/edge/docs/forms/universal-editor/assets/adding-custom-component.png)

        >[!NOTE]
        >
        > 请确保json文件的文件名中包含下划线(_)作为前缀。

1. 导航到`/blocks/form/components/range/_range.json`文件并为自定义组件添加组件定义。

1. **添加组件定义**

   要添加定义，需要在`_range.json`文件中添加的字段包括：

   * **title**：在通用编辑器中显示的组件标题。
   * **id**：组件的唯一标识符。
   * **fieldType**： Forms支持各种&#x200B;**fieldType**&#x200B;来捕获特定类型的用户输入。 您可以在“额外字节”部分](#supported-fieldtypes)中找到[支持的fieldType。
   * **resourceType**：每个自定义组件都有一个基于其fieldType的关联资源类型。 您可以在“额外字节”部分](#supported-resourcetype)中找到[支持的resourceType。
   * **jcr：title**：它类似于标题，但存储在组件的结构中。
   * **fd：viewType**：它表示自定义组件的名称。 它是组件的唯一标识符。 需要为组件创建自定义视图。

添加组件定义后的`_range.json`文件如下所示：

```javascript
{
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ]
}
```

>[!NOTE]
>
> 将块添加到通用编辑器时，所有表单相关组件遵循与Sites相同的方法。 有关详细信息，请参考[创建检测用于通用编辑器的块](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/create-block)一文。

### 2.定义用于创作的自定义组件的属性

自定义组件包括指定哪些属性可由表单作者配置的组件模型。 这些属性显示在通用编辑器的&#x200B;**属性**&#x200B;对话框中，允许作者调整设置，例如标签、验证规则、样式和其他属性。 要定义属性，请执行以下操作：

1. 导航到`/blocks/form/components/range/_range.json`文件并为自定义组件添加组件模型。

1. **添加组件模型**

   要为自定义组件定义组件模型，您需要将相关字段添加到`_range.json`文件。

   1. **创建新模型**

      * 在模型数组中，添加新对象并将组件模型的`id`设置为与组件定义中较早配置的`fd:viewType`属性匹配。
      * 在此对象中包含字段数组。

   2. **定义属性对话框的字段**

      * 字段数组中的每个对象都应该是一个容器类型的组件，使其在&#x200B;**属性**&#x200B;对话框中显示为选项卡。
      * 某些字段可以引用`models/form-common`中可用的可重用属性。

   3. **使用现有组件模型作为引用**

      * 您可以复制与您所选`fieldType`对应的现有组件模型的内容，并根据需要进行修改。 例如，`number-input`组件已扩展为创建&#x200B;**范围**&#x200B;组件，因此我们可以使用`models/form-components/_number-input.json`中的模型数组作为引用。

   添加组件模型后的`_range.json`文件如下所示：

   ```javascript
   "models": [
   {
     "id": "range",
     "fields": [
       {
         "component": "container",
         "name": "basic",
         "label": "Basic",
         "collapsible": false,
         "...": "../../../../models/form-common/_basic-input-fields.json"
       },
       {
         "...": "../../../../models/form-common/_help-container.json"
       },
       {
         "component": "container",
         "name": "validation",
         "label": "Validation",
         "collapsible": true,
         "...": "../../../../models/form-common/_number-validation-fields.json"
       }
     ]
   }
   ]
   ```

   >[!NOTE]
   >
   > 要向自定义组件的&#x200B;**属性**&#x200B;对话框添加新字段，请遵循[定义的架构](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/field-types#loading-model)。

   您还可以[将自定义属性](#adding-custom-properties-for-your-custom-component)添加到自定义组件以扩展其功能。

#### 为自定义组件添加自定义属性

通过自定义属性，可根据在组件的“属性”对话框中设置的值定义特定行为。 这有助于扩展组件的功能和自定义选项。

在本例中，我们将步骤值作为自定义属性添加到范围组件。

![步骤值自定义属性](/help/edge/docs/forms/universal-editor/assets/customcomponent-stepvalue.png)

要添加步骤值自定义属性，请在` _<component>.json`文件中将组件模型附加到以下代码行：

```javascript
      {
      "component": "number",
      "name": "stepValue",
      "label": "Step Value",
      "valueType": "number"
      }
```

JSON代码片段为&#x200B;**Range**&#x200B;组件定义了一个名为&#x200B;**Step Value**&#x200B;的自定义属性。 每个字段的划分如下：

* **组件**：指定属性对话框中使用的输入字段的类型。 在这种情况下，`number`表示该字段接受数字值。
* **name**：属性的标识符，用于在组件的逻辑中引用它。 此处，`stepValue`表示范围的步骤值设置。
* **label**：在“属性”对话框中看到的属性的显示名称。
* **valueType**：定义属性所需的数据类型。 `number`确保只允许数字输入。

您现在可以将`stepValue`用作`range.js`的JSON属性中的自定义属性，并在运行时根据其值实施动态行为。

因此，添加组件定义、组件模型和自定义属性后的最终`_range.json`文件如下所示：

```javascript
 {
  "definitions": [
    {
      "title": "Range",
      "id": "range",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/numberinput/v1/numberinput",
            "template": {
              "jcr:title": "Range",
              "fieldType": "number-input",
              "fd:viewType": "range",
              "enabled": true,
              "visible": true
            }
          }
        }
      }
    }
  ],
  "models": [
    {
      "id": "range",
      "fields": [
        {
          "component": "container",
          "name": "basic",
          "label": "Basic",
          "collapsible": false,
          "...": "../../../../models/form-common/_basic-input-fields.json"
         {
           "component": "number",
           "name": "stepValue",
            "label": "Step Value",
             "valueType": "number"
}
        },
        {
          "...": "../../../../models/form-common/_help-container.json"
        },
        {
          "component": "container",
          "name": "validation",
          "label": "Validation",
          "collapsible": true,
          "...": "../../../../models/form-common/_number-validation-fields.json"
        }
      ]
    }
  ]
}
```

![组件定义和模型](/help/edge/docs/forms/universal-editor/assets/custom-component-json-file.png)


### 3.使您的自定义组件在WYSIWYG组件列表中可见

过滤器定义自定义组件可在通用编辑器中使用的部分。 这样可以确保组件只能在适当的部分中使用，从而维护结构和可用性。

要在WYSIWYG中创作表单期间，确保自定义组件显示在可用组件列表中，请执行以下操作：

1. 导航到`/blocks/form/_form.json`文件。
1. 在具有`id="form"`的对象中查找组件数组。
1. 将来自`definitions[]`的`fd:viewType`值添加到具有`id="form"`的对象的组件数组。

```javascript
 "filters": [
    {
      "id": "form",
      "components": [
        "captcha",
        "checkbox",
        "checkbox-group",
        "date-input",
        "drop-down",
        "email",
        "file-input",
        "form-accordion",
        "form-button",
        "form-fragment",
        "form-image",
        "form-modal",
        "form-reset-button",
        "form-submit-button",
        "number-input",
        "panel",
        "plain-text",
        "radio-group",
        "rating",
        "telephone-input",
        "text-input",
        "tnc",
        "wizard",
        "range"
      ]
    }
  ]
```

![组件筛选器](/help/edge/docs/forms/universal-editor/assets/custom-component-form-file.png)

### 4.注册自定义组件

要使表单块能够识别自定义组件并在表单创作期间加载其在组件模型中定义的属性，请将组件定义中的`fd:viewType`值添加到`mappings.js`文件中。
要注册组件，请执行以下操作：
1. 导航到`/blocks/form/mappings.js`文件。
1. 找到`customComponents[]`阵列。
1. 将`definitions[]`数组中的`fd:viewType`值添加到`customComponents[]`数组。

```javascript
let customComponents = ["range"];
const OOTBComponentDecorators = ['file-input',
                                 'wizard', 
                                 'modal', 'tnc',
                                'toggleable-link',
                                'rating',
                                'datetime',
                                'list',
                                'location',
                                'accordion'];
```

![组件映射](/help/edge/docs/forms/universal-editor/assets/custom-component-mapping-file.png)

完成上述步骤后，自定义组件将显示在通用编辑器的表单组件列表中。 然后，可将其拖放到表单部分中。

![范围组件](/help/edge/docs/forms/universal-editor/assets/custom-component-range.png)

下面的屏幕快照显示了添加到组件模型的`range`组件的属性，该组件指定了表单作者可以配置的属性：

![范围组件](/help/edge/docs/forms/universal-editor/assets/range-properties.png)的属性

您现在可以通过添加样式和功能来定义自定义组件的运行时行为。

### 5.为自定义组件添加运行时行为

您可以使用预定义标记修改自定义组件，如表单字段[样式](/help/edge/docs/forms/style-theme-forms.md)中所述。 这可以通过自定义CSS（层叠样式表）和自定义代码来实现，以增强组件的外观。 要添加组件的运行时行为，请执行以下操作：

1. 要添加样式，请导航到`/blocks/form/components/range/range.css`文件并添加以下代码行：

   ```javascript
   /** Styling for range */
   main .form .range-widget-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, #ADD8E6 calc(100% * var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% * var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-widget-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-widget-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #00008B; /* Dark Blue */
   border: 3px solid #00008B; /* Dark Blue */
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-widget-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: #00008B; /* Dark Blue */
   }
   
   .range-widget-wrapper.decorated .range-bubble {
   color: #00008B; /* Dark Blue */
   font-size: 20px;
   line-height: 28px;
   position: relative;
   display: inline-block;
   padding-bottom: 12px;
   font-weight: bold;
   }
   
   .range-widget-wrapper.decorated .range-min,
   .range-widget-wrapper.decorated .range-max {
   font-size: 14px;
   line-height: 22px;
   color: #494f50;
   margin-top: 16px;
   display: inline-block;
   }
   
   .range-widget-wrapper.decorated .range-max {
   float: right;
   }
   ```
   代码可帮助您定义自定义组件的样式和视觉外观。

1. 要添加功能，请导航到`/blocks/form/components/range/range.js`文件并添加以下代码行：

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
       '--total-steps': Math.ceil((max - min) / step),
       '--current-steps': Math.ceil((value - min) / step),
   };
   const style = Object.entries(steps).map(([varName, varValue]) => `${varName}:${varValue}`).join(';');
   bubble.style.left = `calc(${left})`;
   element.setAttribute('style', style);
   }
   
   export default async function decorate(fieldDiv, fieldJson) {
   console.log('RANGE DIV: ', fieldDiv);
   console.log('RANGE JSON: fieldJson', fieldJson);
    const input = fieldDiv.querySelector('input');
   // modify the type in case it is not range.
   input.type = 'range';
   input.min = input.min || 10;
   input.max = input.max || 1000;
   // create a wrapper div to provide the min/max and current value
   const div = document.createElement('div');
   div.className = 'range-widget-wrapper decorated';
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
   return fieldDiv;
   }
   ```

   它控制自定义组件如何与用户输入交互、处理数据以及与通用编辑器中的表单块集成。

   在合并自定义样式和功能后，范围组件的外观和行为得到了增强。 更新的设计反映了应用的样式，而添加的功能可确保获得更动态、更具交互性的用户体验。
以下屏幕截图说明了更新的范围组件。

![范围组件样式](/help/edge/docs/forms/universal-editor/assets/custom-component-range-1.png)

## 常见问题解答

* **如果我同时在component.css和forms.css中添加样式，哪个样式优先？**
同时在`component.css`和&#x200B;**forms.css**&#x200B;中定义样式时，`component.css`优先。 这是因为组件级样式更加具体，并且覆盖了`forms.css`中的全局样式。

* **我的自定义组件在通用编辑器的可用组件列表中不可见。 如何解决此问题？**
如果未显示您的自定义组件，请检查以下文件，以确保该组件已正确注册：
   * **component-definition.json**：验证是否已正确定义该组件。
   * **component-filters.json**：确保在相应的部分中允许该组件。
   * **component-models.json**：确认组件模型配置正确。

## 最佳实践

* 建议[设置本地AEM开发环境](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#set-up-local-aem-development-environment)，以便在本地开发自定义样式和组件。


## 额外字节

### 支持的资源类型

| 字段类型 | 资源类型 |
|--------------|------------------------------------------------------------------|
| 文本输入 | core/fd/components/form/textinput/v1/textinput |
| 数字输入 | core/fd/components/form/numberinput/v1/numberinput |
| 数据输入 | core/fd/components/form/datepicker/v1/datepicker |
| 面板 | core/fd/components/form/panelcontainer/v1/panelcontainer |
| 复选框 | core/fd/components/form/checkbox/v1/checkbox |
| 下拉面板 | core/fd/components/form/dropdown/v1/dropdown |
| 单选按钮组 | core/fd/components/form/radiobutton/v1/radiobutton |
| 纯文本 | core/fd/components/form/text/v1/text |
| 文件输入 | core/fd/components/form/fileinput/v2/fileinput |
| 电子邮件 | core/fd/components/form/emailinput/v1/emailinput |
| 图像 | core/fd/components/form/image/v1/image |
| 按钮 | core/fd/components/form/button/v1/button |

### 支持的字段类型

表单支持的fieldTypes包括：
* 文本输入
* 数字输入
* 数据输入
* 面板
* 复选框
* 下拉面板
* 单选按钮组
* 纯文本
* 文件输入
* 电子邮件
* 图像
* 按钮

## 另请参阅

{{see-more-forms-eds}}
