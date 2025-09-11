---
title: 为 EDS Form 创建自定义组件
description: 为 EDS Form 创建自定义组件
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 2bbe3f95-d5d0-4dc7-a983-7a20c93e2906
source-git-commit: 23534e7bbff8d663fc3b888baa90f5d84e64d310
workflow-type: tm+mt
source-wordcount: '2121'
ht-degree: 4%

---


# 在自适应表单块中创建自定义表单组件

Edge Delivery Services Forms 提供自定义功能，允许前端开发人员构建定制的表单组件。这些自定义组件可以无缝集成到所见即所得的创作体验中，使表单作者能够在表单编辑器中轻松添加、配置和管理这些组件。通过自定义组件，作者可以增强功能，同时确保流畅、直观的创作过程。

本文档概述了通过设置原生 HTML 表单组件的样式来创建自定义组件的步骤，以改善用户体验并增加表单的视觉吸引力。

## 架构概述

Forms块的自定义组件遵循&#x200B;**MVC (Model-View-Controller)**&#x200B;架构模式：

### 模型

- 由JSON架构为每个`field/component`定义。

- 可创作属性在相应的JSON文件中指定（请参阅块/表单/模型/表单组件）。

- 这些属性可供表单生成器中的作者使用，并作为字段定义(fd)的一部分传递到组件。

### 查看

- 表单字段类型中介绍了每种字段类型的HTML结构。

- 这是组件的基本结构，可以对其进行扩展或修改。

- 表单字段类型中记录了每个OOTB组件的基本HTML结构。

### 控制器/组件逻辑

- 在JavaScript中以OOTB（现成）或自定义组件的形式实施。   — 位于自定义组件的`blocks/form/components`中。

## OOTB组件

**OOTB（现成）**&#x200B;组件为自定义开发奠定了基础：

- OOTB组件位于`blocks/form/models/form-components`中。

- 每个OOTB组件都有一个定义其可创作属性（如` _text-input.json`，`_drop-down.json`）的JSON文件。

- 这些属性在表单生成器中可供作者使用，并作为字段定义(fd)的一部分传递到组件。

- 表单字段类型中记录了每个OOTB组件的基本HTML结构。

扩展现有OOTB组件允许您重复使用其基本结构、行为和属性，同时对其进行自定义以满足您的需求。

- 自定义组件必须从预定义的OOTB组件集进行扩展。

- 系统会根据字段JSON中的`viewType`属性标识要扩展的OOTB组件。

- 系统维护允许的自定义组件变体的注册表。 只能使用此注册表中所列的变体，例如`customComponents[]`中的`mappings.js`。

- 呈现表单时，系统会检查变量属性或`:type/fd:viewType`，如果它与注册的自定义组件匹配，则会从`blocks/form/components`文件夹加载相应的JS和CSS文件。

- 自定义组件随后将应用于OOTB组件的基本HTML结构，允许您增强或覆盖其行为和外观。

## 自定义组件的结构

要创建自定义组件，您可以使用&#x200B;**基架CLI**&#x200B;设置组件所需的文件和文件夹，然后添加自定义组件的代码。

- 自定义组件驻留在`blocks/form/components`文件夹中。

- 每个自定义组件必须置于其自身的文件夹中，以组件命名，例如卡片。 在文件夹中，以下文件应为：

   - **_cards.json** — 扩展OOTB组件的组件定义、定义其可创作属性（模型[]）和加载时内容结构（定义[]）的JSON文件。
   - **cards.js** — 包含主逻辑的JavaScript文件。
   - **卡片.css** — 可选，适用于样式。

- 文件夹名称与JS/CSS文件必须匹配。

### 重用和扩展自定义组件中的字段

在自定义组件的JSON中定义字段时（适用于任何字段组、基本、验证、帮助等），请遵循以下可维护性和一致性最佳实践：

- 通过引用现有的共享容器或字段定义（例如，`../form-common/_basic-input-placeholder-fields.json#/fields`、`../form-common/_basic- validation-fields.json#/fields`）重用标准/共享字段。 这可确保您继承所有标准选项而不复制它们。

- 在容器中明确只添加新的或自定义字段。 这样可使您的架构保持干燥和专注。

- 移除或避免复制已通过引用包含的字段。 仅定义组件的逻辑特有的字段。

- 根据一致性和可维护性的需要，引用帮助容器和其他共享内容（例如`../form-common/_help-container.json`）。

>[!TIP]
>
> - 此模式可让您在未来轻松更新或扩展逻辑，并确保自定义组件与表单系统的其他组件保持一致。
> - 添加新共享容器或字段定义之前，请始终检查现有共享容器或字段定义。

### 为自定义组件定义新属性

- 如果您需要从作者中为自定义组件捕获新属性，可以通过在组件的JSON中的组件的`fields[]`数组中定义字段来实现此操作。

- 自定义组件使用:type属性进行标识，该属性可在JSON文件中设置为`fd:viewType`（例如，`fd:viewType: cards`）。 这允许系统识别和加载正确的自定义组件，因此对于自定义组件是必需的

