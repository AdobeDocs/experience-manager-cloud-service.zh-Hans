---
title: 如何创建和使用自适应表单片段？
description: 表单片段是表单的一个模块化且可重用的组件。 了解如何构建表单片段并在表单间重复使用它们以实现高效的表单装配。
uuid: bb4830b5-82a0-4026-9dae-542daed10e6f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
exl-id: e4d8bcb9-ce1f-425e-b35c-d0a79fa771f3
role: User, Developer
source-git-commit: bcd3a2a813833d7c1705e45829bcf769645cd154
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 1%

---

# 在自适应表单中创建和使用自适应Forms片段  {#adaptive-form-fragments}


| 版本 | 文章链接 |
| -------- | ---------------------------- |
| AEM as a Cloud Service（基础组件） | 本文 |
| AEM as a Cloud Service（核心组件） | [单击此处](/help/forms/adaptive-form-fragments-core-components.md) |
| AEM 6.5 | [单击此处](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/adaptive-form-fragments.html?lang=zh-Hans) |

虽然每个表单都是为特定目的而设计的，但大多数表单中都有一些常见的部分，例如提供个人详细信息，如姓名和地址、家庭详细信息、收入详细信息等。 每次创建新表单时，表单开发人员都需要创建这些常用区段。 自适应表单提供了一种便捷的机制，只需创建一次表单段（如面板或一组字段），并在自适应表单中重复使用它们。 这些可重用的独立区段称为自适应表单片段。


## 创建片段 {#create-a-fragment}

您可以从头开始创建自适应表单片段，或将现有自适应表单中的面板另存为片段。

### 从头开始创建片段 {#create-fragment-from-scratch}

1. 登录到 [!DNL AEM Forms] 作者实例，网址为 https://[*hostname*]：[*port*]/aem/forms.html。
1. 单击“ **创建>自适应表单片段**”。
1. 指定片段的标题、名称、描述和标签。

   >[!NOTE]
   >
   >请确保为片段指定唯一的名称。 如果已存在另一个同名片段，则创建片段失败。

1. 单击以打开&#x200B;**表单模型**&#x200B;选项卡，从&#x200B;**选择自**&#x200B;下拉菜单中，为片段选择以下模型之一：

   * **无**：指定从头开始创建片段，而不使用任何表单模型。

     >[!NOTE]
     >
     > 在自适应Forms中，您可以在表单中多次使用单个表单片段（基于核心组件）。 它支持基于无和基于架构的表单片段。

   * **表单模板**：指定使用上载到[!DNL AEM Forms]的XDP模板创建片段。 选择适当的XDP模板作为片段的表单模型。

   ![使用表单模板作为模型创建自适应表单](assets/form-template-model.png)

   还会显示选定表单模板中标记为片段的子表单。 您可以从下拉列表中选择自适应表单片段的子表单。

   ![从指定的表单模板中选择子表单](assets/fragment-subform.png)

   此外，您还可以通过在下拉框中指定子表单的SOM表达式，使用在表单模板中未标记为片段的子表单创建自适应表单片段。

   * **XML架构**：指定使用上载到[!DNL AEM Forms]的XML架构创建片段。 您可以上传或从可用的XML架构中选择作为片段的表单模型。

   ![创建基于XML架构的自适应表单片段作为模型](assets/xml-schema-model.png)

   您还可以通过从下拉框中选择所选架构中存在的complexType来创建自适应表单片段。

   ![从指定的XML架构模型中选择复杂类型](assets/complex-type.png)

1. 单击“**创建**”，然后单击“**打开**”以使用默认模板在编辑模式下打开片段。

在编辑模式下，您可以将任何自适应表单组件从AEM Sidekick拖放到片段上。<!-- For information about Adaptive Form components, see Introduction to authoring Adaptive Forms. -->

此外，如果您选择了XML架构或XDP表单模板作为片段的表单模型，则内容查找器中会显示一个显示表单模型层次结构的新选项卡。 它可让您将表单模型元素拖放到片段上。 添加的表单模型元素被转换为表单组件，同时保留关联XDP或XSD的原始属性。

### 将面板另存为片段 {#save-panel-as-a-fragment}

1. 打开自适应表单，其中包含要另存为自适应表单片段的面板。
1. 在面板工具栏中，单击&#x200B;**[!UICONTROL 另存为片段]**。 另存为片段对话框随即打开。

   >[!NOTE]
   >
   >如果要另存为片段的面板包含子面板，则生成的片段将包含这些子面板。

1. 在片段创建对话框中，指定以下信息：

   * **名称**：片段的名称。 默认值为面板的元素名称。 它是必填字段。

     >[!NOTE]
     >
     >请确保为片段指定唯一的名称。 如果已存在另一个同名片段，则创建片段失败。

   * **标题**：片段的标题。 默认值为面板的标题。

   * **描述**：片段的描述。

   * **标记**：片段的标记元数据。

   * **目标路径**：保存片段的存储库路径。 如果不指定路径，则会在包含自适应表单的节点旁边创建与片段名称相同的节点。 片段将保存在此节点中。

   * **表单模型**：根据自适应表单的表单模型，此字段显示&#x200B;**XML架构**、**表单模板**&#x200B;或&#x200B;**无**。 它是不可编辑的字段。

   * **片段模型根**：仅在基于XSD的自适应Forms中显示。 它指定片段模型的根。 您可以从下拉列表中选择&#x200B;**/**&#x200B;或XSD复杂类型。 只有在选择复杂类型作为片段模型根时，才能在另一个自适应表单中重用片段。
