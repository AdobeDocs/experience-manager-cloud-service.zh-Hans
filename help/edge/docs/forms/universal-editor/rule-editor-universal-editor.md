---
title: 如何使用规则编辑器将规则应用到表单字段，从而为使用所见即所得创作创建的表单实现动态行为和复杂逻辑？
description: 通用编辑器中的规则编辑器允许您在表单中添加动态行为和构建复杂逻辑，而无需编码或脚本。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
exl-id: 846f56e1-3a98-4a69-b4f7-40ec99ceb348
source-git-commit: 0410e1d16ad26d3169c01cca3ad9040e3c4bfc9f
workflow-type: tm+mt
source-wordcount: '2111'
ht-degree: 100%

---

# 通用编辑器中的规则编辑器介绍

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

在通用编辑器中，规则编辑器默认为未启用。要为您的环境启用规则编辑器扩展，请从您的工作邮件发送一封电子邮件至 [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)，其中附上您的请求。

为您的环境启用规则编辑器扩展后，![编辑-规则](/help/forms/assets/edit-rules-icon.svg)图标会出现在编辑器的右上角。

![通用编辑器规则编辑器](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)

选择要编写规则的表单对象，然后单击![编辑-规则](/help/forms/assets/edit-rules-icon.svg)图标。出现规则编辑器用户界面。

![规则编辑器用户界面](/help/edge/docs/forms/assets/rule-editor-for-field.png)

现在，您可以开始使用[规则编辑器中可用的规则类型](#available-rule-types-in-rule-editor)为所选表单字段编写规则或业务逻辑。

## 了解规则编辑器用户界面

单击![编辑-规则](/help/forms/assets/edit-rules-icon.svg)图标时，将打开规则编辑器的可视化编辑器：

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
      <td>1. 组件-规则显示</td>
      <td>显示启动规则编辑器的表单对象标题和当前选择的规则类型。</td>
    </tr>
    <tr>
      <td>2. 表单对象和函数</td>
      <td><b>表单对象</b>选项卡显示表单中包含的所有对象的分层视图。<b>函数</b>选项卡包含一组内置函数。</td>
    </tr>
    <tr>
      <td>3. 表单对象和函数切换</td>
      <td>点击切换按钮，可切换表单对象和功能窗格。</td>
    </tr>
    <tr>
      <td>4. 可视化规则编辑器</td>
      <td>可视化规则编辑器是规则编辑器用户界面可视化编辑器模式下编写规则的区域。</td>
    </tr>
    <tr>
      <td>5. 完成和取消按钮</td>
      <td><b>完成</b>按钮用于保存规则。<b>取消</b>按钮将放弃对规则所做的任何更改并关闭规则编辑器。</td>
    </tr>
  </tbody>
</table>

选择表单对象时，会列出该对象上的任何现有规则。您可以在可视化规则编辑器上查看标题并预览规则摘要。此外，您还可以更改规则顺序、编辑规则、启用/禁用规则或删除规则。

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
      <td>根据是否满足指定条件设置表单对象的值。</td>
    </tr>
    <tr>
      <td>清除值</td>
      <td>清除指定对象的值。</td>
    </tr>
    <tr>
      <td>隐藏/显示</td>
      <td>根据条件是否满足隐藏或显示表单对象。</td>
    </tr>
    <tr>
      <td>启用/禁用</td>
      <td>根据条件是否满足启用或禁用表单对象。</td>
    </tr>
    <tr>
      <td>验证</td>
      <td>验证表单或指定对象。</td>
    </tr>
    <tr>
      <td>时间</td>
      <td>遵循<i>条件-操作-替代</i>操作规则结构或<i>条件-操作</i>规则结构。指定评估条件，并在条件满足时触发操作。</td>
    </tr>
    <tr>
      <td>格式化</td>
      <td>根据函数或正则表达式格式化表单对象。</td>
    </tr>
    <tr>
      <td>调用服务</td>
      <td>调用表单数据模型（FDM）中配置的服务。</td>
    </tr>
    <tr>
      <td>设置属性</td>
      <td>根据条件设置指定对象的属性值。</td>
    </tr>
    <tr>
      <td>设置焦点</td>
      <td>在指定对象上设置焦点。</td>
    </tr>
    <tr>
      <td>保存表单</td>
      <td>保存表单。</td>
    </tr>
    <tr>
      <td>提交/重置表单</td>
      <td>提交或重置表单。</td>
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

要了解如何在可视化规则编辑器中编写规则，让我们以一个简单的税款计算表单为例：

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
   * 工资总额（文本输入）
   * 额外扣除（文本输入）
   * 应税收入（文本输入）
   * 应缴税款 (文本输入)
   * 提交（提交按钮）
1. 通过打开表单 `Properties`，隐藏 `Additional Deduction` 表单字段。

   ![规则编辑器示例](/help/edge/docs/forms/assets/rule-editor2.png)

### 2. 为表单字段添加条件规则

创作表单后，编写第一条规则，即只有当工资总额超过 50000 美元时才显示 `Additional Deduction` 字段。要添加条件规则：

1. 在通用编辑器中打开表单进行编辑。
1. 在内容树中选择&#x200B;**[!UICONTROL 工资总额]**&#x200B;组件，并选择![编辑-规则](/help/forms/assets/edit-rules-icon.svg)。
   ![规则编辑器示例 1](/help/edge/docs/forms/assets/rule-editor3.png)
出现可视化规则编辑器界面。
1. 单击&#x200B;**[!UICONTROL 创建]**启动规则编辑器。
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

1. 在创作模式下，选择&#x200B;**[!UICONTROL 应税收入]**&#x200B;字段，并选择![编辑-规则](/help/forms/assets/edit-rules-icon.svg)图标。接下来，选择&#x200B;**[!UICONTROL 创建]**启动规则编辑器。
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

1. 在创作模式下，选择&#x200B;**[!UICONTROL 应缴税款]**&#x200B;字段，并选择![编辑-规则](/help/forms/assets/edit-rules-icon.svg)图标。接下来，选择&#x200B;**[!UICONTROL 创建]**启动规则编辑器。
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

1. **预览表单**：预览具有新实施的功能的表单。

## 相关文章

{{see-also-rule-editor}}

## 另请参阅

* [适用于 AEM Forms 的 Edge Delivery Services 快速入门](/help/edge/docs/forms/tutorial.md)
* [使用 Google Sheets 或 Microsoft Excel 创建表单](/help/edge/docs/forms/create-forms.md)
* [设置您的 Google Sheets 或 Microsoft Excel 文件，即可开始接受数据](/help/edge/docs/forms/submit-forms.md)
* [发布您的表单并开始收集数据](/help/edge/docs/forms/publish-forms.md)
* [自定义表单的外观&#x200B;](/help/edge/docs/forms/style-theme-forms.md)
* [将可重复部分添加到表单&#x200B;](/help/edge/docs/forms/repeatable-forms.md)
* [提交表单后显示自定义感谢消息](/help/edge/docs/forms/thank-you-page-form.md)
* [Adaptive Form Block 组件及其属性](/help/edge/docs/forms/form-components.md)
* [实际使用监控](https://www.aem.live/developer/rum#authentication)
