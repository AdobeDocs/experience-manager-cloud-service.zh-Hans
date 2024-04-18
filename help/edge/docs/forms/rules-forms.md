---
title: 使用规则向表单添加动态行为
description: AEM FormsEdge Delivery Services专为实现卓越性能而构建，使您能够预见简化数据收集和用户参与的未来。 使用规则向表单添加动态行为。
feature: Edge Delivery Services
exl-id: 58042016-e655-446f-a2bf-83f1811525e3
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: tm+mt
source-wordcount: '2216'
ht-degree: 0%

---

# 使用规则向表单添加动态行为

使用电子表格创建表单的强大功能之一是，能够使用内置电子表格函数创建规则，允许您有条件地显示或隐藏表单字段，根据用户输入自动执行计算，以及创建更动态的用户体验。

本文主要介绍如何使用各种自适应表单块属性 [`Visible`](#visible-property)， [`Visibility Expression`](#visible-expression-property) 和 [`Value Expression`](#value-expression-property) 属性以及 [电子表格函数](#spreadsheet-functions-for-rules) 以便为表单创建有效规则。 我们还将探索一些示例，以说明如何在实践中实施这些规则。

## 了解规则的结构

规则就像指示我们在不同情况下应该做什么的指令。 规则通常具有以下结构：

* 条件：用于指定应用规则的条件。 将它们视为需要回答的问题（是或否）。

* 操作：这些操作定义在满足(true)或不满足(false)条件时执行的操作。


例如，在选中复选框时，要显示电子邮件框，请执行以下操作：

* 条件： “是否要订阅杂志和活动？” 复选框处于选中状态。 （是或否？）。 此条件设定于 `Visible` 表单的属性。
* 操作(True)：显示电子邮件框。 （如果是，会发生什么情况）。 此 `Visibility Expression`  使用为定义的条件 `visible` 用于动态显示字段的属性。
* 操作(False)：电子邮件框处于隐藏状态。 （如果没有，会发生什么情况）。 此 `Visibility Expression`  使用为定义的条件 `Value` 以动态隐藏字段。

有关详细的分步说明，请参阅 [根据条件显示/隐藏电子邮件字段](#example-1-conditional-email-field)


## 了解“值”、“可见”、“可见性”表达式和“值”表达式属性

### 可见属性

想象一下，你的表单域有一个灯开关。 此 `Visible` 属性类似于开关，用于控制字段在首次加载时是否在表单上初始可见。

* True（如同灯开关处于“开”状态）：该字段显示在表单上。
* False（如同灯光开关处于“关闭”状态）：字段在表单上处于隐藏状态。

您可以使用电子表格公式（包括=标记）来编写公式，并使用类似电子表格的逻辑来确定字段的可见性。 您可以使用此公式中表单其他字段的值。 例如，如果用户在注册类型字段中选择“个人”，您可以使用检查该值的公式隐藏电子邮件字段。

### 可见表达式属性（显示/隐藏字段）

此 `Visible Expression` 属性允许您使用添加到中的规则 `Visible` 根据用户交互情况决定是显示还是隐藏字段的属性。

使用 `=FORMULATEXT("Address of the corresponding Visible property)` 将 `Visible` 将属性作为字符串添加到 `Visible Expression` 属性字段。 要在已发布的表单中动态显示/隐藏字段，必须填写此字段。

![Forumaltext](/help/edge/assets/aem-forms-formulatext.png)

### Value属性（设置初始数据）

想象一下，在调光开关上为房间灯光设置一个预设值。 此 `Value` 属性类似，可确定用户在字段中看到的数据的初始状态。  它会设置或检索表单字段中显示的当前数据。

首次加载表单时， `Value` 属性指定用户在进行任何更改之前在字段中看到的内容。 取消赞 `Visible` 和 `Visible Expression` 属性控制可见性，而Value属性直接影响数据本身。 用户可以通过键入、选择选项（下拉菜单）或与字段交互来修改此值。

您可以使用Excel公式（包括=标记）来编写公式，并使用类似电子表格的逻辑来确定字段中显示的值。 您可以使用此公式中表单其他字段的值。 例如，您可以根据在另一个字段中输入的订单金额自动计算折扣。


### 值表达式属性（计算要在字段中显示的值）

利用此属性，可根据公式控制字段中显示的值，与“可见表达式”类似。 想象一下这个领域内置了一个计算器。

使用 `=FORMULATEXT("Address of the corresponding Value property)` 将 `Value` 将属性作为字符串添加到 `Value Expression` 属性字段。 在已发布的表单中动态计算和显示计算值时需要此项。

![Forumaltext](/help/edge/assets/aem-forms-formulatext-value.png)

下面是巩固这些概念的类比：

* 可见：想象一个像房子一样的形状。 “Visible”属性类似于每个房间（字段）的灯光开关。 当有人进入房间（打开窗体）时，您可以决定房间最初是亮起（可见）还是暗起（隐藏）。
* Visible Expression（可见表达式）：这类似于运动传感器指示灯开关。 房间（字段）最初可能很暗（隐藏），但如果有人路过（更改另一个字段中的值），公式（运动传感器）可以将其打开（显示字段）。
* 值：这类似于灯光的预设调光开关（字段中的初始数据）。 然后，用户可以调整亮度（修改值）。
* 值表达式：这就像是在房屋（窗体）产品的价格标签中内置的花哨计算器。 价格标签（字段）根据公式（例如，将税添加至基本价格）显示最终价格，该公式使用基本价格（来自其他字段的值）等其他信息。

将这些属性与 [电子表格函数](#spreadsheet-functions-for-rules)，则可在表单中实现广泛的动态行为。

## 规则的电子表格函数

自适应Forms Block支持各种可用于创建规则的电子表格函数。 以下是现成可用的功能(OOTB)：

### 逻辑函数

* [NOT()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018452_715980110)：反转逻辑状态（TRUE变为FALSE，反之亦然）。
* [AND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#AND)：仅当指定的所有条件均为TRUE时，才返回TRUE。
* [或()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#OR)：如果指定的条件中至少有一个为TRUE，则返回TRUE。

### 条件函数

* [IF()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018446_715980110)：计算条件并返回特定值（如果为TRUE），以及另一个值（如果为FALSE）。

### 数学函数

* [SUM()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#SUM)：添加指定单元格范围内的值。
* [ROUND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#ROUND)：将数字舍入为指定的小数位数。
* [MIN()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#MIN)：返回指定单元格范围的最小值。

## 创建规则

我们来深入探讨一些实际示例，以说明如何使用规则来增强表单：

## 示例1：条件电子邮件字段

此示例说明复选框如何充当条件。 选中此复选框（条件为true）后，将显示电子邮件框（操作为true）。 如果未选中该复选框（条件为false），则电子邮件框将保持隐藏状态（操作为false）。

创建一个带有复选框和电子邮件框的表单，如下图所示：

![条件电子邮件表单](/help/edge/assets/aem-forms-conditional-email-form.png)


以下示例说明如何使用规则在复选框的选中上显示email字段：

1. 设置 `Value` 复选框字段的属性更改为 `TRUE`.
1. 设置 `Checked` 复选框字段的属性更改为 `FALSE`. 这将确保默认情况下未选中该复选框。
1. 设置 `Visible` 要发送的电子邮件的字段的属性 `=[address of Checked property of the checkbox field] = true()`. 例如 `=Q11=TRUE()`. 无论是否选中复选框，公式都会进行计算。 如果选中此复选框，则公式的计算结果为TRUE。 如果未选中复选框，则公式的计算结果为FALSE。



   此 `TRUE()` 函数中，返回将设置为指向的逻辑值 `Checked` 属性，如果 `checked = false` 它返回false。 如果 `checked=true`，它会返回 `true`. 这确保在默认情况下隐藏电子邮件字段。


1. 设置 `Visible Expression` 复选框字段的属性更改为 `=FORMULATEXT ((address of Visible property of the checkbox field))`. 例如，`=FORMULATEXT((G12))`。FORMULATEXT()函数将公式作为输入，并将公式本身作为文本字符串返回。 这有助于在表单中使用公式。

   ![条件电子邮件字段](/help/edge/assets/aem-forms-visible-expression-formula-text.png)

1. 预览和发布表单。 现在，选中复选框会显示电子邮件字段，但取消选中该复选框将隐藏该字段，从而提供动态用户体验。

   ![条件电子邮件](/help/edge/assets/aem-forms-coditional-email.gif)


## 示例2：自动计算

此示例说明在表单中选择行程日期时，表单如何自动计算预计行程成本。

创建一个表单，该表单具有如下所示的日期字段、房间预算、预计行程成本字段和电子邮件框（如下图所示）：

![条件电子邮件表单](/help/edge/assets/aem-forms-automatic-calculations-form.png)

以下是如何使用执行自动计算来显示预计行程成本：

1. 设置 `Value` 的属性 `amount` 字段至 `=F6*DAYS(F3,F2)`. 此公式计算天数 `Start Date`  和 `End Date`，与文件室预算相乘的天数，并且显示结果 `Estimated Trip Cost` 字段。

1. 设置 `Value Expression` 的属性 `Estimated Trip Cost` 字段至 `=FORMULATEXT ((address of value property of the amount field))`. 例如，`=FORMULATEXT(F7)`。FORMULATEXT()函数将公式作为输入，并将公式本身作为文本字符串返回。 这有助于在表单中使用公式。

1. 预览和发布表单。 现在，在指定 `Start Date`， `End Date`和房间预算。 此 `Estimated Trip Cost` 是自动计算的。

## 电子表格函数示例


以下是常用电子表格函数的一些示例：

**逻辑函数：**

* **NOT()：** 反转逻辑状态（TRUE变为FALSE，反之亦然）。

  示例：如果电子邮件字段留空，则隐藏“确认电子邮件”字段。

   1. 设置 `Visible` “Confirm Email”字段的属性 `=NOT(if('address of email field'=""))`.

      ![AEM Forms隐藏确认电子邮件字段](/help/edge/assets/aem-forms-not-function-hide-email-field.png)


   1. 将“Confirm Email”字段的可见表达式设置为 `=FORMULATEXT ((address of visible property of the Confirm Email field))`

      ![AEM Forms可见表达式公式](/help/edge/assets/aem-forms-visible-expression-formula-text.png)


* AND()：仅当指定的所有条件均为TRUE时才返回TRUE。

   * 示例：仅在填写了所有必填字段时启用“提交”按钮。

   1. 设置 `Visible` “submit”按钮的属性：



      ```JavaScript
      =AND(NOT(address of `value` property of the `name` field = ""), NOT(address of `value` property of the `email` field = ""), NOT(address of `value` property of the `phone` field))
      ```

      例如，

      ```JavaScript
      =AND(NOT(F9=""), NOT(F12=""), NOT(F10=""))
      ```

   1. 将“Confirm Email”字段的可见表达式设置为

      ```JavaScript
      =FORMULATEXT ((address of visible property of the Confirm Email field))
      ```

      例如，

      ```JavaScript
      =FORMULATEXT(G14)
      ```

      仅当填写了所有字段（姓名、电子邮件、电话）时，此公式才会显示“提交”按钮(TRUE)(NOT())为每个字段返回TRUE)，否则它会隐藏按钮(AND(multiple FALSES) = FALSE)。

* OR()：如果指定的条件中至少有一个为TRUE，则返回TRUE。

   * 示例：如果用户输入任何适用的折扣优惠券代码，则应用折扣。

   1. 设置 `Visible` “最终金额”字段的属性设置为：


  ```JavaScript
     =IF(OR(F14="BlackFridaySale", F14="NewYearDiscount"), (F6*DAYS(F3,F2)* 0.7) , (F6*DAYS(F3,F2)))
  ```

   1. 将“确认电子邮件”字段的值表达式设置为

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      例如，

      ```JavaScript
      =FORMULATEXT(F7)
      ```

      如果用户输入优惠券代码（优惠券代码=“NewYearDiscount”）或（优惠券代码=“BlackFridaySale”），则此公式会计算30%的折扣，否则会将折扣设置为0。

**文本函数：**

* IF()：计算条件并返回一个特定值（如果为TRUE），以及另一个值（如果为FALSE）。

   * 示例：显示基于所选产品类别的自定义消息。

   1. 设置 `Value` 的属性 `message` 字段至 `Only upto 7 kg check-in lagguage is allowed!`：

   1. 设置 `Visible` 的属性 `message` 字段至：


      ```JavaScript
      =if(address of value property of chosen product category ="Economy", TRUE(), FALSE())
      ```

      例如，

      ```JavaScript
      =if(F5="Economy", TRUE(), FALSE())
      ```

   1. 设置值表达式 `message` 字段至

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      例如，

      ```JavaScript
      =FORMULATEXT(G15)
      ```

      此公式显示消息“最多只允许使用7公斤的签到行李！” 如果选择的类是“经济”，否则将消息字段留空。

**数学函数：**

* SUM()：将指定单元格范围内的值相加。

  示例：计算购物车中商品的总成本。

  在“总成本”字段的值表达式中：SUM(price x quantity)

  此公式假定您对每个项目的“价格”和“数量”都有单独的字段。 它将其相乘，然后使用SUM()来合计购物车中所有项目的总成本。

* ROUND()：将数字舍入到指定的小数位数。

  示例：将计算的折扣金额四舍五入到两位小数。

  在“折扣金额”字段的值表达式中（假设在其他位置计算折扣）：ROUND(discount， 2)

  此公式将折扣值舍入到两位小数。

* MIN()：返回指定单元格范围的最小值。

  示例：根据选定的国家/地区查找注册表单所需的最低年龄。

  在“最小年龄”字段的值表达式中：MIN(ageLimits[“美国”]，年龄限制[“英国”]，年龄限制[“法国”])

  此公式假设您有一个名为“ageLimits”的表，用于存储不同国家/地区的最低年龄要求。 它使用MIN()来找出其中最小的值。


此外，自适应Forms Block允许您通过创建 [自定义函数](#creating-custom-functions). 自定义函数允许您定义自己的规则和逻辑，使您能够完全控制表单的行为。


## 创建和部署自定义函数

开箱即用(OOTB)自适应Forms块为许多应用程序提供实施 [常用电子表格函数](#spreadsheet-functions-for-rules). 但是，为了更精确地控制表单，您可以在自适应Forms块中使用Microsoft®Excel或Google Sheets中提供的任何OOTB函数。 自适应Forms块不包含Microsoft®Excel或Google Sheets中所有可用OOTB函数的实现。 如果您需要任何此类函数，可以使用类似语法开发自定义函数，以实现Microsoft®Excel或Google Sheets提供的功能。 例如，您可以实施 [Microsoft® Excel的Year()函数](https://support.microsoft.com/en-us/office/calculate-age-113d599f-5fea-448f-a4c3-268927911b37#) 从出生日期开始计算年龄。


### 创建自定义函数

自定义函数位于 `[Adaptive form block]/functions.js` 文件。 创建过程通常涉及以下步骤：

* 函数声明：定义函数名称及其参数（它接受的输入）。
* 逻辑实施：编写概述函数执行的特定计算或操作的代码。
* 函数导出：通过从相关文件导出函数，使其可在规则中访问。

### 示例： Year函数

此示例演示了两个模拟Microsoft的自定义函数®Excel的YEAR()函数来计算年龄：


```JavaScript
/**
 * Get the current date and time
 * @name now
 * @returns {Date} The current date and time as a Date object
 */
function now() {
  const today = new Date();
  return today;
}

/**
 * Get the year from a Date object
 * @name year
 * @param {Date} date The date object
 * @throws {TypeError} If the input is not a Date object
 * @returns {number} The year as a number
 */
function year(date) {
  let inputDate = new Date(date)

  if (!(inputDate instanceof Date)) {
    throw new TypeError("Input must be a Date object");
  }

  const year = inputDate.getFullYear();

  return year;
}

// Make the function accessible for use in rules
export { now, year };
```

### 在表单中使用自定义函数

要在表单中使用自定义函数，请执行以下操作：

1. **添加函数**：将您的自定义函数包含在 `[Adaptive form block]/functions.js` 文件。 请记住将其添加到文件中的导出语句中。
1. **部署文件**：部署更新的 `functions.js` 文件到GitHub项目，并验证是否已成功构建。
1. **函数用法**：使用访问表单电子表格中的函数 `Value`， `Value Expression`， `Visible`，或 `Visible Expression` 属性，类似于任何其他支持OOTB的电子表格函数。
1. **预览表单**：使用AEM Sidekick预览新实现的函数的表单。