如果选择&#x200B;**/**&#x200B;作为片段模型根，则在“自适应表单数据模型”选项卡中将显示该根中的完整XSD树。 对于复杂类型片段模型根，自适应表单数据模型选项卡中仅显示选定复杂类型的后代。

   * **XSD Ref**：仅在基于XSD的自适应Forms中显示。 它显示XML方案的位置。

   * **XDP Ref**：仅在基于XDP的自适应Forms中显示。 它显示XDP表单模板的位置。

   ![save-fragment](assets/save-fragment.png)

   “另存为片段”对话框

1. 单击&#x200B;**确定**。

   面板保存在存储库中的指定位置或默认位置。 在自适应表单中，面板被替换为片段的快照。 如下所示，“常规信息”面板及其子面板“个人信息和地址”将另存为片段。

   要编辑片段，请单击面板工具栏中的&#x200B;**[!UICONTROL 编辑资产]**。 片段在编辑模式下的新选项卡或窗口中打开。

   ![正在编辑片段](assets/edit-fragment.png)

## 使用片段 {#working-with-fragments}

### 配置片段外观 {#configure-fragment-appearance}

您在自适应表单中插入的任何片段都显示为占位符图像。 占位符在片段中最多显示十个子面板的标题。 您可以将[!DNL AEM Forms]配置为显示完整的片段，而不是占位符图像。

执行以下步骤以在表单中显示完整的片段：

1. 转到位于https：[*host*]：[*port*]/system/console/configMgr的AEM Web控制台配置页。

1. 搜索并单击&#x200B;**[!UICONTROL 自适应表单配置服务]**&#x200B;以在编辑模式下打开它。
1. 禁用&#x200B;**[!UICONTROL 启用占位符代替片段]**&#x200B;复选框以显示完整的片段，而不是占位符图像。

### 在自适应表单中插入片段 {#insert-a-fragment-in-an-adaptive-form}

您创建的自适应表单片段将显示在AEM内容查找器的自适应表单片段选项卡中。 要在自适应表单中插入自适应表单片段，请执行以下操作：

1. 在编辑模式下打开要在其中插入自适应表单片段的自适应表单。
1. 单击侧边栏中的&#x200B;**Assets**![assets-browser](assets/assets-browser.png)。 在资产浏览器中，从下拉列表中选择&#x200B;**自适应表单片段**。

   您还可以选择显示所有自适应表单片段或根据其表单模型（表单模板、XML架构或基本）进行筛选。

1. 将自适应表单片段拖放到自适应表单上。

   >[!NOTE]
   >
   >自适应表单片段没有启用在自适应表单中进行创作。 此外，在基于JSON的自适应表单中不能以相反的方式使用基于XSD的片段。

自适应表单片段在自适应表单中通过引用插入，并与独立的自适应表单片段同步。 这意味着在更新自适应表单片段时，更改会反映在使用片段的所有Adaptive Forms中。

### 在自适应表单中嵌入片段 {#embed-a-fragment-in-adaptive-form}

您可以选择在自适应表单中嵌入自适应表单片段，方法是单击所添加片段的面板工具栏上的&#x200B;**嵌入资产： &lt;*fragmentName*>**&#x200B;按钮，如以下示例图像所示。

![在自适应表单中嵌入表单片段](assets/embed-fragment.png)

>[!NOTE]
>
>嵌入的片段不再与独立片段链接。 您可以在自适应表单内编辑嵌入片段中的组件。

### 在片段中使用片段 {#using-fragments-within-fragments}

您可以创建嵌套的自适应表单片段，这意味着您可以将片段拖放到另一个片段中，并且可以具有嵌套的片段结构。

### 更改片段 {#change-fragments}

您可以使用自适应表单片段面板的“编辑组件”对话框中的&#x200B;**选择片段资源**&#x200B;属性来用其他片段替换或更改自适应表单片段。

### 在自适应表单中多次使用表单片段 {#using-form-fragment-mutiple-times-in-af}

您可以在自适应表单中多次使用基于架构的表单片段，以唯一地保存每个表单片段字段的数据。 例如，您可以使用地址表片段收集地址详细信息，以便在贷款申请表中永久性、通信和显示生活地址。

![在自适应表单中使用多个片段](/help/forms/assets/using-multiple-fragment-af.gif)

>[!NOTE]
>
> 如果您在自适应表单中多次使用基于非的表单片段，则会出现片段字段之间的数据同步问题。 您可以在一个表单中多次使用未绑定到任何表单数据模型(FDM)的基于[核心组件的表单片段](/help/forms/adaptive-form-fragments-core-components.md)，而不会遇到数据同步问题。

