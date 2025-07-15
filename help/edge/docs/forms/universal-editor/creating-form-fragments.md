---
title: 如何创建表单片段用于进行基于所见即所得的创作
description: 了解如何在通用编辑器中创建表单片段并将其添加到表单中。
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: e1ead9342fadbdf82815f082d7194c9cdf6d799d
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 96%

---

# 在通用编辑器中创建表单片段

<span class="preview"> 此功能通过早期访问计划提供。要请求获得访问权限，请通过您的官方地址向 <a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a> 发送电子邮件，并附上您的 GitHub 组织名称和存储库名称。例如，如果存储库 URL 为 https://github.com/adobe/abc，则组织名称为 adobe，存储库名称为 abc。</span>

<span class="preview">这是一项预发行功能，可通过我们的[预发行渠道](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=zh-Hans#new-features)访问。</span>

表单通常包含联系方式、身份信息或同意协议等常见部分。表单开发人员每次生成新表单时都要创建这些部分，这是一项重复且耗时的工作。
为了消除这种重复劳动，通用编辑器提供了一种方法，只需创建一次可重复使用的表单片段（如面板或字段组）即可在各种表单中重复使用它们。这些可重复使用的模块化独立片段称为表单片段。例如，相同的紧急联系方式片段可用于表单的不同部分，如员工和主管的联系方式。

在本文末尾，您将了解如何使用通用编辑器在表单中创建和使用片段。

## Edge Delivery Services 表单片段的功能

* **使用表单片段保持一致性：**
您可以将片段集成到不同的表单中，有助于保持一致的布局和标准化的内容。

  >[!NOTE]
  >
  > 通过“一次更改，随处反映”的方法，对片段所做的任何更新都会在预览模式中自动应用于所有表单。但是在发布模式下，您必须发布片段或重新发布表单才能反映更改。

* **在表单中多次添加表单片段：**
您可以在一个表单中多次添加某个表单片段，并将其数据绑定属性配置为数据源或模式。

* **在片段中使用片段：**
您可以创建表单片段嵌套，这意味着您可以在一个片段中添加另一个片段，形成片段嵌套结构。

  >[!NOTE]
  >
  > 您不能将一个片段嵌套在同一个片段内，因为这可能会导致循环引用和意外行为，从而导致错误或出现问题。

## 使用 Edge Delivery Services 表单片段时的考虑事项

* 您需要将同一个 GitHub URL 添加到片段以及您打算使用该片段的表单中。
* 您不能编辑一个表单内的表单片段。要进行更改，请更改独立的表单片段。

## 先决条件

* [设置您的 GitHub 存储库](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)，以在您的 AEM 环境和 GitHub 存储库之间建立连接。
* 如果您已经在使用 Edge Delivery Services，请将最新版本的 [Adaptive Forms Block](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project) 添加到您的 GitHub 存储库。
* AEM Forms 作者实例包含一个基于 Edge Delivery Services 的模板。
* 保存 AEM Forms as a Cloud Service 作者实例的 URL 和您方便的 GitHub 存储库。

## 使用 Edge Delivery Services 表单片段

您可以在通用编辑器中创建 Edge Delivery Services 表单片段，然后将创建的片段添加到 Edge Delivery Services 表单。您可以使用 Edge Delivery Services 表单片段执行以下操作：

* [创建表单片段](#creating-form-fragments)
* [将表单片段添加到一个表单](#adding-form-fragments-to-a-form)
* [管理表单片段](#managing-form-fragments)

### 创建表单片段

要在通用编辑器中创建表单片段，请执行以下步骤：

1. 登录您的 AEM Forms as a Cloud Service 作者实例。
1. 选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。
1. 单击&#x200B;**创建 > 自适应表单片段**。

   ![创建片段](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   现在会出现&#x200B;**创建自适应表单片段**&#x200B;向导。
1. 从&#x200B;**选择模板**&#x200B;选项卡中选择基于 Edge Delivery Services 的模板，然后点击&#x200B;**[!UICONTROL 下一步]**。
   ![选择 Edge Delivery Services 模板](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. 指定片段的标题、名称、描述和标记。确保为片段指定唯一的名称。如果存在另一个同名的片段，该片段创建就会失败。
1. 指定 **GitHub URL**。例如，如果您的 GitHub 存储库名为 `edsforms`，它位于帐户 `wkndforms` 下，其 URL 为 `https://github.com/wkndforms/edsforms`。

   ![基本属性](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. （可选）单击打开&#x200B;**表单模型**&#x200B;选项卡，然后在&#x200B;**从中选择**&#x200B;下拉菜单中为该片段选择下面的一个模型：

   ![显示“表单模型”选项卡中的模型类型](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   * **表单数据模型 (FDM)**：将来自数据源的数据模型对象和服务集成到您的片段中。如果您的表单需要从多个来源读写数据，请选择表单数据模型 (FDM)。

   * **JSON 架构**：通过关联一个定义数据结构的 JSON 架构将您的表单与后端系统集成。它允许您使用架构元素添加动态内容。
   * **无**：指定从头开始创建片段，不使用任何表单模型。

   >[!NOTE]
   >
   > 要了解如何在通用编辑器中将表单或片段与表单数据模型 (FDM) 集成以使用不同的后端数据源，[单击这里](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)。

1. （可选）在&#x200B;**高级**&#x200B;选项卡中为该片段指定&#x200B;**发布日期**&#x200B;或者&#x200B;**取消发布日期**。

   ![高级选项卡](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. 单击&#x200B;**创建**，然后出现一个向导。

   ![编辑片段](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. 单击&#x200B;**编辑**，然后已创建的片段和一个默认模板会在通用编辑器中打开以供创作。

   ![通用编辑器中的片段可用于创作](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

   在编辑模式下，您可以将任何表单组件添加到片段中。要了解如何在通用编辑器中创建表单，请参阅文章[使用通用编辑器完成 Edge Delivery Services for AEM Forms 快速入门](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)。

   下面的屏幕快照显示了在通用编辑器中创建的 `contact fragment`。

   ![通用编辑器中已填写的联系人详细信息表片段的屏幕截图，其中显示了可以在多个表单中重复使用的姓名、电话、电子邮件和地址字段](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

   创建片段后，您可以[在 Edge Delivery Services Forms 中添加创建的片段](#adding-form-fragments-in-forms)。

### 将表单片段添加到一个表单

让我们创建一个包含员工和主管信息的简单 `Employee Details` 表单。您可以在员工和主管面板中使用 `Contact Details` 片段。要在表单中使用表单片段，请执行以下步骤：

1. 在编辑模式下打开该表单。
1. 将表单片段组件添加到表单。
1. 打开内容浏览器，然后导航到&#x200B;**内容树**&#x200B;中的&#x200B;**[!UICONTROL 自适应表单]**&#x200B;组件。
1. 导航到您想要添加片段的那个部分。例如，导航到&#x200B;**员工详细信息**&#x200B;面板。

   ![导航到该部分](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;图标，然后从&#x200B;**自适应表单组件**&#x200B;列表中添加&#x200B;**[!UICONTROL 表单片段]**&#x200B;组件。
   ![添加表单片段](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   如果您选择了&#x200B;**[!UICONTROL 表单片段]**&#x200B;组件，片段就会添加到您的表单中。您可以打开已添加片段的&#x200B;**属性**，对其进行配置。例如，在片段的&#x200B;**属性**&#x200B;中隐藏其标题。

   ![配置片段的属性](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. 在&#x200B;**基本**&#x200B;选项卡中选择&#x200B;**片段引用** 。根据表单的模型，将显示表单可用的所有片段。

   例如，导航至 `/content/forms/af`，然后选择 `Contact Details` 片段。

   ![选择片段](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. 单击&#x200B;**[!UICONTROL 选择]**。

   表单片段通过引用添加到表单，并与独立表单片段保持同步。

   ![屏幕截图显示已成功集成到通用编辑器的员工表单中的联系人详细信息片段，演示片段在重用时如何保持其结构](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   您可以预览表单以查看在&#x200B;**预览**&#x200B;模式中该表单如何显示。

   ![预览](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   同样，您可以重复步骤 3 至 7 来为 `Supervisor Details` 面板插入 `Contact Details` 片段。

   ![员工详细信息表单](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

### 管理表单片段

您可以使用 AEM Forms 用户界面对表单片段执行多项操作。

1. 登录您的 AEM Forms as a Cloud Service 作者实例。
1. 选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。

1. 选择一个表单片段，工具栏就会显示您可以在所选片段上执行以下操作。

   ![管理片段](/help/edge/docs/forms/universal-editor/assets/manage-fragment.png)

   <table>
    <tbody>
    <tr>
   <td><p><strong>操作</strong></p> </td>
   <td><p><strong>描述</strong></p> </td>
    </tr>
    <tr>
   <td><p>编辑</p> </td>
   <td><p>在编辑模式中打开片段。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>属性</p> </td>
   <td><p>提供更改表单片段属性的选项。<br /> <br /> </p> </td>
    </tr>
    <td><p>复制</p> </td>
   <td><p> 提供复制表单片段并将其粘贴到所需位置的选项。<br /> <br /> </p> </td>
    </tr>
   <tr>
   <td><p>预览</p> </td>
   <td><p>提供以 HTML 形式预览片段或通过将某个 XML 文件中的数据与片段合并来执行自定义预览的选项。<br /> </p> </td>
    </tr>
    <tr>
   <td><p>下载</p> </td>
   <td><p>下载选定的片段。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>开始审阅/管理审阅</p> </td>
   <td><p>允许启动和管理对所选片段的审阅。<br /> <br /> </p> </td>
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
   <td><p>删除选定的片段。<br /> <br /> </p> </td>
    </tr>
    <tr>
   <td><p>比较</p> </td>
   <td><p>比较两种不同的表单片段用于预览。<br /> <br /> </p> </td>
    </tr>
    </tbody>
    </table>

## 最佳实践

* 确保片段名称是唯一的。如果已经存在一个同名的片段，该片段创建就会失败。
* 独立表单片段在通过引用插入表单或嵌入表单时，其中的任何表达式、脚本或样式都会被保留。
* 当您发布表单时，表单内通过引用插入的表单片段将自动发布。

## 另请参阅

{{universal-editor-see-also}}
