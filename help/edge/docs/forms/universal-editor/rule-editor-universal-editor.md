---
title: 如何使用规则编辑器将规则应用于表单字段，从而为通过WYSIWYG创作创建的表单启用动态行为和复杂逻辑？
description: 通用编辑器中的规则编辑器允许您添加动态行为并将复杂的逻辑构建到表单中，而无需编码或编写脚本。
feature: Edge Delivery Services
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: c27b8e413c060de601a72a669d86c4add2a4167d
workflow-type: tm+mt
source-wordcount: '2111'
ht-degree: 5%

---


# 通用编辑器中的规则编辑器简介

您可以使用规则编辑器添加动态表单行为，该编辑器允许您创建规则。 这些规则实现了条件字段可视性，基于用户输入自动进行计算，并改善了总体用户体验。 通过简化表单填写流程，规则编辑器可帮助确保准确性和效率。

规则编辑器提供了一个直观的可视化界面，用于创建和管理规则。 其用户友好型方法使所有用户，甚至那些没有广泛技术专业知识的用户都可以访问它，从而允许他们在自己的表单中轻松地实施逻辑。

## 了解规则

规则是指导用户在特定条件下执行哪些操作的说明。

* **条件**：条件是用于评估某些内容是true还是false的检查或规则。 它回答的问题是：“这是否符合要求？”

* **操作**：当条件为true时，将执行操作。 它是根据条件评估触发的任务或行为。

规则通常遵循以下结构之一：

* **Condition-Action**：首先检查条件，然后执行操作。 在规则编辑器中，`When`规则类型强制使用`condition-action`结构。
* **Action-Condition**：先执行操作，然后检查条件。 规则编辑器中的`Set Value Of`和`Validate`规则类型强制实施`action-condition`结构。
* **Action-Condition-Alternate Action**：执行操作，检查条件，然后根据条件执行主操作或替代操作。 例如，默认情况下，`Show`的替代操作是`Hide`，`Enable`的替代操作是`Disable`。

例如，条件可能会检查用户是否在字段中输入了特定值，操作可能是显示或隐藏字段。
* **条件**：检查收入是否大于$50,000。
* **操作**：如果条件为true，则显示`Additional Deduction`字段；否则，执行替代操作：隐藏`Additional Deduction`字段。

有关详细的分步说明，请参阅[添加条件规则](#2-add-a-conditional-rule)。

## 如何启用规则编辑器扩展？

在通用编辑器中，默认情况下不启用规则编辑器。 要为您的环境启用规则编辑器扩展，请使用您的请求将您的正式地址中的电子邮件发送至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)。

为您的环境启用规则编辑器扩展后，![edit-rules](/help/forms/assets/edit-rules-icon.svg)图标将显示在编辑器的右上角。

![通用编辑器规则编辑器](/help/edge/docs/forms/assets/universal-editor-rule-editor.png)

选择要为其编写规则的表单对象，然后单击![edit-rules](/help/forms/assets/edit-rules-icon.svg)图标。 此时将出现“规则编辑器”用户界面。

![规则编辑器用户界面](/help/edge/docs/forms/assets/rule-editor-for-field.png)

