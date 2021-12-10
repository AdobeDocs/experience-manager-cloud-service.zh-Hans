---
title: 自适应表单片段
seo-title: Adaptive Form Fragments
description: 自适应Forms提供了一种机制来创建表单区段，如面板或一组字段，以将其用在任何自适应表单中。 您还可以将现有面板另存为片段。
seo-description: Adaptive Forms provides a mechanism to create a form segment, such as a panel or a group of fields, as use it in any Adaptive Form. You can also save an existing panel as fragment.
uuid: bb4830b5-82a0-4026-9dae-542daed10e6f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '2003'
ht-degree: 1%

---


# 自适应表单片段{#adaptive-form-fragments}

虽然每个表单都是专门为特定目的而设计的，但大多数表单中都有一些常见的区段，例如，提供个人详细信息，如姓名和地址、家庭详细信息、收入详细信息等。 每次创建新表单时，表单开发人员都需要创建这些通用区段。

自适应Forms提供了一种便捷的机制，只需像创建面板或一组字段一样创建表单区段一次，即可在自适应Forms中重复使用。 这些可重用的独立区段称为自适应表单片段。

## 创建片段 {#create-a-fragment}

您可以从头开始创建自适应表单片段，或将现有自适应表单中的面板另存为片段。

### 从头开始创建片段 {#create-fragment-from-scratch}

1. 登录 [!DNL AEM Forms] https://中的创作实例&#x200B;[*主机名*]:[*端口*]/aem/forms.html。
1. 单击 **创建>自适应表单片段**.
1. 为片段指定标题、名称、描述和标记。

   >[!NOTE]
   >
   >确保为片段指定唯一名称。 如果已存在具有相同名称的其他片段，则无法创建该片段。

1. 单击以打开 **表单模型** ，并从 **选择自** 下拉菜单中，为片段选择以下模型之一：

   * **无**:指定从头开始创建片段，而不使用任何表单模型。
   * **表单模板**:指定使用上传到的XDP模板创建片段 [!DNL AEM Forms]. 选择相应的XDP模板作为片段的表单模型。

   ![使用表单模板作为模型创建自适应表单](assets/form-template-model.png)

   此外，还会显示选定表单模板中标记为片段的子表单。 您可以从下拉列表中选择自适应表单片段的子表单。

   ![从指定的表单模板中选择子表单](assets/fragment-subform.png)

   此外，您还可以使用表单模板中未标记为片段的子表单创建自适应表单片段，方法是在下拉框中为子表单指定SOM表达式。

   * **XML架构**:指定使用上传到的XML架构创建片段 [!DNL AEM Forms]. 您可以从可用的XML架构上传或选择作为片段的表单模型。

   ![基于XML架构作为模型创建自适应表单片段](assets/xml-schema-model.png)

   您还可以通过从下拉框中选择选定架构中存在的complexType来创建自适应表单片段。

   ![从指定的XML架构模型中选择复杂类型](assets/complex-type.png)

1. 单击 **创建** 然后单击 **打开** 在编辑模式下使用默认模板打开片段。

在编辑模式下，您可以将任何自适应表单组件从AEM Sidekick拖放到片段上。 <!-- For information about Adaptive Form components, see Introduction to authoring Adaptive Forms. -->

此外，如果您选择XML架构或XDP表单模板作为片段的表单模型，则内容查找器中会显示一个显示表单模型层次结构的新选项卡。 它允许您将表单模型元素拖放到片段上。 添加的表单模型元素将转换为表单组件，同时保留关联XDP或XSD中的原始属性。

### 将面板另存为片段 {#save-panel-as-a-fragment}

1. 打开一个自适应表单，其中包含要另存为自适应表单片段的面板。
1. 在面板工具栏中，单击 **[!UICONTROL 另存为片段]**. 将打开另存为片段对话框。

   >[!NOTE]
   >
   >如果要另存为片段的面板包含子面板，则生成的片段将包含它们。

