---
title: 如何创建表单片段用于进行基于所见即所得的创作
description: 了解如何在通用编辑器中创建表单片段并将其添加到表单中。
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: fd3c53cf5a6d1c097a5ea114a831ff626ae7ad7e
workflow-type: ht
source-wordcount: '1693'
ht-degree: 100%

---

# 在通用编辑器中创建表单片段

表单片段是可重复使用的组件，这样可以避免重复的开发工作，并确保整个组织中表单的一致性。您无需为每个表单重新创建联系方式、地址详细信息或同意声明之类的常见分区，而是可以将这些元素构建为片段，然后在多个表单中重复使用它们。

**通过这篇文章，您将能够：**

- 了解表单片段的业务价值和技术功能
- 使用通用编辑器创建可重复使用的表单片段
- 通过适当的配置将片段集成到现有表单中
- 管理片段生命周期并保持跨表单的一致性

**业务优势：**

- **缩短开发时间**：只需构建一次常用表单分区，就可以在任何地方重复使用
- **增强一致性**：确保所有表单的标准化布局和内容
- **简化维护**：只需更新一次片段，更改就能在使用此片段的所有表单中反映出来
- **增强合规性**：确保监管内容的分区保持一致和最新状态

Edge Delivery Services 中的表单片段支持高级功能，包括嵌套片段、单个表单中的多个实例以及与数据源的无缝集成。

## 了解表单片段

Edge Delivery Services 中的表单片段为模块化表单开发提供了强大的功能：

**核心功能：**

- **一致性管理**：片段在所有表单中保持相同的布局和内容。通过“一次更改，随处反映”的方法，对片段所做的任何更新都会在预览模式中自动应用于所有表单。
- **多次使用**：在同一个表单中多次添加相同的片段，每个片段都与不同的数据源或架构元素进行独立的数据绑定。
- **嵌套结构**：将片段嵌入其他片段中可以创建复杂的层级结构，实现复杂的表单架构。

**技术要求：**

- **GitHub URL 一致性**：片段和使用它的任何表单都必须指定相同的 GitHub 存储库 URL
- **独立形式编辑**：片段只能在独立形式中进行更改，无法在宿主表单中更改

**发布行为：**

>[!IMPORTANT]
>
>在预览模式下，片段更改会立即反映在所有表单中。在发布模式下，您必须重新发布片段和任何使用此片段的表单才能看到更新。

>[!CAUTION]
>
>避免循环引用片段（将一个片段嵌套在这个片段自身当中），因为这会导致渲染错误和意外行为。

## 先决条件

**技术设置要求：**

- 通过在您的 AEM 环境与 GitHub 存储库之间建立的连接[配置 GitHub 存储库](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)
- 将[最新的自适应表单块](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)添加到您的 GitHub 存储库中（对于现有的 Edge Delivery Services 项目）
- 带 Edge Delivery Services 模板的 AEM Forms 作者实例可用
- 能够访问您的 AEM Forms as a Cloud Service 作者实例 URL 和 GitHub 存储库 URL

**必需的知识和权限：**

- 关于表单设计概念和组件层级结构的基本知识
- 熟悉通用编辑器界面和表单创建工作流
- AEM Forms 中的作者级权限，用于创建和管理表单资产
- 了解您组织的表单标准和可复用组件要求

## 使用 Edge Delivery Services 表单片段

您可以在通用编辑器中创建 Edge Delivery Services 表单片段，然后将创建的片段添加到 Edge Delivery Services 表单。您可以使用 Edge Delivery Services 表单片段执行以下操作：

