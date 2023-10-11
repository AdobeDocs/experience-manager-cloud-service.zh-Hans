---
title: 如何使用规则编辑器将规则添加到表单字段以添加动态行为并将复杂逻辑构建到自适应表单？
description: 自适应Forms规则编辑器允许您添加动态行为并将复杂的逻辑构建到表单中，而无需编码或编写脚本。
feature: Adaptive Forms
role: User
level: Beginner, Intermediate
exl-id: 6fd38e9e-435e-415f-83f6-3be177738c00
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '6440'
ht-degree: 1%

---

# 将规则添加到自适应表单 {#adaptive-forms-rule-editor}

<span class="preview">Adobe 建议使用现代、可扩展的数据捕获[核心组件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，以[创建新的自适应表单](/help/forms/creating-adaptive-form-core-components.md)或[将自适应表单添加到 AEM Sites 页面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。这些组件代表有关创建自适应表单的重大改进，确保实现令人印象深刻的用户体验。本文介绍了使用基础组件创作自适应表单的旧方法。</span>

| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/rule-editor.html) |
| AEM as a Cloud Service | 本文 |

## 概述 {#overview}

规则编辑器功能使表单业务用户和开发人员能够编写关于自适应表单对象的规则。 这些规则根据预设条件、用户输入和用户对表单的操作，定义要在表单对象上触发的操作。 它有助于进一步简化表单填写体验，确保准确性和速度。

规则编辑器提供了用于编写规则的直观且简化的用户界面。 规则编辑器为所有用户提供可视编辑器。<!-- In addition, only for forms power users, rule editor provides a code editor to write rules and scripts. --> 您可以使用规则对自适应表单对象执行的一些关键操作包括：

* 显示或隐藏对象
* 启用或禁用对象
* 设置对象的值
* 验证对象的值
* 执行函数以计算对象的值
* 调用表单数据模型服务并执行操作
* 设置对象属性

<!-- Rule editor replaces the scripting capabilities in [!DNL Experience Manager 6.1 Forms] and earlier releases. However, your existing scripts are preserved in the new rule editor. For more information about working with existing scripts in the rule editor, see [Impact of rule editor on existing scripts](rule-editor.md#p-impact-of-rule-editor-on-existing-scripts-p). -->

添加到forms-power-users组的用户可以创建脚本并编辑现有脚本。 中的用户 [!DNL forms-users] 组可以使用脚本，但不能创建或编辑脚本。

## 了解规则 {#understanding-a-rule}

规则是操作和条件的组合。 在规则编辑器中，操作包括隐藏、显示、启用、禁用或计算表单中对象值等活动。 条件是对表单对象的状态、值或属性执行检查和操作而计算的布尔表达式。 根据值( `True` 或 `False`)的计算返回。

规则编辑器提供了一组预定义的规则类型（如When、Show、Hide、Enable、Disable、Set Value Of和Validate）以帮助您编写规则。 每个规则类型都允许您在规则中定义条件和操作。 本文档进一步详细说明了每种规则类型。

规则通常遵循以下结构之一：

**条件 — 操作** 在此构造中，规则首先定义条件，然后定义要触发的操作。 这种构造与编程语言中的if-then语句类似。

在规则编辑器中， **时间** 规则类型强制使用condition-action结构。

**操作-条件** 在此构造中，规则首先定义一个要触发的操作，后跟评估的条件。 此构造的另一个变量是操作条件-备用操作，它还定义了当条件返回 False 时触发的替代操作。

显示，隐藏、启用、禁用、设置值，以及验证规则编辑者中的规则类型可强制实施操作条件规则构造。 默认情况下，显示的替换操作是 &quot;隐藏&quot;，&quot;启用&quot; 是禁用的，相反方式。 您无法更改默认的替换操作。

>[!NOTE]
>
>可用的规则类型，包括您在规则编辑者中定义的条件和操作，也取决于您在其上创建规则的表单对象的类型。 规则编辑者仅显示有效的规则类型以及特定表单对象类型的写入条件和操作语句的选项。 例如，您不会看到验证、设置值、启用和禁用 panel 对象的规则类型。

有关规则编辑器中可用的规则类型的更多信息，请参阅 [规则编辑器中的可用规则类型](rule-editor.md#p-available-rule-types-in-rule-editor-p).

### 选择规则结构的准则 {#guidelines-for-choosing-a-rule-construct}

虽然您可以使用任何规则构建来实现大多数用例，但以下是选择一种构建而不是另一种构建的一些准则。 有关规则编辑器中可用规则的更多信息，请参阅 [规则编辑器中的可用规则类型](rule-editor.md#p-available-rule-types-in-rule-editor-p).

* 创建规则时，一个典型的经验法则是考虑您所编写规则的对象的上下文。 假定您要根据用户在字段A中指定的值隐藏或显示字段B。在这种情况下，您要评估字段A的条件，并根据它返回的值，触发字段B的操作。

  因此，如果您在字段B（评估条件的对象）上编写规则，请使用condition-action结构或When规则类型。 同样，在字段A上使用操作条件结构或显示或隐藏规则类型。

* 有时，您必须根据一个条件执行多个操作。 在这种情况下，建议使用条件 — 操作构造。 在此构造中，您可以计算一次条件并指定多个操作语句。

  例如，要根据检查用户在字段A中指定的值的条件隐藏字段B、C和D，请编写一条规则，其中在字段A上使用condition-action结构或When规则类型，并指定操作以控制字段B、C和D的可见性。否则，您需要在字段B、C和D上分别使用三个规则，其中每个规则都会检查条件，并显示或隐藏各自的字段。 在此示例中，在一个对象上编写When规则类型比在三个对象上编写Show或Hide规则类型更有效。

* 要根据多个条件触发操作，建议使用action-condition构造。 例如，要通过评估字段B、C和D的条件来显示和隐藏字段A，请在字段A上使用显示或隐藏规则类型。
* 如果规则包含一个条件的一个操作，则使用condition-action或action condition结构。
* 如果规则检查条件，并在字段中提供值或退出字段时立即执行操作，则建议在评估条件的字段中编写具有condition-action结构或When规则类型的规则。
* 当用户更改应用When规则的对象的值时，将评估When规则中的条件。 但是，如果您希望操作在服务器端更改时触发（如预填充值），则建议编写一个When规则以在字段初始化时触发操作。
* 在编写下拉列表、单选按钮或复选框对象的规则时，表单中这些表单对象的选项或值会在规则编辑器中预填充。

## 规则编辑器中的可用运算符类型和事件 {#available-operator-types-and-events-in-rule-editor}

规则编辑器提供了以下逻辑运算符和事件，您可以使用这些运算符和事件创建规则。

* **等于**
* **不等于**
* **开始于**
* **结束**
* **包含**
* **为空**
* **不为空**
* **已选择：** 当用户为复选框、下拉菜单单选按钮选择特定选项时，返回true。
* **已初始化（事件）：** 在浏览器中呈现表单对象时返回true。
* **已更改（事件）：** 当用户更改表单对象的输入值或选定选项时，返回true。
* **导航（事件）：** 当用户单击导航对象时返回true。 导航对象用于在面板之间移动。
* **步骤完成（事件）：** 完成规则的步骤时返回true。
* **提交成功（事件）：** 成功将数据提交到表单数据模型时返回true。
* **提交时出错（事件）：**  向表单数据模型提交数据失败时返回true。

## 规则编辑器中的可用规则类型 {#available-rule-types-in-rule-editor}

规则编辑器提供了一组可用于编写规则的预定义规则类型。 让我们详细了解一下每种规则类型。 有关在规则编辑器中编写规则的更多信息，请参阅 [写入规则](rule-editor.md#p-write-rules-p).

### [!UICONTROL 时间] {#whenruletype}

此 **[!UICONTROL 时间]** 规则类型遵循 **condition-action-alternate action** 规则结构，或者有时只是 **condition-action** 构造。 在此规则类型中，首先指定求值的条件，然后指定满足该条件时要触发的操作( `True`)。 使用When规则类型时，您可以使用多个AND和OR运算符来创建 [嵌套表达式](#nestedexpressions).

使用When规则类型，您可以评估表单对象的条件，并对一个或多个对象执行操作。

在普通词语中，规则的典型结构如下：

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

对象 B 上的操作 2;
和
对象 C 上的操作 3;

_

如果您有多值组件（如单选按钮或列表），则在创建该组件的规则时，会自动检索选项，并将其提供给规则创建者使用。 您无需再次键入选项值。

例如，列表包含四个选项：红色、蓝色、绿色和黄色。 创建规则时，将自动检索选项（单选按钮）并使规则创建者可以使用此选项，如下所示：

![多值显示选项](assets/multivaluefcdisplaysoptions.png)

编写When规则时，可以触发Clear Value Of操作。 清除值操作清除指定对象的值。 通过在When语句中将Clear Value设置为选项，可以创建具有多个字段的复杂条件。

![清除值](assets/clearvalueof.png)

**[!UICONTROL 隐藏]** 隐藏指定的对象。

**[!UICONTROL 显示]** 显示指定的对象。

**[!UICONTROL 启用]** 启用指定的对象。

**[!UICONTROL 禁用]** 禁用指定的对象。

**[!UICONTROL 调用服务]** 调用在表单数据模型中配置的服务。 选择“调用服务”操作时，会出现一个字段。 点按该字段，它会显示您的网站上所有表单数据模型中配置的所有服务 [!DNL Experience Manager] 实例。 在选择表单数据模型服务时，会显示更多字段，您可以在其中将表单对象与指定服务的输入和输出参数进行映射。 请参阅调用表单数据模型服务的示例规则。

除了表单数据模型服务之外，您还可以指定直接WSDL URL来调用Web服务。 但是，表单数据模型服务具有许多好处，并且推荐调用服务的方法。

有关在表单数据模型中配置服务的更多信息，请参阅 [[!DNL Experience Manager Forms] 数据集成](data-integration.md).

**[!UICONTROL 设置值]** 计算并设置指定对象的值。 您可以将对象值设置为字符串、另一个对象的值、使用数学表达式或函数的计算值、对象的属性值或来自已配置表单数据模型服务的输出值。 当您选择Web服务选项时，它会显示您的页面上所有表单数据模型中配置的所有服务。 [!DNL Experience Manager] 实例。 在选择表单数据模型服务时，会出现更多字段，您可以在其中映射具有指定服务的输入和输出参数的表单对象。

有关在表单数据模型中配置服务的更多信息，请参阅 [[!DNL Experience Manager Forms] 数据集成](data-integration.md).

此 **[!UICONTROL 设置属性]** 规则类型允许您根据条件操作设置指定对象的属性值。 您可以将属性设置为以下项之一：
* 可见（布尔值）
* dorExclusion（布尔型）
* chartType（字符串）
* title（字符串）
* 已启用（布尔值）
* 必填（布尔值）
* validationsDisabled（布尔型）
* validateExpMessage（字符串）
* 值（数字、字符串、日期）
* 项（列表）
* 有效（布尔值）
* errorMessage（字符串）

例如，您可以定义规则以动态地将复选框添加到自适应表单。 您可以使用自定义函数、表单对象或对象属性来定义规则。

![设置属性](assets/set_property_rule_new.png)

要根据自定义函数定义规则，请选择 **[!UICONTROL 函数输出]** ，然后从以下位置拖放自定义函数： **[!UICONTROL 函数]** 选项卡。 如果满足条件操作，则自定义函数中定义的复选框数将添加到自适应表单中。

要根据表单对象定义规则，请选择 **[!UICONTROL 表单对象]** 从下拉列表中，拖放表单对象 **[!UICONTROL 表单对象]** 选项卡。 如果满足条件操作，则表单对象中定义的复选框数将添加到自适应表单。

通过基于对象属性的设置属性规则，您可以根据自适应表单中包含的其他对象属性在自适应表单中添加复选框的数量。

下图展示了一个根据自适应表单中的下拉列表数量动态添加复选框的示例：

![对象属性](assets/object_property_set_property_new.png)

**[!UICONTROL 清除值]** 清除指定对象的值。

**[!UICONTROL 设置焦点]** 设置对指定对象的焦点。

**[!UICONTROL 保存表单]** 保存表单。

**[!UICONTROL 提交Forms]** 提交表单。

**[!UICONTROL 重置表单]** 重置表单。

**[!UICONTROL 验证表单]** 验证表单。

**[!UICONTROL 添加实例]** 添加指定可重复面板或表行的实例。

**[!UICONTROL 删除实例]** 删除指定可重复面板或表行的实例。

**[!UICONTROL 导航到]** 导航到其他 <!--Interactive Communications,--> 自适应Forms、图像或文档片段等其他资源或外部URL。 <!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

### [!UICONTROL 设置值] {#set-value-of}

此 **[!UICONTROL 设置值]** 规则类型允许您根据是否满足指定的条件来设置表单对象的值。 该值可以设置为另一个对象的值、文本字符串、从数学表达式或函数派生的值、另一个对象的属性值或表单数据模型服务的输出。 同样，您可以检查组件、字符串、属性或从函数或数学表达式派生的值的条件。

此 **设置值** 规则类型并非适用于所有表单对象，例如面板和工具栏按钮。 标准的“设置值”规则具有以下结构：

将对象A的值设置为：

（字符串ABC） OR（对象C的对象属性X） OR（函数值） OR（数学表达式值） OR（数据模型服务或Web服务的输出值）；

时间（可选）：

（条件1和条件2和条件3）为 TRUE;

以下示例将字段中 `dependentid` 的值作为输入，并将字段的值 `Relation` 设置为表单数据模型服务的参数 `getDependent` 输出 `Relation` 。

![设置-值-web 服务](assets/set-value-web-service.png)

使用表单数据模型服务设置值规则的示例

>[!NOTE]
>
>此外，您可以使用规则的“设置值”从表单数据模型服务或Web服务的输出填充下拉列表组件中的所有值。 但是，请确保您选择的输出参数为数组类型。 数组中返回的所有值在指定的下拉列表中变为可用。

### [!UICONTROL 显示] {#show}

使用 **[!UICONTROL 显示]** 规则类型，您可以编写规则以根据是否满足条件来显示或隐藏表单对象。 显示规则类型也会在条件不满足或返回时触发“隐藏”操作 `False`.

典型的显示规则的结构如下所示：

`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`

### [!UICONTROL 隐藏] {#hide}

与显示规则类型类似，您可以使用 **[!UICONTROL 隐藏]** 规则类型，用于根据是否满足条件来显示或隐藏表单对象。 如果条件未得到满足或返回，则隐藏规则类型也会触发显示操作 `False`.

典型的“隐藏”规则的结构如下所示：

`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`

### [!UICONTROL 启用] {#enable}

此 **[!UICONTROL 启用]** 规则类型允许您根据是否满足条件启用或禁用表单对象。 启用规则类型还会触发禁用操作，以防条件未得到满足或返回 `False`.

典型的Enable规则的结构如下所示：

`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`

### [!UICONTROL 禁用] {#disable}

与启用规则类型类似， **[!UICONTROL 禁用]** 规则类型允许您根据是否满足条件启用或禁用表单对象。 禁用规则类型还会触发启用操作，以防条件未得到满足或返回 `False`.

典型的禁用规则的结构如下所示：

`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

### [!UICONTROL 验证] {#validate}

此 **[!UICONTROL 验证]** 规则类型使用表达式验证字段中的值。 例如，您可以编写一个表达式来检查用于指定名称的文本框是否不包含特殊字符或数字。

典型的验证规则的结构如下所示：

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>如果指定的值不符合验证规则，则可以为用户显示验证消息。 您可以在 **[!UICONTROL 脚本验证消息]** 侧栏中组件属性的字段。

![脚本验证](assets/script-validation.png)

### [!UICONTROL 设置选项] {#setoptionsof}

此 **[!UICONTROL 设置选项]** 规则类型允许您定义规则以动态地将复选框添加到自适应表单。 您可以使用表单数据模型或自定义函数来定义规则。

要根据自定义函数定义规则，请选择 **[!UICONTROL 函数输出]** ，然后从以下位置拖放自定义函数： **[!UICONTROL 函数]** 选项卡。 自定义函数中定义的复选框数将添加到自适应表单中。

![自定义函数](assets/custom_functions_set_options_new.png)

要创建自定义函数，请参见 [规则编辑器中的自定义函数](#custom-functions).

要根据表单数据模型定义规则，请执行以下操作：

1. 选择 **[!UICONTROL 服务输出]** 下拉列表中。
1. 选择数据模型对象。
1. 从中选择数据模型对象属性 **[!UICONTROL 显示值]** 下拉列表。 自适应表单中的复选框数派生自数据库中为该属性定义的实例数。
1. 从中选择数据模型对象属性 **[!UICONTROL 保存值]** 下拉列表。

![FDM设置选项](assets/fdm_set_options_new.png)

## 了解规则编辑器用户界面 {#understanding-the-rule-editor-user-interface}

规则编辑器提供了一个全面而简单的用户界面来编写和管理规则。 您可以在创作模式下从自适应表单中启动规则编辑器用户界面。

要启动规则编辑器用户界面，请执行以下操作：

1. 在创作模式下打开自适应表单。
1. 点按要为其编写规则的表单对象，然后在组件工具栏中点按 ![edit-rules](assets/edit-rules-icon.svg). 此时将显示规则编辑器用户界面。

   ![create-rules](assets/create-rules.png)

   此视图中列出了选定表单对象上的任何现有规则。 有关管理现有规则的信息，请参见 [管理规则](rule-editor.md#p-manage-rules-p).

1. 点按 **[!UICONTROL 创建]** 编写新规则。 默认情况下，首次启动规则编辑器时会打开规则编辑器用户界面的可视化编辑器。

   ![规则编辑器用户界面](assets/rule-editor-ui.png)

让我们详细了解一下规则编辑器UI的每个组件。

### A.组件规则显示 {#a-component-rule-display}

显示自适应表单对象的标题（通过自适应表单对象启动规则编辑器）和当前选定的规则类型。 在上述示例中，规则编辑器从名为Salary的自适应表单对象启动，并且选定的规则类型是When。

### B.表单对象和功能 {#b-form-objects-and-functions-br}

规则编辑器用户界面左侧的窗格包含两个选项卡： **[!UICONTROL Forms对象]** 和 **[!UICONTROL 函数]**.

“表单对象”选项卡显示自适应表单中包含的所有对象的分层视图。 它显示对象的标题和类型。 在编写规则时，可以将表单对象拖放到规则编辑器中。 在将对象或函数拖放到占位符中时，在创建或编辑规则时，占位符会自动采用相应的值类型。

应用了一个或多个有效规则的表单对象将标有绿点。 如果应用于表单对象的任意规则无效，则表单对象将标有黄点。

“函数”选项卡包含一组内置函数，例如“总和”、“最小值”、“最大值”、“平均值”、“数目”和“验证表单”。 您可以使用这些函数计算可重复面板和表格行中的值，并在编写规则时在操作和条件语句中使用它们。 但是，您可以创建 [自定义函数](#custom-functions) 也是。

![“函数”选项卡](assets/functions.png)

>[!NOTE]
>
>您可以在Forms的“对象”和“函数”选项卡中对对象和函数名称和标题执行文本搜索。

在表单对象的左侧树中，您可以点按表单对象以显示应用于每个对象的规则。 您不仅可以浏览各种表单对象的规则，还可以复制粘贴表单对象之间的规则。 有关更多信息，请参阅 [复制粘贴规则](rule-editor.md#p-copy-paste-rules-p).

### C.表单对象和功能切换 {#c-form-objects-and-functions-toggle-br}

点按切换按钮可切换表单对象和函数窗格。

### D.可视规则编辑器 {#visual-rule-editor}

可视规则编辑器是规则编辑器用户界面的可视编辑器模式中用于编写规则的区域。 它允许您选择规则类型并相应地定义条件和操作。 在规则中定义条件和操作时，您可以从表单对象和函数窗格中拖放表单对象和函数。

有关使用可视规则编辑器的更多信息，请参阅 [写入规则](rule-editor.md#p-write-rules-p).
<!-- 
### E. Visual-code editors switcher {#e-visual-code-editors-switcher}

Users in the forms-power-users group can access code editor. For other users, code editor is not available. If you have the rights, you can switch from visual editor mode to code editor mode of the rule editor, and vice versa, using the switcher right above the rule editor. When you launch rule editor the first time, it opens in the visual editor mode. You can write rules in the visual editor mode or switch to the code editor mode to write a rule script. However, note that if you modify a rule or write a rule in code editor, you cannot switch back to the visual editor for that rule unless you clear the code editor.

[!DNL Experience Manager Forms] tracks the rule editor mode you used last to write a rule. When you launch the rule editor next time, it opens in that mode. However, you can also configure a default mode to open the rule editor in the specified mode. To do so:

1. Go to [!DNL Experience Manager] web console at `https://[host]:[port]/system/console/configMgr`.
1. Click to edit **[!UICONTROL Adaptive Form Configuration Service]**.
1. choose **[!UICONTROL Visual Editor]** or **[!UICONTROL Code Editor]** from the **[!UICONTROL Default Mode for Rule Editor]** drop-down

1. Click **[!UICONTROL Save]**.
-->

### E.完成和取消按钮 {#done-and-cancel-buttons}

此 **[!UICONTROL 完成]** 按钮用于保存规则。 您可以保存不完整的规则。 但是，不完整部分无效，因此不会运行。 当您下次从同一表单对象启动规则编辑器时，会列出表单对象中已保存的规则。 您可以在该视图中管理现有规则。 有关更多信息，请参阅 [管理规则](rule-editor.md#p-manage-rules-p).

此 **[!UICONTROL 取消]** 按钮会放弃您对规则所做的任何更改并关闭规则编辑器。

## 写入规则 {#write-rules}

您可以使用可视规则编辑器编写规则 &lt;!> — 或代码编辑器>。 首次启动规则编辑器时，它将在可视编辑器模式下打开。 您可以切换到代码编辑器模式并编写规则。 但是，如果在代码编辑器中编写或修改规则，则除非清除代码编辑器，否则无法切换到该规则的可视编辑器。 当您下次启动规则编辑器时，它将在您最后创建规则时使用的模式下打开。

我们首先看一下如何使用可视编辑器编写规则。

### 使用可视编辑器 {#using-visual-editor}

让我们了解如何使用以下示例表单在可视编辑器中创建规则。

![Create-rule-example](assets/create-rule-example.png)

示例贷款申请表中的“贷款要求”部分要求申请人指定其婚姻状况、工资，如果已婚，还须指定其配偶的工资。 根据用户输入，规则将计算贷款资格金额，并显示在贷款资格字段中。 应用以下规则来实施方案：

* 配偶的“薪金”字段仅在婚姻状况为已婚时显示。
* 贷款资格金额为工资总额的50%。

要编写规则，请执行以下步骤：

1. 首先，根据用户为“婚姻状况”单选按钮选择的选项，编写规则以控制“配偶薪金”字段的可见性。

   以创作模式打开贷款申请表单。 点按 **[!UICONTROL 婚姻状况]** 组件和点按 ![edit-rules](assets/edit-rules-icon.svg). 下一步，点击 **[!UICONTROL 创建]** 以启动规则编辑器。

   ![write-rules-visual-editor-1](assets/write-rules-visual-editor-1.png)

   在启动规则编辑器时，默认情况下会选中When规则。 此外，从中启动规则编辑器的表单对象（在本例中为“婚姻状况”）在When语句中指定。

   虽然不能更改或修改所选对象，但可以使用如下所示的规则下拉列表选择其他规则类型。 如果要在其他对象上创建规则，请点按取消以退出规则编辑器，然后从所需的表单对象中再次启动该编辑器。

1. 点按 **[!UICONTROL 选择状态]** 下拉并选择 **[!UICONTROL 等于]**. 此 **[!UICONTROL 输入字符串]** 字段。

   ![write-rules-visual-editor-2](assets/write-rules-visual-editor-2.png)

   在“婚姻状况”单选按钮中， **[!UICONTROL 已婚]** 和 **[!UICONTROL 单身]** 已分配选项 **0** 和 **1** 个值。 您可以在“编辑”单选按钮对话框的“标题”选项卡中验证分配的值，如下所示。

   ![规则编辑器中的单选按钮值](assets/radio-button-values.png)

1. 在 **[!UICONTROL 输入字符串]** 字段中，指定 **0**.

   ![write-rules-visual-editor-4](assets/write-rules-visual-editor-4.png)

   您已定义条件 `When Marital Status is equal to Married`. 接下来，定义此条件为True时要执行的操作。

1. 在Then语句中，选择 **[!UICONTROL 显示]** 从 **[!UICONTROL 选择操作]** 下拉菜单。

   ![write-rules-visual-editor-5](assets/write-rules-visual-editor-5.png)

1. 拖放 **[!UICONTROL 配偶薪金]** 字段，该字段位于 **[!UICONTROL 放置对象或在此选择]** 字段。 或者，点按 **[!UICONTROL 放置对象或在此选择]** 字段并选择 **[!UICONTROL 配偶薪金]** 弹出式菜单中的字段，其中列出了表单中的所有表单对象。

   ![write-rules-visual-editor-6](assets/write-rules-visual-editor-6.png)

   规则在规则编辑器中如下所示。

   ![write-rules-visual-editor-7](assets/write-rules-visual-editor-7.png)

1. 点按 **[!UICONTROL 完成]** 以保存规则。

1. 如果婚姻状况为“单身”，请重复步骤1至5以定义另一个规则来隐藏“配偶薪金”字段。 规则在规则编辑器中如下所示。

   ![write-rules-visual-editor-8](assets/write-rules-visual-editor-8.png)

   >[!NOTE]
   >
   >或者，您可以在“配偶薪金”字段编写一个“显示”规则，而不是在“婚姻状况”字段编写两个“何时规则”，以实施相同的行为。

   ![write-rules-visual-editor-9](assets/write-rules-visual-editor-9.png)

1. 接下来，编写规则以计算贷款资格金额（占总薪金的50%），并在“贷款资格”字段中显示。 要实现此结果，请创建 **[!UICONTROL 设置值]** 贷款资格字段规则。

   在创作模式下，点按 **[!UICONTROL 贷款资格]** 字段并点按 ![edit-rules](assets/edit-rules-icon.svg). 下一步，点击 **[!UICONTROL 创建]** 以启动规则编辑器。

1. 选择 **[!UICONTROL 设置值]** 规则。

   ![write-rules-visual-editor-10](assets/write-rules-visual-editor-10.png)

1. 点按 **[!UICONTROL 选择选项]** 并选择 **[!UICONTROL 数学表达式]**. 用于编写数学表达式的字段打开。

   ![write-rules-visual-editor-11](assets/write-rules-visual-editor-11.png)

1. 在表达式字段中：

   * 从Forms的“对象”选项卡中选择或拖放 **[!UICONTROL 薪金]** 第一个字段中的字段 **[!UICONTROL 放置对象或在此选择]** 字段。

   * 选择 **[!UICONTROL 加号]** 从 **[!UICONTROL 选择运算符]** 字段。

   * 从Forms的“对象”选项卡中选择或拖放 **[!UICONTROL 配偶薪金]** 另一个字段中的 **[!UICONTROL 放置对象或在此选择]** 字段。

   ![write-rules-visual-editor-12](assets/write-rules-visual-editor-12.png)

1. 接下来，点按表达式字段周围高亮显示的区域，然后点按 **[!UICONTROL 扩展表达式]**.

   ![write-rules-visual-editor-13](assets/write-rules-visual-editor-13.png)

   在扩展表达式字段中，选择 **[!UICONTROL 除以]** 从 **[!UICONTROL 选择运算符]** 字段和 **[!UICONTROL 数字]** 从 **[!UICONTROL 选择选项]** 字段。 然后，指定 **[!UICONTROL 2]** 在数字字段中。

   ![write-rules-visual-editor-14](assets/write-rules-visual-editor-14.png)

   >[!NOTE]
   >
   >您可以从“选择选项”字段中使用组件、函数、数学表达式和属性值来创建复杂表达式。

   接下来，创建一个条件，当该条件返回True时，表达式将执行。

1. 点按 **[!UICONTROL 添加条件]** 添加When语句。

   ![write-rules-visual-editor-15](assets/write-rules-visual-editor-15.png)

   在When语句中：

   * 从Forms的“对象”选项卡中选择或拖放 **[!UICONTROL 婚姻状况]** 第一个字段中的字段 **[!UICONTROL 放置对象或在此选择]** 字段。

   * 选择 **[!UICONTROL 等于]** 从 **[!UICONTROL 选择运算符]** 字段。

   * 选择另一个中的字符串 **[!UICONTROL 放置对象或在此选择]** 字段并指定 **[!UICONTROL 已婚]** 在 **[!UICONTROL 输入字符串]** 字段。

   规则编辑器中的结果如下所示。  ![write-rules-visual-editor-16](assets/write-rules-visual-editor-16.png)

1. 点按 **[!UICONTROL 完成]**. 保存规则。

1. 重复步骤7至14，定义另一条规则，以计算婚姻状况为“单身”的贷款资格。 规则在规则编辑器中如下所示。

   ![write-rules-visual-editor-17](assets/write-rules-visual-editor-17.png)

>[!NOTE]
>
>或者，您可以使用设置值规则在您创建的When规则中计算贷款资格，以显示 — 隐藏“配偶薪金”字段。 当“婚姻状况”为“单身”时，生成的合并规则将在规则编辑器中显示如下。
>
>同样，您可以编写合并规则以控制“配偶薪金”字段的可见性，并在婚姻状况为“已婚”时计算贷款资格。

![write-rules-visual-editor-18](assets/write-rules-visual-editor-18.png)

<!-- ### Using code editor {#using-code-editor}

Users added to the forms-power-users group can use code editor. The rule editor auto generates the JavaScript code for any rule you create using visual editor. You can switch from visual editor to the code editor to view the generated code. However, if you modify the rule code in the code editor, you cannot switch back to the visual editor. If you prefer writing rules in code editor rather than visual editor, you can write rules afresh in the code editor. The visual-code editors switcher helps you switch between the two modes.

The code editor JavaScript is the expression language of Adaptive Forms. All the expressions are valid JavaScript expressions and use Adaptive Forms scripting model APIs. These expressions return values of certain types. For the complete list of Adaptive Forms classes, events, objects, and public APIs, see [JavaScript Library API reference for Adaptive Forms](https://helpx.adobe.com/experience-manager/6-5/forms/javascript-api/index.html).

For more information about guidelines to write rules in the code editor, see [Adaptive Form Expressions](adaptive-form-expressions.md).

While writing JavaScript code in the rule editor, the following visual cues help you with the structure and syntax:

* Syntax highlights

* Auto Indentation

* Hints and suggestions for Form objects, functions, and their properties

* Auto completion of form component names and common JavaScript functions

![javascriptruleeditor](assets/javascriptruleeditor.png)
-->

#### 规则编辑器中的自定义函数 {#custom-functions}

除了开箱即用的功能，例如 *总和* 列在函数输出下的自定义函数，您可以编写经常需要的自定义函数。 确保您编写的函数附带 `jsdoc` 高于它。

随附 `jsdoc` 为必填项：

* 如果您需要自定义配置和描述
* 因为有多种方法可以在中声明函数 `JavaScript,` 和注释可让您跟踪功能。

规则编辑器支持脚本和自定义函数的JavaScript ES2015语法。
有关更多信息，请参阅 [jsdoc.app](https://jsdoc.app/).

支持 `jsdoc` 标记：

* **私有**
语法： `@private`
专用函数未作为自定义函数包含在内。

* **名称**
语法： `@name funcName <Function Name>`
或者 `,` 您可以使用： `@function funcName <Function Name>` **或** `@func` `funcName <Function Name>`.
  `funcName` 是函数的名称（不允许有空格）。
  `<Function Name>` 是函数的显示名称。

* **会员**
语法： `@memberof namespace`
将命名空间附加到函数。

* **参数**
语法： `@param {type} name <Parameter Description>`
或者，您可以使用： `@argument` `{type} name <Parameter Description>` **或** `@arg` `{type}` `name <Parameter Description>`.
显示函数使用的参数。 一个函数可以有多个参数标记，每个参数按其出现顺序对应一个标记。
  `{type}` 表示参数类型。 允许的参数类型包括：

   1. 字符串
   1. 数字
   1. 布尔型
   1. 范围

  范围是指自适应表单的字段。 当表单使用延迟加载时，您可以使用 `scope` 以访问其字段。 在加载字段时或字段标记为全局时，您可以访问这些字段。

  所有参数类型均被归入上述参数类型之一。 不支持无。 确保选择以上类型之一。 类型不区分大小写。 参数中不允许有空格 `name`. `<Parameter Descrption>` `<parameter>  can have multiple words. </parameter>`

* **返回类型**
语法： `@return {type}`
或者，您可以使用 `@returns {type}`.
添加有关函数的信息，例如其目标。
{type} 表示函数的返回类型。 允许的返回类型包括：

   1. 字符串
   1. 数字
   1. 布尔型

  所有其他退货类型均归入上述任一类型下。 不支持无。 确保选择以上类型之一。 返回类型不区分大小写。

   * **此**
语法： `@this currentComponent`

  使用@this引用编写了规则的自适应表单组件。

  以下示例基于字段值。 在以下示例中，规则隐藏了表单中的字段。 此 `this` 部分 `this.value` 是指用于编写规则的底层自适应表单组件。

  ```
     /**
     * @function myTestFunction
     * @this currentComponent
     * @param {scope} scope in which code inside function is run.
     */
     myTestFunction = function (scope) {
        if(this.value == "O"){
              scope.age.visible = true;
        } else {
           scope.age.visible = false;
        }
     }
  ```

  >[!NOTE]
  >
  >使用自定义函数之前的注释进行摘要。 在遇到标记之前，摘要可以扩展到多行。 将大小限制为单个，以便在规则生成器中提供简要说明。

**添加自定义函数**

例如，要添加一个计算正方形区域的自定义函数。 侧边长度是自定义函数的用户输入，可使用表单中的数字框接受该输入。 计算的输出显示在表单的另一个数字框中。 要添加自定义函数，您必须先创建客户端库，然后将其添加到CRX存储库。

要创建客户端库并将其添加到CRX存储库中，请执行以下步骤：

1. 创建客户端库。 有关更多信息，请参阅 [使用客户端库](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/full-stack/clientlibs.html#developing).
1. 在CRXDE中，添加属性 `categories`字符串类型值为 `customfunction` 到 `clientlib` 文件夹。

   >[!NOTE]
   >
   >`customfunction`是一个示例类别。 您可以为在中创建的类别选择任意名称 `clientlib`文件夹。

在CRX存储库中添加客户端库后，在自适应表单中使用它。 它可让您在表单中将自定义函数用作规则。 要在自适应表单中添加客户端库，请执行以下步骤：

1. 在编辑模式下打开表单。
要在编辑模式下打开表单，请选择一个表单并点按 **[!UICONTROL 打开]**.
1. 在编辑模式下，选择一个组件，然后点按 ![字段级](assets/select_parent_icon.svg) > **[!UICONTROL 自适应表单容器]**，然后点击 ![cmppr](assets/configure-icon.svg).
1. 在侧栏中的“Name of Client Library”（客户端库名称）下，添加您的客户端库。 ( `customfunction` 在此示例中。)

   ![添加自定义函数客户端库](assets/clientlib.png)

1. 选择输入数字框，然后点击 ![edit-rules](assets/edit-rules-icon.svg) 以打开规则编辑器。
1. 点按 **[!UICONTROL 创建规则]**. 使用以下显示的选项，创建一个规则以在表单的“输出”字段中保存输入的平方值。

   [![使用自定义函数创建规则](assets/add_custom_rule_new.png)](assets/add-custom-rule.png)

1. 点按 **[!UICONTROL 完成]**. 您的自定义函数已添加。

   >[!NOTE]
   >
   > 要使用自定义函数从规则编辑器调用表单数据模型， [查看此处](/help/forms/using-form-data-model.md#invoke-services-in-adaptive-forms-using-rules-invoke-services).

#### 函数声明支持的类型 {#function-declaration-supported-types}

**函数语句**

```javascript
function area(len) {
    return len*len;
}
```

此函数包含但不包含 `jsdoc` 注释。

**函数表达式**

```javascript
var area;
//Some codes later
/** */
area = function(len) {
    return len*len;
};
```

**函数表达式和语句**

```javascript
var b={};
/** */
b.area = function(len) {
    return len*len;
}
```

**函数声明作为变量**

```javascript
/** */
var x1,
    area = function(len) {
        return len*len;
    },
    x2 =5, x3 =true;
```

限制：自定义函数仅从变量列表中选取第一个函数声明（如果同时选取）。 您可以对每个声明的函数使用函数表达式。

**函数声明作为对象**

```javascript
var c = {
    b : {
        /** */
        area : function(len) {
            return len*len;
        }
    }
};
```

>[!NOTE]
>
>确保使用 `jsdoc` 每个自定义函数。 尽管 `jsdoc`鼓励发表评论，包括空的 `jsdoc`用于将函数标记为自定义函数的注释。 它支持默认处理自定义函数。

## 管理规则 {#manage-rules}

当您点按表单对象并点按时，会列出该对象上的任何现有规则 ![edit-rules1](assets/edit-rules-icon.svg). 您可以查看标题并预览规则摘要。 此外，您还可以通过UI展开和查看完整的规则摘要、更改规则的顺序、编辑规则以及删除规则。

![List-rules](assets/list-rules.png)

您可以对规则执行以下操作：

* **展开/折叠**：规则列表中的内容列显示规则内容。 如果整个规则内容在默认视图中不可见，请点按 ![expand-rule-content](assets/Smock_ChevronDown.svg) 以将其展开。

* **重新排序**：您创建的任何新规则都会栈叠在规则列表的底部。 规则将从上到下执行。 顶部的规则先执行，然后是相同类型的其他规则。 例如，如果您分别从顶部开始，在第一、第二、第三和第四个位置执行When、Show、Enable和When规则，则顶部的When规则将首先执行，然后在第四个位置执行When规则。 然后，执行显示和启用规则。
您可以通过点按来更改规则的顺序 ![sort-rules](assets/sort-rules.svg) 或将其拖放到列表中的所需顺序。

* **编辑**：要编辑规则，请选中规则标题旁边的复选框。 将显示用于编辑和删除规则的选项。 点按 **[!UICONTROL 编辑]** 以在规则编辑器中打开选定的规则 <!-- in visual  or code editor mode depending on the mode used to create the rule -->.

* **删除**：要删除规则，请选择该规则并点按 **[!UICONTROL 删除]**.

* **启用/禁用**：您必须暂时暂停使用规则时，您可以选择一个或多个规则并点击 **[!UICONTROL 禁用]** “操作”工具栏中的以禁用它们。 如果禁用某个规则，则它不会在运行时执行。 要启用已禁用的规则，您可以选择该规则并点按操作工具栏中的启用。 规则的状态列显示规则是启用还是禁用。

![禁用规则](assets/disablerule.png)

## 复制粘贴规则 {#copy-paste-rules}

您可以将规则从一个字段复制粘贴到其他类似字段，以节省时间。

要复制粘贴规则，请执行以下操作：

1. 点按要从中复制规则的表单对象，然后在组件工具栏中点按 ![编辑规则](assets/edit-rules-icon.svg). 此时将显示规则编辑器用户界面，其中选定了表单对象，并显示现有规则。

   ![复制规则](assets/copyrule.png)

   有关管理现有规则的信息，请参见 [管理规则](rule-editor.md#p-manage-rules-p).

1. 选中规则标题旁边的复选框，将显示用于管理规则的选项。 点按&#x200B;**[!UICONTROL 复制]**。

   ![copyrule2](assets/copyrule2.png)

1. 选择要将规则粘贴到的其他表单对象，然后点击 **[!UICONTROL 粘贴]**. 此外，您可以编辑规则以对其进行更改。

   >[!NOTE]
   >
   >仅当表单对象支持复制的规则事件时，才能将规则粘贴到另一个表单对象。 例如，按钮支持click事件。 您可以将包含点击事件的规则粘贴到按钮，但不能粘贴到复选框。

1. 点按 **[!UICONTROL 完成]** 以保存规则。

## 嵌套表达式 {#nestedexpressions}

规则编辑器允许您使用多个AND和OR运算符创建嵌套规则。 您可以在规则中混合使用多个AND和OR运算符。

以下是嵌套规则的示例，该规则会在满足所需条件时向用户显示有关儿童监护权资格的消息。

![复杂表达式](assets/complexexpression.png)

您还可以拖放规则中的条件以进行编辑。 点按并悬停在手柄上( ![句柄](assets/drag-handle.svg))。 指针变为手形符号后（如下所示），将条件拖放到规则中的任意位置。 规则结构会发生变化。

![拖放](assets/drag-and-drop.png)

## 日期表达式条件 {#dateexpression}

规则编辑器允许您使用日期比较来创建条件。

以下是一个示例条件，当房屋抵押贷款已被抵押时，该条件会显示一个静态文本对象，用户通过填写日期字段来表示该条件。

当用户填写的财产抵押日期为过去时，自适应表单会显示有关收入计算的说明。 以下规则将用户填写的日期与当前日期进行比较，如果用户填写的日期早于当前日期，则表单将显示文本消息（名为Income）。

![日期表达式条件](assets/dateexpressioncondition.png)

如果填写日期早于当前日期，则表单会显示如下文本消息（收入）：

![满足日期表达式条件](assets/dateexpressionconditionmet.png)

## 数字比较条件 {#number-comparison-conditions}

规则编辑器可让您创建比较两个数字的条件。

下面是一个示例条件，它显示申请人在当前地址停留的月数小于36时的静态文本对象。

![数字比较条件](assets/numbercomparisoncondition.png)

当用户表示在当前居住地址居住不到36个月时，该表格显示可以请求更多居住证明的通知。

![已请求更多验证](assets/additionalproofrequested.png)

<!-- ## Impact of rule editor on existing scripts {#impact-of-rule-editor-on-existing-scripts}

In [!DNL Experience Manager Forms] versions prior to [!DNL Experience Manager 6.1 Forms] feature pack 1, form authors and developers used to write expressions in the Scripts tab of the Edit component dialog to add dynamic behavior to Adaptive Forms. The Scripts tab is now replaced by the rule editor.

Any scripts or expressions that you must have written in the Scripts tab are available in the rule editor. While you cannot view or edit them in visual editor, if you are a part of the forms-power-users group you can edit scripts in code editor. -->

## 示例规则 {#example}

### 调用表单数据模型服务 {#invoke}

考虑使用Web服务 `GetInterestRates` 它将贷款金额、使用期和申请人的信用评分作为输入，并返回包含EMI金额和利率的贷款计划。 您可以使用Web服务作为数据源来创建表单数据模型。 添加数据模型对象和 `get` 表单模型的服务。 该服务将显示在表单数据模型的“服务”选项卡中。 然后，创建一个自适应表单，其中包含数据模型对象中的字段，以捕获贷款金额、使用期和信用评分的用户输入。 添加触发Web服务获取计划详细信息的按钮。 输出将填充到相应的字段中。

以下规则显示了如何配置Invoke service操作以完成示例方案。

![Example-invoke-services](assets/example-invoke-services.png)

>[!NOTE]
>
>如果输入的类型为数组，则支持数组的字段在“输出”下拉部分下可见。

### 使用When规则触发多个操作 {#triggering-multiple-actions-using-the-when-rule}

在贷款申请表中，您要获取贷款申请人是否为现有客户。 根据用户提供的信息，客户ID字段应显示或隐藏。 此外，如果用户是现有客户，则还需要将焦点设置为“客户ID”字段。 贷款申请表包括以下组成部分：

* 单选按钮， **[!UICONTROL 您是否为Geometrixx现有客户？]**，它提供 [!UICONTROL 是] 和 [!UICONTROL 否] 选项。 “是”的值为 **0** 不是 **1**.

* 文本字段， **[!UICONTROL Geometrixx客户ID]**，以指定客户ID。

在用于实施此行为的单选按钮上编写When规则时，该规则在可视规则编辑器中如下所示。

![When-rule-example](assets/when-rule-example.png)

可视编辑器中的规则

在示例规则中，When部分中的语句是条件，当返回True时，该条件将执行Then部分中指定的操作。

<!-- The rule appears as follows in the code editor.

![when-rule-example-code](assets/when-rule-example-code.png) 

Rule in the code editor -->

### 在规则中使用函数输出 {#using-a-function-output-in-a-rule}

在采购订单表单中，您有下表，用户可在其中填写订单。 在此表中：

* 第一行是可重复的，因此用户可以订购多个产品并指定不同的数量。 其元素名称为 `Row1`.
* 可重复行的“产品数量”列中的单元格的标题为“数量”。 此单元格的元素名称为 `productquantity`.
* 表中的第二行是不可重复的，该行中“产品数量”列中的单元格的标题为“总数量”。

![Example-function-table](assets/example-function-table.png)

**答：** Row1 **B.** 数量 **C.** 总数量

现在，您要在所有产品的“产品数量”列中添加指定数量，并在“总数量”单元格中显示总和。 通过在“总数量”单元格中写入“设置值”规则，可以实现此总和，如下所示。

![Example-function-output](assets/example-function-output.png)

可视编辑器中的规则

<!-- he rule appears as follows in the code editor.

![example-function-output-code](assets/example-function-output-code.png)

Rule in the code editor -->

### 使用表达式验证字段值 {#validating-a-field-value-using-expression}

在上一个示例中说明的采购订单表单中，您需要限制用户订购任何数量超过此10000价的产品。 要执行此验证，您可以编写验证规则，如下所示。

![Example-validate](assets/example-validate.png)

可视编辑器中的规则

<!-- The rule appears as follows in the code editor.

![example-validate-code](assets/example-validate-code.png)

Rule in the code editor -->