- 在JSON定义中添加的任何新属性在字段定义中均可作为属性使用。 组件的JS逻辑中的`<propertyName>`

## 自定义组件JavaScript API

自定义组件JavaScript API定义了如何控制自定义表单组件的行为、外观和反应性。

### 装饰功能

**decorate**&#x200B;函数是自定义组件的入口点。 它会初始化组件，将其链接到其JSON定义，并允许您处理其HTML结构和行为。

>[!NOTE]
>
> 自定义组件的JavaScript文件必须将默认函数导出为decorate：

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

- **修改元素**：添加事件侦听器、更新属性或插入其他标记。

- **访问JSON属性**：使用`fd.properties.<propertyName>`读取JSON架构中定义的值并在组件逻辑中应用这些值。

## 订阅函数

**subscribe**&#x200B;函数使您的组件能够对字段值或自定义事件的更改做出反应。 这可确保组件与表单的数据模型保持同步，并可动态更新其UI。

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

- **注册回调**：调用&#x200B;**subscribe(element， formId， callback)**&#x200B;将您的回调注册为每当字段数据更改时运行。使用两个回调参数：
   - **element**：表示字段的HTML元素。
   - **fieldModel**：表示字段状态和事件API的对象。

- **侦听更改或事件**：每当值更改或触发自定义事件时，使用`fieldModel.subscribe((event) => { ... }, 'eventName')`执行逻辑。 事件对象包含有关更改内容的详细信息。

## 创建自定义组件

在本节中，您将了解通过扩展OOTB单选按钮组件来创建&#x200B;**卡自定义组件**&#x200B;的过程。

