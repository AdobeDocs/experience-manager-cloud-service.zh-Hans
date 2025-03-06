---
title: 如何使用规则编辑器将规则应用到表单字段，从而为使用所见即所得创作创建的表单实现动态行为和复杂逻辑？
description: 通用编辑器中的规则编辑器允许您在表单中添加动态行为和构建复杂逻辑，而无需编码或脚本。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 9127c58a72dc4942312907f9e8f0cdcc8de9aa4b
workflow-type: tm+mt
source-wordcount: '2214'
ht-degree: 96%

---


# 所见即所得创作中的规则编辑器简介

<span class="preview">此功能可通过提前访问计划使用。 要请求访问，请将包含您的GitHub组织名称和存储库名称的电子邮件(从您的官方地址发送到<a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> )。 例如，如果存储库URL为https://github.com/adobe/abc，则组织名称为adobe，存储库名称为abc。</span>


您可以使用规则编辑器添加动态表单行为，该编辑器允许您创建规则。这些规则可实现条件字段的可见性，根据用户输入进行自动计算，并改善整体用户体验。通过简化表单填写流程，规则编辑器有助于确保准确性和效率。

规则编辑器提供了用于创建和管理规则的直观可视化界面。它的用户友好型方法使所有用户都能使用，即使是那些没有丰富专业技术知识的用户，也能毫不费力地在表单中实施逻辑。

## 了解规则

规则是指导用户在特定条件下执行什么操作的指令。

* **条件**：条件是一种检查或规则，用于评估某事物是真还是假。它回答了下面的问题：“这符合要求吗？”

* **操作**：操作是指条件为真时发生的事情。它是根据条件评估而触发的任务或行为。

规则通常遵循下面的其中一个结构：

* **条件-操作**：先检查条件，然后执行操作。在规则编辑器中，`When` 规则类型强制执行 `condition-action` 结构。
* **操作-条件**：先执行操作，然后检查条件。`Set Value Of` 和规则编辑器中的 `Validate` 规则类型强制执行 `action-condition` 结构。
* **操作-条件-替代操作**：执行操作，检查条件，然后根据条件执行主要操作或替代操作。例如，默认情况下，`Show` 的替代操作是 `Hide`；而 `Enable` 的替代操作是 `Disable`。

例如，条件可以检查用户是否在某个字段中输入了某个值，而操作可以是显示或隐藏某个字段。
* **条件**：检查收入是否大于 50000 美元。
* **操作**：如果条件为真，则显示 `Additional Deduction` 字段；否则，执行替代操作：隐藏 `Additional Deduction` 字段。

有关详细的分步说明，请参阅[添加条件规则](#2-add-a-conditional-rule)。

## 如何启用规则编辑器扩展？

在通用编辑器中，规则编辑器扩展默认为未启用。要启用规则编辑器扩展，请使用您的官方电子邮件 ID 写信至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)。

为您的环境启用规则编辑器扩展后，![编辑-规则](/help/forms/assets/edit-rules-icon.svg)图标会出现在编辑器的右上角。

![通用编辑器规则编辑器](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)

选择要编写规则的表单组件，然后单击![编辑-规则](/help/forms/assets/edit-rules-icon.svg)图标。出现规则编辑器用户界面。

![规则编辑器用户界面](/help/edge/docs/forms/assets/rule-editor-for-field.png)

在本文中，`form object` 和 `form component` 可交替使用。

