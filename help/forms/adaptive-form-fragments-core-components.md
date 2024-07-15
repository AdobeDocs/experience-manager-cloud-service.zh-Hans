---
title: 什么是自适应表单片段？
description: 自适应Forms提供了一种机制，可创建在任何自适应表单中使用的表单区段，例如面板或一组字段。 您还可以将现有面板另存为片段。
topic-tags: author
keywords: 添加自适应表单片段、自适应表单片段、创建表单片段、将片段添加到自适应表单、管理片段
feature: Adaptive Forms, Core Components
exl-id: 3a9ad1b7-2f6f-4ca9-a1c9-549c4238c59e
role: User, Developer
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 6%

---

# 在基于核心组件的自适应表单中创建和使用自适应Forms片段 {#adaptive-form-fragments}


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service（核心组件） | 本文 |
| AEM as a Cloud Service（基础组件） | [单击此处](/help/forms/adaptive-form-fragments.md) |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/adaptive-form-fragments.html) |

虽然每个表单都针对特定目的而设计，但大多数表单中都存在一些通用区段，例如提供个人详细信息，如姓名和地址、家庭详细信息、收入详细信息。 每次创建新表单时，表单开发人员都需要创建这些常用区段。

自适应Forms提供了一种便捷的机制，只需像创建面板或一组字段一样创建表单片段一次，即可在自适应Forms中重复使用。 这些可重用的独立区段称为自适应表单片段。

表单片段无缝集成到多个表单中，从而简化了创建一致且具有专业外观的表单的过程。 利用“一次更改，随处反映”功能，表单片段确保实现可重用性、标准化和品牌一致性。由于在一处作出的更新自动传播到所有利用这些片段的表单，因此可体验到更高的可维护性和效率。

您可以将片段多次添加到文档，并使用其组件的数据绑定属性将其绑定到不同的数据源或架构。 例如，您可以将相同的地址片段用于永久地址、通信地址和账单地址，并将它连接到数据源或架构的其他字段。

