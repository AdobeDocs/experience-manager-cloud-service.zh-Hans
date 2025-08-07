---
title: 为 EDS Form 创建自定义组件
description: 为 EDS Form 创建自定义组件
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 2e2a0bdb7604168f0e3eb1672af4c2bc9b12d652
workflow-type: tm+mt
source-wordcount: '1789'
ht-degree: 98%

---

# 在“所见即所得创作”中创建自定义组件

Edge Delivery Services Forms 提供自定义功能，允许前端开发人员构建定制的表单组件。这些自定义组件可以无缝集成到所见即所得的创作体验中，使表单作者能够在表单编辑器中轻松添加、配置和管理这些组件。通过自定义组件，作者可以增强功能，同时确保流畅、直观的创作过程。

本文档概述了通过设置原生 HTML 表单组件的样式来创建自定义组件的步骤，以改善用户体验并增加表单的视觉吸引力。

## 先决条件

在开始创建自定义组件之前，您应该：

- 掌握 [原生 HTML 组件](/help/edge/docs/forms/form-components.md)的基本知识。
- 了解如何 [使用 CSS 选择器根据字段类型设置表单字段的样式](/help/edge/docs/forms/style-theme-forms.md)

## 创建自定义组件

在通用编辑器中添加自定义组件意味着表单作者可以在设计表单时使用新组件。这包括注册组件、定义组件属性以及配置组件的使用位置。创建自定义组件的步骤：