现在，您可以开始使用[规则编辑器中可用的规则类型](#available-rule-types-in-rule-editor)为所选表单字段编写规则或业务逻辑。

## 了解规则编辑器用户界面

单击![编辑-规则](/help/forms/assets/edit-rules-icon.svg)图标后，规则编辑器的编辑器打开：

![规则编辑器用户界面](/help/edge/docs/forms/assets/rule-editor-interface.png)

<table border="1">
  <thead>
    <tr>
      <th>规则编辑器组件</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1. 标题</td>
      <td>显示表单组件的标题和所选规则类型。例如，“输入工资总额”是一个文本框组件，选择了“时间”规则类型。 </td>
    </tr>
    <tr>
      <td>2. 表单对象和函数</td>
      <td><b>表单对象</b>选项卡显示表单中包含的所有组件的分层视图。在规则编辑器中，<b>函数</b>选项卡包含一组内置函数。</td>
    </tr>
    <tr>
      <td>3. 表单对象和函数切换</td>
      <td>切换按钮可交替显示或隐藏表单对象和函数窗格。 </td>
    </tr>
    <tr>
      <td>4. 可视化规则编辑器</td>
      <td>可视化规则编辑器是为表单组件创建规则的界面。</td>
    </tr>
    <tr>
      <td>5. 完成和取消按钮</td>
      <td><b>完成</b>按钮用于保存规则。<b>取消</b>按钮将放弃对规则所做的任何更改并关闭规则编辑器。</td>
    </tr>
  </tbody>
</table>

选择表单组件时，会列出该组件上的任何现有规则。您可以在规则编辑器上查看标题并预览规则摘要。此外，您还可以更改规则顺序、编辑规则、启用/禁用规则或删除规则。

![显示表单对象的可用规则](/help/edge/docs/forms/assets/rule-editor15.png)

## 可用规则类型

规则编辑器提供了一组预定义规则类型，您可以使用这些类型编写规则，如下表所示：

<table border="1">
  <thead>
    <tr>
      <th>规则类型</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>设置值</td>
      <td>根据是否满足指定条件设置表单组件的值。</td>
    </tr>
    <tr>
      <td>清除值</td>
      <td>清除指定表单组件的值。</td>
    </tr>
    <tr>
      <td>隐藏/显示</td>
      <td>根据条件是否满足隐藏或显示表单组件。</td>
    </tr>
    <tr>
      <td>启用/禁用</td>
      <td>根据条件是否满足启用或禁用表单组件。</td>
    </tr>
    <tr>
      <td>验证</td>
      <td>根据条件检查表单组件，如果不符合条件则显示错误。 </td>
    </tr>
    <tr>
      <td>时间</td>
      <td>指定评估条件，并在条件满足时触发操作。遵循<i>条件-操作-替代</i>操作规则结构或<i>条件-操作</i>规则结构。 </td>
    </tr>
    <tr>
      <td>格式化</td>
      <td> 当表单组件的值发生变化时，使用给定表达式修改表单组件的显示值。</td>
    </tr>
    <tr>
      <td>调用服务</td>
      <td>调用使用外部 API、表单数据模型或 RESTful Web 服务配置的服务。</td>
    </tr>
    <tr>
      <td>设置属性</td>
      <td>根据条件设置指定表单组件的属性值。</td>
    </tr>
    <tr>
      <td>设置焦点</td>
      <td>在指定的表单组件上设置焦点。</td>
    </tr>
    <tr>
      <td>保存表单</td>
      <td>允许用户使用“草稿和提交”表单门户组件将表单保存为草稿。 </td>
    </tr>
    <tr>
      <td>提交表单</td>
      <td>提交表单。</td>
    </tr>
    <tr>
      <td>重设表单</td>
      <td>重置表单。</td>
    </tr>
    <tr>
      <td>添加/移除实例</td>
      <td>添加或移除指定可重复面板或表格行的实例。</td>
    </tr>
    <tr>
      <td>导航至</td>
      <td>导航到其他自适应表单、其他资产（例如图像或文档片段）或外部 URL。</td>
    </tr>
    <tr>
      <td>分派事件</td>
      <td>根据预定义条件或事件触发特定操作。</td>
    </tr>
    <tr>
      <td>在面板之间导航</td>
      <td>允许在表单中的不同面板之间转移焦点。</td>
    </tr>
  </tbody>
</table>


现在，让我们浏览如何[在规则编辑器中编写规则](#write-rules)。

## 编写规则

要了解如何在可视规则编辑器中编写规则，下面举一个简单的计税表单示例：

![规则编辑器示例](/help/edge/docs/forms/assets/rule-editor-1.png)

在上述表单中，用户输入工资总额。根据此输入，显示条件字段并计算应缴税款。

**表单字段：**
* 工资总额（用户输入）
* 额外扣除（条件字段）
* 应税收入（计算字段）
* 应缴税款（计算字段）

**条件规则：**
* 条件：工资总额 > 50000
* 操作：显示额外扣除字段

**计算规则：**

* 应税收入=工资总额 - 额外扣除（如适用）
* 应缴税款 = 应税收入 * 税率（为简单起见，假设固定税率为 10%）

要编写规则，请执行以下步骤：

### 1. 创作表单

要在通用编辑器中创作表单：

1. 在通用编辑器中打开表单进行编辑。
1. 添加以下表单组件：
   * 税款计算表单（标题）
   * 工资总额（数字输入）
   * 额外扣除（数字输入）
   * 应税收入（数字输入）
   * 应缴税款 (数字输入)
   * 提交（提交按钮）
1. 通过打开表单 `Properties`，隐藏 `Additional Deduction` 表单字段。

   ![规则编辑器示例](/help/edge/docs/forms/assets/rule-editor2.png)

### 2. 为表单字段添加条件规则

创作表单后，编写第一条规则，即只有当工资总额超过 50000 美元时才显示 `Additional Deduction` 字段。要添加条件规则：

1. 在通用编辑器中打开要编辑的表单，在内容树中选择&#x200B;**[!UICONTROL 工资总额]**&#x200B;字段，然后选择![编辑-规则](/help/forms/assets/edit-rules-icon.svg)。或者，也可以直接从&#x200B;**[!UICONTROL 表单对象]**&#x200B;窗格中选择&#x200B;**[!UICONTROL 工资总额]**字段。
   ![规则编辑器示例 1](/help/edge/docs/forms/assets/rule-editor3.png)
出现可视化规则编辑器界面。
1. 单击&#x200B;**[!UICONTROL 创建]**以创建规则。
   ![规则编辑器示例 2](/help/edge/docs/forms/assets/rule-editor4.png)
默认情况下，已选择 `Set Value Of` 规则类型。虽然不能更改或修改所选对象，但可以使用规则下拉列表选择其他规则类型。\
   ![规则编辑器示例 3](/help/edge/docs/forms/assets/rule-editor5.png)
1. 打开规则类型下拉列表，并选择&#x200B;**[!UICONTROL 时间]**规则类型。
   ![规则编辑器示例 4](/help/edge/docs/forms/assets/rule-editor6.png)
1. 选择&#x200B;**[!UICONTROL 选择状态]**&#x200B;下拉列表，并选择&#x200B;**[!UICONTROL 大于]**。出现&#x200B;**[!UICONTROL 输入数字]**字段。
   ![规则编辑器示例 5](/help/edge/docs/forms/assets/rule-editor7.png)
1. 在规则&#x200B;**[!UICONTROL 输入数字]**&#x200B;字段中输入 `50000`。
   ![规则编辑器示例 6](/help/edge/docs/forms/assets/rule-editor8.png)
您已将条件定义为 `When Gross Salary is greater than 50000`。接下来，定义如果条件为 `True` 时要执行的操作。
1. 在 `Then` 声明中，从&#x200B;**[!UICONTROL 选择操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 显示]**。
   ![规则编辑器示例 7](/help/edge/docs/forms/assets/rule-editor9.png)
1. 从&#x200B;**[!UICONTROL 放置对象或选择此处]**&#x200B;字段上的“表单对象”选项卡拖放&#x200B;**[!UICONTROL 额外扣除]**&#x200B;字段。或者，从列出了表单中所有表单对象的弹出窗口菜单选择&#x200B;**[!UICONTROL 放置对象或选择此处]**&#x200B;字段，并选择&#x200B;**[!UICONTROL 额外扣除]**字段。
   ![规则编辑器示例 8](/help/edge/docs/forms/assets/rule-editor10.png)
1. 如果输入的工资低于 `50000`，单击&#x200B;**[!UICONTROL 添加其他部分]**&#x200B;为&#x200B;**[!UICONTROL 工资总额]**字段添加另一个条件。
   ![规则编辑器示例 9](/help/edge/docs/forms/assets/rule-editor11.png)
1. 在 `Else` 声明中，从&#x200B;**[!UICONTROL 选择操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 隐藏]**。
   ![规则编辑器示例 10](/help/edge/docs/forms/assets/rule-editor12.png)
1. 从&#x200B;**[!UICONTROL 放置对象或选择此处]**&#x200B;字段上的“表单对象”选项卡拖放&#x200B;**[!UICONTROL 额外扣除]**&#x200B;字段。或者，从列出了表单中所有表单对象的弹出窗口菜单选择&#x200B;**[!UICONTROL 放置对象或选择此处]**&#x200B;字段，并选择&#x200B;**[!UICONTROL 额外扣除]**字段。
   ![规则编辑器示例 11](/help/edge/docs/forms/assets/rule-editor13.png)
1. 选择&#x200B;**[!UICONTROL 完成]**保存规则。
规则编辑器中的规则显示如下。
   ![规则编辑器示例 12](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> 或者，您也可以在“额外扣除”字段上编写“显示”规则，而不是在“工资总额”字段上编写“时间”规则，以实施相同的行为。

### 3. 添加表单字段的计算规则

接下来，编写规则计算 `Taxable Income`，即 `Gross Salary` 和 `Additional Deduction` 之间的差值（如果适用）。要在&#x200B;**[!UICONTROL 应税收入]**&#x200B;字段添加计算规则，请执行以下步骤：

1. 在创作模式下，选择&#x200B;**[!UICONTROL 应税收入]**&#x200B;字段，并选择![编辑-规则](/help/forms/assets/edit-rules-icon.svg)图标。或者，也可以直接从&#x200B;**[!UICONTROL 表单对象]**&#x200B;窗格中选择&#x200B;**[!UICONTROL 应税收入]**&#x200B;字段。
1. 接下来，选择&#x200B;**[!UICONTROL 创建]**以创建规则。
   ![规则编辑器示例 13](/help/edge/docs/forms/assets/rule-editor16.png)
1. 选择&#x200B;**[!UICONTROL 选择选项]**，并选择&#x200B;**[!UICONTROL 数学表达式]**。打开用于编写数学表达式的字段。
   ![规则编辑器示例 14](/help/edge/docs/forms/assets/rule-editor17.png)

1. 在数学表达式字段中：

   * 从“表单对象”选项卡中选择或拖放第一个&#x200B;**[!UICONTROL 放置对象或在此处选择]**&#x200B;字段中的&#x200B;**[!UICONTROL 工资总额]**&#x200B;字段。

   * 从&#x200B;**[!UICONTROL 选择运算符]**&#x200B;字段中选择&#x200B;**[!UICONTROL 减号]**。

   * 从“表单对象”选项卡中选择或拖放另一个&#x200B;**[!UICONTROL 放置对象或在此处选择]**&#x200B;字段中的&#x200B;**[!UICONTROL 额外扣除]**字段。
     ![规则编辑器示例 15](/help/edge/docs/forms/assets/rule-editor18.png)

1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;保存规则。

   现在，为 `Tax Payable ` 字段添加规则，该规则由应税收入乘以税率确定。为简单起见，假设固定税率为 `10%`。

1. 在创作模式下，选择&#x200B;**[!UICONTROL 应缴税款]**&#x200B;字段，并选择![编辑-规则](/help/forms/assets/edit-rules-icon.svg)图标。接下来，选择&#x200B;**[!UICONTROL 创建]**以创建规则。
   ![规则编辑器示例 16](/help/edge/docs/forms/assets/rule-editor19.png)
1. 选择&#x200B;**[!UICONTROL 选择选项]**，并选择&#x200B;**[!UICONTROL 数学表达式]**。打开用于编写数学表达式的字段。
   ![规则编辑器示例 17](/help/edge/docs/forms/assets/rule-editor20.png)
1. 在数学表达式字段中：

   * 从“表单对象”选项卡中选择或拖放第一个&#x200B;**[!UICONTROL 放置对象或在此处选择]**&#x200B;字段中的&#x200B;**[!UICONTROL 应税收入]**&#x200B;字段。

   * 从&#x200B;**[!UICONTROL 选择运算符]**&#x200B;字段中选择&#x200B;**[!UICONTROL 乘以]**。

   * 从&#x200B;**[!UICONTROL 选择选项]**&#x200B;字段中选择&#x200B;**数字**，然后在&#x200B;**[!UICONTROL 输入数字]**&#x200B;字段中输入值 `10`。
     ![规则编辑器示例 18](/help/edge/docs/forms/assets/rule-editor21.png)
1. 接下来，选择表达式字段周围的突出显示区域，并选择&#x200B;**[!UICONTROL 扩展表达式]**。
   ![规则编辑器示例 19](/help/edge/docs/forms/assets/rule-editor22.png)
1. 在扩展表达式字段中，从&#x200B;**[!UICONTROL 选择运算符]**&#x200B;字段中选择&#x200B;**[!UICONTROL 除以]**，并从&#x200B;**[!UICONTROL 选择选项]**&#x200B;字段中选择&#x200B;**[!UICONTROL 数字]**。然后，在数字字段中指定 `100`。
   ![规则编辑器示例 20](/help/edge/docs/forms/assets/rule-editor23.png)
1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;保存规则。

### 4. 预览表单

现在，当您预览表单并将&#x200B;**工资总额**&#x200B;输入为 `60,000` 时，会出现&#x200B;**额外扣除**&#x200B;字段，并会相应地计算出&#x200B;**应税收入**&#x200B;和&#x200B;**应缴税款**。

![预览表单](/help/edge/docs/forms/assets/rule-editor-form.png)

除了“函数输出”下列出的现成函数（如总和、平均值）之外，您还可以[编写自定义函数](#create-a-custom-function)，实现复杂的业务逻辑。

## 规则编辑器中的自定义函数

Edge Delivery Services Forms 支持自定义函数，允许用户通过定义 JavaScript 函数来实现复杂的业务规则。自定义函数可扩展表单的功能，便于操作和处理输入的数据，以满足指定的要求。

### 创建自定义功能

要创建自定义函数，请编辑 `../[blocks]/form/functions.js` 文件。创建过程一般包括以下步骤：

* **函数声明**：定义函数名称及其参数（它接受的输入内容）。
* **逻辑实施**：编写概述函数执行的具体计算或操作的代码。
* **函数导出**：通过从相关文件导出该函数，使您的规则内可以访问该函数。


此示例演示了两个自定义函数 `getFullName` 和 `days`：

```JavaScript
/**
 * Get Full Name
 * @name getFullName Concats first name and last name
 * @param {string} firstname in Stringformat
 * @param {string} lastname in Stringformat
 * @return {string}
 */
function getFullName(firstname, lastname) {
  return `${firstname} ${lastname}`.trim();
}

/**
 * Calculate the number of days between two dates.
 * @param {*} endDate
 * @param {*} startDate
 * @name days Calculates the numebr of days between two dates
 * @returns {number} returns the number of days between two dates
 */
function days(endDate, startDate) {
  const start = typeof startDate === 'string' ? new Date(startDate) : startDate;
  const end = typeof endDate === 'string' ? new Date(endDate) : endDate;

  // return zero if dates are valid
  if (Number.isNaN(start.getTime()) || Number.isNaN(end.getTime())) {
    return 0;
  }

  const diffInMs = Math.abs(end.getTime() - start.getTime());
  return Math.floor(diffInMs / (1000 * 60 * 60 * 24));
}

// eslint-disable-next-line import/prefer-default-export
export { getFullName, days };
```
![添加自定义函数](/help/edge/docs/forms/assets/create-custom-function.png)

### 使用规则编辑器中的自定义函数

要在规则编辑器中使用自定义函数：

1. **添加函数**：在 `../[blocks]/form/functions.js` 文件中包含您的自定义函数。请记得将其添加到文件内的 `export` 声明中。
1. **部署文件**：将更新后的 `functions.js` 文件部署到您的 GitHub 项目并验证是否成功构建。
1. **函数的使用**：在&#x200B;**[!UICONTROL 选择操作]**&#x200B;字段中选择 `Function Output` 选项，访问表单规则编辑器中的函数。

   ![规则编辑器中的自定义函数](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

1. **预览表单**：预览具有新实施功能的表单。

## 附加信息

>[!NOTE]
>
> 在通用编辑器中，自定义函数脚本不支持静态和动态导入。您需要在 `../[blocks]/form/functions.js` 文件中添加完整代码。

本文提供了有关通用编辑器中可用规则编辑器的有限信息。要了解有关规则编辑器和自定义函数的更多信息，请参阅以下文章：

{{see-also-rule-editor}}

## 另请参阅

{{universal-editor-see-also}}
