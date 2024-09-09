---
title: 使用规则向表单添加动态行为
description: AEM Forms的Edge Delivery Services旨在提供最佳性能，使您能够未来有效地收集数据和进行用户参与。 使用规则向您的表单添加动态行为
feature: Edge Delivery Services
exl-id: 58042016-e655-446f-a2bf-83f1811525e3
role: Admin, Architect, Developer
source-git-commit: 4a8153ffbdbc4da401089ca0a6ef608dc2c53b22
workflow-type: tm+mt
source-wordcount: '2218'
ht-degree: 98%

---

# 使用规则向您的表单添加动态行为

使用电子表格创建表单的强大功能之一，是能够使用内置电子表格函数来创建规则，允许您有条件地显示或隐藏表单字段、根据用户输入自动进行计算并且还能创建更加动态的用户体验。

本文将会指导您使用各种自适应表单块属性（主要为 [`Visible`](#visible-property)、[`Visibility Expression`](#visible-expression-property) 和 [`Value Expression`](#value-expression-property) 属性）以及[电子表格函数](#spreadsheet-functions-for-rules)，以便为您的表单创建有效的规则。我们还会探讨一些示例来说明如何在实践中实施这些规则。

## 理解规则的构造

规则就像指令，告诉我们在不同情况下该做什么。规则通常具有以下结构：

* 条件：指定了规则适用的情况。可以把它们看做是一个需要回答的问题（是或否）。

* 操作：定义了当条件满足（真）或不满足（假）时发生的情况。


例如，当选中复选框时，显示电子邮件框：

* 条件：“您喜欢订阅杂志和活动信息吗？”复选框被选中。（是还是不是？）。此条件在表单的 `Visible` 属性中进行设置。
* 操作（真）：显示电子邮件。（如果是，则会发生什么情况）。 `Visibility Expression` 使用为 `visible` 属性定义的条件来动态显示字段。
* 操作（假）：隐藏电子邮件。（如果否，则会发生什么情况）。 `Visibility Expression` 使用为 `Value` 定义的条件来动态隐藏字段。

有关详细的分步说明，请参阅[根据条件显示/隐藏电子邮件字段](#example-1-conditional-email-field)


## 了解值、可见、可见性表达式和值表达式属性

### 可见属性

想象您的表单字段中有一个电灯开关。 `Visible` 属性就像是那个开关，可以控制字段在首次加载时是否在表单上可见。

* 真（就像电灯开关处于“开启”状态）：表单上显示该字段。
* 假（如电灯开关处于“关闭”状态）：表单上隐藏该字段。

您可以使用电子表格公式（包括 = 标记）来编写一个采用类似于电子表格的逻辑的公式来确定字段的可见性。您可以在此公式中使用表单中其他字段的值。例如，如果用户在注册类型字段中选择“个人”，则可以使用检查该值的公式隐藏电子邮件字段。

### 可见表达式属性（显示/隐藏字段）

 `Visible Expression` 属性允许您使用添加到 `Visible` 属性的规则来决定是否根据用户交互情况来显示或隐藏该字段。

使用 `=FORMULATEXT("Address of the corresponding Visible property)` 将 `Visible` 属性中提到的公式作为字符串带到 `Visible Expression` 属性字段。这对于动态显示/隐藏已发布表单中的字段是必需的。

![Forumaltext](/help/edge/assets/aem-forms-formulatext.png)

### 值属性（设置初始数据）

想象一下房间灯光的调光开关上的预设值。`Value` 属性类似于这样的预设值，用于确定用户在字段中看到的数据的初始状态。它可以设置或检索表单字段内显示的当前数据。

首次加载表单时，`Value` 属性决定了用户在进行任何更改之前在字段中看到的内容。与控制可见性的 `Visible` 和 `Visible Expression` 属性不同，值属性可以直接对数据本身产生影响。用户可以通过键入、选择选项（下拉菜单）或与字段交互来修改该值。

您可以使用 Excel 公式（包括 = 标记）编写一个采用类似于电子表格的逻辑的公式来确定字段中显示的值。您可以在此公式中使用表单中其他字段的值。例如，您可以根据在另一个字段中输入的订单金额自动计算折扣。


### 值表达式属性（计算要在字段中显示的值）

此属性允许您根据公式控制字段内显示的值，这类似于可见表达式。想象一下在字段中内置一个计算器。

使用 `=FORMULATEXT("Address of the corresponding Value property)` 将 `Value` 属性中提到的公式作为字符串带到 `Value Expression` 属性字段。这是动态计算并在发布的表单中显示计算值所必需的。

![Forumaltext](/help/edge/assets/aem-forms-formulatext-value.png)

为了巩固这些概念，我们来打个比方：

* 可见：将表单想象成一个房子“可见”属性就像是每个房间（字段）的灯光开关。您可以决定当有人进入房间（打开表单）时房间最初是亮着（可见）还是暗着（隐藏）。
* 可见表达式：这就像是一个运动传感器灯光开关。房间（字段）最初可能会很暗（隐藏），但如果有人走过（更改另一个字段的值），则公式（运动传感器）可以将其打开（显示字段）。
* 值：这就像是灯光的预设调光开关（字段内的初始数据）。然后用户可以调整亮度（修改值）。
* 值表达式：这就像是房间里某个产品的价格标签上内置的一个精美计算器（表单）。价格标签（字段）会根据公式显示最终价格（例如，在基础价格加上税费），该公式会使用其他信息，如基础价格（来自另一个字段的值）。

通过将这些属性与[电子表格函数](#spreadsheet-functions-for-rules)相结合，您便可以在表单中实现各种动态行为。

## 规则的电子表格函数

自适应表单块支持多种可用于创建规则的电子表格函数。以下是开箱即用 (out-of-the-box, OOTB) 的功能：

### 逻辑函数

* [NOT()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018452_715980110)：反转逻辑状态（TRUE 变为 FALSE，反之亦然）。
* [AND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#AND)：仅当所有指定条件都为 TRUE 时才返回 TRUE。
* [OR()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#OR)：如果指定的条件中至少有一个为 TRUE，则返回 TRUE。

### 条件函数

* [IF()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#__RefHeading__1018446_715980110)：计算条件，如果为 TRUE，则返回特定值，如果为 FALSE，则返回另一个值。

### 数学函数

* [SUM()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#SUM)：从指定的单元格区域添加值。
* [ROUND()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#ROUND)：将数字四舍五入到指定的小数位数。
* [MIN()](https://docs.oasis-open.org/office/v1.2/os/OpenDocument-v1.2-os-part2.html#MIN)：返回指定单元格范围内的最小值。

## 创建规则

让我们深入研究一些实际的例子来说明如何使用规则来增强表单：

## 示例 1：有条件的电子邮件字段

此示例显示了复选框是如何充当条件的。当选择它时（条件为真），就会出现电子邮件框（为真时的操作）。如果未选择（条件为假），则电子邮件框保持隐藏状态（为假时的操作）。

创建一个带有复选框和电子邮件框的表单，如下图所示：

![有条件的电子邮件表单](/help/edge/assets/aem-forms-conditional-email-form.png)


以下是如何使用规则在选择复选框时显示电子邮件字段：

1. 将复选框字段的 `Value` 属性设置为 `TRUE`。
1. 将复选框字段的 `Checked` 属性设置为 `FALSE`。这可以确保默认情况下不会选中该复选框。
1. 将电子邮件字段的 `Visible` 属性设置为 `=[address of Checked property of the checkbox field] = true()`。例如 `=Q11=TRUE()`。该公式会计算复选框是否被选中。如果选中该复选框，则公式计算结果为 TRUE。如果未选中复选框，则公式计算结果为 FALSE。



   当您将其设置为指向 `Checked` 属性时，`TRUE()` 函数会返回逻辑值，如果 `checked = false`，它会返回 false。如果 `checked=true`，它会返回 `true`。这可以确保电子邮件字段在默认情况下是隐藏的。


1. 将复选框字段的 `Visible Expression` 属性设置为 `=FORMULATEXT ((address of Visible property of the checkbox field))`。例如，`=FORMULATEXT((G12))`。FORMULATEXT() 函数会将公式作为输入，并会将公式本身作为文本字符串返回。这有助于使用表单中的公式。

   ![有条件的电子邮件字段](/help/edge/assets/aem-forms-visible-expression-formula-text.png)

1. 预览和发布表单。现在，选中复选框就会显示电子邮件字段，取消选中则会隐藏该字段，从而提供动态的用户体验。

   ![有条件的电子邮件](/help/edge/assets/aem-forms-coditional-email.gif)


## 示例 2：自动计算

此示例显示了表单如何在选择旅行日期时自动计算预计旅行费用。

创建一个表单，其中包含日期字段、房间预算、预计旅行费用字段（如下所示）和电子邮件框（如下图所示）：

![有条件的电子邮件表单](/help/edge/assets/aem-forms-automatic-calculations-form.png)

以下是如何使用自动计算功能来显示预计旅行费用：

1. 将 `amount` 字段的 `Value` 属性设置为 `=F6*DAYS(F3,F2)`。此公式根据 `Start Date` 和 `End Date` 计算天数，将天数与房间预算相乘，并将结果显示在 `Estimated Trip Cost` 字段中。

1. 将 `Estimated Trip Cost` 字段的 `Value Expression` 属性设置为 `=FORMULATEXT ((address of value property of the amount field))`。例如，`=FORMULATEXT(F7)`。FORMULATEXT() 函数会将公式作为输入，并会将公式本身作为文本字符串返回。这有助于使用表单中的公式。

1. 预览和发布表单。现在，当指定一个 `Start Date`、`End Date` 以及房间预算。`Estimated Trip Cost` 也是自动计算的。

## 电子表格函数示例


以下是一些常用电子表格函数的示例：

**逻辑函数：**

* **NOT()**：反转逻辑状态（TRUE 变为 FALSE，反之亦然）。

  示例：如果电子邮件字段留空，则隐藏“确认电子邮件”字段。

   1. 将“确认电子邮件”字段的 `Visible` 属性设置为 `=NOT(if('address of email field'=""))`。

      ![AEM Forms 隐藏确认电子邮件字段](/help/edge/assets/aem-forms-not-function-hide-email-field.png)


   1. 将“确认电子邮件”字段的可见表达式设置为 `=FORMULATEXT ((address of visible property of the Confirm Email field))`

      ![AEM Forms 可见表达式公式](/help/edge/assets/aem-forms-visible-expression-formula-text.png)


* AND()：仅当所有指定条件都为 TRUE 时才返回 TRUE。

   * 示例：仅当填写了所有必填字段时才启用“提交”按钮。

   1. 将“提交”按钮的 `Visible` 属性设置为：



      ```JavaScript
      =AND(NOT(address of `value` property of the `name` field = ""), NOT(address of `value` property of the `email` field = ""), NOT(address of `value` property of the `phone` field))
      ```

      例如，

      ```JavaScript
      =AND(NOT(F9=""), NOT(F12=""), NOT(F10=""))
      ```

   1. 将“确认电子邮件”字段的可见表达式设置为 

      ```JavaScript
      =FORMULATEXT ((address of visible property of the Confirm Email field))
      ```

      例如，

      ```JavaScript
      =FORMULATEXT(G14)
      ```

      此公式仅当所有字段（姓名、电子邮件、电话）都填写完毕（NOT(()) 对每个字段都返回 TRUE）时才显示“提交”按钮 (TRUE)，否则会隐藏该按钮 (AND(multiple FALSES) = FALSE)。

* OR()：如果指定的条件中至少有一个为 TRUE，则返回 TRUE。

   * 示例：如果用户输入任何适用的折扣券代码，则会应用折扣。

   1. 将“最终金额”字段的 `Visible` 属性设置为：


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

      如果用户输入优惠券代码 (couponCode = &quot;NewYearDiscount&quot;) 或 (couponCode = &quot;BlackFridaySale&quot;)，此公式将会计算 30％ 的折扣，否则会将折扣设置为 0。

**文本功能：**

* IF()：计算条件，如果为 TRUE，则返回特定值，如果为 FALSE，则返回另一个值。

   * 示例：根据所选产品类别显示自定义消息。

   1. 将 `message` 字段的 `Value` 属性设置为 `Only upto 7 kg check-in lagguage is allowed!`：

   1. 将 `message` 字段的 `Visible` 属性设置为：


      ```JavaScript
      =if(address of value property of chosen product category ="Economy", TRUE(), FALSE())
      ```

      例如，

      ```JavaScript
      =if(F5="Economy", TRUE(), FALSE())
      ```

   1. 将 `message` 字段的值表达式设置为

      ```JavaScript
      =FORMULATEXT ((address of value property of the final amount field))
      ```

      例如，

      ```JavaScript
      =FORMULATEXT(G15)
      ```

      此公式显示消息“仅允许携带最多 7 公斤的托运行李！”如果选择的类别是“经济”，则将消息字段留空。

**数学函数：**

* SUM()：从指定的单元格区域添加值。

  示例：计算购物车中商品的总价格。

  在“总成本”字段的值表达式中：
SUM(price * quantity)

  此公式假设每个项目的“价格”和“数量”都有单独的字段。它会将其相乘并使用 SUM() 将购物车中所有商品的总价格加起来。

* ROUND()：将数字四舍五入到指定的小数位数。

  示例：将计算出的折扣金额四舍五入到小数点后两位。

  在“折扣金额”字段的值表达式中（假设折扣在其他地方计算）：
ROUND(discount, 2)

  此公式会将折扣值四舍五入到小数点后两位。

* MIN()：返回指定单元格范围内的最小值。

  示例：根据所选国家/地区查找注册表单所要求的最低年龄。

  在“最低年龄”字段的值表达式中：
MIN(ageLimits[&quot;US&quot;], ageLimits[&quot;UK&quot;], ageLimits[&quot;France&quot;])

  此公式假设您有一个名为“ageLimits”的表格，其中存储了不同国家的最低年龄要求。它使用 MIN() 来找出其中最小的值。


此外，自适应表单块允许您通过创建[自定义函数](#creating-custom-functions)全面管理您的表单。自定义函数允许您定义自己的规则和逻辑，让您能够完全控制表单的行为。


## 创建和部署自定义函数

开箱即用 (OOTB) 自适应表单块可以实施许多[常见电子表格功能](#spreadsheet-functions-for-rules)。但是，为了对表单进行更精细的控制，您可以使用自适应表单块中的 Microsoft® Excel 或 Google 表中提供的任何 OOTB 函数。自适应表单块不包含 Microsoft® Excel 或 Google 表中可用的所有 OOTB 功能的实施。如果您需要任何此类功能，您可以开发具有类似语法的自定义函数来实现 Microsoft® Excel 或 Google Sheets 提供的功能。例如，您可以通过实施 [Microsoft® Excel&#39;s Year() 函数](https://support.microsoft.com/zh-Hans/office/calculate-age-113d599f-5fea-448f-a4c3-268927911b37#)来根据出生日期计算年龄。


### 创建自定义功能

自定义函数驻留在 `[Adaptive form block]/functions.js` 文件中。创建过程一般包括以下步骤：

* 函数声明：定义函数名称及其参数（它接受的输入内容）。
* 逻辑实施：编写概述函数执行的具体计算或操作的代码。
* 函数导出：通过从相关文件导出该函数，使您的规则内可以访问该函数。

### 例如：“年份”函数

此示例演示了两个模仿 Microsoft® Excel 的 YEAR() 函数来计算年龄的自定义函数：


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

要在表单中使用自定义函数：

1. **添加函数**：在 `[Adaptive form block]/functions.js` 文件中包含您的自定义函数。请记得将其添加到文件内的导出声明中。
1. **部署文件**：将更新后的 `functions.js` 文件部署到您的 GitHub 项目并验证是否成功构建。
1. **函数的使用**：访问使用 `Value`、 `Value Expression`、 `Visible` 或 `Visible Expression` 属性在表单电子表格中使用函数，这类似于任何其他 OOTB 支持的电子表格函数。
1. **预览表单**：使用 AEM Sidekick 预览具有新实施的功能的表单。