[1. 为新的自定义组件添加结构](#1-adding-structure-for-new-custom-component)
[2.定义自定义组件的属性以供创作](#2-defining-the-properties-of-your-custom-component-for-authoring)
[3.使您的自定义组件在所见即所得的组件列表中可见](#3-making-your-custom-component-visible-in-the-wysiwyg-component-list)
[4.注册您的自定义组件](#4-registering-your-custom-component)
[5.添加自定义组件的运行时行为](#5-adding-the-runtime-behaviour-for-your-custom-component)

现在我们以创建一个名为 **Range** 的新自定义组件为例。Range 组件外表为直线形式，显示最小值、最大值或选定值等数值。

![范围组件的可视化示意图，展示了具有最小值和最大值的滑块以及选定值指示器](/help/edge/docs/forms/universal-editor/assets/custom-component-range-style.png)

本文结束时，您将学会从头开始创建自定义组件。

### &#x200B;1. 为新的自定义组件添加结构

自定义组件在使用之前必须先注册，以便通用编辑器将其识别为可用选项。这是通过组件定义实现的，组件定义包括唯一标识符、默认属性和组件的结构。执行以下步骤，使自定义组件可用于表单创作：

1. **添加新文件夹和文件**&#x200B;在 AEM 项目中为新的自定义组件添加新文件夹和文件。
   1. 打开 AEM 项目并导航到 `../blocks/form/components/`。
   1. 在 `../blocks/form/components/<component_name>` 为自定义组件添加一个新文件夹。在这个例子中，我们创建一个名为 `range` 的文件夹。
   1. 导航到在 `../blocks/form/components/<component_name>` 新创建的文件夹。例如，导航到 `../blocks/form/components/range`，并添加以下文件：
      - `/blocks/form/components/range/_range.json`：包含自定义组件的定义。
      - `../blocks/form/components/range/range.css`：定义自定义组件的样式。
      - `../blocks/form/components/range/range.js`：在运行时定制自定义组件。

        ![添加自定义组件以供创作](/help/edge/docs/forms/universal-editor/assets/adding-custom-component.png)

        >[!NOTE]
        >
        > 确保 json 文件的文件名包含下划线（_）作为前缀。

1. 导航到 `/blocks/form/components/range/_range.json` 文件，并添加自定义组件的组件定义。

1. **添加组件定义**

   要添加定义，需要在 `_range.json` 文件中添加以下字段：

   - **标题**：通用编辑器中显示的组件的标题。
   - **ID**：组件的唯一标识符。
   - **fieldType**：表单支持各种 **fieldType** 来捕获特定类型的用户输入。您可以在 Extra Byte 分区中找到[支持的 fieldType](#supported-fieldtypes)。
   - **resourceType**：每个自定义组件都有一个基于其 fieldType 关联的资源类型。您可以在 Extra Byte 分区中找到[支持的 resourceType](#supported-resourcetype)。
   - **jcr:title**：它类似于标题，但存储在组件的结构中。
   - **fd:viewType**：表示自定义组件的名称。它是组件的唯一标识符。需要为组件创建自定义视图。

添加组件定义之后，`_range.json` 文件如下：

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
> 在通用编辑器中添加块时，所有与表单相关的组件都遵循与 Sites 相同的方法。您可以参考[创建与通用编辑器配合使用的块](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/create-block)文章以获取更多信息。

### &#x200B;2. 定义自定义组件的属性以供创作

自定义组件包括一个组件模型，该模型指定了表单作者可以配置哪些属性。这些属性出现在通用编辑器的&#x200B;**属性**&#x200B;对话框中，允许作者调整标签、验证规则、样式和其他属性等设置。定义属性：

1. 导航到 `/blocks/form/components/range/_range.json` 文件，并添加自定义组件的组件模型。

1. **添加组件模型**

   要定义自定义组件的组件模型，您需要将相关字段添加到 `_range.json` 文件中。

   1. **创建新的模型**

      - 在模型数组中，添加一个新对象并设置组件模型的 `id`，以匹配先前在组件定义中配置的 `fd:viewType` 属性。
      - 在此对象内包含一个字段数组。

   2. **定义属性对话框的字段**

      - 字段数组中的每个对象都应为容器类型组件，这样它就会作为选项卡出现在&#x200B;**属性**&#x200B;对话框中。
      - 某些字段可以参考 `models/form-common` 中提供的可重复使用属性。

   3. **使用现有组件模型作为参考**

      - 您可以复制与您选择的 `fieldType` 相对应的现有组件模型的内容，并根据需要进行修改。例如，扩展 `number-input` 组件以创建 **Range** 组件，因此我们可以使用 `models/form-components/_number-input.json` 中的模型数组作为参考。

   添加组件模型之后，`_range.json` 文件如下：

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
   > 要向自定义组件的&#x200B;**属性**&#x200B;对话框中添加新字段，请遵循[定义的模式](https://experienceleague.adobe.com/zh-hans/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/field-types#loading-model)。

   您还可以在自定义组件中[添加自定义属性](#adding-custom-properties-for-your-custom-component)以扩展其功能。

#### 添加自定义组件的自定义属性

自定义属性可让您根据组件属性对话框中设置的值定义特定行为。这有助于扩展组件的功能和自定义选项。

在这个例子中，我们将步进值作为自定义属性添加到 Range 组件。

![步进值自定义属性](/help/edge/docs/forms/universal-editor/assets/customcomponent-stepvalue.png)

要添加步进值自定义属性，需要在组件模型 ` _<component>.json` 文件中加入以下代码行：

```javascript
      {
      "component": "number",
      "name": "stepValue",
      "label": "Step Value",
      "valueType": "number"
      }
```

JSON 代码片段为 **Range** 组件定义了一个名为 **Step Value** 的自定义属性。以下是每个字段的细分：

- **组件**：指定“属性”对话框中使用的输入字段的类型。在这种情况下，`number` 表示该字段接受数值。
- **名称**：属性的标识符，用于在组件的逻辑中引用它。这里的 `stepValue` 代表范围的步长值设置。
- **标签**：在“属性”对话框中看到的属性的显示名称。
- **valueType**：定义属性所需的数据类型。`number` 确保只允许数字输入。

您现在可以使用 `stepValue` 作为 `range.js` 的 JSON 属性中的自定义属性，并根据其运行时的值实施动态行为。

因此，在添加完组件定义、组件模型和自定义属性后，最终的 `_range.json` 文件如下：

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


### &#x200B;3. 使您的自定义组件在所见即所得的组件列表中可见

过滤器定义了在通用编辑器中可以使用自定义组件的分区。这可确保组件只能在适当的分区中使用，从而保持结构和可用性。

确保在所见即所得表单创作过程中自定义组件出现在可用组件列表中：

1. 导航到 `/blocks/form/_form.json` 文件。
1. 定位组件数组在具有 `id="form"` 的对象中的位置。
1. 将 `fd:viewType` 值从 `definitions[]` 添加到带有 `id="form"` 的对象组件数组中。

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

![组件过滤器](/help/edge/docs/forms/universal-editor/assets/custom-component-form-file.png)

### &#x200B;4. 注册您的自定义组件

要使表单块能够识别自定义组件并在表单创作期间加载其在组件模型中定义的属性，请将组件定义中的`fd:viewType`值添加到`mappings.js`文件中。

注册组件：

1. 导航到 `/blocks/form/mappings.js` 文件。
1. 找到 `customComponents[]` 数组的位置。
1. 将 `fd:viewType` 值从 `definitions[]` 数组添加到 `customComponents[]` 数组。

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

完成上述步骤后，自定义组件将出现在通用编辑器内的表单组件列表中。然后您可以将其拖放到表单分区。

![通用编辑器组件面板截图，展示了可拖放至表单中的自定义范围组件](/help/edge/docs/forms/universal-editor/assets/custom-component-range.png)

下面的屏幕快照显示了添加到组件模型中的 `range` 组件的属性，该组件指定了表单作者可以配置的属性：

![通用编辑器属性面板截图，展示了可配置的范围组件设置，包括基本属性、验证规则及样式选项](/help/edge/docs/forms/universal-editor/assets/range-properties.png)

您现在可以通过添加样式和功能来定义自定义组件的运行时行为。

### &#x200B;5. 添加自定义组件的运行时行为

您可以使用预定义标记来修改自定义组件，如[表单字段的样式](/help/edge/docs/forms/style-theme-forms.md)中所述。这可以通过自定义 CSS（级联样式表）和自定义代码来实现，以增强组件的外观。添加组件的运行时行为：

1. 要添加样式，请导航到 `/blocks/form/components/range/range.css` 文件，并添加以下代码行：

   ```javascript
   /** Styling for range */
   main .form .range-widget-wrapper.decorated input[type="range"] {
   margin: unset;
   padding: unset;
   appearance: none;
   height: 5px;
   border-radius: 5px;
   border: none;
   background-image: linear-gradient(to right, #ADD8E6 calc(100% - var(--current-steps)/var(--total-steps)), #C5C5C5 calc(100% - var(--current-steps)/var(--total-steps)));
   }
   
   main .form .range-widget-wrapper.decorated input[type="range"]:focus {
   outline: none;
   }
   
   .range-widget-wrapper.decorated input[type="range"]::-webkit-slider-thumb {
   appearance: none;
   width: 25px;
   height: 25px;
   border-radius: 50%;
   background: #00008B; /- Dark Blue */
   border: 3px solid #00008B; /- Dark Blue */
   cursor: pointer;
   outline: 3px solid #fff;
   }
   
   .range-widget-wrapper.decorated input[type="range"]:focus::-webkit-slider-thumb {
   border-color: #00008B; /- Dark Blue */
   }
   
   .range-widget-wrapper.decorated .range-bubble {
   color: #00008B; /- Dark Blue */
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

1. 要添加功能，请导航到 `/blocks/form/components/range/range.js` 文件，并添加以下代码行：

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
   const left = `${(current / total) - 100}% - ${(current / total) - bubbleWidth}px`;
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

   它可以控制自定义组件与用户输入的交互方式、数据处理方式以及与通用编辑器中表单块的集成方式。

   加入自定义样式和功能后，Range 组件的外观和行为得到增强。更新后的设计反映了应用的样式，而增加的功能则确保了更动态化和交互式的用户体验。
下面的屏幕快照显示了更新的 Range 组件。

![最终效果中的范围组件截图，展示了通用编辑器中的样式化滑块、数值气泡显示及交互功能的组件](/help/edge/docs/forms/universal-editor/assets/custom-component-range-1.png)

## 常见问题解答

- **如果同时在 component.css 和 forms.css 中添加样式，哪个优先？**
同时在 `component.css` 和 **forms.css** 中定义样式时，`component.css` 优先。这是因为组件级样式更具体，并且会覆盖 `forms.css` 的全局样式。

- **我的自定义组件在通用编辑器的可用组件列表中不可见。如何解决这个问题？**
如果您的自定义组件没有出现，请检查以下文件，确保组件已正确注册：
   - **component-definition.json**：验证组件是否已正确定义。
   - **component-filters.json**：确保在适当的分区中允许使用该组件。
   - **component-models.json**：确认组件模型已正确配置。

## 最佳实践

- 建议[设置本地 AEM 开发环境](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#set-up-local-aem-development-environment)，以便在本地开发自定义样式和组件。


## Extra Byte

### 支持的 resourceType

| 字段类型 | 资源类型 |
|--------------|------------------------------------------------------------------|
| 文本输入 | core/fd/components/form/textinput/v1/textinput |
| 数字输入 | core/fd/components/form/numberinput/v1/numberinput |
| 日期输入 | core/fd/components/form/datepicker/v1/datepicker |
| 面板 | core/fd/components/form/panelcontainer/v1/panelcontainer |
| 复选框 | core/fd/components/form/checkbox/v1/checkbox |
| 下拉面板 | core/fd/components/form/dropdown/v1/dropdown |
| 单选按钮组 | core/fd/components/form/radiobutton/v1/radiobutton |
| 纯文本 | core/fd/components/form/text/v1/text |
| 文件输入 | core/fd/components/form/fileinput/v2/fileinput |
| 电子邮件 | core/fd/components/form/emailinput/v1/emailinput |
| 图像 | core/fd/components/form/image/v1/image |
| 按钮 | core/fd/components/form/button/v1/button |

### 支持的 fieldTypes

表单支持的 fieldTypes 有：

- 文本输入
- 数字输入
- 日期输入
- 面板
- 复选框
- 下拉面板
- 单选按钮组
- 纯文本
- 文件输入
- 电子邮件
- 图像
- 按钮

