---
title: 内容片段模型
description: 了解内容片段模型如何作为AEM中无头内容的基础，以及如何使用结构化内容创建内容片段。
feature: Content Fragments
role: User
exl-id: fd706c74-4cc1-426d-ab56-d1d1b521154b
source-git-commit: 7d67bdb5e0571d2bfee290ed47d2d7797a91e541
workflow-type: tm+mt
source-wordcount: '2256'
ht-degree: 7%

---

# 内容片段模型 {#content-fragment-models}

AEM中的内容片段模型定义[内容片段的内容结构，](/help/assets/content-fragments/content-fragments.md)用作无头内容的基础。

要使用内容片段模型，您可以：

1. [为实例启用内容片段模型功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [创建](#creating-a-content-fragment-model)和配 [置](#defining-your-content-fragment-model)内容片段模型
1. [启用内容片段模](#enabling-disabling-a-content-fragment-model) 型，以便在创建内容片段时使用
1. [通过配置策略，在所需的资产文件夹上允](#allowing-content-fragment-models-assets-folder) 许您的内容 **片段模型**。

## 创建内容片段模型 {#creating-a-content-fragment-model}

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。
1. 导航到适合您的[配置](/help/assets/content-fragments/content-fragments-configuration-browser.md)的文件夹。
1. 使用&#x200B;**Create**&#x200B;打开向导。

   >[!CAUTION]
   >
   >如果[对内容片段模型的使用尚未启用](/help/assets/content-fragments/content-fragments-configuration-browser.md)，则&#x200B;**创建**&#x200B;选项将不可用。

1. 指定&#x200B;**模型标题**。您还可以添加&#x200B;**Tags**、**Description**，并根据需要选择&#x200B;**将模型**&#x200B;启用到[启用模型](#enabling-disabling-a-content-fragment-model)。

   ![标题和描述](assets/cfm-models-02.png)

1. 使用&#x200B;**Create**&#x200B;保存空模型。 将显示一条消息，指示操作成功，您可以选择&#x200B;**打开**&#x200B;以立即编辑模型，或选择&#x200B;**完成**&#x200B;以返回到控制台。

## 定义内容片段模型 {#defining-your-content-fragment-model}

内容片段模型使用&#x200B;**[数据类型](#data-types)**&#x200B;的选项有效地定义了生成的内容片段的结构。 使用模型编辑器，您可以添加数据类型的实例，然后对其进行配置以创建必填字段：

>[!CAUTION]
>
>编辑现有内容片段模型可能会影响依赖的片段。

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。

1. 导航到包含内容片段模型的文件夹。
1. 打开&#x200B;**Edit**&#x200B;所需的模型；使用快速操作，或选择模型，然后从工具栏中选择操作。

   打开模型编辑器后，会显示：

   * 左：字段已定义
   * 右侧：可用于创建字段的&#x200B;**数据类型**（可在创建字段后使用的&#x200B;**属性**）

   >[!NOTE]
   >
   >当字段为&#x200B;**必填字段**&#x200B;时，左窗格中显示的&#x200B;**标签**&#x200B;将标有一个星号标记 (*****)。

![属性](assets/cfm-models-03.png)

1. **添加字段**

   * 将字段的必需数据类型拖到所需位置：

      ![数据类型到字段](assets/cfm-models-04.png)

   * 将字段添加到模型后，右侧面板将显示可为该特定数据类型定义的&#x200B;**属性**。 您可以在此定义该字段的必需内容。

      * 许多属性都不言而喻，有关更多详细信息，请参阅[属性](#properties)。
      * 键入&#x200B;**字段标签**&#x200B;将自动完成&#x200B;**属性名称** — 如果为空，随后可手动更新。

      例如：

      ![字段属性](assets/cfm-models-05.png)


1. **删除字段**

   选择必填字段，然后单击/点按垃圾桶图标。 系统将要求您确认该操作。

   ![删除](assets/cfm-models-06.png)

1. 添加所有必填字段，并根据需要定义相关属性。 例如：

   ![保存](assets/cfm-models-07.png)

1. 选择&#x200B;**Save**&#x200B;以保留定义。

## 数据类型 {#data-types}

可以选择数据类型以定义模型：

* **单行文本**
   * 添加一行文本的一个或多个字段；可以定义最大长度
* **多行文本**
   * 可以是富文本、纯文本或标记的文本区域
* **数字**
   * 添加一个或多个数字字段
* **布尔型**
   * 添加布尔复选框
* **日期和时间**
   * 添加日期和/或时间
* **枚举**
   * 添加一组复选框、单选按钮或下拉字段
* **标记**
   * 允许片段作者访问和选择标记区域
* **内容引用**
   * 引用任何类型的其他内容；可用于[创建嵌套内容](#using-references-to-form-nested-content)
   * 如果图像被引用，您可以选择显示缩略图
* **片段引用**
   * 引用其他内容片段；可用于[创建嵌套内容](#using-references-to-form-nested-content)
   * 数据类型可配置为允许片段作者执行以下操作：
      * 直接编辑引用的片段。
      * 根据相应的模型创建新内容片段
* **JSON 对象**
   * 允许内容片段作者在片段的相应元素中输入JSON语法。
      * 允许AEM存储您从其他服务复制/粘贴的直接JSON。
      * 该JSON将被传递，并在GraphQL中输出为JSON。
      * 内容片段编辑器中包括JSON语法高亮显示、自动完成和错误高亮显示。
* **制表符占位符**
   * 允许引入选项卡，以在编辑内容片段内容时使用。
这将在模型编辑器中显示为分隔符，用于分隔内容数据类型列表的各个部分。 每个实例表示新选项卡的开头。
在片段编辑器中，每个实例都将显示为一个选项卡。

      >[!NOTE]
      此数据类型仅用于格式设置，因此AEM GraphQL架构会忽略此数据类型。

## 属性 {#properties}

许多属性不言而喻，对于某些属性，其他详细信息如下：

* **呈现**
方式用于在片段中实现/呈现字段的各种选项。通常，这允许您定义作者将看到字段的单个实例，还是允许创建多个实例。

* **字段**
标签输入 
**字段** 标签将自动生成 **属性名称**，然后可以根据需要手动更新属性名称。

* ****
ValidationBasic验证可由Requiredproperty等机制 **** 使用。某些数据类型具有附加的验证字段。 有关更多详细信息，请参阅[验证](#validation)。

* 对于数据类型&#x200B;**多行文本**，可将&#x200B;**默认类型**&#x200B;定义为以下任一类型：

   * **富文本**
   * **Markdown**
   * **纯文本**

   如果未指定，则此字段将使用默认值&#x200B;**富文本**。

   更改内容片段模型中的&#x200B;**默认类型**&#x200B;仅会对在编辑器中打开并保存的现有相关内容片段生效。

* ****
对于从当前模型创建的所有内容片段，UniqueContent（对于特定字段）必须是唯一的。

   用于确保内容作者不能重复已在同一模型的另一个片段中添加的内容。

   例如，内容片段模型中名为`Country`的&#x200B;**单行文本**&#x200B;字段不能在两个从属内容片段中具有值`Japan`。 尝试第二个实例时将发出警告。

   >[!NOTE]
   确保每个语言根的唯一性。

   >[!NOTE]
   变量可以具有与同一片段的变量相同的&#x200B;*唯一*&#x200B;值，但与其他片段的任何变量中使用的值不同。

* 有关该特定数据类型及其属性的更多详细信息，请参阅&#x200B;**[内容引用](#content-reference)**。

* 有关该特定数据类型及其属性的更多详细信息，请参阅&#x200B;**[片段引用（嵌套片段）](#fragment-reference-nested-fragments)**。

<!--
* **Translatable**
  Checking the **Translatable** checkbox on a field in the Content Fragment Model editor will:

  * Ensure the field's property name is added to the translation configuration, context `/content/dam/<sites-configuration>`, if not already present. 
  * For GraphQL: set a `<translatable>` property on the Content Fragment field to `yes`, to allow GraphQL query filter for JSON output with only translatable content.
-->

## 验证 {#validation}

各种数据类型现在包括定义在结果片段中输入内容时的验证要求：

* **单行文本**
   * 与预定义正则表达式进行比较。
* **数字**
   * 检查特定值。
* **内容引用**
   * 测试特定类型的内容。
   * 只能引用指定文件大小或更小的资产。
   * 只能引用预定义的宽度和/或高度范围（以像素为单位）内的图像。
* **片段引用**
   * 测试特定内容片段模型。

## 使用引用表单嵌套内容 {#using-references-to-form-nested-content}

内容片段可以使用以下任一数据类型形成嵌套内容：

* **[内容引用](#content-reference)**
   * 提供对其他内容的简单引用；任何类型的。
   * 可以为一个或多个引用（在生成的片段中）配置。

* **[片段引用](#fragment-reference-nested-fragments)** （嵌套片段）
   * 引用其他片段，具体取决于指定的特定模型。
   * 允许您包含/检索结构化数据。

      >[!NOTE]
      此方法特别需要与[结合使用内容片段和GraphQL](/help/assets/content-fragments/content-fragments-graphql.md)的无头内容交付结合使用。
   * 可以为一个或多个引用（在生成的片段中）配置。

>[!NOTE]
AEM具有以下重复保护：
* 内容引用
这会阻止用户添加对当前片段的引用。 这可能导致出现空的片段引用选取器对话框。
* GraphQL中的片段引用
如果创建一个深层查询，该查询返回多个相互引用的内容片段，则该查询在第一次出现时将返回空值。


### 内容引用 {#content-reference}

内容引用允许您渲染来自其他源的内容；例如，图像或内容片段。

除了标准属性之外，您还可以指定：

* 任何引用内容的&#x200B;**根路径**
* 可引用的内容类型
* 文件大小限制
* 如果引用了图像：
   * 显示缩略图
   * 图像高度和宽度的限制

![内容引用](assets/cfm-content-reference.png)

### 片段引用（嵌套片段） {#fragment-reference-nested-fragments}

片段引用引用引用一个或多个内容片段。 此功能在检索内容以在您的应用程序中使用时特别感兴趣，因为它允许您使用多个层来检索结构化数据。

例如：

* 定义员工详细信息的模型；这包括：
   * 对定义雇主（公司）的模型的引用

```xml
type EmployeeModel {
    name: String
    firstName: String
    company: CompanyModel
}

type CompanyModel {
    name: String
    street: String
    city: String
}
```

>[!NOTE]
与[结合使用内容片段和GraphQL](/help/assets/content-fragments/content-fragments-graphql.md)的无头内容交付特别值得关注。

除了标准属性之外，您还可以定义：

* **呈现为**:

   * **多字段**  — 片段作者可以创建多个单独的引用

   * **fragmentreference**  — 允许片段作者选择对片段的单个引用

* **模型**
类型可选择多个模型。创作内容片段时，必须使用这些模型创建了任何引用的片段。

* **根路**
径这为引用的任何片段指定根路径。

* **允许创建片段**

   这将允许片段作者根据相应的模型创建新片段。

   * **fragmentreferencecompresition**  — 允许片段作者通过选择多个片段来构建复合

   ![片段引用](assets/cfm-fragment-reference.png)

>[!NOTE]
已建立复发保护机制。 它禁止用户在片段引用中选择当前内容片段。 这可能导致出现空的片段引用选取器对话框。
GraphQL中还对片段引用提供了定期保护。 如果在两个相互引用的内容片段之间创建深层查询，则将返回空值。

## 内容片段模型 — 属性 {#content-fragment-model-properties}

您可以编辑内容片段模型的&#x200B;**属性**:

* **基本**
   * **模型标题**
   * **标记**
   * **描述**
   * **上传图像**

## 启用或禁用内容片段模型 {#enabling-disabling-a-content-fragment-model}

要完全控制内容片段模型的使用，可设置其状态。

### 启用内容片段模型 {#enabling-a-content-fragment-model}

创建模型后，需要启用该模型，以便：

* 可在创建新内容片段时进行选择。
* 可以在内容片段模型中引用。
* 可用于GraphQL;这样架构就会生成。

要启用标记为以下任一类型的模型：

* **草稿** :mew（从未启用）。
* **已禁用** :已被特别禁用。

使用以下任一位置的&#x200B;**Enable**&#x200B;选项：

* 选择所需的“模型”(Model)时，顶部工具栏。
* 相应的快速操作（将鼠标悬停在所需模型上）。

![启用草稿或禁用的模型](assets/cfm-status-enable.png)

### 禁用内容片段模型 {#disabling-a-content-fragment-model}

也可以禁用模型，以便：

* 模型不再可用作创建&#x200B;*new*&#x200B;内容片段的基础。
* 但是:
   * GraphQL架构一直在生成，并且仍可查询（以避免影响JSON API）。
   * 仍可以从GraphQL端点查询和返回任何基于模型的内容片段。
* 不能再引用模型，但现有引用将保持不变，并且仍可以从GraphQL端点查询和返回。

要禁用标记为&#x200B;**Enabled**&#x200B;的模型，请使用以下任一位置的&#x200B;**Disable**&#x200B;选项：

* 选择所需的“模型”(Model)时，顶部工具栏。
* 相应的快速操作（将鼠标悬停在所需模型上）。

![禁用启用的模型](assets/cfm-status-disable.png)

## 允许在Assets文件夹中使用内容片段模型 {#allowing-content-fragment-models-assets-folder}

要实施内容管理，您可以在Assets文件夹上配置&#x200B;**Policys**&#x200B;以控制允许在该文件夹中创建片段的内容片段模型。

>[!NOTE]
该机制类似于在页面的高级属性中允许页面模板](/help/sites-cloud/authoring/features/templates.md#allowing-a-template-author)及其子项。[

要为&#x200B;**允许的内容片段模型**&#x200B;配置&#x200B;**策略**，请执行以下操作：

1. 导航并打开所需Assets文件夹的&#x200B;**属性** 。

1. 打开&#x200B;**Policys**&#x200B;选项卡，您可以在其中配置：

   * **继承自`<folder>`**

      创建新子文件夹时，会自动继承策略；如果子文件夹需要允许与父文件夹不同的模型，则可以重新配置策略（并中断继承）。

   * **按照路径允许的内容片段模型**

      可以允许使用多个模型。

   * **允许的内容片段模型（按标记）**

      可以允许使用多个模型。
   ![内容片段模型策略](assets/cfm-model-policy-assets-folder.png)

1. **** 保存任何更改。

文件夹允许的内容片段模型将按照以下方式进行解析：
* ******允许的内容片段模型**&#x200B;的策略。
* 如果为空，请尝试使用继承规则确定策略。
* 如果继承链未传递结果，请查看该文件夹的&#x200B;**Cloud Services**&#x200B;配置（也先直接进行，然后通过继承）。
* 如果以上所有内容均未提供任何结果，则该文件夹不允许使用模型。

## 删除内容片段模型 {#deleting-a-content-fragment-model}

>[!CAUTION]
删除内容片段模型可能会影响相关片段。

要删除内容片段模型，请执行以下操作：

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。

1. 导航到包含内容片段模型的文件夹。
1. 选择模型，然后从工具栏中选择&#x200B;**Delete**。

   >[!NOTE]
   如果引用了模型，则会发出警告。 采取适当措施。

## 发布内容片段模型 {#publishing-a-content-fragment-model}

在发布任何相关内容片段时/之前，需要发布内容片段模型。

要发布内容片段模型，请执行以下操作：

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。

1. 导航到包含内容片段模型的文件夹。
1. 选择您的模型，然后从工具栏中选择&#x200B;**Publish** 。
控制台中将指示已发布状态。

   >[!NOTE]
   如果发布的内容片段的模型尚未发布，则会显示一个选择列表来指示该情况，并且模型将随该片段一起发布。

## 取消发布内容片段模型 {#unpublishing-a-content-fragment-model}

如果任何片段未引用内容片段模型，则可以取消发布这些模型。

要取消发布内容片段模型，请执行以下操作：

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。

1. 导航到包含内容片段模型的文件夹。
1. 选择您的模型，然后从工具栏中选择&#x200B;**取消发布** 。
控制台中将指示已发布状态。

<!--
## Locked Content Fragment Models {#locked-content-fragment-models}

This feature provides governance for Content Fragment Models that have been published. 

The challenge:

* Content Fragment Models determine the schema for GraphQL queries in AEM. 

  * AEM GraphQL schemas are created as soon as a Content Fragment Model is created, and they can exist on both author and publish environments. 

  * Schemas on publish are the most critical as they provide the foundation for live delivery of Content Fragment content in JSON format.  

* Problems can occur when Content Fragment Models are modified, or in other words edited. This means that the schema changes, which in turn may affect existing GraphQL queries. 

* Adding new fields to a Content Fragment Model should (typically) not have any detrimental effects. However, modifying existing data fields (for example, their name) or deleting field definitions, will break existing GraphQL queries when they are requesting these fields. 

The solution:

* To make users aware of the risks when editing models that are already used for live content delivery (i.e. that have been published). Also, to avoid unintended changes. As either of these might break queries if the modified models are re-published. 

* To address this issue, Content Fragment Models are put in a READ-ONLY mode on author - as soon as they have been published. 

* In READ-ONLY mode, users can still see contents and structure of models but they cannot edit them. 
-->
