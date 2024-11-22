---
title: 内容片段模型
description: 了解内容片段模型如何作为AEM中内容片段的基础，允许您创建结构化内容用于Headless投放或页面创作。
feature: Content Fragments
role: User, Developer, Architect
exl-id: 8ab5b15f-cefc-45bf-a388-928e8cc8c603
solution: Experience Manager Sites
source-git-commit: e59c432a2f6b0f2034829b3cb3f88679aa182048
workflow-type: tm+mt
source-wordcount: '3591'
ht-degree: 79%

---

# 内容片段模型 {#content-fragment-models}

>[!IMPORTANT]
>
>内容片段模型的各种功能可通过早期采用者计划获得。
>
>要查看状态以及如果您有兴趣如何应用，请查看[发行说明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

Adobe Experience Manager (AEM) as a Cloud Service 中的内容片段模型定义[内容片段](/help/sites-cloud/administering/content-fragments/overview.md)的内容结构。随后可使用这些片段创作页面或作为 Headless 内容的基础。

要使用内容片段模型，您可以：

1. [为您的实例启用内容片段模型功能](/help/sites-cloud/administering/content-fragments/setup.md)
1. [创建](#creating-a-content-fragment-model)和[配置](#defining-your-content-fragment-model)，内容片段模型
1. [启用您的内容片段模型](#enabling-disabling-a-content-fragment-model)，以便在创建内容片段时使用
1. 通过配置[策略](#allowing-content-fragment-models-assets-folder)，**允许在所需的 Assets 文件夹上创建内容片段模型**。

## 创建内容片段模型 {#creating-a-content-fragment-model}

1. 导航到&#x200B;**“工具”**、**“常规”**，然后打开&#x200B;**“内容片段模型”**。
1. 导航到适合您的[配置或子配置](/help/sites-cloud/administering/content-fragments/setup.md)的文件夹。
1. 使用&#x200B;**创建**&#x200B;打开向导。

   >[!CAUTION]
   >
   >如果[尚未允许使用内容片段模型](/help/sites-cloud/administering/content-fragments/setup.md)，则将没有&#x200B;**创建**&#x200B;选项可用。

1. 指定&#x200B;**模型标题**。还可定义多种属性；例如，添加&#x200B;**标记**、**描述**，如果需要，请选择&#x200B;**启用模型**&#x200B;以[启用模型](#enabling-disabling-a-content-fragment-model)，并定义
   **默认预览 URL 模式**。

   >[!NOTE]
   >
   >有关完整详细信息，请参阅[内容片段模型 - 属性](#content-fragment-model-properties)。

   ![标题和描述](assets/cf-cfmodels-create.png)

1. 使用&#x200B;**创建**&#x200B;保存空模型。随后将显示一条消息，指示操作成功，您可选择&#x200B;**打开**&#x200B;以立即编辑模型或选择&#x200B;**完成**&#x200B;以返回控制台。

>[!CAUTION]
>
>如果要查询多个引用的片段，则建议不要让各种片段模型具有具有相同名称但类型不同的字段名称。
>
>有关详细信息，请参阅用于内容片段的[AEM GraphQL API — 限制](/help/headless/graphql-api/content-fragments.md#limitations)

### 内容片段模型 – 属性 {#content-fragment-model-properties}

在您创建模型时定义这些属性，随后可用内容片段模型的&#x200B;**属性**&#x200B;选项编辑这些属性：

* **基本**
   * **模型标题**
   * **标记**
   * **描述**
   * **启用模型**
   * **默认预览 URL 模式**
通过内容片段编辑器，作者可在外部前端应用程序中**预览**&#x200B;其内容。在配置&#x200B;**预览服务**&#x200B;后，添加该前端应用程序的 URL。

     预览 URL 应遵循此模式：
`https://<preview_url>?param=${expression}`

     可用的表达式为：

      * `${contentFragment.path}`
      * `${contentFragment.model.path}`
      * `${contentFragment.model.name}`
      * `${contentFragment.variation}`
      * `${contentFragment.id}`

   * **上传图像**

<!-- CHECK: currently under FT -->
<!--
* **GraphQL**
  Define names relevant for GraphQL.
  Changing the GraphQL API Name, or Query field names will impact client applications.
  * **API Name**
    Represents the GraphQL type and query field names in the GraphQL schema.
  * **Single Query Field Name**
    Represents the GraphQL single query field name in the GraphQL schema.
  * **Multiple Query Field Name**
    Represents the GraphQL multiple query field name in the GraphQL schema.
-->

## 定义内容片段模型 {#defining-your-content-fragment-model}

内容片段模型使用一批&#x200B;**[数据类型](#data-types)**&#x200B;有效地定义所得内容片段的结构。可使用模型编辑器添加数据类型的实例，然后配置它们以创建必填字段：

>[!CAUTION]
>
>编辑现有内容片段已使用的模型可能会影响那些从属的片段。

1. 导航到&#x200B;**工具**、**常规**，然后打开&#x200B;**内容片段模型**。

1. 导航到容纳您的内容片段模型的文件夹。
1. 打开所需的模型进行&#x200B;**“编辑”**；使用快速操作或选择模型，然后从工具栏中选择操作。

   打开模型编辑器后，会显示：

   * 左：字段已定义
   * 右侧：可用于创建字段的&#x200B;**数据类型**（可在创建字段后使用的&#x200B;**属性**）

   >[!NOTE]
   >
   >将字段定义为&#x200B;**必填**&#x200B;时，将为左侧窗格中所示的&#x200B;**标签**&#x200B;标星号 (**&#42;**)。

![属性](assets/cf-cfmodels-empty-model.png)

1. **添加字段**

   * 将字段的必需数据类型拖到所需位置：

     ![拖动数据类型以创建字段](assets/cf-cfmodels-create-field.png)

   * 将字段添加到模型后，右侧面板将显示可以为该特定数据类型定义的&#x200B;**属性**。您可以在此定义该字段的必需内容。

      * 许多属性的含义一目了然，有关更多详细信息，请参阅[属性](#properties)。
      * 键入&#x200B;**字段标签**&#x200B;将自动补全&#x200B;**属性名称** - 如果为空，则以后可手动更新它。

        >[!CAUTION]
        >
        在手动更新数据类型的&#x200B;**属性名称**&#x200B;属性时，名称必须&#x200B;*仅*&#x200B;包含 A-Z、a-z、0-9 和作为特殊字符的下划线“_”。
        >
        如果在 AEM 早期版本中创建的模型包含非法字符，请移除或更新这些字符。

     例如：

     ![字段属性](assets/cf-cfmodels-field-properties.png)

1. **移除字段**

   选择必填字段，然后选择垃圾桶图标。 系统会要求您确认该操作。

   ![删除](assets/cf-cfmodels-remove-icon.png)

1. 添加所有必填字段，并根据需要定义相关属性。例如：

   ![保存](assets/cf-cfmodels-save.png)

1. 选择&#x200B;**“保存”**&#x200B;来保留定义。

## 数据类型 {#data-types}

有一批数据类型可用于定义您的模型：

* **单行文本**
   * 为单行文本添加字段；可以定义最大长度
   * 字段可以配置为允许片段作者创建新字段实例

* **多行文本**
   * 一个文本区域，它可为富文本、纯文本或 Markdown
   * 字段可以配置为允许片段作者创建新字段实例

  >[!NOTE]
  >
  在模型中由&#x200B;**默认类型**&#x200B;属性定义该文本区域是富文本、纯文本还是 Markdown。
  >
  无法从[内容片段编辑器](/help/sites-cloud/administering/content-fragments/authoring.md)更改此格式，而只能从模型更改。

* **数字**
   * 添加数字字段
   * 字段可以配置为允许片段作者创建新字段实例

* **布尔型**
   * 添加布尔复选框

* **日期和时间**
   * 添加日期和/或时间字段

* **枚举**
   * 添加一组复选框、单选按钮或下拉字段
      * 您可以指定对片段作者可用的选项

* **标记**
   * 允许片段作者访问和选择标记区域
* **片段引用**
   * 引用其他内容片段；可用于[创建嵌套内容](#using-references-to-form-nested-content)
   * 数据类型可配置为允许片段作者执行以下操作：
      * 直接编辑引用的片段。
      * 根据相应的模型创建新内容片段
      * 创建字段的新实例
   * 引用指定了引用资源的路径；例如`/content/dam/path/to/resource`
* **片段引用(UUID)**
   * 引用其他内容片段；可用于[创建嵌套内容](#using-references-to-form-nested-content)
   * 数据类型可配置为允许片段作者执行以下操作：
      * 直接编辑引用的片段。
      * 根据相应的模型创建新内容片段
      * 创建字段的新实例
   * 在编辑器中，引用指定被引用资源的路径；在内部，引用作为引用该资源的通用唯一ID (UUID)来保存
      * 您无需知道UUID；在片段编辑器中，您可以浏览到所需的片段

* **内容引用**
   * 引用任何类型的其他内容；可用于[创建嵌套内容](#using-references-to-form-nested-content)
   * 如果图像被引用，您可以选择显示缩略图
   * 字段可以配置为允许片段作者创建新字段实例
   * 引用指定了引用资源的路径；例如`/content/dam/path/to/resource`
* **内容引用(UUID)**
   * 引用任何类型的其他内容；可用于[创建嵌套内容](#using-references-to-form-nested-content)
   * 如果图像被引用，您可以选择显示缩略图
   * 字段可以配置为允许片段作者创建新字段实例
   * 在编辑器中，引用指定被引用资源的路径；在内部，引用作为引用该资源的通用唯一ID (UUID)来保存
      * 您无需知道UUID；在片段编辑器中，您可以浏览到所需的资源资源

* **JSON 对象**
   * 使内容片段作者可将 JSON 语法输入到片段的相应元素中。
      * 使 AEM 可存储您从另一服务复制/粘贴的直接 JSON。
      * JSON 将被传递，并在 GraphQL 中作为 JSON 输出。
      * 在内容片段编辑器中包括 JSON 语法高亮显示、自动补全和错误高亮显示。

* **选项卡占位符**
   * 允许引入选项卡，以供在编辑内容片段内容时使用。
      * 这些选项卡在模型编辑器中显示为分隔条，用于分隔内容数据类型的列表的各个部分。每个实例表示一个新选项卡的开始。
      * 在片段编辑器中，每个实例都显示为一个选项卡。

     >[!NOTE]
     >
     此数据类型仅用于格式设置，因此 AEM GraphQL 架构会忽略此数据类型。

## 属性 {#properties}

许多属性含义一目了然，对于某些属性，其他详细信息如下：

* **属性名称**

  在手动更新数据类型的此属性时，名称&#x200B;**必须***仅*&#x200B;包含 A-Z、a-z、0-9 和作为特殊字符的下划线“_”。

  >[!CAUTION]
  >
  如果在 AEM 早期版本中创建的模型包含非法字符，请移除或更新这些字符。

* **呈现为**

  用于在片段中实现/呈现字段的各种选项。 通常，这允许您定义作者将看到字段的单个实例，还是允许作者创建多个实例。 当使用&#x200B;**多个字段**&#x200B;时，您可以定义项目的最小和最大数量 — 有关详细信息，请参阅[验证](#validation)。

* **字段标签**
输入**字段标签**&#x200B;将自动生成&#x200B;**属性名称**，如有必要，可以手动更新该名称。

* **验证**
基本验证可由以下机制提供： **必需** 属性。某些数据类型具有附加的验证字段。请参阅[验证](#validation)，了解更多详细信息。

* 对于数据类型&#x200B;**多行文本**，可将&#x200B;**默认类型**&#x200B;定义为以下任一类型：

   * **富文本**
   * **Markdown**
   * **纯文本**

  如果未指定，则默认值&#x200B;**富文本**&#x200B;用于此字段。

  在编辑器中打开并保存现有相关的内容片段后，更改内容片段模型中的&#x200B;**默认类型**&#x200B;才对该片段生效。

* **唯一**
（特定字段的）内容必须在从当前模型创建的所有内容片段上都唯一。

  用于确保内容作者不能重复已添加到同一模型的另一个片段中的内容。

  例如，内容片段模型中名为 `Country` 的&#x200B;**单行文本**&#x200B;字段在两个相关内容片段中不能具有值`Japan`。尝试第二个实例时会发出警告。

  >[!NOTE]
  >
  确保每个语言根的唯一性。

  >[!NOTE]
  >
  变体可以具有与同一片段变体相同的&#x200B;*唯一*&#x200B;值，但与其他片段变体中使用的值不同。

* 有关特定数据类型及其属性的更多详细信息，请参阅&#x200B;**[内容参考](#content-reference)**。

* 有关特定数据类型及其属性的更多详细信息，请参阅&#x200B;**[片段引用（嵌套片段）](#fragment-reference-nested-fragments)**。

* **可翻译**

  选中内容片段模型编辑器中字段上的&#x200B;**可翻译**&#x200B;复选框将：

   * 如果属性名称尚不存在，请确保字段的属性名称已添加到翻译配置上下文`/content/dam/<sites-configuration>`。
   * 对于 GraphQL：请将 `<translatable>`Content Fragment 字段上的属性设置为 `yes`，以允许 GraphQL 查询过滤仅包含可翻译内容的 JSON 输出。

## 验证 {#validation}

现在，各种数据类型都可以定义在结果片段中输入内容时的验证要求：

* **单行文本**
   * 与预定义正则表达式进行比较。
* **数字**
   * 检查特定值。
* **内容引用**
   * 测试特定类型的内容。
   * 只能引用指定文件大小或更小的资源。
   * 只能引用预定义的宽度和/或高度范围（以像素为单位）内的图像。
* **片段引用**
   * 为特定的内容片段模型测试。
* **最小项数** / **最大项数**

  已定义为&#x200B;**多个字段**（使用&#x200B;**渲染为**&#x200B;设置）的字段具有以下选项：

   * **最小项目数**
   * **最大项数**

  已在[内容片段编辑器](/help/sites-cloud/administering/content-fragments/authoring.md)中验证这些内容。

## 使用引用表单嵌套内容 {#using-references-to-form-nested-content}

内容片段可以使用以下任一数据类型形成嵌套内容：

* [内容引用](#content-reference)
   * 提供对其他内容的简单引用；任何类型的。
   * 由数据类型提供：
      * **内容引用** — 基于路径
      * **内容引用(UUID)** — 基于UUID
   * 可为（所得片段中的）一个或多个引用配置它。

* [片段引用](#fragment-reference-nested-fragments)（嵌套片段）
   * 引用其他片段，具体取决于指定的特定模型。
   * 由数据类型提供：
      * **片段引用** — 基于路径
      * **片段引用(UUID)** — 基于UUID
   * 允许您包含/检索结构化数据。

     >[!NOTE]
     >
     当您使用[通过 GraphQL 使用内容片段投放 Headless 内容](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md)时，此方法尤其值得关注。
   * 可为（所得片段中的）一个或多个引用配置它。

>[!NOTE]
>
有关内容/片段引用和内容/片段引用(UUID)以及升级到基于UUID的数据类型的详细信息，请参阅[为UUID引用升级内容片段](/help/headless/graphql-api/uuid-reference-upgrade.md)。

>[!NOTE]
>
AEM 对于以下各项具有重复保护：
>
* 内容引用
这会阻止用户添加对当前片段的引用，并可能导致出现空的片段引用选取器对话框。
>
* GraphQL中的片段引用
如果创建一个深层查询，且该查询返回多个相互引用的内容片段，则该查询在第一次出现时返回null。

>[!CAUTION]
>
如果要查询多个引用的片段，则建议不要让各种片段模型具有具有相同名称但类型不同的字段名称。
>
有关详细信息，请参阅用于内容片段的[AEM GraphQL API — 限制](/help/headless/graphql-api/content-fragments.md#limitations)

### 内容引用 {#content-reference}

**内容引用**&#x200B;和&#x200B;**内容引用(UUID)**&#x200B;数据类型允许您呈现来自其他源的内容；例如，图像、页面或体验片段。

除了标准属性之外，您还可以指定：

* **根路径**，它指定或表示存储任何引用内容的位置
  >[!NOTE]
  >
  如果您在使用内容片段编辑器时要在此字段中直接上传并引用图像，则必须指定此属性。
  >
  有关进一步详细信息，请参阅[引用图像](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images)。

* 可引用的内容类型
  >[!NOTE]
  >
  如果您在使用内容片段编辑器时要直接在此字段中上传并引用图像，则其中必须包括&#x200B;**图像**。
  >
  有关进一步详细信息，请参阅[引用图像](/help/sites-cloud/administering/content-fragments/authoring.md#reference-images)。

* 文件大小限制
* 如果引用了图像：
   * 显示缩略图
   * 图像高度和宽度的限制

![内容引用](assets/cf-cfmodels-content-reference.png)

### 片段引用（嵌套片段） {#fragment-reference-nested-fragments}

**片段引用**&#x200B;和&#x200B;**片段引用(UUID)**&#x200B;数据类型可以引用一个或多个内容片段。 在检索内容以供用于您的应用程序时，此功能尤其值得关注，因为通过此功能可检索有多层的结构化数据。

例如：

* 定义员工详细信息的模型；包括：
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
>
片段引用对于[通过 GraphQL 使用内容片段投放 Headless 内容](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md)尤其值得关注。

除了标准属性之外，您还可以定义：

* **呈现为**:

   * **多字段** – 片段作者可以创建多个单个引用

   * **片段** – 允许片段作者选择对片段的单个引用

* **模型类型**
可以选择多个模型。在添加对内容片段的引用时，必须使用这些模型创建任何引用的片段。

* **根路径**
这会指定或表示引用的任何片段的根路径。

* **允许创建片段**

  这将允许片段作者根据相应的模型创建片段。

   * **片段引用组合** – 允许片段作者通过选择多个片段来构建复合

  ![片段引用](assets/cf-cfmodels-fragment-reference.png)

>[!NOTE]
>
已建立重复保护机制。它禁止用户在片段引用中选择当前内容片段，可能导致片段引用选取器对话框为空。
>
GraphQL 中也有针对片段引用的重复保护。如果在两个互相引用的内容片段之间创建深层查询，则它返回 null。

## 启用或禁用内容片段模型 {#enabling-disabling-a-content-fragment-model}

可&#x200B;**启用**&#x200B;或&#x200B;**禁用**&#x200B;内容片段模型，从而全面控制其使用。

### 启用内容片段模型 {#enabling-a-content-fragment-model}

创建模型后必须启用它，以使其：

* 可在创建内容片段时进行选择。
* 可以在内容片段模型中引用。
* 可用于 GraphQL；这样就会生成架构。

要启用标记为以下任一类型的模型：

* **草稿**：新（从未启用）。
* **已禁用**：已被特别禁用。

您可以从以下任一位置使用&#x200B;**“启用”**&#x200B;选项：

* 选择所需的“模型”时，顶部工具栏。
* 相应的快速操作（将鼠标悬停在所需模型上）。

![启用草稿或禁用的模型](assets/cf-cfmodels-status-enable.png)

### 禁用内容片段模型 {#disabling-a-content-fragment-model}

也可以禁用模型，这样：

* 该模型将无法再用来创建&#x200B;*新*&#x200B;内容片段。
* 但是:
   * GraphQL 架构一直在生成，并且仍可查询（以避免影响 JSON API）。
   * 仍可以从 GraphQL 端点查询和返回任何基于模型的内容片段。
* 该模型无法再次引用，但现有引用将保持不变，并且仍可以从 GraphQL 端点查询和返回。

要禁用标为&#x200B;**已启用**&#x200B;的模型，可从以下任意一处使用&#x200B;**禁用**&#x200B;选项：

* 选择所需的“模型”时，顶部工具栏。
* 相应的快速操作（将鼠标悬停在所需模型上）。

![禁用启用的模型](assets/cf-cfmodels-status-disable.png)

## 允许在 Assets 文件夹中使用内容片段模型 {#allowing-content-fragment-models-assets-folder}

要实施内容管理，您可以在 Assets 文件夹中配置&#x200B;**策略**，以控制允许在该文件夹中创建片段的内容片段模型。

>[!NOTE]
>
该机制类似于[允许在页面的高级属性](/help/sites-cloud/authoring/page-editor/templates.md#allowing-a-template-author)中为页面及其子页面设置页面模板。

要为&#x200B;**允许的内容片段模型**&#x200B;配置&#x200B;**策略**：

1. 导航并打开&#x200B;**属性**，以访问所需的 Assets 文件夹。

1. 打开&#x200B;**策略**&#x200B;选项卡，您可以在其中配置：

   * **继承自`<folder>`**

     在创建新的子文件夹时自动继承策略；如果子文件夹需要允许模型与父文件夹不同，则可重新配置策略（并中断继承）。

   * **按照路径允许的内容片段模型**

     可以允许使用多个模型。

   * **按标记允许的内容片段模型**

     可以允许使用多个模型。

   ![内容片段模型策略](assets/cf-cfmodels-policy-assets-folder.png)

1. **保存**&#x200B;任何更改。

文件夹允许的内容片段模型解析如下：
* 针对&#x200B;**允许的内容片段模型**&#x200B;的&#x200B;**策略**。
* 如果为空，请尝试使用继承规则确定策略。
* 如果继承链未投放结果，请查看 **Cloud Services** 文件夹的配置（也请先直接配置，然后通过继承配置）。
* 如果以上所有内容均未提供任何结果，则该文件夹不允许使用模型。

## 删除内容片段模型 {#deleting-a-content-fragment-model}

>[!CAUTION]
>
删除内容片段模型可能会影响从属片段。

要删除内容片段模型，请执行以下操作：

1. 导航到&#x200B;**工具**、**常规**，然后打开&#x200B;**内容片段模型**。

1. 导航到容纳您的内容片段模型的文件夹。
1. 选择您的模型，然后从工具栏中选择&#x200B;**删除**。

   >[!NOTE]
   >
   如果引用该模型，则显示一条警告，以使您可执行适当的操作。

## 发布内容片段模型 {#publishing-a-content-fragment-model}

需要在发布任何从属的内容片段时/之前发布内容片段模型。

要发布内容片段模型，请执行以下操作：

1. 导航到&#x200B;**工具**、**常规**，然后打开&#x200B;**内容片段模型**。

1. 导航到容纳您的内容片段模型的文件夹。
1. 选择您的模型，然后从工具栏中选择&#x200B;**发布**。随后将在控制台中显示已发布状态。

   >[!NOTE]
   >
   如果发布尚未发布其模型的内容片段，则将有一个选择列表指出这一点，并将与该片段一起发布模型。

## 取消发布内容片段模型 {#unpublishing-a-content-fragment-model}

如果没有任何片段引用内容片段模型，则可取消发布这些模型。

要取消发布内容片段模型，请执行以下操作：

1. 导航到&#x200B;**工具**、**常规**，然后打开&#x200B;**内容片段模型**。

1. 导航到容纳您的内容片段模型的文件夹。
1. 选择您的模型，然后从工具栏中选择&#x200B;**取消发布**。控制台中会指示已发布状态。

如果尝试取消发布当前由一个或多个片段使用的模型，则显示一条错误警告。例如：

![取消发布正在使用的模型时的内容片段模型错误消息](assets/cf-cfmodels-unpublish-error.png)

该消息建议您检查[引用](/help/sites-cloud/authoring/basic-handling.md#references)面板以进一步调查：

![引用中的内容片段模型](assets/cf-cfmodels-references.png)

## 锁定（已发布）内容片段模型 {#locked-published-content-fragment-models}

此功能为已发布的内容片段模型提供管理服务。

### 挑战 {#the-challenge}

* 内容片段模型确定 AEM 中 GraphQL 查询的架构。

   * AEM GraphQL 架构在创建内容片段模型后即会创建，并且它们可以同时存在于创作和发布环境中。

   * 发布架构是最为关键，因为它们为 JSON 格式的内容片段的实时投放奠定了基础。

* 修改内容片段模型或进行其他编辑时，可能会出现问题。这意味着架构发生更改，进而可能影响现有 GraphQL 查询。

* 向内容片段模型添加新字段通常不应产生任何有害影响。但是，修改现有数据字段（例如，其名称）或删除字段定义时，将在请求这些字段时中断现有 GraphQL 查询。

### 要求 {#the-requirements}

* 使用户了解在编辑已用于实时内容投放的模型（即已发布的模型）时的风险。

* 此外，还可以避免意外的更改。

如果重新发布经过修改的模型，则这些条件中的任意一项都可能会中断查询。

### 解决方案 {#the-solution}

为了解决这些问题，内容片段模型在发布后立即在作者上被&#x200B;*锁定为*&#x200B;只读模式。**已锁定**&#x200B;指示此状态：

![锁定内容片段模型的信息卡](assets/cf-cfmodels-locked.png)

当模型&#x200B;**已锁定**（在“只读”模式下），您可以查看模型的内容和结构，但无法进行编辑。

您可以从控制台或模型编辑器中管理&#x200B;**已锁定**&#x200B;模型：

* 控制台

  从控制台中，您可以使用&#x200B;**解锁**&#x200B;和&#x200B;**锁定**&#x200B;操作管理制度模式：

  ![锁定的内容片段模型的工具栏](assets/cf-cfmodels-locked.png)

   * 您可以&#x200B;**解锁**&#x200B;用于启用编辑的模型。

     如果您选择&#x200B;**解锁**，则显示一条警告，而您必须确认&#x200B;**解锁**操作：
     ![解锁内容片段模型时的消息](assets/cf-cfmodels-unlock-message.png)

     然后，可以打开模型进行编辑。

   * 您之后还可以&#x200B;**锁定**&#x200B;模型。
   * 重新发布模型将立即使它恢复&#x200B;**已锁定**（只读）模式。

* 模型编辑器

   * 打开锁定的模型时，系统会发出警告，并会显示三个操作：**取消**、**查看只读**、**编辑**：

     ![查看锁定的内容片段模型时的消息](assets/cf-cfmodels-editor-lock-message.png)

   * 如果您选择&#x200B;**查看只读**，则您可以查看模型的内容和结构：

     ![查看只读 – 锁定的内容片段模型](assets/cf-cfmodels-editor-locked-view-only.png)

   * 如果您选择&#x200B;**编辑**，则您可以编辑并保存您的更新：

     ![编辑 – 锁定的内容片段模型](assets/cf-cfmodels-editor-locked-edit.png)

     >[!NOTE]
     >
     顶部可能仍会显示警告，但此时模型已由现有内容片段使用。

   * **取消**&#x200B;将带您返回控制台。
