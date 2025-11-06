---
title: 为 EDS Form 创建自定义组件
description: 为 EDS Form 创建自定义组件
feature: Edge Delivery Services
role: Admin, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 100%

---


# 在自适应表单块中创建自定义表单组件

Edge Delivery Services Forms 提供自定义功能，允许前端开发人员构建定制的表单组件。这些自定义组件可以无缝集成到所见即所得的创作体验中，使表单作者能够在表单编辑器中轻松添加、配置和管理这些组件。通过自定义组件，作者可以增强功能，同时确保流畅、直观的创作过程。

本文档概述了通过设置原生 HTML 表单组件的样式来创建自定义组件的步骤，以改善用户体验并增加表单的视觉吸引力。

## 架构概述

表单块的自定义组件遵循 **MVC（模型-视图-控制器）**&#x200B;架构模式：

### 模型

- 由每个 `field/component` 的 JSON 架构定义。

- 可编辑属性在相应的 JSON 文件中指定（参见 blocks/form/models/form-components）。

- 这些属性可在表单构建器中供作者使用，并作为字段定义（fd）的一部分传递给组件。

### 视图

- 每种字段类型的 HTML 结构在 form-field-types 中进行描述。

- 这是组件的基础结构，可扩展或修改。

- 每个 OOTB（开箱即用）组件的基础 HTML 结构在 form-field-types 中均有文档说明。

### 控制器/组件逻辑

- 通过 JavaScript 实施，可以是 OOTB（开箱即用）组件，也可以是自定义组件。- 自定义组件位于 `blocks/form/components` 文件夹中。

## OOTB 组件

**OOTB（开箱即用）**&#x200B;组件为自定义开发提供基础：

- OOTB 组件位于 `blocks/form/models/form-components` 中。

- 每个 OOTB 组件都有一个 JSON 文件，用于定义其可编辑属性（例如 ` _text-input.json`、`_drop-down.json`）。

- 这些属性可在表单构建器中供作者使用，并作为字段定义（fd）的一部分传递给组件。

- 每个 OOTB（开箱即用）组件的基础 HTML 结构在 form-field-types 中均有文档说明。

扩展现有的 OOTB 组件，可以复用其基础结构、行为和属性，并根据需要进行自定义。

- 自定义组件必须从预定义的 OOTB 组件集扩展。

- 系统会根据字段 JSON 中的 `viewType` 属性识别应扩展的 OOTB 组件。

- 系统维护了允许的自定义组件变体注册表。只能使用注册表中列出的变体，例如 `mappings.js` 中的 `customComponents[]`。

- 渲染表单时，系统会检查变体属性或 `:type/fd:viewType`，如果与已注册的自定义组件匹配，则从 `blocks/form/components` 文件夹加载相应的 JS 和 CSS 文件。

- 然后系统会将自定义组件应用到 OOTB 组件的基础 HTML 结构上，从而增强或覆盖其行为和外观。

## 自定义组件的结构

要创建自定义组件，可以使用 **Scaffolder CLI** 设置组件所需的文件和文件夹，然后为自定义组件编写代码。

- 自定义组件存放在 `blocks/form/components` 文件夹中。

- 每个自定义组件必须放置在其独立文件夹中，文件夹名称与组件名称相同，例如卡片。在该文件夹内，应包含以下文件：

   - **_cards.json**——扩展某个 OOTB 组件定义的 JSON 文件，定义其可编辑属性（模型[]）以及加载时的内容结构（定义[]）。
   - **cards.js**——包含主要逻辑的 JavaScript 文件。
   - **cards.css**——可选，用于样式。

- 文件夹名称必须与 JS/CSS 文件名称保持一致。

### 在自定义组件中复用和扩展字段

在自定义组件的 JSON 文件中定义字段（无论是基础、验证、帮助等任意字段组）时，请遵循以下最佳做法以保持可维护性和一致性：

- 通过引用现有的共享容器或字段定义来复用标准/共享字段（例如 `../form-common/_basic-input-placeholder-fields.json#/fields`、`../form-common/_basic- validation-fields.json#/fields`）。这样可继承所有标准选项，而无需重复定义。

