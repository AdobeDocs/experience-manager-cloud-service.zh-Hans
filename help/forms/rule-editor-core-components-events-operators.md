---
title: 在基于核心组件的自适应表单的规则编辑器中可用的各种运算符类型和事件是什么？
description: 自适应Forms规则编辑器支持各种运算符类型和事件。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner, Intermediate
source-git-commit: 780c68f0c21ef94ff6a73ce991370100b1a88db9
workflow-type: tm+mt
source-wordcount: '1921'
ht-degree: 1%

---


# 基于核心组件的自适应表单的规则编辑器中的运算符类型和事件

在AEM Forms as a Cloud中，规则编辑器包括各种运算符类型和事件，使您能够轻松定义和执行复杂的条件和操作。

自适应表单的规则编辑器中提供的运算符类型为构建精确条件提供了一个强大的框架。 它们允许您以逻辑和一致的方式处理数据、执行计算并组合多个条件。 无论您是比较值、执行算术运算还是处理字符串，这些运算符都可以确保您的规则既灵活又强大。

规则编辑器中的事件用作激活规则的触发器。 它们定义在满足某些条件时发生的具体操作。 利用不同类型的事件，您可以自动响应范围广泛的场景，例如用户交互、计划时间、数据更改和系统状态。 通过指定这些触发器，您可以创建符合您特定要求的动态响应规则。

通过了解并使用可用的运算符类型和事件，您可以释放规则编辑器的全部潜力，从而创建高效、有效的规则来满足独特需求并改进整体系统功能。

## 规则编辑器中的可用运算符类型和事件 {#available-operator-types-and-events-in-rule-editor}

规则编辑器提供了以下逻辑运算符和事件，您可以使用这些运算符和事件创建规则。

* **等于**
* **不等于**
* **开头为**
* **结尾为**
* **包含**
* **不包含**
* **为空**
* **不为空**
* **已选择：**&#x200B;当用户为复选框、下拉菜单单选按钮选择特定选项时，返回true。
* **已初始化（事件）：**&#x200B;当表单对象在浏览器中呈现时返回true。
* **Is Changed (event)：**&#x200B;当用户更改表单对象的输入值或选定选项时，返回true。

<!--
* **Navigation(event):** Returns true when the user clicks a navigation object. Navigation objects are used to move between panels. 
* **Step Completion(event):** Returns true when a step of a rule completes.
* **Successful Submission(event):** Returns true on successful submission of data to a form data model.
* **Error in Submission(event):**  Returns true on unsuccessful submission of data to a form data model. -->

### 规则编辑器中的可用规则类型 {#available-rule-types-in-rule-editor}

