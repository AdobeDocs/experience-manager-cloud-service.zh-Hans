---
title: 内容片段模型
description: 内容片段模型用于创建包含结构化内容的内容片段。
translation-type: tm+mt
source-git-commit: da8fcf1288482d406657876b5d4c00b413461b21
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 10%

---


# 内容片段模型 {#content-fragment-models}

>[!CAUTION]
>
>AEM GraphQL API for Content Fragments投放可应请求提供。
>
>请联系[Adobe支持](https://experienceleague.adobe.com/?lang=en&amp;support-solution=General#support)，为AEM启用API作为Cloud Service项目。

内容片段模型定义[内容片段](/help/assets/content-fragments/content-fragments.md)的内容结构。

要使用内容片段模型，请：

1. [为实例启用内容片段模型功能](/help/assets/content-fragments/content-fragments-configuration-browser.md)
1. [创建](#creating-a-content-fragment-model)、配 [置内容](#defining-your-content-fragment-model)片段模型
1. [启用内容片段模](#enabling-disabling-a-content-fragment-model) 型，以在创建内容片段时使用

## 创建内容片段模型{#creating-a-content-fragment-model}

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。
1. 导览至适合您的[配置](/help/assets/content-fragments/content-fragments-configuration-browser.md)的文件夹。
1. 使用&#x200B;**创建**&#x200B;打开向导。

   >[!CAUTION]
   >
   >如果[未启用内容片段模型的使用](/help/assets/content-fragments/content-fragments-configuration-browser.md)，则&#x200B;**创建**&#x200B;选项将不可用。

1. 指定&#x200B;**模型标题**。如果需要，还可以添加&#x200B;**标记**&#x200B;和&#x200B;**说明**。

   ![标题和说明](assets/cfm-models-02.png)

1. 使用&#x200B;**创建**&#x200B;保存空模型。 将显示一条消息，指示操作成功，您可以选择&#x200B;**打开**&#x200B;以立即编辑模型，或选择&#x200B;**完成**&#x200B;以返回控制台。

## 定义内容片段模型{#defining-your-content-fragment-model}

内容片段模型使用选择&#x200B;**[数据类型](#data-types)**&#x200B;有效地定义所生成内容片段的结构。 使用模型编辑器，您可以添加数据类型的实例，然后配置它们以创建必需字段：

>[!CAUTION]
>
>编辑现有内容片段模型可能会影响相关片段。

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。

1. 导航到包含内容片段模型的文件夹。
1. 打开&#x200B;**Edit**&#x200B;所需的型号；使用快速操作，或先选择模型，然后从工具栏中选择操作。

   打开模型编辑器后，将显示：

   * 左：字段已定义
   * 右侧：可用于创建字段的&#x200B;**数据类型**（可在创建字段后使用的&#x200B;**属性**）

   >[!NOTE]
   >
   >当字段为&#x200B;**必填字段**&#x200B;时，左窗格中显示的&#x200B;**标签**&#x200B;将标有一个星号标记 (*****)。

1. **添加字段**

   * 将所需数据类型拖动到字段的所需位置。

   * 将字段添加到模型后，右面板将显示可为该特定数据类型定义的&#x200B;**属性**。 您可以在此处定义该字段的必需内容。
许多属性是自解释的，有关其他详细信息，请参阅[属性](#properties)。

1. **删除字段**

   选择所需字段，然后单击／点按垃圾桶图标。 系统将要求您确认该操作。

1. 添加所有必填字段，并根据需要定义相关属性。

1. 选择&#x200B;**保存**&#x200B;以保留定义。

<!--
## Defining your Content Fragment Model {#defining-your-content-fragment-model}

The content fragment model effectively defines the structure of the resulting content fragments using a selection of **[Data Types](#data-types)**. Using the model editor you can add instances of the data types, then configure them to create the required fields:

>[!CAUTION]
>
>Editing an existing content fragment model can impact dependent fragments.

1. Navigate to **Tools**, **Assets**, then open **Content Fragment Models**.

1. Navigate to the folder holding your content fragment model.
1. Open the required model for **Edit**; use either the quick action, or select the model and then the action from the toolbar.

   Once open the model editor shows:

    * left: fields already defined
    * right: **Data Types** available for creating fields (and **Properties** for use once fields have been created)

   >[!NOTE]
   >
   >When a field as **Required**, the **Label** indicated in the left pane will be marked with an asterix (**&#42;**).

   ![properties](assets/cfm-models-03.png)

1. **To Add a Field**

    * Drag a required data type to the required location for a field:

      ![data type to field](assets/cfm-models-04.png)

    * Once a field has been added to the model, the right panel will show the **Properties** that can be defined for that particular data type. Here you can define what is required for that field. 
      Many properties are self-explanatory, for additional details see [Properties](#properties).
      For example:

      ![field properties](assets/cfm-models-05.png)

1. **To Remove a Field**

   Select the required field, then click/tap the trash-can icon. You will be asked to confirm the action.

   ![remove](assets/cfm-models-06.png)

1. Add all required fields, and define the related properties, as required. For example:

   ![save](assets/cfm-models-07.png)

1. Select **Save** to persist the definition.
-->

## 数据类型 {#data-types}

可以选择数据类型来定义模型：

* **单行文本**
   * 添加一行文本的一个或多个字段；可以定义最大长度
* **多行文本**
   * 可以是富文本、纯文本或标记的文本区域
* **数字**
   * 添加一个或多个数字字段
* **布尔型**
   * 添加布尔复选框
* **日期和时间**
   * 添加日期和／或时间
* **枚举**
   * 添加一组复选框、单选按钮或下拉字段
* **标记**
   * 允许片段作者访问和选择标记区域
* **内容引用**
   * 引用任何类型的其他内容；可用于[创建嵌套内容](#using-references-to-form-nested-content)

<!--
* **Fragment Reference**
  * References other content fragments; can be used to [create nested content](#using-references-to-form-nested-content)
  * The data type can be configured to allow fragment authors to:
    * Edit the referenced fragment directly.
    * Create a new content fragment, based on the appropriate model  
* **JSON Object**
  * Allows the content fragment author to enter JSON syntax into the corresponding elements of a fragment. 
    * To allow AEM to store direct JSON that you have copy/pasted from another service.
    * The JSON will be passed through, and output as JSON in GraphQL.
    * Includes JSON syntax-highlighting, auto-complete and error-highlighting in the content fragment editor.
-->

## 属性 {#properties}

许多属性是自解释的，对于某些属性，其他详细信息如下：

* **呈现**
方式用于在片段中实现／呈现字段的各种选项。通常，这允许您定义作者将看到字段的单个实例，还是允许创建多个实例。

* **字段**
标签输入 
**字段** 标签将自动生 **成属性名称**，然后可以根据需要手动更新该名称。

* **ValidationBasic**
验证可由Required属性等机制 **** 使用。某些数据类型具有附加验证字段。 有关更多详细信息，请参阅[验证](#validation)。

* 对于数据类型&#x200B;**多行文本**，可将&#x200B;**默认类型**&#x200B;定义为以下任一类型：

   * **富文本**
   * **Markdown**
   * **纯文本**

   如果未指定，则此字段使用默认值&#x200B;**富文本**。

   更改内容片段模型中的&#x200B;**默认类型**&#x200B;仅会对在编辑器中打开并保存的现有相关内容片段生效。

<!--
* **Translatable**
  Checking the "Translatable" checkbox on a field in CF model editor will

  * Ensure the field's property name is added in translation config, context `/content/dam/<tenant>`, if not already present. 
  * For GraphQL: set a `<translatable>` property on the Content Fragment field to `yes`, to allow GraphQL query filter for JSON output with only translatable content.

* See **[Fragment Reference (Nested Fragments)](#fragment-reference-nested-fragments)** for more details about that specific data type and its properties.
-->

## 验证{#validation}

各种数据类型现在都可以定义在生成片段中输入内容的验证要求：

* **单行文本**
   * 与预定义正则表达式进行比较。
* **数字**
   * 检查特定值。

<!--
* **Content Reference**
  * Test for specific types of content.
  * Only images within a predefined range of width and height (in pixels) can be referenced. 
  * Only assets of specified file size or smaller can be referenced. 
  * Only predefined file types can be referenced.
  * No more than the predefined number of assets can be referenced. 
  * No more than the predefined number of fragments can be referenced.
* **Fragment Reference**
  * Test for a specific content fragment model.
-->

<!--
## Using References to form Nested Content {#using-references-to-form-nested-content}

Content Fragments can form nested content, using either of the following data types:

* **[Content Reference](#content-reference)**
  * Provides a simple reference to other content; of any type.
  * Can be configured for a one or multiple references (in the resulting fragment).

* **[Fragment Reference](#fragment-reference-nested-fragments)** (Nested Fragments)
  * References other fragments, dependent on the specific models specified.
  * Allows you to include/retrieve structured data.
    >[!NOTE]
    >
    >This method is of particular interest in conjunction with [Headless Content Delivery using Content Fragments with GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).
  * Can be configured for one or multiple references (in the resulting fragment)..

>[!NOTE]
>
>AEM has a recurrence protection for:
>
>* Content References
>  This prevents the user from adding a reference to the current fragment. This may lead to an empty Fragment Reference picker dialog.
>
>* Fragment References in GraphQL 
>  If you create a deep query that returns multiple Content Fragments referenced by each another, it will return null at first occurence.

### Content Reference {#content-reference}

The Content Reference allows you to render content from another source; for example, image or content fragment.

In addition to standard properties you can specify:

* The **Root Path** for any referenced content.
* The content types that can be referenced.
* Limitations for file sizes.
* Image restraints.
-->

<!-- Check screenshot - might need update

   ![Content Reference](assets/cfm-content-reference.png)
-->

<!--
### Fragment Reference (Nested Fragments) {#fragment-reference-nested-fragments}

The Fragment Reference references one, or more, content fragments. This feature of particular interest when retrieving content for use in your app, as it allows you to retrieve structured data with multiple layers.

For example:

* A model defining details for an employee; these include:
  * A reference to the model that defines the employer (company)

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
>
>This is of particular interest in conjunction with [Headless Content Delivery using Content Fragments with GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).

In addition to standard properties you can define:

* **Render As**:

  * **multifield** - the fragment author can create multiple, individual, references

  * **fragmentreference** - allows the fragment author to select a single reference to a fragment

* **Model Type**
  Multiple models can be selected. When authoring the Content Fragment any referenced fragments must have been created using these models.

* **Root Path**
  This specifies a root path for any fragments referenced.

* **Allow Fragment Creation**

  This will allow the fragment author to create a new fragment based on the appropriate model.
-->

<!--
  * **fragmentreferencecomposite** - allows the fragment author to build a composite, by selecting multiple fragments
-->

<!-- Check screenshot - might need update

   ![Fragment Reference](assets/cfm-fragment-reference.png)
-->

<!--
>[!NOTE]
>
>A recurrence protection mechanism is in place. It prohibits the user from selecting the current Content Fragment in the Fragment Reference. This may lead to an empty Fragment Reference picker dialog.
>
>There is also a recurrence protection for Fragment References in GraphQL. If you create a deep query across two Content Fragments that reference each other, it will return null.
-->

## 启用或禁用内容片段模型{#enabling-disabling-a-content-fragment-model}

要完全控制内容片段模型的使用，您可以设置这些模型的状态。

### 启用内容片段模型{#enabling-a-content-fragment-model}

创建模型后，需要启用该模型，以便：

* 创建新内容片段时可供选择。
* 可以从内容片段模型中引用。
* 可用于GraphQL;因此生成模式。

要启用标记为以下任一类型的模型：

* **草稿** :mew（从未启用）。
* **禁用** :已特别禁用。

使用&#x200B;**启用**&#x200B;选项，可从以下任一位置进行：

* 选择所需的“模型”(Model)时，顶部工具栏显示。
* 相应的快速操作（将鼠标悬停在所需的模型上）。

![启用草图或禁用模型](assets/cfm-status-enable.png)

### 禁用内容片段模型{#disabling-a-content-fragment-model}

还可以禁用模型，以便：

* 该模型不再作为创建&#x200B;*new*&#x200B;内容片段的基础。
* 但是:
   * GraphQL模式不断生成，并且仍可查询（以避免影响JSON API）。
   * 仍然可以查询基于模型的任何内容片段并从GraphQL端点返回。
* 模型不能再被引用，但现有引用保持不变，仍可从GraphQL端点查询和返回。

要禁用标为&#x200B;**Enabled**&#x200B;的模型，请使用以下任一选项中的&#x200B;**Disable**&#x200B;选项：

* 选择所需的“模型”(Model)时，顶部工具栏显示。
* 相应的快速操作（将鼠标悬停在所需的模型上）。

![禁用启用的模型](assets/cfm-status-disable.png)

## 删除内容片段模型{#deleting-a-content-fragment-model}

>[!CAUTION]
删除内容片段模型可能会影响相关片段。

要删除内容片段模型，请执行以下操作：

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。

1. 导航到包含内容片段模型的文件夹。
1. 从工具栏中选择您的型号，然后选择&#x200B;**删除**。

   >[!NOTE]
   如果模型被引用，则会发出警告。 采取适当措施。

## 发布内容片段模型{#publishing-a-content-fragment-model}

内容片段模型需要在发布任何相关内容片段时／之前发布。

要发布内容片段模型，请执行以下操作：

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。

1. 导航到包含内容片段模型的文件夹。
1. 从工具栏中选择您的型号，然后选择&#x200B;**发布**。
发布状态将在控制台中指示。

   >[!NOTE]
   如果发布的内容片段尚未发布模型，则将显示一个选择列表来指示此情况，并且该模型将随片段一起发布。

## 取消发布内容片段模型{#unpublishing-a-content-fragment-model}

如果内容片段模型未被任何片段引用，则可以取消发布这些模型。

要取消发布内容片段模型，请执行以下操作：

1. 导航到&#x200B;**工具**、**资产**，然后打开&#x200B;**内容片段模型**。

1. 导航到包含内容片段模型的文件夹。
1. 从工具栏中选择您的型号，然后选择&#x200B;**取消发布**。
发布状态将在控制台中指示。