- 仅在容器中显式添加新的或自定义字段。这样可以保持架构精简（DRY）且聚焦。

- 移除或避免重复已通过引用包含的字段。只需定义与组件逻辑唯一相关的字段。

- 根据需要引用帮助容器和其他共享内容（例如 `../form-common/_help-container.json`），以确保一致性和可维护性。

>[!TIP]
>
> - 这种模式可简化未来的逻辑更新或扩展，并确保自定义组件与表单系统的其他部分保持一致。
> - 在添加新字段之前，请务必检查是否已有共享容器或字段定义可用。

### 为自定义组件定义新属性

- 如果需要从作者那里获取自定义组件的新属性，可以在组件的 JSON 文件中通过在 `fields[]` 数组中定义字段来实现。

- 自定义组件通过 :type 属性进行识别，该属性可在 JSON 文件中设置为 `fd:viewType`（例如 `fd:viewType: cards`）。这样系统就能识别并加载正确的自定义组件，因此这对自定义组件来说是必需的。

- 在 JSON 定义中添加的任何新属性都会作为属性在字段定义中可用。组件的 JS 逻辑中的 `<propertyName>`

## 自定义组件 JavaScript API

自定义组件 JavaScript API 定义了如何控制自定义表单组件的行为、外观和响应性。

### 修饰函数

**修饰**&#x200B;函数是自定义组件的入口点。它会初始化组件，将其与 JSON 定义关联，并允许您操作组件的 HTML 结构和行为。

>[!NOTE]
>
> 自定义组件的 JavaScript 文件必须导出一个默认函数作为修饰：

#### 函数签名：

```javascript
export default function decorate(element, fieldJson, container, formId) 
{
  // element: The HTML structure of the OOTB component you are extending
  // fieldJson: The JSON field definition (all authorable properties)
  // container: The parent element (fieldset or form)
  // formId: The id of the form

  // ... your logic here ...
}
```

它可以：

- **修改元素**：添加事件监听器、更新属性或插入额外标记。

- **访问 JSON 属性**：使用 `fd.properties.<propertyName>` 读取 JSON 架构中定义的值，并在组件逻辑中应用。

## 订阅函数

**订阅**&#x200B;函数使您的组件能够对字段值或自定义事件的变化作出响应。这确保组件与表单的数据模型保持同步，并可动态更新其 UI。

### 函数签名：

```javascript
import { subscribe } from '../../rules/index.js';
export default function decorate(fieldDiv, fieldJson, container, formId) {
  // Access custom properties defined in the JSON
  const { initialText, finalText, time } = fieldJson?.properties;

  // ... setup logic ...

  subscribe(fieldDiv, formId, (_fieldDiv, fieldModel) => {
    fieldModel.subscribe(() => {
      // React to custom event (e.g., resetCardOption)
      // ... logic ...
    }, 'resetCardOption');
  });
}
```

它可以：

- **注册回调**：调用 **subscribe(element, formId, callback)** 来注册回调，以便在字段数据发生变化时执行。使用两个回调参数：
   - **element**：表示字段的 HTML 元素。
   - **fieldModel**：表示字段状态和事件 API 的对象。

- **监听更改或事件**：使用 `fieldModel.subscribe((event) => { ... }, 'eventName')` 在值发生变化或触发自定义事件时执行逻辑。事件对象包含有关更改的详细信息。

## 创建自定义组件

在本节中，您将学习如何通过扩展 OOTB 单选按钮组件来创建一个&#x200B;**卡片自定义组件**。