1. 在片段创建对话框中，指定以下信息：

   * **名称**:片段的名称。 默认值是面板的元素名称。 它是必填字段。
      >[!NOTE]
      >
      >确保为片段指定唯一名称。 如果已存在具有相同名称的其他片段，则无法创建该片段。

   * **标题**:片段的标题。 默认值是面板的标题。

   * **描述**:片段的描述。

   * **标记**:片段的标记元数据。

   * **目标路径**:保存片段的存储库路径。 如果未指定路径，则会在包含自适应表单的节点旁边创建与片段名称同名的节点。 片段保存在此节点中。

   * **表单模型**:根据自适应表单的表单模型，此字段显示 **XML架构**, **表单模板**&#x200B;或 **无**. 它是一个不可编辑的字段。

   * **片段模型根**:仅在基于XSD的自适应Forms中显示。 它指定片段模型的根。 您可以选择 **/** 或下拉列表中的XSD复杂类型。 请注意，仅当选择复杂类型作为片段模型根时，才能在另一个自适应表单中重复使用该片段。
如果您选择 **/** 作为片段模型根，根中的完整XSD树在“自适应表单数据模型”选项卡中可见。 对于复杂类型片段模型根，“自适应表单数据模型”选项卡中只显示所选复杂类型的子体。

   * **XSD引用**:仅在基于XSD的自适应Forms中显示。 它显示XML架构的位置。

   * **XDP参考**:仅在基于XDP的自适应Forms中显示。 它会显示XDP表单模板的位置。

   ![保存片段](assets/save-fragment.png)

   另存为片段对话框

1. 单击&#x200B;**确定**。

   面板保存在存储库中的指定或默认位置。 在自适应表单中，面板将被片段的快照替换。 如下所示，“常规信息”面板及其子面板“个人信息和地址”将另存为片段。

   要编辑片段，请单击 **[!UICONTROL 编辑资产]** 中。 片段在编辑模式下的新选项卡或窗口中打开。

   ![编辑片段](assets/edit-fragment.png)

## 使用片段 {#working-with-fragments}

### 配置片段外观 {#configure-fragment-appearance}

您在自适应Forms中插入的任何片段都显示为占位符图像。 占位符在片段中显示最多十个子面板的标题。 您可以配置 [!DNL AEM Forms] 以显示完整片段，而不是占位符图像。

执行以下步骤以在表单中显示完整片段：

1. 转到位于https的AEM Web控制台配置页面：[*主机*]:[*端口*]/system/console/configMgr。

1. 搜索并单击 **[!UICONTROL 自适应表单配置服务]** 以在编辑模式下将其打开。
1. 禁用 **[!UICONTROL 启用占位符代替片段]** 复选框以显示完整片段，而不是占位符图像。

### 在自适应表单中插入片段 {#insert-a-fragment-in-an-adaptive-form}

您创建的自适应表单片段显示在AEM内容查找器的自适应表单片段选项卡中。 要在自适应表单中插入自适应表单片段，请执行以下操作：

1. 在编辑模式下打开自适应表单，您要在该模式下插入自适应表单片段。
1. 单击 **资产** ![assets-browser](assets/assets-browser.png) 中。 在资产浏览器中，选择 **自适应表单片段** 从下拉菜单中。

   您还可以选择显示所有自适应表单片段或根据其表单模型（表单模板、XML架构或基本）进行过滤。

1. 将自适应表单片段拖放到自适应表单上。

   >[!NOTE]
   >
   >未启用自适应表单片段以在自适应表单中进行创作。 此外，您不能在基于JSON的自适应表单中使用基于XSD的片段，反之。

自适应表单片段由引用插入到自适应表单中，并与独立的自适应表单片段同步。 这意味着当您更新自适应表单片段时，所做的更改将反映在使用该片段的所有自适应Forms中。

### 在自适应表单中嵌入片段 {#embed-a-fragment-in-adaptive-form}

您可以通过单击 **嵌入资产：&lt;*fragmentName*>** 按钮，如以下示例图像中所示。

![在自适应表单中嵌入表单片段](assets/embed-fragment.png)

>[!NOTE]
>
>嵌入式片段不再与独立片段链接。 您可以从自适应表单中编辑嵌入片段中的组件。

### 在片段中使用片段 {#using-fragments-within-fragments}

您可以创建嵌套的自适应表单片段，这意味着您可以将一个片段拖放到另一个片段中，并且可以具有嵌套的片段结构。

### 更改片段 {#change-fragments}

您可以使用 **选择片段资产** 属性。

## 为数据绑定自动映射片段 {#auto-mapping-of-fragments-for-data-binding}

当您使用XFA表单模板或XSD复杂类型创建自适应表单片段并将该片段拖放到自适应表单时，XFA片段或XSD复杂类型将自动替换为相应的自适应表单片段，其片段模型根目录映射到XFA片段或XSD复杂类型。

您可以从编辑组件对话框中更改片段资产及其绑定。