- [在通用编辑器中创建表单片段](#creating-form-fragments-in-universal-editor)
   - [了解表单片段](#understanding-form-fragments)
   - [先决条件](#prerequisites)
   - [使用 Edge Delivery Services 表单片段](#working-with-edge-delivery-services-form-fragments)
   - [最佳做法](#best-practices)
   - [摘要](#summary)

+++ 创建表单片段

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

   - **表单数据模型 (FDM)**：将来自数据源的数据模型对象和服务集成到您的片段中。如果您的表单需要从多个来源读写数据，请选择表单数据模型 (FDM)。

   - **JSON 架构**：通过关联一个定义数据结构的 JSON 架构将您的表单与后端系统集成。它允许您使用架构元素添加动态内容。
   - **无**：指定从头开始创建片段，不使用任何表单模型。

   >[!NOTE]
   >
   > 要了解如何在通用编辑器中将表单或片段与表单数据模型 (FDM) 集成以使用不同的后端数据源，请参阅[在通用编辑器中将表单与表单数据模型集成](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)。

1. （可选）在&#x200B;**高级**&#x200B;选项卡中为该片段指定&#x200B;**发布日期**&#x200B;或者&#x200B;**取消发布日期**。

   ![高级选项卡](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. 点击&#x200B;**创建**，生成片段。现在出现一个带有编辑选项的成功对话框。

   ![编辑片段](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. 点击&#x200B;**编辑**，在通用编辑器中打开已应用了默认模板的片段。

   ![通用编辑器中用于创作的片段](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

1. **设计您的片段内容**：添加表单组件（文本字段、下拉菜单、复选框），构建可重复使用的分区。有关详细的组件指导，请参阅[使用通用编辑器完成适用于 AEM Forms 的 Edge Delivery Services 快速入门](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)。

1. **配置组件属性**：根据您的用例需要设置字段名称、验证规则和默认值。

1. **保存与预览**：保存您的片段，使用预览模式验证布局和功能。

   ![通用编辑器中已完成的联系人信息表单片段屏幕快照，其中包含姓名、电话、电子邮件和地址字段，这些可在多个表单中重复使用](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

**验证检查点：**

- 通用编辑器中片段加载无误
- 所有表单组件均正确显现
- 字段属性和验证规则按预期工作
- 片段已保存，可在 Forms &amp; Documents 控制台中使用

片段完成后，您可以[将其集成到任何 Edge Delivery Services 表单中](#adding-form-fragments-to-a-form)。

+++


+++ 将表单片段添加到一个表单

此示例演示了如何创建`Employee Details`使用一个片段的表单`Contact Details`，这个片段中包含员工信息和主管信息的分区。这种方法可确保一致的数据收集，同时减少开发工作。

要将表单片段集成到表单中：

1. 在编辑模式下打开该表单。
1. 将表单片段组件添加到表单。
1. 打开内容浏览器，然后导航到&#x200B;**内容树**&#x200B;中的&#x200B;**[!UICONTROL 自适应表单]**&#x200B;组件。
1. 导航到您想要添加片段的那个部分。例如，导航到&#x200B;**员工详细信息**&#x200B;面板。

   ![导航到该部分](/help/edge/docs/forms/universal-editor/assets/navigate-to-section.png)

1. 单击&#x200B;**[!UICONTROL 添加]**&#x200B;图标，然后从&#x200B;**自适应表单组件**&#x200B;列表中添加&#x200B;**[!UICONTROL 表单片段]**组件。
   ![添加表单片段](/help/edge/docs/forms/universal-editor/assets/add-fragment.png)

   如果您选择了&#x200B;**[!UICONTROL 表单片段]**&#x200B;组件，片段就会添加到您的表单中。您可以打开已添加片段的&#x200B;**属性**，对其进行配置。例如，在片段的&#x200B;**属性**&#x200B;中隐藏其标题。

   ![配置片段的属性](/help/edge/docs/forms/universal-editor/assets/fragment-properties.png)

1. 在&#x200B;**基本**&#x200B;选项卡中选择&#x200B;**片段引用** 。根据表单的模型，将显示表单可用的所有片段。

   例如，导航至 `/content/forms/af`，然后选择 `Contact Details` 片段。

   ![选择片段](/help/edge/docs/forms/universal-editor/assets/select-fragment.png)

1. 单击&#x200B;**[!UICONTROL 选择]**。

   表单片段通过引用的方式添加到表单中，并与独立表单片段保持同步。

   ![通用编辑器中的员工表单屏幕快照，展示了成功嵌入的联系人信息片段，说明了片段在重复使用时如何保持其结构一致性](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   >[!NOTE]
   >
   > **编辑片段**&#x200B;按钮可让用户直接导航到表单片段进行编辑。

   您可以预览表单以查看在&#x200B;**预览**&#x200B;模式中该表单如何显示。

   ![预览](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   同样，您可以重复步骤 3 至 7 来为 `Supervisor Details` 面板插入 `Contact Details` 片段。

   ![员工详细信息表单](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

+++



+++ 管理表单片段

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

+++ 

## 最佳做法

**片段设计和命名：**

- **使用描述性的唯一名称**：选择能够清楚表明片段用途的名称（例如“contact-details-with-validation”而不是“fragment1”）
- **规划可复用性**：将片段设计为与上下文无关，这样它们就能在各种不同类型的表单中正常工作
- **保持片段目的明确**：创建单一用途的片段，而不是复杂的多功能组件

**开发工作流：**

- **独立测试片段**：验证片段功能之后再集成到表单中
- **保持一致的 GitHub URL**：确保所有相关的片段和表单都使用相同的存储库 URL
- **记录片段的用途**：包含清晰的描述和标记，以帮助团队成员了解何时使用每个片段

**发布与维护：**

- **协调发布**：更新片段后，计划同时重新发布所有依赖表单
- **版本控制**：更新片段后，使用意思明确的提交消息来跟踪各时期的更改
- **监控依赖项**：为每个片段跟踪哪些表单使用此片段，来评估更新的影响

>[!TIP]
>
>片段样式、脚本和表达式在嵌入时会被保留，因此在设计时应考虑到这种继承。

## 摘要

您已成功了解如何使用 Edge Delivery Services 中的表单片段来提高开发效率并保持整个组织中表单的一致性。

**主要技能：**

- **理解**：掌握表单片段的业务价值和技术功能
- **创建**：使用通用编辑器和适当的配置构建可重复使用的表单片段
- **集成**：在表单中添加片段，使用正确的引用设置和属性配置
- **管理**：了解片段生命周期操作和维护工作流

**后续步骤：**

- 为您的组织创建一个常用片段库。
- 制定片段使用的命名规范和治理策略。
- 了解与[表单数据模型](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)的高级集成，以实现动态数据驱动的片段
- 实施基于片段的表单模板，以确保一致的用户体验。

现在，您的表单受益于模块化、易维护的架构，能够在各项目间高效扩展，同时确保一致的用户体验。