![卡自定义组件](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### 1.代码设置

#### 1.1文件和文件夹

第一步是设置自定义组件的必要文件，并将其连接到存储库中的代码。 此过程由&#x200B;**AEM Forms Scaffolder CLI**&#x200B;自动完成，这样可以更快地搭建基架并连接必要的文件。

>[!VIDEO](https://video.tv.adobe.com/v/3474752)

1. 打开终端并导航到表单项目的根目录。
2. 运行以下命令：

```bash
npm install
npm run create:custom-component
```

![基架CLI](/help/edge/docs/forms/universal-editor/assets/scaffolder-cli.png)

它将：

- **提示您为新组件命名**。 例如，在此例中，使用卡。
- **要求您选择**&#x200B;基本组件（选择单选按钮组）

这将创建所有必需的文件夹和文件，包括：

```
blocks/form/
└── components/
  └── cards/
    ├── cards.js
    └── cards.css
    └── _cards.json
```

并将其与存储库中的其余代码连接起来，如CLI的输出中所示。
它自动执行以下功能：

- 将卡片添加到过滤器中，允许在自适应表单块内添加。
- 更新`mappings.js`的允许列表以包含新卡片组件。
- 在通用编辑器中的&#x200B;**自定义组件**&#x200B;列表下注册卡片组件的定义。

>[!NOTE]
>
> 您也可以使用手动（旧版）方法创建自定义组件。 有关详细信息，请参阅[手动或旧式方法](#manual-or-legacy-method-to-create-custom-component)以创建自定义组件部分。

#### 1.2在通用编辑器中使用组件

1. **刷新通用编辑器**：在通用编辑器中打开您的表单并刷新页面，以确保它从存储库加载最新代码。

2. **添加自定义组件**

   1. 单击表单画布上的&#x200B;**添加(+)**&#x200B;按钮。
   2. 滚动到自定义组件部分。
   3. 选择新创建的&#x200B;**卡片组件**&#x200B;以将其插入到您的表单中。

      ![选择自定义组件](/help/edge/docs/forms/universal-editor/assets/select-custom-component.png)

由于`cards.js`内不存在代码，因此自定义组件呈现为单选按钮组。

#### 1.3在本地预览和测试

现在，表单包含自定义组件，您可以代理表单并在本地对其进行更改并查看更改：

1. 转到终端并运行`aem up`。

2. 打开在`http://localhost:3000/{path-to-your-form}`启动的代理服务器（路径示例： `/content/forms/af/custom-component-form`）


### 2.为自定义组件实施自定义行为

#### 2.1设置自定义组件的样式

让我们将类&#x200B;**卡**&#x200B;添加到组件中以设置样式，并为每个无线电添加图像，为此使用以下代码。

**在cards.js中使用修饰函数设置自定义组件的样式**

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

**在cards.css中为自定义组件添加运行时行为**

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

现在，卡片组件显示如下：

![添加卡片css和js](/help/edge/docs/forms/universal-editor/assets/add-card-css.png)

#### 2.2使用Subscribe函数添加动态行为

更改下拉列表后，将获取卡片并将其设置在单选按钮组的枚举中。 但当前视图无法处理此情况。 因此，它呈现如下：

![订阅函数](/help/edge/docs/forms/universal-editor/assets/card-subscribe.png)

调用API时，它会设置字段模型，并且必须侦听更改并相应地呈现视图。 这是使用&#x200B;**subscribe函数**&#x200B;实现的。

让我们将上一步中的视图代码转换为函数，并在`cards.js`中的subscribe函数中调用它，如下所示：

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

**使用Subscribe函数监听cards.js中的事件更改**

现在，当您更改下拉列表时，信息卡会被填充，如下所示：

![订阅函数](/help/edge/docs/forms/universal-editor/assets/card-subscribe-final.png)

#### 2.3正在将视图更新与字段模型同步

要将视图更改同步到“模型”字段，必须设置选定卡片的值。 因此，在cards.js中添加以下更改事件侦听器，如下所示：

**在cards.js中使用字段模型API**

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

现在会显示自定义卡组件，如下所示：

![卡自定义组件](/help/edge/docs/forms/universal-editor/assets/cc-ue-card-component.png)

### 3.提交和推送更改

为自定义组件实施JavaScript和CSS并在本地验证后，提交更改并将其推送到Git存储库。

```bash
git add . && git commit -m "Add card custom component" && git push
```

您仅需几个简单步骤即可成功创建复杂的自定义信息卡选择组件。

+++ **创建自定义组件的手动或传统方法**

传统的方法是手动执行以下步骤：

1. **选择要扩展的OOTB组件**（例如，按钮、下拉列表、文本输入等）。 在这种情况下，请扩展单选按钮组件。

2. **在**&#x200B;中创建包含组件名称（在此例中为卡片）的文件夹`blocks/form/components`。

3. **添加同名JS文件**：
   - `blocks/form/components/cards/cards.js`。

4. （可选） **为自定义样式添加CSS文件**：
   - `blocks/form/components/cards/cards.css.`

5. **在与**&#x200B;组件JS文件` _cards.json` (**)相同的文件夹中定义新的JSON文件** （例如，`blocks/form/components/cards/_cards.json`）。 此JSON应扩展现有组件，并在其定义中，将`fd:viewType`设置为组件的名称（在此例中为卡片）：

   - 对于所有字段组（基本、验证、帮助等），请显式添加自定义字段。

6. **实施JS和CSS逻辑：**
   - 导出默认函数，如上所述。
   - 使用&#x200B;**element**&#x200B;参数修改基本HTML结构。
   - 如果需要，请使用标准字段数据的&#x200B;**fieldJson**&#x200B;参数。
   - 如果需要，可使用&#x200B;**subscribe**&#x200B;函数侦听字段更改或自定义事件。

     >[!NOTE]
     >
     >如上所述，为自定义组件实施JS和CSS逻辑。

7. 在表单生成器中将组件注册为变体并设置变体属性或
   将JSON中的`fd:viewType/:type`添加到组件的名称，例如，将`fd:viewType`中的`definitions[]`值作为卡片添加到具有`id="form`的对象的组件数组。

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

8. **更新mappings.js**：将组件名称添加到&#x200B;**OOTBComponentDecorators**（对于OOTB样式组件）或&#x200B;**customComponents**&#x200B;列表，以便系统能够识别并加载该组件。

   ```javascript
   let customComponents = ["cards"];
   const OOTBComponentDecorators = [];
   ```

9. **更新_form.json**：将组件的名称添加到`filters.components`数组，以便在创作UI中放置该组件。

   ```javascript
   "filters": [
   {
       "id": "form",
       "components": [ "cards"]}
       ]
   ```

10. **更新_component-definition.json**：在`models/_component-definition.json`中，通过以下方式使用对象`id custom-components`更新组中的数组：

   ```javascript
   {
   "...":"../blocks/form/components/cards/_cards.json#/definitions"
   }
   ```

   这是为了提供对将与其余组件一起构建的新卡组件的引用

11. **运行生成:json脚本**：执行`npm run build:json`以编译所有组件JSON定义并将其合并到单个文件中，以便从服务器提供服务。 这可确保在合并输出中包含新组件的架构。

12. 提交更改并将其推送到Git存储库。

现在，您可以将自定义组件添加到表单。

+++

## 创建复合组件

组合组件是通过组合多个组件创建的。
例如，条款和条件复合组件包含一个父面板，其中包含：

- 用于显示术语的纯文本字段

- 用于捕获用户协议的复选框

此组合结构在相应组件的JSON文件中定义为模板。 以下示例说明如何为条款和条件组件定义模板：

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

## 最佳实践

在创建您自己的自定义组件之前，请记住以下要点：

- **让组件逻辑保持集中**：仅添加/覆盖自定义行为所需的内容

- **利用基本结构**：使用OOTB HTML作为起点

- **使用可创作属性：**&#x200B;通过JSON架构公开可配置选项

- **命名空间CSS**：使用唯一的类名避免样式冲突

## 引用

- form-field-types：所有字段类型的基本HTML结构和属性。 [单击此处](/help/edge/docs/forms/eds-form-field-properties)查看详细的表单字段结构和属性。

- **块/表单/模型/表单组件**： OOTB和自定义组件属性定义。

- **块/表单/组件**：放置您的自定义组件。 例如： `blocks/form/components/countdown-timer/_countdown-timer.json`显示如何扩展基础组件和添加新属性。
