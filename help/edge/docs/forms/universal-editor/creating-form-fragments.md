---
title: 如何创建表单片段用于进行基于所见即所得的创作
description: 了解如何在通用编辑器中创建表单片段并将其添加到表单中。
feature: Edge Delivery Services
role: Admin, User, Developer
exl-id: 7b0d4c7f-f82f-407b-8e25-b725108f8455
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 40%

---

# 在通用编辑器中创建表单片段

表单片段是可重用的组件，可消除重复开发工作并确保组织表单之间的一致性。 您可以一次性将这些元素构建为片段并在多个表单中重复使用，而不是为每个表单重新创建常用部分，如联系信息、地址详细信息或同意协议。

**您将在本文中完成的内容：**

- 了解表单片段的业务价值和技术功能
- 使用通用编辑器创建可重用的表单片段
- 通过正确的配置将片段集成到现有表单中
- 管理片段生命周期并维护各表单的一致性

**业务优势：**

- **缩短开发时间**：一次性构建通用表单节，随时随地重复使用
- **已改进一致性**：所有表单中的标准化版面和内容
- **简化的维护**：更新片段一次，以反映使用片段的所有表单中的更改
- **合规性增强**：确保法规部分保持一致且最新

Edge Delivery Services中的表单片段支持各种高级功能，包括嵌套片段、单个表单中的多个实例以及与数据源的无缝集成。

## 了解表单片段

Edge Delivery Services中的表单片段为模块化表单开发提供了强大的功能：

**核心功能：**

- **一致性管理**：片段在多个表单中维护相同的布局和内容。 通过“更改一次，随处反映”方法，片段的更新将自动应用于预览模式中的所有表单。
- **多种用法**：在单个表单中多次添加相同的片段，每个片段都具有到不同数据源或架构元素的独立数据绑定。
- **嵌套结构**：通过将片段嵌入其他片段以创建复杂的层次结构。

**技术要求：**

- **GitHub URL一致性**：片段和使用它的任何表单都必须指定相同的GitHub存储库URL
- **独立编辑**：片段只能在其独立表单中修改；无法在主机表单中进行更改

**发布行为：**

>[!IMPORTANT]
>
>在预览模式下，片段更改会在所有表单中立即反映。 在发布模式下，必须重新发布片段以及使用该片段查看更新的任何表单。

>[!CAUTION]
>
>避免递归片段引用（在其自身内嵌套片段），因为这会导致渲染错误和意外行为。

## 先决条件

**技术设置要求：**

