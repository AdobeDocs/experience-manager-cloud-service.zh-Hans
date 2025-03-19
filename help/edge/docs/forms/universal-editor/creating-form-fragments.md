---
title: 如何为基于WYSIWYG的创作创建表单片段
description: 了解如何在通用编辑器中创建表单片段并将它们添加到表单。
feature: Edge Delivery Services
role: Admin, User, Developer
hide: true
hidefromtoc: true
source-git-commit: 62c58ceb2d2d659bad591b3eba1bfd924f2a848b
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 8%

---


# 在通用编辑器中创建和使用Edge Delivery Services表单片段

Forms通常包括常用部分，如联系信息、身份识别详细信息或同意协议。 表单开发人员每次构建新表单时都会创建这些部分，这样既重复又耗时。
为了消除这种重复工作，Universal Editor提供了一种方法，只需创建一次可重用的表单区段（例如面板或字段组），并在各种表单中重复使用。 这些可重用、模块化和独立的区段称为表单片段。 例如，相同的紧急联系人片段可用于表单的不同部分，如员工和主管联系人详细信息。

在文章末尾，您将了解如何使用通用编辑器在表单中创建和使用片段。

## Edge Delivery Services表单片段的功能

* **与表单片段保持一致**
您可以将片段集成到不同的表单中，从而帮助您保持一致的布局和标准化的内容。 通过“更改一次，随处反映”方法，对片段所做的任何更新都会自动应用于所有表单。

* **在表单中多次添加表单片段**
您可以在表单中多次添加表单片段，并将其数据绑定属性配置为数据源或架构。

* **在片段中使用片段**
您可以创建嵌套表单片段，这意味着您可以向另一个片段添加片段，并且可以具有嵌套片段结构。

  >[!NOTE]
  >
  > 不能在片段内部嵌套片段，因为这样可能会导致递归引用和意外行为，从而导致错误或呈现问题。

## 使用Edge Delivery Services表单片段时的注意事项

* 您需要在片段和打算使用片段的表单中添加相同的GitHub URL。
* 您无法从表单中编辑通过引用插入的表单片段。 要编辑，请修改独立表单片段。

## 创建Edge Delivery Services表单片段的先决条件