现在，您可以使用规则编辑器中的[可用规则类型](#available-rule-types-in-rule-editor)开始为所选表单字段编写规则或业务逻辑。

## 了解规则编辑器用户界面

单击![edit-rules](/help/forms/assets/edit-rules-icon.svg)图标后，将打开规则编辑器的可视编辑器：

![规则编辑器用户界面](/help/edge/docs/forms/assets/rule-editor-interface.png)

<table border="1">
  <thead>
    <tr>
      <th>规则编辑器的组件</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1.组件规则显示</td>
      <td>显示从中启动规则编辑器的表单对象的标题以及当前选定的规则类型。</td>
    </tr>
    <tr>
      <td>2.表单对象和函数</td>
      <td><b>Forms对象</b>选项卡显示表单中包含的所有对象的分层视图。 <b>函数</b>选项卡包含一组内置函数。</td>
    </tr>
    <tr>
      <td>3.表单对象和函数切换</td>
      <td>点按切换按钮可切换表单对象和函数窗格。</td>
    </tr>
    <tr>
      <td>4.可视规则编辑器</td>
      <td>可视规则编辑器是规则编辑器用户界面的可视编辑器模式中用于编写规则的区域。</td>
    </tr>
    <tr>
      <td>5. “完成”和“取消”按钮</td>
      <td><b>Done</b>按钮用于保存规则。 使用<b>取消</b>按钮可放弃对规则所做的任何更改并关闭规则编辑器。</td>
    </tr>
  </tbody>
</table>

选择表单对象时，会列出该对象上的任何现有规则。 您可以在可视规则编辑器中查看标题和预览规则摘要。 此外，您还可以更改规则的顺序、编辑规则、启用/禁用规则或删除规则。

![显示表单对象的可用规则](/help/edge/docs/forms/assets/rule-editor15.png)

## 可用的规则类型

规则编辑器提供了一组可用于编写规则的预定义规则类型，如下表所示：

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
      <td>根据是否满足指定的条件设置表单对象的值。</td>
    </tr>
    <tr>
      <td>清除值</td>
      <td>清除指定对象的值。</td>
    </tr>
    <tr>
      <td>隐藏/显示</td>
      <td>根据是否满足条件隐藏或显示表单对象。</td>
    </tr>
    <tr>
      <td>启用/禁用</td>
      <td>根据是否满足条件启用或禁用表单对象。</td>
    </tr>
    <tr>
      <td>验证</td>
      <td>验证表单或指定的对象。</td>
    </tr>
    <tr>
      <td>时间</td>
      <td>遵循<i>condition-action-alternate</i>操作规则构造或<i>condition-action</i>规则构造。 它指定评估条件，并在满足该条件时触发操作。</td>
    </tr>
    <tr>
      <td>格式化</td>
      <td>根据函数或正则表达式设置表单对象的格式。</td>
    </tr>
    <tr>
      <td>调用服务</td>
      <td>调用在表单数据模型(FDM)中配置的服务。</td>
    </tr>
    <tr>
      <td>设置属性</td>
      <td>根据条件设置指定对象的属性值。</td>
    </tr>
    <tr>
      <td>设置焦点</td>
      <td>设置对指定对象的焦点。</td>
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
      <td>添加/删除实例</td>
      <td>添加或删除指定可重复面板或表格行的实例。</td>
    </tr>
    <tr>
      <td>导航到</td>
      <td>导航到其他自适应Forms、其他资源（如图像或文档片段）或外部URL。</td>
    </tr>
    <tr>
      <td>分派事件</td>
      <td>根据预定义的条件或事件触发特定操作。</td>
    </tr>
    <tr>
      <td>在面板之间导航</td>
      <td>允许在表单的不同面板之间切换焦点。</td>
    </tr>
  </tbody>
</table>


现在，我们来探索如何在规则编辑器中[编写规则](#write-rules)。

## 写入规则

要了解如何在可视规则编辑器中编写规则，下面举一个简单的计税表单示例：

![规则编辑器示例](/help/edge/docs/forms/assets/rule-editor-1.png)

按照上述形式，用户输入薪金总额。 根据此输入，显示条件字段并计算应缴税金。

**表单字段：**
* 薪金总额（用户输入）
* 附加扣款（条件字段）
* 应纳税收入（计算字段）
* 应付税（计算字段）

**条件规则：**
* 条件：薪金毛额> 50,000
* 操作：显示附加扣减额字段

**计算规则：**

* 应纳税所得=薪金总额 — 附加扣减额（如果适用）
* 应付税额=应纳税所得额*税率（为简单起见，假设固定税率为10%）

要编写规则，请执行以下步骤：

### 1.创建表单

在通用编辑器中创作表单：

1. 在通用编辑器中打开窗体以进行编辑。
1. 添加以下表单组件：
   * 计税表单（标题）
   * 薪金总额（文本输入）
   * 附加扣减（文本输入）
   * 应纳税所得（文本输入）
   * 应付税（文字输入）
   * 提交（“提交”按钮）
1. 通过打开表单字段`Properties`隐藏`Additional Deduction`表单字段。

   ![规则编辑器示例](/help/edge/docs/forms/assets/rule-editor2.png)

### 2.为表单字段添加条件规则

在创作完表单后，编写第一条规则以在总薪金超过$50,000时显示`Additional Deduction`字段。 要添加条件规则，请执行以下操作：

1. 在通用编辑器中打开窗体以进行编辑。
1. 在内容树中选择&#x200B;**[!UICONTROL Gross Salary]**&#x200B;组件，然后选择![edit-rules](/help/forms/assets/edit-rules-icon.svg)。
   ![规则编辑器示例1](/help/edge/docs/forms/assets/rule-editor3.png)
此时会显示可视规则编辑器界面。
1. 单击&#x200B;**[!UICONTROL 创建]**以启动规则编辑器。
   ![规则编辑器示例2](/help/edge/docs/forms/assets/rule-editor4.png)
默认情况下，选择`Set Value Of`规则类型。 虽然不能更改或修改所选对象，但可以使用规则下拉列表选择其他规则类型。\
   ![规则编辑器示例3](/help/edge/docs/forms/assets/rule-editor5.png)
1. 打开规则类型下拉列表，然后选择&#x200B;**[!UICONTROL When]**规则类型。
   ![规则编辑器示例4](/help/edge/docs/forms/assets/rule-editor6.png)
1. 选择&#x200B;**[!UICONTROL 选择状态]**&#x200B;下拉列表并选择&#x200B;**[!UICONTROL 大于]**。 出现&#x200B;**[!UICONTROL 输入数字]**字段。
   ![规则编辑器示例5](/help/edge/docs/forms/assets/rule-editor7.png)
1. 在&#x200B;**[!UICONTROL 输入规则中的数字]**&#x200B;字段中输入`50000`。
   ![规则编辑器示例6](/help/edge/docs/forms/assets/rule-editor8.png)
您已将条件定义为`When Gross Salary is greater than 50000`。 接下来，定义此条件为`True`时要执行的操作。
1. 在`Then`语句中，从&#x200B;**[!UICONTROL 选择操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 显示]**。
   ![规则编辑器示例7](/help/edge/docs/forms/assets/rule-editor9.png)
1. 从“表单对象”选项卡的&#x200B;**[!UICONTROL 放置对象上拖放**[!UICONTROL &#x200B;附加扣缴&#x200B;]**字段，或选择此处]**&#x200B;字段。 或者，选择&#x200B;**[!UICONTROL Drop对象或选择此处]**&#x200B;字段，然后从弹出菜单中选择&#x200B;**[!UICONTROL Additional Deduction]**字段，该菜单列出了表单中的所有表单对象。
   ![规则编辑器示例8](/help/edge/docs/forms/assets/rule-editor10.png)
1. 单击&#x200B;**[!UICONTROL 添加Else部分]**&#x200B;为&#x200B;**[!UICONTROL Gross Salary]**&#x200B;字段添加其他条件，以防您输入的薪金小于`50000`。
   ![规则编辑器示例9](/help/edge/docs/forms/assets/rule-editor11.png)
1. 从`Else`语句的&#x200B;**[!UICONTROL 选择操作]**&#x200B;下拉列表中选择&#x200B;**[!UICONTROL 隐藏]**。
   ![规则编辑器示例10](/help/edge/docs/forms/assets/rule-editor12.png)
1. 从“表单对象”选项卡的&#x200B;**[!UICONTROL 放置对象上拖放**[!UICONTROL &#x200B;附加扣缴&#x200B;]**字段，或选择此处]**&#x200B;字段。 或者，选择&#x200B;**[!UICONTROL Drop对象或选择此处]**&#x200B;字段，然后从弹出菜单中选择&#x200B;**[!UICONTROL Additional Deduction]**字段，该菜单列出了表单中的所有表单对象。
   ![规则编辑器示例11](/help/edge/docs/forms/assets/rule-editor13.png)
1. 选择&#x200B;**[!UICONTROL 完成]**以保存规则。
规则在规则编辑器中如下所示。
   ![规则编辑器示例12](/help/edge/docs/forms/assets/rule-editor14.png)

>[!NOTE]
>
> 或者，您可以在Additional Deduction字段上编写Show规则，而不是Gross Salary字段上的When规则，以实施相同的行为。

### 3.为表单字段添加计算规则

接下来，编写规则以计算`Taxable Income`，这是`Gross Salary`和`Additional Deduction`之间的差值（如果适用）。 要在&#x200B;**[!UICONTROL 应纳税所得]**&#x200B;字段中添加计算规则，请执行以下步骤：

1. 在创作模式下，选择&#x200B;**[!UICONTROL 应纳税所得]**&#x200B;字段并选择![编辑 — 规则](/help/forms/assets/edit-rules-icon.svg)图标。 接下来，选择&#x200B;**[!UICONTROL 创建]**以启动规则编辑器。
   ![规则编辑器示例13](/help/edge/docs/forms/assets/rule-editor16.png)
1. 选择&#x200B;**[!UICONTROL 选择选项]**&#x200B;并选择&#x200B;**[!UICONTROL 数学表达式]**。 用于编写数学表达式的字段打开。
   ![规则编辑器示例14](/help/edge/docs/forms/assets/rule-editor17.png)

1. 在数学表达式字段中：

   * 从Forms的“对象”选项卡中，选择或拖放第一个&#x200B;**[!UICONTROL 放置对象中的**[!UICONTROL  Gross Salary ]**字段，或选择此处]**&#x200B;字段。

   * 从&#x200B;**[!UICONTROL 选择运算符]**&#x200B;字段中选择&#x200B;**[!UICONTROL 减号]**。

   * 从“Forms对象”选项卡中选择或拖放另一个&#x200B;**[!UICONTROL 放置对象中的**[!UICONTROL &#x200B;附加扣缴&#x200B;]**字段，或选择此处]**字段。
     ![规则编辑器示例15](/help/edge/docs/forms/assets/rule-editor18.png)

1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存规则。

   现在，为`Tax Payable `字段添加一条规则，该规则是通过将应纳税收入乘以税率确定的。 为简单起见，假设固定税率为`10%`。

1. 在创作模式下，选择&#x200B;**[!UICONTROL 应付税]**&#x200B;字段并选择![编辑规则](/help/forms/assets/edit-rules-icon.svg)图标。 接下来，选择&#x200B;**[!UICONTROL 创建]**以启动规则编辑器。
   ![规则编辑器示例16](/help/edge/docs/forms/assets/rule-editor19.png)
1. 选择&#x200B;**[!UICONTROL 选择选项]**&#x200B;并选择&#x200B;**[!UICONTROL 数学表达式]**。 用于编写数学表达式的字段打开。
   ![规则编辑器示例17](/help/edge/docs/forms/assets/rule-editor20.png)
1. 在数学表达式字段中：

   * 从“Forms对象”选项卡中选择或拖放第一个&#x200B;**[!UICONTROL 放置对象中的**[!UICONTROL &#x200B;应纳税所得&#x200B;]**字段，或选择此处]**&#x200B;字段。

   * 从&#x200B;**[!UICONTROL 选择运算符]**&#x200B;字段中选择&#x200B;**[!UICONTROL 乘以]**。

   * 从&#x200B;**[!UICONTROL 选择选项]**&#x200B;字段中选择&#x200B;**数字**，并在&#x200B;**[!UICONTROL 输入数字]**&#x200B;字段中输入值为`10`。
     ![规则编辑器示例18](/help/edge/docs/forms/assets/rule-editor21.png)
1. 接下来，在表达式字段周围高亮显示的区域中选择，然后选择&#x200B;**[!UICONTROL 扩展表达式]**。
   ![规则编辑器示例19](/help/edge/docs/forms/assets/rule-editor22.png)
1. 在扩展表达式字段中，从&#x200B;**[!UICONTROL Select Operator]**&#x200B;字段中选择&#x200B;**[!UICONTROL 除以]**&#x200B;并从&#x200B;**[!UICONTROL Select Option]**&#x200B;字段中选择&#x200B;**[!UICONTROL Number]**。 然后在数字字段中指定`100`。
   ![规则编辑器示例20](/help/edge/docs/forms/assets/rule-editor23.png)
1. 选择&#x200B;**[!UICONTROL 完成]**&#x200B;以保存规则。

### 4.预览表单

现在，当您预览表单并输入&#x200B;**薪金总额**&#x200B;作为`60,000`时，将显示&#x200B;**额外扣减**&#x200B;字段，并相应地计算&#x200B;**应纳税所得**&#x200B;和&#x200B;**应付税**。

![预览表单](/help/edge/docs/forms/assets/rule-editor-form.png)

除了在函数输出下列出的现成函数（如Sum、Average）之外，您还可以[编写自定义函数](#create-a-custom-function)以实现复杂的业务逻辑。

## 规则编辑器中的自定义函数

Edge Delivery Services Forms支持自定义函数，这些函数允许用户定义JavaScript函数以实施复杂的业务规则。 自定义函数通过促进对输入数据的操作和处理来扩展表单的功能，以满足特定要求。

### 创建自定义功能

要创建自定义函数，请编辑`../[blocks]/form/functions.js`文件。 创建过程一般包括以下步骤：

* **函数声明**：定义函数名及其参数（它接受的输入）。
* **逻辑实现**：编写描述函数执行的特定计算或操作的代码。
* **函数导出**：通过从相关文件导出函数，使其可在规则中访问。


此示例演示了`getFullName`和`days`这两个自定义函数：

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

### 在规则编辑器中使用自定义函数

要在规则编辑器中使用自定义函数，请执行以下操作：

1. **添加函数**：在`../[blocks]/form/functions.js`文件中包含您的自定义函数。 请记得将它添加到文件中的`export`语句中。
1. **部署文件**：将更新后的 `functions.js` 文件部署到您的 GitHub 项目并验证是否成功构建。
1. **函数用法**：通过在&#x200B;**[!UICONTROL 选择操作]**&#x200B;字段中选择`Function Output`选项，访问表单的规则编辑器中的函数。

   规则编辑器中的![自定义函数](/help/edge/docs/forms/assets/custom-function-rule-editor.png)

1. **预览表单**：使用新实现的函数预览表单。

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