![卡片自定义组件](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;1. 代码设置

#### 1.1 文件与文件夹

第一步是设置自定义组件所需的文件，并将其与代码库中的代码连接起来。此过程由 **AEM Forms Scaffolder CLI** 自动完成，可更快速地生成基架并连接所需文件。

>[!VIDEO](https://video.tv.adobe.com/v/3474752)

1. 打开终端并导航到表单项目的根目录。
2. 运行以下命令：

```bash
npm install
npm run create:custom-component
```

![Scaffolder CLI](/help/edge/docs/forms/universal-editor/assets/scaffolder-cli.png)

该命令将：

- **提示您为新组件命名**。例如，在此用例中输入卡片。
- **要求您选择**&#x200B;一个基础组件（选择单选按钮组）

这将创建所有必要的文件夹和文件，包括：

```
blocks/form/
└── components/
  └── cards/
    ├── cards.js
    └── cards.css
    └── _cards.json
```

如 CLI 输出所示，将其与代码库的其他部分连接起来。
它会自动执行以下功能：

- 将卡片添加到过滤器中，以便在自适应表单块中进行添加。
- 更新 `mappings.js` 的允许列表，以包含新的卡片组件。
- 在通用编辑器中的&#x200B;**自定义组件**&#x200B;列表下注册卡片组件的定义。

>[!NOTE]
>
> 您还可以使用手动（旧版）方法创建自定义组件。有关详细信息，请参阅[创建自定义组件的手动或旧版方法](#manual-or-legacy-method-to-create-custom-component)部分。

#### 1.2 在通用编辑器中使用组件

1. **刷新通用编辑器**：在通用编辑器中打开表单并刷新页面，以确保加载来自代码库的最新代码。

2. **添加自定义组件**

   1. 单击表单画布上的&#x200B;**添加 (+)** 按钮。
   2. 滚动到“自定义组件”部分。
   3. 选择新创建的&#x200B;**卡片组件**&#x200B;并将其插入表单中。

      ![选择自定义组件](/help/edge/docs/forms/universal-editor/assets/select-custom-component.png)

由于 `cards.js` 中尚无代码，自定义组件将呈现为一个单选组。

#### 1.3 在本地预览和测试

现在表单已包含自定义组件，您可以为该表单创建代理，在本地进行修改并实时查看变更：

1. 前往终端并运行 `aem up`。

2. 打开在 `http://localhost:3000/{path-to-your-form}` 启动的代理服务器（路径示例：`/content/forms/af/custom-component-form`）。


### &#x200B;2. 为自定义组件实施自定义行为

#### 2.1 设置自定义组件的样式

为组件添加 **card** 类以进行样式化，并为每个单选项添加一张图片；请使用以下示例代码。

**使用 card.js 设置组件的样式**

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';

export default function decorate(element, fieldJson, container, formId) {
  element.classList.add('card');

  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper) => {
    const image = createOptimizedPicture(
      'https://main--afb--jalagari.hlx.live/lab/images/card.png',
      'card-image'
    );
    radioWrapper.appendChild(image);
  });

  return element;
}
```

**使用 cards.css 添加运行时行为**

```javascript
.card .radio-wrapper {
  min-width: 320px; /* or whatever width fits your design */
  max-width: 340px;
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  flex: 0 0 auto;
  scroll-snap-align: start;
  padding: 24px 16px;
  margin-bottom: 0;
  position: relative;
  transition: box-shadow 0.2s;
  display: flex;
  align-items: flex-start;
  gap: 12px;
}
```

现在，卡片组件将显示如下效果：

![添加卡片 css 和 js](/help/edge/docs/forms/universal-editor/assets/add-card-css.png)

#### 2.2 使用订阅函数添加动态行为

当下拉列表发生变化时，会获取卡片并设置在单选按钮组的枚举中。但当前视图并未对此进行处理。因此呈现效果如下：

![订阅函数](/help/edge/docs/forms/universal-editor/assets/card-subscribe.png)

当调用 API 时，会设置字段模型，并且必须监听其变化以相应地渲染视图。这可以通过&#x200B;**订阅函数**&#x200B;实现。

让我们将上一步的视图代码转换为一个函数，并在 `cards.js` 的订阅函数中调用，如下所示：

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';
import { subscribe } from '../../rules/index.js';

function createCard(element, enums) {
  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {
    if (enums[index]?.name) {
      let label = radioWrapper.querySelector('label');

      if (!label) {
        label = document.createElement('label');
        radioWrapper.appendChild(label);
      }

      label.textContent = enums[index]?.name;
    }

    const image = createOptimizedPicture(
      enums[index]?.image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png',
      'card-image'
    );

    radioWrapper.appendChild(image);
  });
}

export default function decorate(element, fieldJson, container, formId) {
  element.classList.add('card');
  createCard(element, fieldJson.enum);

  subscribe(element, formId, (fieldDiv, fieldModel) => {
    fieldModel.subscribe((e) => {
      const { payload } = e;

      payload?.changes?.forEach((change) => {
        if (change?.propertyName === 'enum') {
          createCard(element, change.currentValue);
        }
      });
    });
  });

  return element;
}
```

**在 cards.js 中使用订阅函数监听事件变化**

现在，当您更改下拉列表时，卡片会自动填充，如下所示：

![订阅函数](/help/edge/docs/forms/universal-editor/assets/card-subscribe-final.png)

#### 2.3 将视图更新与字段模型同步

为了将视图中的更改同步到字段模型，您需要设置所选卡片的值。因此，请在 cards.js 中添加如下所示的更改事件监听器：

**在 cards.js 中使用字段模型 API**

```javascript
import { createOptimizedPicture } from '../../../../scripts/aem.js';
import { subscribe } from '../../rules/index.js';

function createCard(element, enums) {
  element.querySelectorAll('.radio-wrapper').forEach((radioWrapper, index) => {
    if (enums[index]?.name) {
      let label = radioWrapper.querySelector('label');

      if (!label) {
        label = document.createElement('label');
        radioWrapper.appendChild(label);
      }

      label.textContent = enums[index]?.name;
    }

    // Attach index to input element for later reference
    radioWrapper.querySelector('input').dataset.index = index;

    const image = createOptimizedPicture(
      enums[index]?.image || 'https://main--afb--jalagari.hlx.page/lab/images/card.png',
      'card-image'
    );

    radioWrapper.appendChild(image);
  });
}

export default function decorate(element, fieldJson, container, formId) {
  element.classList.add('card');
  createCard(element, fieldJson.enum);

  subscribe(element, formId, (fieldDiv, fieldModel) => {
    fieldModel.subscribe((e) => {
      const { payload } = e;

      payload?.changes?.forEach((change) => {
        if (change?.propertyName === 'enum') {
          createCard(element, change.currentValue);
        }
      });
    });

    element.addEventListener('change', (e) => {
      e.stopPropagation();
      const value = fieldModel.enum?.[parseInt(e.target.dataset.index, 10)];
      fieldModel.value = value.name;
    });
  });

  return element;
}
```

现在，自定义卡片组件会呈现如下效果：

![卡片自定义组件](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### &#x200B;3. 提交并推送更改

在为自定义组件实现了 JavaScript 和 CSS 并完成本地验证后，将更改提交并推送到 Git 存储库。

```bash
git add . && git commit -m "Add card custom component" && git push
```

这样，您就通过几个简单步骤成功创建了一个复杂的自定义卡片选择组件。

+++ **创建自定义组件的手动或旧版方法**

旧版的方法是手动执行以下步骤：

1. **选择一个 OOTB 组件进行扩展**（如按钮、下拉框、文本输入框等）。在此示例中，扩展单选按钮组件。

2. **在 `blocks/form/components` 中创建一个文件夹**，并使用您的组件名称命名（此处为卡片）。

3. **添加一个同名的 JS 文件**：
   - `blocks/form/components/cards/cards.js`。

4. （可选）**添加一个 CSS 文件**&#x200B;用于自定义样式：
   - `blocks/form/components/cards/cards.css.`

5. 在与&#x200B;**组件 JS 文件**&#x200B;相同的文件夹中&#x200B;**定义一个新的 JSON 文件**（例如 ` _cards.json`，路径为 `blocks/form/components/cards/_cards.json`）。该 JSON 应继承现有组件，并在定义中将 `fd:viewType` 设置为您的组件名称（此处为卡片）：

   - 针对所有字段组（基础、验证、帮助等），显式添加您的自定义字段。

6. **实施 JS 和 CSS 逻辑：**
   - 导出一个默认函数，如上所述。
   - 使用 **element** 参数修改基础 HTML 结构。
   - 如需标准字段数据，可使用 **fieldJson** 参数。
   - 如需监听字段变化或自定义事件，可使用&#x200B;**订阅**&#x200B;函数。

     >[!NOTE]
     >
     >按照上述说明为自定义组件实现 JS 和 CSS 逻辑。

7. 在表单生成器中将您的组件注册为一个变体，并在 JSON 中设置变体属性或
   `fd:viewType/:type` 为您的组件名称。例如，将 `definitions[]` 中的 `fd:viewType` 值（卡片）添加到 `id="form` 对象的组件数组中。

   ```
       {
     "definitions": [
       {
         "title": "Cards",
         "id": "cards",
         "plugins": {
           "xwalk": {
             "page": {
               "resourceType": "core/fd/components/form/radiobutton/v1/radiobutton",
               "template": {
                 "jcr:title": "Cards",
                 "fieldType": "radio-button",
                 "fd:viewType": "cards",
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

8. **更新 mappings.js**：将您的组件名称添加到 **OOTBComponentDecorators**（用于 OOTB 风格组件）或 **customComponents** 列表中，以便系统识别并加载该组件。

   ```javascript
   let customComponents = ["cards"];
   const OOTBComponentDecorators = [];
   ```

9. **更新 _form.json**：将您的组件名称添加到 `filters.components` 数组中，以便在创作 UI 中使用。

   ```javascript
   "filters": [
   {
       "id": "form",
       "components": [ "cards"]}
       ]
   ```

10. **更新 _component-definition.json**：在 `models/_component-definition.json` 中，更新 `id custom-components` 组内的数组，新增一个对象，如下所示：

    ```javascript
    {
    "...":"../blocks/form/components/cards/_cards.json#/definitions"
    }
    ```

    这样可为新建的卡片组件提供引用，以便与其他组件一起构建。

11. **运行 build:json 脚本**：执行 `npm run build:json`，将所有组件 JSON 定义编译并合并为一个文件，以便服务器提供服务。这将确保新组件的架构包含在合并的输出中。

12. 将更改提交并推送到 Git 存储库。

现在，您可以在表单中添加该自定义组件。

+++

## 创建复合组件

复合组件是通过组合多个组件创建的。
例如，一个“条款与条件”复合组件包含一个父面板，其中包括：

- 一个用于显示条款的纯文本字段

- 一个用于获取用户同意的复选框

这种组合结构在相应组件的 JSON 文件中定义为一个模板。以下示例展示了如何为“条款与条件”组件定义一个模板：

```javascript
{
  "definitions": [
    {
      "title": "Terms and conditions",
      "id": "tnc",
      "plugins": {
        "xwalk": {
          "page": {
            "resourceType": "core/fd/components/form/termsandconditions/v1/termsandconditions",
            "template": {
              "jcr:title": "Terms and conditions",
              "fieldType": "panel",
              "fd:viewType": "tnc",
              "text": {
                "value": "Text related to the terms and conditions come here.",
                "sling:resourceType": "core/fd/components/form/text/v1/text",
                "fieldType": "plain-text",
                "textIsRich": true
              },
              "approvalcheckbox": {
                "name": "approvalcheckbox",
                "jcr:title": "I agree to the terms & conditions.",
                "sling:resourceType": "core/fd/components/form/checkbox/v1/checkbox",
                "fieldType": "checkbox",
                "required": true,
                "type": "string",
                "enum": [
                  "true"
                ]
              }
            }
          }
        }
      }
    }
  ],
  ...
}
```

## 最佳做法

在创建自定义组件前，请注意以下几点：

- **保持组件逻辑聚焦：**&#x200B;仅添加或覆盖实现自定义行为所必需的内容

- **充分利用基础结构**：以 OOTB HTML 为起点

- **使用可编辑属性：**&#x200B;通过 JSON 架构提供可配置选项

- **为 CSS 添加命名空间**：使用唯一的类名以避免样式冲突

## 引用

- [form-field-types](/help/edge/docs/forms/eds-form-field-properties.md)：所有字段类型的基本 HTML 结构和属性。

- **blocks/form/models/form-components**：OOTB 和自定义组件的属性定义。

- **blocks/form/components**：用于放置自定义组件的目录。例如：`blocks/form/components/countdown-timer/_countdown-timer.json` 展示了如何扩展基础组件并添加新属性。