规则编辑器提供了一组可用于编写规则的预定义规则类型。 让我们详细看看每种规则类型。 有关在规则编辑器中编写规则的详细信息，请参阅 [编写规则](/help/forms/rule-editor-core-components-user-interface.md#write-rules)。

#### [!UICONTROL 时间] {#whenruletype}

**[!UICONTROL When]**&#x200B;规则类型遵循&#x200B;**condition-action-alternate action**&#x200B;规则结构，有时只遵循&#x200B;**condition-action**&#x200B;结构。 在此规则类型中，首先指定评估条件，然后指定满足该条件时要触发的操作(`True`)。 在使用When规则类型时，您可以使用多个AND和OR运算符来创建[嵌套表达式](/help/forms/rule-editor-core-components-usecases.md#nested-expressions)。

使用When规则类型，您可以评估表单对象的条件，并对一个或多个对象执行操作。

简单地说，典型的When规则的结构如下所示：

`When on Object A:`

`(Condition 1 AND Condition 2 OR Condition 3) is TRUE;`

`Then, do the following:`

`Action 2 on Object B;`
`AND`
&#39;对对象C执行操作3；

`Else, do the following:`

`Action 2 on Object C;`
_

当具有多值组件（如单选按钮或列表）时，在为该组件创建规则时，会自动检索选项并使这些选项可用于规则创建者。 您无需再次键入选项值。

例如，列表包含四个选项：红色、蓝色、绿色和黄色。 创建规则时，将自动检索选项（单选按钮）并使规则创建者可以使用此选项，如下所示：

![多值显示选项](assets/multivaluefcdisplaysoptions.png)

编写 When 规则时，可以触发“清除值”操作。 清除操作值 清除指定对象的值。 在 When 语句中将“清除值”作为一个选项，可以创建具有多个字段的复杂条件。 您可以添加 Else 语句以添加更多条件

![的明确值](assets/clearvalueof.png)

>[!NOTE]
>
> 当规则类型仅支持单级then-else语句时。

##### [!UICONTROL When]中允许使用多个字段 {#allowed-multiple-fields}

在&#x200B;**When**&#x200B;条件中，您可以选择添加应用规则的字段以外的其他字段。

例如，使用When规则类型，您可以评估不同表单对象上的条件并执行操作：

时间：

（对象A条件1）

和/或

（对象B条件2）

然后，执行以下操作：

对对象A执行操作1

_

![在When](/help/forms/assets/allowed-multiple-field-when.png)中允许使用多个字段

**在When条件功能**&#x200B;中使用允许多个字段时的注意事项

* [确保将核心组件设置为 3.0.14 或更高版本](https://github.com/adobe/aem-core-forms-components)，以便在规则编辑器中使用此功能。
* 如果规则应用于 When 条件内的不同字段，则即使仅更改其中一个字段，规则也会触发。


<!--
* It is not possible to add multiple fields in the When condition while applying rules to a button.

##### To enable Allowed Multiple fields in When condition feature

Allowed Multiple fields in When condition feature is disabled by default. To enable this feature, add a custom property at the template policy:

1. Open the corresponding template associated with an Adaptive Form in the template editor.
1. Select the existing policy as **formcontainer-policy**.
1. Navigate to the **[!UICONTROL Structure]**  view and, from the **[!UICONTROL Allowed Components]** list, open the **[!UICONTROL Adaptive Forms Container]** policy.
1. Go to the **[!UICONTROL Custom Properties]** tab and to add a custom property, click **[!UICONTROL Add]**.
1. Specify the **Group Name** of your choice. For example, in our case, we added the group name as **allowedfeature**.
1. Add the **key** and **value** pair as follows:
   * key: fd:changeEventBehaviour
   * value: deps
1. Click **[!UICONTROL Done]**. -->

如果“当条件”功能中允许的多个字段遇到任何问题，请按照以下步骤执行故障排除步骤：

1. 在编辑模式下打开表单。
1. 打开内容浏览器并选择 **[!UICONTROL 自适应表单的指南容器]** 组件。
1. 单击指南容器属性![指南属性](/help/forms/assets/configure-icon.svg)图标。这将打开“自适应表单容器”对话框。
1. 单击完成，然后再次保存对话框。

**[!UICONTROL 隐藏]**&#x200B;隐藏指定的对象。

**[!UICONTROL 显示]**&#x200B;显示指定的对象。

**[!UICONTROL 启用]**&#x200B;启用指定的对象。

**[!UICONTROL 禁用]**&#x200B;禁用指定的对象。

**[!UICONTROL 调用服务]**&#x200B;调用表单数据模型(FDM)中配置的服务。 选择“调用服务”操作时，会出现一个字段。 点按该字段时，会显示在[!DNL Experience Manager]实例上的所有表单数据模型(FDM)中配置的所有服务。 在选择表单数据模型服务时，会出现更多字段，您可以在其中映射具有指定服务的输入和输出参数的表单对象。 请参阅有关调用表单数据模型(FDM)服务的示例规则。

除了表单数据模型服务之外，您还可以指定直接WSDL URL来调用Web服务。 但是，表单数据模型服务具有许多好处，并且推荐调用服务的方法。

有关在表单数据模型(FDM)中配置服务的详细信息，请参阅[[!DNL Experience Manager Forms] 数据集成](data-integration.md)。

**[!UICONTROL 设置值]**&#x200B;计算并设置指定对象的值。 您可以将对象值设置为字符串、另一个对象的值、使用数学表达式或函数的计算值、对象的属性值或来自已配置表单数据模型服务的输出值。 当您选择Web服务选项时，它将显示在[!DNL Experience Manager]实例上的所有表单数据模型(FDM)中配置的所有服务。 在选择表单数据模型服务时，会出现更多字段，您可以在其中映射具有指定服务的输入和输出参数的表单对象。

有关在表单数据模型(FDM)中配置服务的详细信息，请参阅[[!DNL Experience Manager Forms] 数据集成](data-integration.md)。

**[!UICONTROL Set Property]**&#x200B;规则类型允许您根据条件操作设置指定对象的属性值。 您可以将属性设置为以下项之一：
* 可见（布尔值）
* label.value（字符串）
* label.visible（布尔值）
* description（字符串）
* 已启用（布尔值）
* readOnly（布尔值）
* 必需（布尔值）
* screenReaderText（字符串）
* 有效（布尔值）
* 错误消息（字符串）
* 默认值（数字、字符串、日期）
* enumNames （字符串[]）
* chartType（字符串）

例如，您可以定义规则以在单击按钮时显示文本框。 您可以使用自定义函数、表单对象、对象属性或服务输出来定义规则。

![设置属性](assets/set_property_rule_new.png)

要基于自定义函数定义规则，请从下拉列表中选择&#x200B;**[!UICONTROL 函数输出]**，然后从&#x200B;**[!UICONTROL 函数]**&#x200B;选项卡中拖放自定义函数。 如果满足条件操作，则文本输入框将可见。

要基于表单对象定义规则，请从下拉列表中选择&#x200B;**[!UICONTROL 表单对象]**，然后从&#x200B;**[!UICONTROL 表单对象]**&#x200B;选项卡中拖放表单对象。 如果满足条件操作，则文本输入框在自适应表单中可见。

通过基于对象属性的“设置属性”规则，您可以根据自适应表单中包含的其他对象属性在自适应表单中显示文本输入框。

下图展示了一个基于隐藏或显示自适应表单中的文本框动态启用该复选框的示例：

![对象属性](assets/object_property_set_property_new.png)

**[!UICONTROL 清除值]**&#x200B;清除指定对象的值。

**[!UICONTROL 设置焦点]** 将焦点设置在指定对象上。

**[!UICONTROL 提交表单]**&#x200B;提交表单。

**[!UICONTROL 重置]** 重置窗体或指定的对象。

**[!UICONTROL 验证]** 验证表单或指定的对象。

**[!UICONTROL 添加实例]** 添加指定的可重复面板或表格行的实例。

**[!UICONTROL 删除实例]** 删除指定的可重复面板或表行的实例。

**[!UICONTROL 函数输出]**&#x200B;根据预定义的函数或自定义函数定义规则。

**[!UICONTROL 导航到]**&#x200B;导航到其他自适应Forms、图像或文档片段等其他资源或外部URL。<!-- For more information, see [Add button to the Interactive Communication](create-interactive-communication.md#addbuttontothewebchannel). -->

**[!UICONTROL 调度事件]**&#x200B;根据预定义的条件或事件触发特定操作或行为。

#### [!UICONTROL 设置值] {#set-value-of}

]**规则类型的**[!UICONTROL &#x200B;设置值允许您根据是否满足指定的条件来设置表单对象的值。 该值可以设置为另一个对象的值、文本字符串、从数学表达式或函数派生的值、另一个对象的属性值或表单数据模型服务的输出。 同样，您可以检查组件、字符串、属性或从函数或数学表达式派生的值的条件。

**Set Value Of**&#x200B;规则类型不适用于所有表单对象，例如面板和工具栏按钮。 标准的“设置值”规则具有以下结构：

将对象A的值设置为：

（字符串ABC）或
（对象C的对象属性X）或
（函数中的值）或
（数学表达式中的值）或
（数据模型服务的输出值）；

时间（可选）：

（条件 1 和条件 2 和条件 3）为 TRUE;

下面的示例选择 as `True` 的值`Question2`并设置 as `correct`的值`Result`。

![Set-value-web-service](assets/set-value-web-service.png)

使用表单数据模型服务的设置值规则示例。

#### [!UICONTROL 节目] {#show}

使用&#x200B;**[!UICONTROL Show]**&#x200B;规则类型，您可以编写规则以根据条件是否满足来显示或隐藏表单对象。 Show规则类型还会触发Hide操作，以防条件不满足或返回`False`。

典型的显示规则的结构如下所示：

`Show Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Hide Object A;`

#### [!UICONTROL 隐藏] {#hide}

与“显示”规则类型类似，您可以使用&#x200B;**[!UICONTROL 隐藏]**&#x200B;规则类型，根据是否满足条件来显示或隐藏表单对象。 如果条件不满足或返回`False`，隐藏规则类型还会触发“显示”操作。

典型的“隐藏”规则的结构如下所示：

`Hide Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Show Object A;`

#### [!UICONTROL 启用] {#enable}

**[!UICONTROL 启用]**&#x200B;规则类型允许您根据条件是否满足来启用或禁用表单对象。 Enable规则类型也会在条件不满足或返回`False`时触发Disable操作。

典型的Enable规则的结构如下所示：

`Enable Object A;`

`When:`

`(Condition 1 AND Condition 2 AND Condition 3) is TRUE;`

`Else:`

`Disable Object A;`

#### [!UICONTROL 禁用] {#disable}

与“启用”规则类型类似，**[!UICONTROL 禁用]**&#x200B;规则类型允许您根据条件是否满足来启用或禁用表单对象。 Disable规则类型还会触发Enable操作，以防条件不满足或返回`False`。

典型的禁用规则的结构如下所示：

`Disable Object A;`

`When:`

`(Condition 1 OR Condition 2 OR Condition 3) is TRUE;`

`Else:`

`Enable Object A;`

#### [!UICONTROL 验证] {#validate}

**[!UICONTROL Validate]**&#x200B;规则类型使用表达式验证字段中的值。 例如，您可以编写表达式来检查用于指定名称的文本框是否不包含特殊字符或数字。

典型的验证规则的结构如下所示：

`Validate Object A;`

`Using:`

`(Expression 1 AND Expression 2 AND Expression 3) is TRUE;`

>[!NOTE]
>
>如果指定的值不符合验证规则，则可以为用户显示验证消息。 您可以在侧边栏中组件属性的&#x200B;**[!UICONTROL 脚本验证消息]**&#x200B;字段中指定消息。

![脚本验证](assets/script-validation.png)

<!--
### [!UICONTROL Set Options Of] {#setoptionsof}

The **[!UICONTROL Set Options Of]** rule type enables you to define rules to add check boxes dynamically to the Adaptive Form. You can use a Form Data Model or a custom function to define the rule.

To define a rule based on a custom function, select **[!UICONTROL Function Output]** from the drop-down list, and drag-and-drop a custom function from the **[!UICONTROL Functions]** tab. The number of checkboxes defined in the custom function are added to the Adaptive Form.

![Custom Functions](assets/custom_functions_set_options_new.png)

To create a custom function, see [custom functions in rule editor](#custom-functions).

To define a rule based on a form data model:

1. Select **[!UICONTROL Service Output]** from the drop-down list.
1. Select the data model object.
1. Select a data model object property from the **[!UICONTROL Display Value]** drop-down list. The number of checkboxes in the Adaptive Form is derived from the number of instances defined for that property in the database.
1. Select a data model object property from the **[!UICONTROL Save Value]** drop-down list.

![FDM set options](assets/fdm_set_options_new.png) -->

## 后续步骤

现在，让我们了解基于核心组件](/help/forms/rule-editor-core-components-usecases.md)的自适应表单的规则编辑器的各种[示例。

## 另请参阅

{{see-also-rule-editor}}