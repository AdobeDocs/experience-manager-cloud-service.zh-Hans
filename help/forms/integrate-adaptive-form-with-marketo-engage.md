---
Title: How to integrate Marketo Engage with AEM Forms using Form wizard?
Description: Learn how to integrate your Marketo Engage instance with AEM Forms using form wizard.
Keywords: How to connect a Marketo instance with form? , Connect a form to Marketo, Integrate a form with Marketo Engage, Integrate an Adaptive Form with a Marketo instance.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
source-git-commit: 681c194f997ab66f93beedad4eea273614e6797d
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 5%

---


# 配置新表单以与Marketo Engage集成

<span class="preview">该功能在早期采用者计划下可用。 您可以使用官方电子邮件 ID 写信给 aem-forms-ea@adobe.com，加入早期采用者计划并申请使用该功能。</span>

![工作流](/help/forms/assets/workflow-marketo-4.png)

在创建云服务配置以将Marketo Engage与AEM Forms集成后，您可以配置自适应表单以与[Adobe Marketo Engage](https://experienceleague.adobe.com/en/docs/marketo/using/home)集成。

您可以使用表单向导将Marketo Engage连接到自适应表单，该向导通过指导您完成每个步骤来简化配置过程。 这包括选择模板、样式和数据字段，以及设置数据映射以确保您的表单在创建后可以与Marketo Engage通信。 使用表单向导，您还可以配置自适应表单，以在提交时直接将数据提交到Adobe Marketo Engage。

## 为表单配置Marketo Engage数据源的注意事项

为表单配置Marketo Engage数据源时的注意事项如下：

* 无法将Edge Delivery ServicesForms与Marketo Engage连接。

## 将Marketo Engage与表单连接的先决条件

将Marketo Engage与表单连接的先决条件：

* 创建[云服务配置以将Marketo Engage与表单](/help/forms/integrate-form-to-marketo-engage.md)集成。

## 如何配置新的自适应表单以与Marketo Engage集成？

要配置新的自适应表单以与Marketo Engage集成，请执行以下步骤：

1. 选择&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms和文档]**。

   ![选择Forms和文档](/help/forms/assets/select-forms.png)

1. 选择&#x200B;**[!UICONTROL 创建]** > **[!UICONTROL 自适应Forms]**。 将打开表单创建向导。

   ![选择AF](/help/forms/assets/select-create-forms.png)

1. 在&#x200B;**[!UICONTROL Source]**&#x200B;选项卡中，选择一个模板

   ![选择模板](/help/forms/assets/select-template.png)

1. 从&#x200B;**[!UICONTROL 样式]**&#x200B;中选择主题。

   ![选择主题](/help/forms/assets/select-form-theme.png)


1. 在&#x200B;**[!UICONTROL 数据]**&#x200B;选项卡中，选择一个数据模型作为&#x200B;**Marketo Engage**。

1. 从屏幕右窗格中显示的下拉列表中选择&#x200B;**[!UICONTROL 云配置]**。
默认情况下，将显示关联配置的所有字段。 该向导通过使用复选框来为您提供便利性，允许您有选择地选择应在自适应表单中包含的字段。

   ![选择数据模型](/help/forms/assets/select-marketo-data.png)

1. 在&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡中，选择提交操作作为&#x200B;**[!UICONTROL 提交到Marketo]**。

   当您将数据模型选择为&#x200B;**Marketo Engage**&#x200B;时，将自动选择作为&#x200B;**提交到Marketo**&#x200B;的提交操作。 您可以从&#x200B;**[!UICONTROL 提交]**&#x200B;选项卡中选择其他提交操作。 **[!UICONTROL 提交]**&#x200B;选项卡显示所有可用的提交操作。

   ![提交到Marketo engage](/help/forms/assets/select-marketo-engage.png)

1. 选择&#x200B;**[!UICONTROL 创建]**。指定标题、名称和位置以保存自适应表单。

   ![创建表单](/help/forms/assets/create-marketo-form.png)

1. 选择&#x200B;**[!UICONTROL 创建]**。

自适应表单现在配置为与Marketo Engage实例连接。 或者，您也可以编辑自适应表单属性以更改其关联配置。

## 常见问题解答(FAQ)

**问：是否可以更改配置为与Marketo Engage架构连接的表单的提交操作？**
**A：**&#x200B;默认情况下，将表单配置为与Marketo Engage架构连接时，将选择&#x200B;**提交到Marketo**&#x200B;操作。 但是，您可以根据需要更改表单的提交操作。


**问：更改表单的连接器时会出现什么情况？**\
**A：**&#x200B;如果更改表单的连接器，则现有绑定将无效。

**问：对于与Marketo Engage集成的表单，在规则编辑器的调用服务中可用的三项操作是什么？**\
**A：**&#x200B;在与Marketo Engage集成的&#x200B;**调用服务**&#x200B;中可用的三个现成操作是：
* 同步潜在客户
* 按ID获取潜在客户
* 按筛选器类型获取潜在客户

## 下一步

您还可以将自适应表单与[Munchkin库](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/setup/munchkin)连接以跟踪访问次数、点击次数和表单提交次数。

## 相关文章

{{af-submit-action}}

## 另请参阅

{{marketo-engage-see-also}}
