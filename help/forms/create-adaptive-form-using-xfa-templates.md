---
title: 如何使用XFA表单模板基于核心组件创建自适应表单？
description: 了解如何使用 [!DNL Experience Manager Forms] 使用XFA表单模板或XDP文件创建自适应表单。
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
source-git-commit: 681c194f997ab66f93beedad4eea273614e6797d
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 12%

---


# 基于XFA表单模板创建自适应表单（核心组件）

<span class="preview">该功能在早期采用者计划下可用。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

AEM as a Cloud Service为用户提供了使用XFA (XML Forms架构)表单模板或`*.XDP` （XML数据包）文件基于核心组件创建自适应Forms的选项。 此功能允许用户通过将字段从XFA表单模板或XDP文件直接迁移到自适应Forms中来节省时间。

您可以重新利用XFA表单模板或XDP文件表单模板，以创建基于核心组件的自适应Forms。 要重新调整用途，请上传XFA表单模板或XDP文件并将其与自适应表单关联。 XFA表单模板或XDP文件的元素在自适应表单创作期间可用于内容查找器。 从内容查找器中，您可以将表单模板元素拖放到表单上。

## 基于XFA表单模板或XDP文件创建表单的优势

基于XFA表单模板或XDP文件创建表单的好处很少，包括：

* **节省时间**：您可以快速重用现有的XFA表单模板（XDP文件），而无需重新创建表单结构，从而节省创作过程中的时间和精力。
* **轻松迁移**：如果您已在使用XFA表单模板，则此选项可提供到自适应Forms的轻松迁移路径，让您能够利用现代AEM核心组件的优势，而不会丢失现有的表单数据和逻辑。
* **改进的用户体验**：自适应Forms比XFA表单响应更快且更可自定义。 通过转换为自适应Forms，您可以确保跨不同设备和屏幕大小获得更友好的用户体验。
* **增强集成**：自适应Forms可更好地与其他功能（如工作流、数据绑定和表单提交）集成，从而实现更流畅的工作流和更全面的表单管理。

## 先决条件

要使用XFA表单模板或XDP文件基于核心组件创建自适应表单，您需要满足以下条件：

* [为您的环境启用自适应Forms核心组件](enable-adaptive-forms-core-components.md)。
* 建议熟悉以下方面：
   * 创建自适应表单
   * XFA(XML Forms架构)

## 如何使用XFA表单模板或XDP文件创建自适应表单？

执行以下步骤以使用XFA或XDP表单模板创建自适应表单：

1. 登录到您的[!DNL Experience Manager Forms]创作实例。
1. 在 Experience Manager 登录页面上输入您的凭据。登录后，在左上角选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。

   ![Forms和文档](/help/forms/assets/create-fdm.png)

1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 自适应Forms]**。

   ![创建自适应表单](/help/forms/assets/create-af.png)

   将打开表单创建向导。
1. 在&#x200B;**Source**&#x200B;选项卡中，选择基于核心组件的模板。

   ![选择模板](/help/forms/assets/select-template.png)

   选择模板时，将自动选择模板中指定的主题和提交操作，并启用&#x200B;**[!UICONTROL 创建]**&#x200B;按钮。

   ![选择主题](/help/forms/assets/select-form-theme.png)

1. 选择&#x200B;**[!UICONTROL 创建]**。此时将显示一个对话框，其中指定标题、名称和保存自适应表单的位置。
1. 指定其标题、名称和位置。
1. 选择&#x200B;**[!UICONTROL 创建]**。
   ![提供名称和标题](/help/forms/assets/create-form.png)

   自适应表单将创建并在自适应表单编辑器中打开。编辑器将显示模板中可用的内容。
1. 选择![页面信息](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL 打开属性]**。

   ![打开属性](/help/forms/assets/form-properties.png)

   这将打开“表单属性”页面。
1. 转到&#x200B;**[!UICONTROL 表单模型]**&#x200B;选项卡，然后选择&#x200B;**表单模板**。
1. 从下拉列表中选择.xdp文件。

   ![选择XDP文件](/help/forms/assets/select-xdp-file.png)

   屏幕上会显示一个警告对话框。 单击&#x200B;**确定**&#x200B;以继续。

   ![警告对话框](/help/forms/assets/fdm-warning.png)

1. 选择&#x200B;**[!UICONTROL 保存并关闭]**&#x200B;以保存属性。

   >[!NOTE]
   >
   > 在表单&#x200B;**模型**&#x200B;选项卡中选择&#x200B;**表单模板**&#x200B;后，无法对其进行更改。


自适应表单将创建并在自适应表单编辑器中打开。该编辑器显示模板中可用的内容。根据自适应表单的类型，关联的XFA表单模板中存在的表单元素会显示在侧边栏中&#x200B;**[!UICONTROL 内容浏览器]**&#x200B;的&#x200B;**[!UICONTROL 数据模型对象]**&#x200B;选项卡中。 您还可以拖放这些元素来生成自适应表单。

>[!NOTE]
>
> 您可以使用添加字段的面板工具栏禁用XDP表单字段的脚本。 使用[可视规则编辑器](/help/forms/rule-editor-core-components.md)为添加的字段创建逻辑。

## 另请参阅

{{see-also}}
* [使用规则编辑器将动态行为添加到表单](/help/forms/rule-editor-core-components.md)