>[!NOTE]
>
> 您可以使用表单片段组件](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/adaptive-form-fragment)的[配置对话框和设计对话框轻松自定义用户的片段体验。

## 创建自适应表单片段 {#create-a-fragment}

您可以从头开始创建自适应表单片段，或将现有自适应表单中的面板另存为片段。 要创建表单片段，请执行以下操作：

1. 登录您的AEM Forms实例，网址为https://[*主机名*]：[*端口*]/aem/forms.html。
1. 单击&#x200B;**创建>自适应表单片段**。

   ![创建自适应表单片段](/help/forms/assets/adaptive-form-fragment.png)

1. 指定片段的标题、名称、描述和标记。 请确保为片段指定唯一的名称。 如果存在具有相同名称的其他片段，则无法创建该片段。
1. 选择表单模板。 您可以为基于核心组件的自适应Forms或基于基础组件的自适应Forms创建表单片段。 要为基于核心组件的表单创建表单片段，请选择一个基于核心组件的模板。

   为基于核心组件的表单创建表单片段时，使用选择表单主题选项选择基于核心组件的主题。

1. 单击以打开&#x200B;**表单模型**&#x200B;选项卡，从&#x200B;**选择自**&#x200B;下拉菜单中，为片段选择以下模型之一：

   ![在表单模型选项卡中显示模型类型](assets/create-af-1-1.png)

   * **无**：指定从头开始创建片段，而不使用任何表单模型。

     >[!NOTE]
     >
     > 在自适应Forms中，您可以多次使用单个表单片段（基于核心组件）。 它支持基于无和基于架构的表单片段。

   * **架构**：指定使用上载到AEM Forms的XML或JSON架构创建片段。 您可以上传或从可用的XML或JSON架构中选择作为片段的表单模型。 选择XML架构时，您还可以通过从&#x200B;**[!UICONTROL XML架构复杂类型]**&#x200B;下拉框中选择所选架构中存在的complexType来创建自适应表单片段。 选择JSON架构时，您还可以通过从&#x200B;**[!UICONTROL JSON架构定义]**&#x200B;下拉框中选择所选架构中存在的架构定义来创建自适应表单片段。
   * **表单数据模型**：指定使用表单数据模型(FDM)创建片段。 您可以仅基于表单数据模型(FDM)中的一个数据模型对象创建自适应表单片段。 展开表单数据模型(FDM)定义下拉列表。 它列出了指定表单数据模型(FDM)中的所有数据模型对象。 从列表中选择数据模型对象。

   ![表单数据模型(FDM)](assets/create-af-3.png)

1. 单击“**创建**”，然后单击“**打开**”以使用默认模板在编辑模式下打开片段。 在编辑模式下，您可以将任何自适应表单组件添加到片段。

<!-- For information about Adaptive Form components, see [Introduction to authoring Adaptive Forms](../../forms/using/introduction-forms-authoring.md). --> 此外，如果选择XML架构作为片段的表单模型，则内容查找器中会显示一个显示表单模型层次结构的新选项卡。 它可让您将表单模型元素拖放到片段上。<!--The added form-model elements get converted into form components while retaining the original properties from the associated XDP or XSD. -->

创建基于架构或表单数据模型(FDM)的自适应表单片段后，表单数据模型(FDM)或架构元素会显示在自适应表单编辑器的内容浏览器的数据源选项卡中。 您可以将表单模型元素拖放到片段上。 添加的表单模型元素转换为表单组件，同时保留关联架构中的原始属性。


## 将片段添加到自适应表单 {#insert-a-fragment-in-an-adaptive-form}

要将自适应表单片段添加到自适应表单：

1. 在编辑模式下打开自适应表单。
1. 将&#x200B;**自适应表单片段**&#x200B;组件添加到表单中。
1. 打开&#x200B;**自适应表单片段**&#x200B;组件的“配置”对话框。
1. 在&#x200B;**基本**&#x200B;选项卡中选择&#x200B;**片段引用**。 您的表单可用的所有自适应Forms片段都会显示，具体取决于表单的模型。

1. 选择自适应表单片段到您的自适应表单上的&#x200B;**自适应表单片段**&#x200B;组件上。

   ![选择自适应表单片段选项](/help/forms/assets/adaptive-form-fragment-basic.png)

<!-- >[!NOTE]
   >
   >The Adaptive Form fragment is not enabled for authoring from within the Adaptive Form. Moreover, you cannot use an XSD-based fragment in a JSON-based Adaptive Form and the opposite way. -->

自适应表单片段是通过引用自适应表单添加的，并与独立的自适应表单片段保持同步。 这意味着对自适应表单片段所做的任何修改都会在片段合并到自适应Forms的所有实例中镜像。

<!--### Embed a fragment in Adaptive Form {#embed-a-fragment-in-adaptive-form}

You can choose to embed an Adaptive Form fragment in an Adaptive Form by clicking the ![Embed](assets/Smock_Import_18_N.svg) icon the panel toolbar of the added fragment

The embedded fragment is no longer linked with the standalone fragment. You can edit the components in the embedded fragment from within the Adaptive Form.-->

<!-- 
## Configure fragment appearance {#configure-fragment-appearance}

Any fragment you insert in Adaptive Forms appears as a placeholder image. The placeholder displays titles of up to a maximum of ten child panels in the fragment. You can configure AEM Forms to show the complete fragment instead of the placeholder image.

Perform the following steps to show complete fragments in forms:

1. Go to AEM web console configuration page at https:[*host*]:[*port*]/system/console/configMgr.

1. Search and click **[!UICONTROL Adaptive Form and Interactive Communication Web Channel Configuration]** to open it in edit mode.
1. Disable **[!UICONTROL Enable Placeholder in place of Fragment]** checkbox to show complete fragments rather than the placeholder image.

-->

### 在片段中使用片段 {#using-fragments-within-fragments}

您可以创建嵌套式自适应表单片段，这意味着您可以向其他片段添加片段，并且可以具有嵌套式片段结构。

### 在自适应表单中多次使用表单片段 {#using-form-fragment-mutiple-times-in-af}

您可以在自适应表单中多次使用基于无和基于架构的表单片段，以唯一地保存每个表单片段字段的数据。 例如，您可以使用地址表片段收集地址详细信息，以便在贷款申请表中永久性、通信和显示生活地址。

![在自适应表单中使用多个片段](/help/forms/assets/using-multiple-fragment-af.gif)

<!--

## Auto mapping of fragments for data binding {#auto-mapping-of-fragments-for-data-binding}

When you create an Adaptive Form fragment using an XFA form template or XSD complex type and drag-drop the fragment to an Adaptive Form, the XFA fragment or the XSD complex type is automatically replaced by the corresponding Adaptive Form fragment whose fragment model root is mapped to the XFA fragment or XSD complex Type.

You can change the fragment asset and its bindings from the Edit component dialog.

You can also drag-drop a bound Adaptive Form fragment from Adaptive Form Fragment library in AEM content finder and provide the correct bind reference from the Edit component dialog of the Adaptive Form fragment panel. -->

## 管理片段 {#manage-fragments}

您可以使用AEM Forms UI对自适应表单片段执行多项操作。

1. 转到 `https://[hostname]/aem/forms.html`.

1. 单击AEM Forms UI工具栏中的&#x200B;**选择**，然后选择自适应表单片段。 工具栏显示您可以对选定的自适应表单片段执行的以下操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>编辑</p> </td>
   <td><p>在编辑模式下打开选定的自适应表单片段。<br /> <br /> </p> </td>
  </tr>
   <tr>
   <td><p>预览</p> </td>
   <td><p>提供选项，用于将XML文件中的数据与片段合并，以HTML形式预览片段或自定义预览。 有关详细信息，请参阅<a>预览表单</a>。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>下载</p> </td>
   <td><p>下载所选片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>开始审核/管理审核</p> </td>
   <td><p>允许启动和管理对所选片段的审核。 有关详细信息，请参阅<a>创建和管理审核</a>。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>新增字典</p> </td>
   <td><p>生成用于本地化所选片段的字典。 有关详细信息，请参阅<a>本地化自适应Forms</a>。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publish/取消发布</p> </td>
   <td><p>发布/取消发布选定的片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>删除</p> </td>
   <td><p>删除所选片段。<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## 使用片段时要记住的要点 {#key-points-to-remember-when-working-with-fragments}

* 确保片段名称是唯一的。 如果存在具有相同名称的现有片段，则创建片段失败。
* 通过引用插入或嵌入自适应表单中的独立自适应表单片段中的任何表达式、脚本或样式都会保留。
* 您无法从自适应表单中编辑通过引用插入的自适应表单片段。 要编辑，请修改独立的自适应表单片段。
* 发布自适应表单时，您需要发布在自适应表单中通过引用插入的独立自适应表单片段。
* 当您重新发布更新的自适应表单片段时，更改会反映在使用片段的自适应表单的已发布实例中。
* 包含Verify组件的自适应表单不支持匿名用户。 此外，不建议在自适应表单片段中使用验证组件。

## 引用片段 {#reference-fragments}

提供了可用于创建表单的参考自适应表单片段。
<!-- For more information, see [Reference Fragments](../../forms/using/reference-adaptive-form-fragments.md). -->



## 另请参阅 {#see-also}

{{see-also}}