- [GitHub存储库已配置](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#get-started-with-the-aem-forms-boilerplate-repository-template)，您的AEM环境与GitHub存储库之间已建立连接
- [最新自适应Forms块](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#add-adaptive-forms-block-to-your-existing-aem-project)已添加到您的GitHub存储库(适用于现有Edge Delivery Services项目)
- 提供了带有Edge Delivery Services模板的AEM Forms创作实例
- 访问您的AEM Forms as a Cloud Service创作实例URL和GitHub存储库URL

**所需的知识和权限：**

- 基本了解表单设计概念和组件层次结构
- 熟悉通用编辑器界面和表单创建工作流
- 在AEM Forms中创建和管理表单资产的作者级别权限
- 了解贵组织的表单标准和可重用组件要求

## 使用 Edge Delivery Services 表单片段

您可以在通用编辑器中创建 Edge Delivery Services 表单片段，然后将创建的片段添加到 Edge Delivery Services 表单。您可以使用 Edge Delivery Services 表单片段执行以下操作：

- [创建表单片段](#creating-form-fragments)
- [将表单片段添加到一个表单](#adding-form-fragments-to-a-form)
- [管理表单片段](#managing-form-fragments)

+++ 创建表单片段

要在通用编辑器中创建表单片段，请执行以下步骤：

1. 登录到您的AEM Forms as a Cloud Service创作实例。
1. 选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 表单]** > **[!UICONTROL 表单和文档]**。
1. 单击&#x200B;**创建 > 自适应表单片段**。

   ![创建片段](/help/edge/docs/forms/universal-editor/assets/create-fragment.png)

   现在会出现&#x200B;**创建自适应表单片段**&#x200B;向导。
1. 从&#x200B;**选择模板**&#x200B;选项卡中选择基于 Edge Delivery Services 的模板，然后点击&#x200B;**[!UICONTROL 下一步]**。
   ![选择 Edge Delivery Services 模板](/help/edge/docs/forms/universal-editor/assets/create-form-fragment.png)

1. 指定片段的标题、名称、描述和标记。确保为片段指定唯一的名称。如果存在另一个同名的片段，该片段创建就会失败。
1. 指定 **GitHub URL**。例如，如果您的GitHub存储库名为`edsforms`，则它位于帐户`wkndforms`下，URL为`https://github.com/wkndforms/edsforms`。

   ![基本属性](/help/edge/docs/forms/universal-editor/assets/fragment-basic-properties.png)

1. （可选）单击打开&#x200B;**表单模型**&#x200B;选项卡，然后在&#x200B;**从中选择**&#x200B;下拉菜单中为该片段选择下面的一个模型：

   ![显示“表单模型”选项卡中的模型类型](/help/edge/docs/forms/universal-editor/assets/select-fdm-for-fragment.png)

   - **表单数据模型 (FDM)**：将来自数据源的数据模型对象和服务集成到您的片段中。如果您的表单需要从多个来源读写数据，请选择表单数据模型 (FDM)。

   - **JSON 架构**：通过关联一个定义数据结构的 JSON 架构将您的表单与后端系统集成。它允许您使用架构元素添加动态内容。
   - **无**：指定从头开始创建片段，不使用任何表单模型。

   >[!NOTE]
   >
   > 要了解如何将表单或片段与通用编辑器中的表单数据模型(FDM)集成以使用多种后端数据源，请参阅[将表单与通用编辑器中的表单数据模型集成](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)。

1. （可选）在&#x200B;**高级**&#x200B;选项卡中为该片段指定&#x200B;**发布日期**&#x200B;或者&#x200B;**取消发布日期**。

   ![高级选项卡](/help/edge/docs/forms/universal-editor/assets/advanced-properties-fragment.png)
1. 单击&#x200B;**创建**&#x200B;以生成片段。 此时将显示一个包含编辑选项的成功对话框。

   ![编辑片段](/help/edge/docs/forms/universal-editor/assets/edit-fragment.png)

1. 单击&#x200B;**编辑**&#x200B;以在应用了默认模板的情况下在通用编辑器中打开片段。

   通用编辑器中的![片段用于创作](/help/edge/docs/forms/universal-editor/assets/fragment-in-ue.png)

1. **设计片段内容**：添加表单组件（文本字段、下拉列表、复选框）以构建可重用部分。 有关详细的组件指南，请参阅[使用通用编辑器的AEM FormsEdge Delivery Services快速入门](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md#author-forms-using-wysiwyg)。

1. **配置组件属性**：根据用例需要设置字段名称、验证规则和默认值。

1. **保存并预览**：保存片段并使用预览模式验证布局和功能。

   ![通用编辑器中已完成的联系人信息表单片段截图，其中包含姓名、电话、电子邮件和地址字段，这些可在多个表单中重复使用](/help/edge/docs/forms/universal-editor/assets/contact-fragment.png)

**验证检查点：**

- 在通用编辑器中加载片段时没有出现错误
- 所有表单组件均正确呈现
- 字段属性和验证规则按预期工作
- 片段已保存并可在Forms和文档控制台中使用

片段完成后，您可以[将其集成到任何Edge Delivery Services表单](#adding-form-fragments-to-a-form)。

+++


+++ 将表单片段添加到一个表单

此示例演示了如何创建一个`Employee Details`表单，该表单将`Contact Details`片段同时用于雇员和主管信息部分。 此方法可确保数据收集的一致性，同时减少开发工作。

要将表单片段集成到表单中，请执行以下操作：

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

   该表单片段将引用该表单片段进行添加，并且保持与独立表单片段的同步。

   ![通用编辑器中的员工表单截图，展示了成功嵌入的联系人信息片段，说明了片段在重复使用时如何保持其结构一致性](/help/edge/docs/forms/universal-editor/assets/fragment-in-form.png)

   您可以预览表单以查看在&#x200B;**预览**&#x200B;模式中该表单如何显示。

   ![预览](/help/edge/docs/forms/universal-editor/assets/preview-form-with-fragment.png)

   同样，您可以重复步骤 3 至 7 来为 `Supervisor Details` 面板插入 `Contact Details` 片段。

   ![员工详细信息表单](/help/edge/docs/forms/universal-editor/assets/employee-detail-form-with-fragments.png)

+++



+++ 管理表单片段

您可以使用 AEM Forms 用户界面对表单片段执行多项操作。

1. 登录到您的AEM Forms as a Cloud Service创作实例。
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

## 最佳实践

**片段设计和命名：**

- **使用描述性的、唯一的名称**：选择明确指示片段用途的名称（例如，“contact-details-with-validation”而不是“fragment1”）
- **规划可重用性**：设计片段与上下文无关，因此它们可以在不同的表单类型中使用
- **使片段聚焦**：创建单一用途的片段，而不是创建复杂的多功能组件

**开发工作流：**

- **独立测试片段**：在集成到表单中之前验证片段功能
- **保持一致的GitHub URL**：确保在所有相关片段和表单中使用相同的存储库URL
- **文档片段用途**：包含清晰的描述和标记，以帮助团队成员了解何时使用每个片段

**发布和维护：**

- **协调发布**：更新片段时，计划同时重新发布所有依赖的表单
- **版本控制**：在更新片段时使用有意义的提交消息来跟踪一段时间的更改
- **监视依赖项**：跟踪哪些表单使用每个片段来评估更新影响

>[!TIP]
>
>嵌入时，会保留片段样式、脚本和表达式，因此设计时要牢记此继承。

## 摘要

您已成功了解如何在Edge Delivery Services中利用表单片段提高开发效率并保持组织表单的一致性。

**关键成就：**

- **了解**：了解表单片段的业务价值和技术功能
- **创建**：使用具有正确配置的通用编辑器生成可重用的表单片段
- **集成**：将片段添加到具有正确引用设置和属性配置的表单
- **管理**：探索了片段生命周期操作和维护工作流

**后续步骤：**

- 为您的组织创建常用片段库
- 为片段使用建立命名约定和治理策略
- 探索与动态数据驱动片段的[表单数据模型](/help/edge/docs/forms/universal-editor/integrate-forms-with-data-source.md)的高级集成
- 实施基于片段的表单模板以实现一致的用户体验

您的表单现在受益于模块化、可维护的架构，该架构可在各个项目中高效扩展，同时确保一致的用户体验。