>[!NOTE]
>
>您还可以在AEM内容查找器中，从自适应表单片段库中拖放绑定的自适应表单片段，并从自适应表单片段面板的编辑组件对话框中提供正确的绑定引用。

## 管理片段 {#manage-fragments}

您可以使用 [!DNL AEM Forms] UI。

1. 转到 `https://[hostname]:'port'/aem/forms.html`.

1. 单击 **选择** 在 [!DNL AEM Forms] UI工具栏中，然后选择自适应表单片段。 工具栏显示您可以对所选自适应表单片段执行的以下操作。

<table>
 <tbody>
  <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
  </tr>
  <tr>
   <td><p>打开</p> </td>
   <td><p>在编辑模式下打开选定的自适应表单片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>查看属性</p> </td>
   <td><p>打开“属性”面板。 从“属性”面板中，您可以查看和编辑属性、生成预览以及上传选定片段的缩略图。 有关更多信息，请参阅 <a href="manage-form-metadata.md" target="_blank">管理元数据</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>复制</p> </td>
   <td><p>复制所选片段。 “粘贴”按钮将显示在工具栏中。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>下载</p> </td>
   <td><p>下载所选片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>预览</p> </td>
   <td><p>提供用于通过将XML文件中的数据与片段合并来将片段作为HTML或自定义预览来预览的选项。 <!-- For more information, see <a href="previewing-forms.md" target="_blank">Previewing a form</a>.<br /> <br /> --></p> </td>
  </tr>
  <tr>
   <td><p>开始审阅/管理审阅</p> </td>
   <td><p>允许启动和管理所选片段的审阅。 <!-- For more information, see <a href="create-reviews-forms.md" target="_blank">Creating and managing reviews</a>.<br /> <br /> </p> --> </td>
  </tr>
  <tr>
   <td><p>创建字典</p> </td>
   <td><p>生成用于本地化所选片段的字典。 <!-- For more information, see <a href="lazy-loading-adaptive-forms.md" target="_blank">Localizing Adaptive Forms</a>.<br /> <br /> --> </p> </td>
  </tr>
  <tr>
   <td><p>发布/取消发布</p> </td>
   <td><p>发布/取消发布选定的片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>删除</p> </td>
   <td><p>删除所选片段。<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## 本地化包含片段的自适应表单 {#localizing-adaptive-form-containing-fragments}

要将包含自适应表单片段的自适应表单本地化，您需要将片段和表单分别本地化。 其思想是将片段本地化一次，并在多个自适应Forms中重复使用。

>[!NOTE]
>
>片段中的本地化键不会显示在自适应表单的XLIFF文件中。

## 使用片段时要记住的要点 {#key-points-to-remember-when-working-with-fragments}

* 确保片段名称是唯一的。 如果存在具有相同名称的现有片段，则无法创建该片段。
* 在基于XDP的自适应表单中，如果将面板另存为包含其他XDP片段的片段，则生成的片段将自动绑定到子XDP片段。 如果是基于XSD的自适应表单，则生成的片段将绑定到架构根。
* 创建自适应表单片段时，将创建一个片段节点，该节点类似于CRXDe Lite中自适应表单的guideContainer节点。
* 不支持自适应表单中使用不同表单数据模型的片段。 例如，基于XSD的自适应表单中不支持基于XDP的片段，反之亦然。
* 自适应表单片段可通过AEM内容查找器中的自适应表单片段选项卡使用。
* 独立自适应表单片段中的任何表达式、脚本或样式在通过引用插入或嵌入自适应表单时会保留。
* 您无法从自适应表单中编辑通过引用插入的自适应表单片段。 要进行编辑，您可以编辑独立的自适应表单片段，或将该片段嵌入自适应表单中。
* 发布自适应表单时，您需要发布由引用插入到自适应表单中的独立自适应表单片段。
* 当您重新发布更新的自适应表单片段时，所做的更改会反映在使用片段的自适应表单的已发布实例中。
* 包含验证组件的自适应表单不支持匿名用户。 此外，不建议在自适应表单片段中使用验证组件。
* (**仅Mac**)要确保表单片段功能在所有情况下都能正常工作，请将以下条目添加到/private/etc/hosts文件中：
   `127.0.0.1 <Host machine>` **主机**:Apple·Mac的机器 [!DNL AEM Forms] 已部署。

## 引用片段 {#reference-fragments}

可以使用引用自适应表单片段来创建表单。 有关更多信息，请参阅 [引用片段](reference-adaptive-form-fragments.md).