## 数据绑定的片段自动映射 {#auto-mapping-of-fragments-for-data-binding}

当您使用XFA表单模板或XSD复杂类型创建自适应表单片段并将片段拖放到自适应表单时，XFA片段或XSD复杂类型会自动替换为相应的自适应表单片段，其片段模型根映射到XFA片段或XSD复杂类型。

您可以通过编辑组件对话框更改片段资源及其绑定。

>[!NOTE]
>
>您还可以从AEM内容查找器中的自适应表单片段库拖放绑定的自适应表单片段，并从自适应表单片段面板的“编辑组件”对话框中提供正确的绑定引用。

## 管理片段 {#manage-fragments}

您可以使用[!DNL AEM Forms] UI对自适应表单片段执行多项操作。

1. 转到 `https://[hostname]:'port'/aem/forms.html`.

1. 单击[!DNL AEM Forms] UI工具栏中的&#x200B;**选择**&#x200B;并选择自适应表单片段。 工具栏显示您可以对选定的自适应表单片段执行的以下操作。

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
   <td><p>打开属性面板。 从“属性”面板中，您可以查看和编辑属性、生成预览并上传所选片段的缩略图图像。 有关详细信息，请参阅<a href="manage-form-metadata.md" target="_blank">管理元数据</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>复制</p> </td>
   <td><p>复制选定的片段。 工具栏中会显示“粘贴”按钮。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>下载</p> </td>
   <td><p>下载所选片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>预览</p> </td>
   <td><p>提供选项，用于将XML文件中的数据与片段合并，以HTML形式预览片段或自定义预览。 <!-- For more information, see <a href="previewing-forms.md" target="_blank">Previewing a form</a>.<br /> <br /> --></p> </td>
  </tr>
  <tr>
   <td><p>开始审核/管理审核</p> </td>
   <td><p>允许启动和管理对所选片段的审核。<!-- For more information, see <a href="create-reviews-forms.md" target="_blank">Creating and managing reviews</a>.<br /> <br /> </p> --> </td>
  </tr>
  <tr>
   <td><p>创建词典</p> </td>
   <td><p>生成用于本地化所选片段的字典。<!-- For more information, see <a href="lazy-loading-adaptive-forms.md" target="_blank">Localizing Adaptive Forms</a>.<br /> <br /> --> </p> </td>
  </tr>
  <tr>
   <td><p>Publish/取消发布</p> </td>
   <td><p>发布/取消发布选定的片段。<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>删除</p> </td>
   <td><p>删除选定的片段。<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## 本地化包含片段的自适应表单 {#localizing-adaptive-form-containing-fragments}

要本地化包含自适应表单片段的自适应表单，您需要分别本地化片段和表单。 这个想法是将片段本地化一次，然后在多个自适应表单中重复使用它。

>[!NOTE]
>
>片段中的本地化键不会出现在自适应表单的XLIFF文件中。

## 使用片段时要记住的要点 {#key-points-to-remember-when-working-with-fragments}

* 确保片段名称是唯一的。 如果存在具有相同名称的现有片段，则创建片段失败。
* 在基于 XDP 的自适应表单中，如果将面板另存为包含另一个 XDP 片段的片段，则生成的片段将自动绑定到子 XDP 片段。 对于基于 XSD 的自适应表单，生成的片段将绑定到架构根。
* 当您创建自适应表单片段时，将创建一个片段节点，该节点类似于 CRXDe Lite 中自适应表单的 guideContainer 节点。
* 不支持自适应表单中使用不同表单数据模型 （FDM） 的片段。 例如，基于 XDP 的自适应表单不支持基于 XDP 的片段，反之亦然。
* 自适应表单片段可通过AEM内容查找器中的自适应表单片段选项卡使用。
* 通过引用插入或嵌入自适应表单中的独立自适应表单片段中的任何表达式、脚本或样式都会保留。
* 您无法从自适应表单中编辑通过引用插入的自适应表单片段。 要编辑，您需要编辑独立的自适应表单片段或将片段嵌入自适应表单中。
* 发布自适应表单时，您需要发布在自适应表单中通过引用插入的独立自适应表单片段。
* 当您重新发布更新的自适应表单片段时，更改会反映在使用片段的自适应表单的已发布实例中。
* 包含Verify组件的自适应表单不支持匿名用户。 此外，不建议在自适应表单片段中使用验证组件。
* （**仅限** Mac）为确保表单片段功能在所有场景中都能完美运行，请将以下条目添加到 /private/etc/hosts 文件中：
  `127.0.0.1 <Host machine>`**&#x200B;**&#x200B;主机：部署在[!DNL AEM Forms]的 Apple Mac 计算机。

<!--
## Reference Fragments {#reference-fragments}

Reference Adaptive Form Fragments that you can use to create your form are available. For more information, see [Reference Fragments](reference-adaptive-form-fragments.md).
-->

>[!MORELIKETHIS]
>
>* [核心组件中的自适应表单片段](/help/forms/adaptive-form-fragments-core-components.md)