* [设置您的 GitHub 存储库](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)，以在您的 AEM 环境和 GitHub 存储库之间建立连接。
* 如果您已经在使用 Edge Delivery Services，请将最新版本的[自适应表单区块](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)添加到您的 GitHub 存储库。
* AEM Forms 作者实例包含一个基于 Edge Delivery Services 的模板。确保您的环境中安装了[最新版本的核心组件](https://github.com/adobe/aem-core-forms-components)。
* 保存 AEM Forms as a Cloud Service 作者实例的 URL 和您方便的 GitHub 存储库。

## 使用Edge Delivery Services表单片段

您可以在通用编辑器中创建Edge Delivery Services表单片段，并将创建的片段添加到Edge Delivery Services表单中。 您可以使用Edge Delivery Services表单片段执行以下操作：

* [创建表单片段](#creating-form-fragments)
* [向表单添加表单片段](#adding-form-fragments-to-a-form)
* [管理表单片段](#managing-form-fragments)

### 创建表单片段

要在通用编辑器中创建表单片段，请执行以下步骤：

1. 登录AEM Forms as a Cloud Service创作实例。
1. 选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。
1. 单击&#x200B;**创建>自适应表单片段**。

   ![创建片段](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   出现&#x200B;**创建自适应表单片段**&#x200B;向导。
1. 从&#x200B;**选择模板**&#x200B;选项卡中选择基于Egde Delivery Services的模板，然后单击&#x200B;**[!UICONTROL 下一步]**。
   ![选择Edge Delivery Services模板](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. 指定片段的标题、名称、描述和标记。 请确保为片段指定唯一的名称。 如果存在具有相同名称的其他片段，则无法创建该片段。
1. 指定 **GitHub URL**。例如，如果您的GitHub存储库名为`edsforms`，则它位于帐户`wkndforms`下，URL为`https://github.com/wkndforms/edsforms`。

   ![基本属性](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. （可选）单击以打开&#x200B;**表单模型**&#x200B;选项卡，从&#x200B;**选择自**&#x200B;下拉菜单中，为片段选择以下模型之一：

   ![在表单模型选项卡中显示模型类型](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   * **表单数据模型(FDM)**：将数据源中的数据模型对象和服务集成到片段中。 如果您的表单需要从多个源读取和写入数据，请选择表单数据模型(FDM)。

   * **JSON架构**：通过关联定义数据结构的JSON架构，将表单与后端系统集成。 它允许您使用架构元素添加动态内容。
   * **无**：指定从头开始创建片段，而不使用任何表单模型。

   >[!NOTE]
   >
   > 要了解如何在通用编辑器中将表单或片段与表单数据模型(FDM)集成以使用各种后端数据源，请[单击此处](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)。

1. （可选）在&#x200B;**高级**&#x200B;选项卡中为片段指定&#x200B;**发布日期**&#x200B;或&#x200B;**取消发布日期**。

   ![高级选项卡](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. 单击&#x200B;**创建**，将显示向导。

   ![编辑片段](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. 单击&#x200B;**编辑**，使用默认模板创建的片段将在通用编辑器中打开以进行创作。

   在通用编辑器中用于创作的![片段](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

   在编辑模式下，您可以将任何表单组件添加到片段。 要了解如何在通用编辑器中创建片段，请参阅[使用通用编辑器的Edge Delivery Services for AEM Forms快速入门](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)文章。

   以下屏幕截图显示了在Universal Editor中创建的`contact fragment`。

   ![联系人片段](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

   创建片段后，您可以[将创建的片段添加到Edge Delivery Services Forms](#adding-form-fragments-in-forms)中。

### 向表单添加表单片段

让我们创建一个包含员工和主管信息的简单`Employee Details`表单。 您可以在员工和主管面板中使用`Contact Details`片段。 要在表单中使用表单片段，请执行以下步骤：

1. 在编辑模式下打开表单。
1. 将表单片段组件添加到表单。
1. 打开内容浏览器，然后导航到&#x200B;**内容树**&#x200B;中的&#x200B;**[!UICONTROL 自适应表单]**&#x200B;组件。
1. 导航到要添加片段的部分。 例如，导航到&#x200B;**员工详细信息**&#x200B;面板。

   ![导航到分区](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;图标并从&#x200B;**自适应表单组件**&#x200B;列表中添加&#x200B;**[!UICONTROL 表单片段]**组件。
   ![添加表单片段](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   选择&#x200B;**[!UICONTROL 表单片段]**&#x200B;组件后，该片段将被添加到您的表单中。 您可以通过打开添加片段的&#x200B;**属性**&#x200B;来配置该片段的属性。 例如，从片段的&#x200B;**属性**&#x200B;中隐藏片段的标题。

   ![配置片段的属性](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. 在&#x200B;**基本**&#x200B;选项卡中选择&#x200B;**片段引用**。 根据表单的模型，将会显示可用于表单的所有片段。

   例如，导航到`/content/forms/af`并选择`Contact Details`片段。

   ![选择片段](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. 单击&#x200B;**[!UICONTROL 选择]**。

   该表单片段将引用该表单片段进行添加，并且保持与独立表单片段的同步。 这意味着对片段所做的任何修改都会在片段合并到表单中的所有实例之间镜像。

   ![表单中的片段](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   您可以预览表单，以查看表单在&#x200B;**预览**&#x200B;模式下的显示方式。

   ![预览](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   同样，您可以重复步骤3至7，为`Supervisor Details`面板插入`Contact Details`片段。

   ![员工详细信息表单](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

### 管理表单片段

您可以使用AEM Forms用户界面对表单片段执行多项操作。

1. 登录AEM Forms as a Cloud Service创作实例。
1. 选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。

1. 选择一个表单片段，工具栏会显示您可以对所选片段执行的以下操作。

   ![管理片段](/help/edge/docs/forms/universal-editor/assets/manage-fragment.png)

   <table>
    <tbody>
    <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
    </tr>
    <tr>
   <td><p>编辑</p> </td>
   <td><p>在编辑模式下打开表单片段。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>属性</p> </td>
   <td><p>提供用于修改表单片段属性的选项。<br /> <br /> </p> </td>
    </tr>
    <td><p>复制</p> </td>
   <td><p> 提供相应选项，用于复制表单片段并将其粘贴到所需位置。<br /> <br /> </p> </td>
    </tr>
   <tr>
   <td><p>预览</p> </td>
   <td><p>提供以HTML预览片段的选项，或通过将XML文件中的数据与片段合并来执行自定义预览。<br /> </p> </td>
    </tr>
    <tr>
   <td><p>下载</p> </td>
   <td><p>下载所选片段。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>开始审核/管理审核</p> </td>
   <td><p>允许启动和管理所选片段的审核。<br /> <br /> </p> </td>
    </tr>
    <!--<tr>
   <td><p>Add Dictionary</p> </td>
   <td><p>Generates a dictionary for localizing the selected fragment. For more information, see <a>Localizing Adaptive Forms</a>.<br /> <br /> </p> </td>
    </tr>-->
    <tr>
   <td><p>发布/取消发布</p> </td>
   <td><p>发布/取消发布选定的片段。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>删除</p> </td>
   <td><p>删除所选片段。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>比较</p> </td>
   <td><p>比较两个不同的表单片段以进行预览。<br /> <br /> </p> </td>
    </tr>
    </tbody>
    </table>

## 最佳实践

* 确保片段名称是唯一的。 如果存在具有相同名称的现有片段，则创建片段失败。
* 通过引用插入或嵌入到表单中时，独立表单片段中的任何表达式、脚本或样式都会保留。
* 发布表单时，将自动发布通过引用在表单中插入的表单片段。

## 另请参阅

{{universal-editor-see-also}}